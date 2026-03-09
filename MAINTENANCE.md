# Maintaining Vicky

This file defines how the Vicky repo stays current. A second brain that drifts from reality is worse than no brain at all — it gives confident wrong answers.

---

## The Three Tiers of Maintenance

### Tier 1: Automated (set and forget)

These run on schedules or triggers with no human intervention. Once built, they just work.

| What | Trigger | Output | Status |
|------|---------|--------|--------|
| Schema index refresh | Weekly (Sunday night) | Regenerates schema/_index.md with current table names, row counts, comments | NOT YET BUILT |
| Core table row counts | Weekly (Sunday night) | Updates row count in each schema/core/*.md file | NOT YET BUILT |
| Reference data refresh | Weekly (Sunday night) | Regenerates reference/membership-types.md, reference/enums.md, reference/staff-roles.md from Supabase | NOT YET BUILT |
| SOP sync from admin_sop | On insert/update in admin_sop table | Creates or updates corresponding stub file in sops/ with task metadata | NOT YET BUILT |
| Membership version sync | On insert in membership_versions | Flags rules/memberships/pricing.md as potentially stale, sends Slack notification | NOT YET BUILT |
| New staff trigger | On insert in staff_database | Sends Slack reminder to update org/ files | NOT YET BUILT |

### Tier 2: Conversation-Driven (you + Claude)

These happen naturally as part of working with Claude. The key habit: if we define or change a rule in conversation, the file gets written before the conversation ends.

**How it works:**

1. You and Claude discuss a business rule, policy change, or new process
2. Claude drafts the markdown file (or update to an existing file)
3. You review it, correct anything, and commit to the repo
4. Claude prompts you if it notices a rule was discussed but not committed

**Prompt to give Claude at the start of relevant conversations:**

> "We're working on Lockeroom business logic. If we establish or change any rules, draft the updated Vicky repo file for me at the end. Repo structure is at github.com/towshau/vicky."

### Tier 3: Quarterly Review (30 minutes, once per quarter)

A lightweight scan — not a full audit.

1. Open CHANGELOG.md — scan for gaps (any month with zero entries is suspicious)
2. Check rule file last_updated dates in frontmatter — anything over 6 months old, ask yourself: "has this actually not changed, or did I forget to update it?"
3. Run the schema index refresh manually and diff against the current _index.md — any new tables that appeared in Supabase but aren't documented?
4. Spot-check 3 random rule files by asking Vicky a question that should use them — does she give the right answer?

---

## Automation Implementation Checklist

These are the specific items to build. Each one is a discrete piece of work — do them one at a time, test, then move on.

### 1. Schema Index Auto-Refresh (n8n workflow)

**Priority:** High — easiest win, biggest impact on schema docs staying current

**What it does:**

- Runs weekly (Sunday 11pm AEST)
- Queries Supabase information_schema for all public tables
- Queries row counts via pg_stat_user_tables
- Generates markdown for schema/_index.md
- Commits to github.com/towshau/vicky via GitHub API

**Implementation steps:**

- Create n8n workflow: `vicky_schema-index-refresh`
- Node 1: Schedule trigger (weekly, Sunday 23:00 AEST)
- Node 2: Supabase SQL query — pull table names, row counts, comments

```sql
SELECT
  schemaname || '.' || relname AS table_name,
  n_live_tup AS row_count,
  obj_description((schemaname || '.' || relname)::regclass) AS comment
FROM pg_stat_user_tables
WHERE schemaname = 'public'
ORDER BY relname;
```

- Node 3: Code node — format results into markdown table
- Node 4: GitHub API — read current schema/_index.md (GET contents)
- Node 5: GitHub API — update file if changed (PUT contents with SHA)
- Node 6: Slack notification to #claude-bot — "Schema index refreshed. X tables, Y new since last week."

---

### 2. Reference Data Auto-Refresh (n8n workflow)

**Priority:** High — membership types and enums change occasionally and agents need current data

**What it does:**

- Runs weekly (after schema refresh)
- Pulls membership_types table → regenerates reference/membership-types.md
- Pulls custom enum definitions → regenerates reference/enums.md
- Pulls distinct roles from staff_database → regenerates reference/staff-roles.md
- Commits to GitHub

**Implementation steps:**

- Create n8n workflow: `vicky_reference-data-refresh`
- Node 1: Schedule trigger (weekly, Sunday 23:15 AEST)
- Node 2: Supabase SQL — pull membership types

```sql
SELECT name, category, session_frequency_per_week, session_total, tod_category, sort_order
FROM membership_types
ORDER BY sort_order, name;
```

- Node 3: Supabase SQL — pull enums

```sql
SELECT t.typname AS enum_name, e.enumlabel AS enum_value
FROM pg_type t
JOIN pg_enum e ON t.oid = e.enumtypid
JOIN pg_namespace n ON t.typnamespace = n.oid
WHERE n.nspname = 'public'
ORDER BY t.typname, e.enumsortorder;
```

- Node 4: Supabase SQL — pull staff roles

```sql
SELECT DISTINCT role, employment_type,
  unnest(supplementary_roles) AS supplementary_role
FROM staff_database
WHERE staff_status = 'active'
ORDER BY role;
```

- Node 5: Code node — format each into markdown
- Node 6-8: GitHub API — update each file
- Node 9: Slack notification

---

### 3. SOP Table → Vicky Repo Sync (Supabase trigger + n8n webhook)

**Priority:** Medium — connects the existing admin_sop task tracker to Vicky's SOP docs

**What it does:**

- When a row is inserted or updated in admin_sop, fires a webhook to n8n
- n8n checks if a corresponding SOP file exists in the repo
- If no file exists: creates a stub SOP file with metadata from the table row
- If file exists: updates the metadata header (assignee, frequency, etc.) but leaves the body untouched
- Sends Slack notification: "SOP file created/updated for: [task name]"

**Implementation steps:**

**Supabase side:**

- Create a Postgres function `notify_vicky_sop_change()`

```sql
CREATE OR REPLACE FUNCTION notify_vicky_sop_change()
RETURNS trigger AS $$
BEGIN
  PERFORM net.http_post(
    url := 'https://your-n8n-instance.com/webhook/vicky-sop-sync',
    body := jsonb_build_object(
      'event', TG_OP,
      'id', NEW.id,
      'name', NEW.name,
      'description', NEW.description,
      'dod', NEW.dod,
      'assignee', NEW.assignee,
      'frequency', NEW.frequency,
      'weekday', NEW.weekday,
      'time_estimation', NEW.time_estimation,
      'team_member', NEW.team_member,
      'active', NEW.active
    )
  );
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- Create trigger on admin_sop

```sql
CREATE TRIGGER trg_vicky_sop_sync
  AFTER INSERT OR UPDATE ON admin_sop
  FOR EACH ROW
  EXECUTE FUNCTION notify_vicky_sop_change();
```

- Ensure pg_net extension is enabled (for net.http_post)

**n8n side:**

- Create n8n workflow: `vicky_sop-sync`
- Node 1: Webhook trigger (receives POST from Supabase)
- Node 2: Code node — determine file path from SOP name (map admin_sop.name to a folder; infer department from team_member or assignee; generate filename: slugify the name → sops/{department}/{slug}.md)
- Node 3: GitHub API — check if file exists (GET contents, handle 404)
- Node 4: IF node — file exists vs doesn't exist
- Node 5a (new file): Code node — generate stub SOP markdown from template (name, role, frequency, estimated time, definition of done, active; placeholder Steps and Related Rules)
- Node 5b (existing file): Code node — update only the metadata header, preserve body
- Node 6: GitHub API — create or update file
- Node 7: Slack notification to #claude-bot

---

### 4. Membership Version Change Alert (Supabase trigger + Slack)

**Priority:** Medium — catches pricing/policy changes that need rule file updates

**What it does:**

- When a new row is inserted in membership_versions, fires a Slack notification
- Message tells Shaun to review and update rules/memberships/pricing.md
- Does NOT auto-update the rule file (pricing rules need human judgment)

**Implementation steps:**

- Create Supabase function `notify_vicky_membership_version()`
- Create trigger on membership_versions AFTER INSERT
- Webhook to n8n → Slack message: "New membership version added: {membership_name} v{version_number}. Review rules/memberships/pricing.md — it may need updating."

---

### 5. New Staff Alert (Supabase trigger + Slack)

**Priority:** Low — happens infrequently but easy to forget

**What it does:**

- When a new row is inserted in staff_database, sends Slack reminder
- Reminds to update org/org-chart.md, org/roles.md, and assign onboarding docs

**Implementation steps:**

- Create Supabase function `notify_vicky_new_staff()`
- Create trigger on staff_database AFTER INSERT
- Webhook to n8n → Slack message: "New staff member added: {first_name} {last_name} ({role}). Update org/ files in Vicky."

---

### 6. Stale File Detection (n8n workflow)

**Priority:** Low — nice to have, catches drift over time

**What it does:**

- Runs monthly (1st of the month)
- Scans all rule files via GitHub API
- Checks last_updated in frontmatter
- Any rule file not updated in 6+ months gets flagged in Slack
- Sends a summary: "5 rule files haven't been touched in 6+ months: [list]"

**Implementation steps:**

- Create n8n workflow: `vicky_stale-file-check`
- Node 1: Schedule trigger (monthly, 1st at 09:00 AEST)
- Node 2: GitHub API — list all files in rules/ recursively
- Node 3: For each .md file — GitHub API get contents
- Node 4: Code node — parse YAML frontmatter, extract last_updated
- Node 5: Code node — filter to files where last_updated < 6 months ago
- Node 6: Slack notification with list

---

## What NOT to Automate

Some things should stay manual and conversation-driven:

- **Writing rule content** — Business logic needs human input. Automation can create stubs and flag staleness, but the actual rules come from Shaun + Claude conversations.
- **SOP procedure steps** — The admin_sop sync creates stub files, but the actual "how to do this" content needs to be written by someone who knows the process.
- **Architecture decisions** — ADRs are written at decision time, not retroactively generated.
- **SOUL.md** — Vicky's personality evolves through conversation, not automation.
