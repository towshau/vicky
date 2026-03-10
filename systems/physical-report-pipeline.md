# Physical Report Pipeline

> Generates and emails on-demand Physical Report PDFs for Lockeroom members via Retool → n8n → Supabase → Railway PDF API → email.

## Purpose

Automates the creation of personalised Physical Report PDFs. A coach or admin clicks a button in Retool, and the member receives a branded PDF summarising their assessment history across Health, Fitness, and Strength pillars.

## How It Connects

- **To Supabase:** Calls `get_physical_report_data(member_id)` RPC function which reads from `member_database`, `member_memberships`, `staff_database`, `member_physicals_raw`, and `member_health_metrics`
- **To Retool:** Trigger form with member selector and email input; fires a webhook to n8n
- **To n8n:** Orchestrates the pipeline — receives webhook, calls Supabase, calls PDF API, sends email
- **To Railway:** Hosts the Dockerised FastAPI PDF generator at `physicalsv2-production.up.railway.app`
- **To Gmail:** n8n sends the PDF as an email attachment to the specified address

## Architecture

```
Retool Button
    │
    ▼
n8n Webhook (POST /webhook/generate-physical-report)
    │
    ├── HTTP Request → Supabase RPC: get_physical_report_data(member_id)
    │       Returns: { name, dob, assessor, category, result_groups, ... }
    │
    ├── HTTP Request → Railway PDF API: POST /generate-report
    │       Sends: full JSON payload
    │       Returns: PDF binary
    │
    └── Send Email → Gmail with PDF attachment
```

## Key Components

### 1. Supabase Function: `get_physical_report_data(member_id uuid)`

- **Returns:** `jsonb` with complete report payload
- **Security:** `SECURITY DEFINER`, executable by `anon` role
- **Logic:**
  - Member info from `member_database` (name, DOB, gender → category)
  - Effective coach (RM) from `member_memberships` where `primary_membership_id IS NULL AND status = 'active'`, using `COALESCE(handoff_coach_id, coach_id)` joined to `staff_database`
  - For each test: first, second-most-recent, and most-recent values/dates/stages
  - Body Fat % and Body Weight from `member_health_metrics` (not `member_physicals_raw`)
  - All other tests from `member_physicals_raw` with corresponding `_score` columns for stage

### 2. Railway PDF API

- **Repo:** `towshau/physicals_v2` → `reporting/deploy/`
- **Stack:** Python 3.11, FastAPI, Jinja2, Playwright (Chromium)
- **Endpoints:**
  - `GET /health` → `{"status": "ok"}`
  - `POST /generate-report` → accepts JSON payload, returns PDF bytes
- **Domain:** `physicalsv2-production.up.railway.app`
- **Docker:** builds from `reporting/deploy/Dockerfile`, auto-deploys on push to master
- **Assets:** `logo.png` and `hero.png` embedded as base64 data URIs in the HTML

### 3. n8n Workflow: "Generate Physical Report PDF"

| Node | Type | Purpose |
|------|------|---------|
| Webhook | Trigger | Receives `{ member_id, email }` from Retool |
| Fetch Report Data | HTTP Request | POST to Supabase RPC, returns report JSON |
| Generate PDF | HTTP Request | POST JSON to Railway API, returns PDF binary |
| Email PDF | Send Email | Sends PDF attachment to the specified email |

### 4. Retool Form

- Member dropdown (from `member_database`)
- Email text input
- "Generate & Send Report" button → POST to n8n webhook URL

## Report Payload Shape

```json
{
  "name": "Chris Sprowles",
  "dob": "12. 12. 1977",
  "assessor": "Andy Kong",
  "report_date": "10. 03. 2026",
  "category": "Masters 40+",
  "total_pages": 3,
  "result_groups": [
    {
      "pillar": "Health",
      "tests": [
        {
          "name": "InBody Points",
          "first_value": "N/A",
          "first_date": "",
          "first_stage": 0,
          "second_value": "N/A",
          "second_date": "",
          "second_stage": 0,
          "most_recent_value": "N/A",
          "most_recent_date": "",
          "most_recent_stage": 0,
          "s1": "< 70",
          "s2": "70-79",
          "s3": "80-89",
          "s4": "90+"
        }
      ]
    }
  ]
}
```

Fields injected by the PDF API (not required in payload): `logo_b64`, `hero_b64`, `stages` (journey text).

## Column Mapping

| Report Test | Table | Value Column | Score Column |
|-------------|-------|-------------|-------------|
| InBody Points | `member_physicals_raw` | `inbody_value` | `inbody_score` |
| Body Fat % | `member_health_metrics` | `bf` | — (no score) |
| Body Weight | `member_health_metrics` | `weight` | — (no score) |
| VO2 Max | `member_physicals_raw` | `vo2_value` | `vo2_score` |
| Push Ups | `member_physicals_raw` | `push_ups_value` | `push_ups_score` |
| Chin Hold | `member_physicals_raw` | `chin_hold_value` | `chin_hold_score` |
| Grip Strength | `member_physicals_raw` | `grip_strength_value` | `grip_strength_score` |
| 4 Jump RSI | `member_physicals_raw` | `rsi_value` | `rsi_score` |
| Cross Over Hop | `member_physicals_raw` | `coh_value` | `coh_score` |
| Max Vertical Jump | `member_physicals_raw` | `vertical_jump_value` | `vertical_jump_score` |

## Naming Conventions

- Supabase function: `get_physical_report_data`
- Railway service: `physicals-v2` in project `physicals-pdf`
- n8n workflow: "Generate Physical Report PDF"
- PDF filename: `{Member_Name}_Physical_Report.pdf`

## Troubleshooting

- **Railway 500 error:** Check Railway deployment logs. Common cause: Playwright/Chromium crash (memory, missing deps). Redeploy if needed.
- **Supabase RPC fails:** Verify the function exists with `SELECT proname FROM pg_proc WHERE proname = 'get_physical_report_data'`. Check `anon` has EXECUTE privilege.
- **RM shows N/A:** Member has no active primary membership. Query `member_memberships` for `member_id` with `primary_membership_id IS NULL AND status = 'active'`.
- **Missing test data:** Check `member_physicals_raw` for the member. If Body Fat/Weight missing, check `member_health_metrics`.

## Related Docs

- SOP: [sops/coaching/on-demand-physical-report.md](../sops/coaching/on-demand-physical-report.md)
- Source code: [towshau/physicals_v2](https://github.com/towshau/physicals_v2) → `reporting/` and `reporting/deploy/`
- Schema rules: effective coach = `COALESCE(handoff_coach_id, coach_id)` from active primary membership
