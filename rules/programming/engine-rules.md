---
title: Engine Rules
domain: programming
version: 1.0
effective_date: 2026-03-09
applies_to: [bligh, bridge, collins]
last_updated: 2026-03-11
updated_by: Shaun
status: active
replaces: null
tags: [engine, programming-rules, supabase, cohort, priority]
---

# Engine Rules

## Summary

How the programming engine selects members, loads rules, and applies priority/overrides. Rules live in Supabase `programming_rules` table; this file documents the logic.

## Rules

### Cohort Selection

- Only generate programs for **active members**: `member_database.current_status = 'active'`.
- Exclude test accounts: `member_database.test_account = false`.
- Member IDs come from `member_database.id`; join to `member_tbresults.member_id` for past programs.

### Rules Table: `programming_rules`

- Columns: `id`, `gym` (nullable), `name`, `category`, `rule_key`, `rule_value` (jsonb), `priority`, `active`, `created_at`, `updated_at`, `source` (nullable), `source_ref` (nullable).
- **`source`** — Who or what created this rule. Use `'manual'` or `'seed'` for human-created rules; later e.g. `'agent:slack_feedback'` or `'agent:coach_note'` when an agent layer proposes rules.
- **`source_ref`** — Link to the original input (e.g. Slack message URL, coach note ID). NULL for manually created rules. Enables audit trail and “why does this rule exist?”.
- Engine loads rows where `(gym = :gym OR gym IS NULL) AND active = true`.
- NULL gym = applies to all gyms. Non-null = gym-specific override.
- Higher `priority` value overrides lower when multiple rules share a `rule_key`.

### Rule Categories

- `volume` — sets per muscle group, total session volume.
- `progression` — rep range progressions, phase duration.
- `exercise_selection` — which exercises to include/exclude.
- `structure` — series composition, pairing constraints.
- `member_specific` — individual overrides (injuries, goals).

### First Program Logic

- Assignment via Programming Slack channel.
- Wait for physicals data before building.
- Load base program (2D/3D/4D, 3 sets) from TeamBuildr templates.
- Choose starting reps (10–12 most common).
- Set completion weeks = 4 (first program), then 6 (standard).

## Site Exceptions

> Gym-specific rules are handled by the `gym` column in `programming_rules`. NULL = all gyms.

## Examples

**Example 1: Loading rules for Bridge Street**

Engine queries: `SELECT * FROM programming_rules WHERE (gym = 'bridge' OR gym IS NULL) AND active = true ORDER BY priority DESC`. A gym-specific rule for Bridge overrides the all-gym default if they share the same `rule_key`.

**Example 2: Member with injuries**

`programming_exercise_exclusions` table holds member-specific exclusions. Engine checks this before assigning exercises.

## Changelog

| Date       | Version | Change          | By    |
|------------|---------|-----------------|-------|
| 2026-03-09 | 1.0     | Initial version | Shaun |
| 2026-03-11 | 1.1     | Added source, source_ref columns for agent/provenance | Shaun |
