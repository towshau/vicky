# On-Demand Physical Report

**Role:** Coach / Admin  
**Frequency:** As needed (after a member completes physicals)  
**Estimated time:** 2 minutes  
**Systems used:** Retool, n8n, Supabase, Railway (PDF API), Gmail

## Summary

Generate and email a personalised Physical Report PDF for any member. The report shows their first, second most recent, and most recent assessment results across Health, Fitness, and Strength pillars — with stage progression highlighting. One button in Retool triggers the full pipeline: data is pulled from Supabase, a PDF is generated on Railway, and the report lands in the member's inbox.

## Prerequisites

- Member has at least one physicals assessment in `member_physicals_raw`
- Member has an active primary membership in `member_memberships` (for RM attribution)
- You have the member's email address
- The n8n workflow "Generate Physical Report PDF" is active

## Steps

1. **Open the Physicals Report page in Retool**
2. **Select the member** from the dropdown (searches `member_database`)
3. **Enter or confirm the email address** the report should be sent to
4. **Click "Generate & Send Report"**
5. **Wait for confirmation** — Retool will show a success or error message once the pipeline completes (typically 10–20 seconds)

That's it. The member receives their Physical Report PDF as an email attachment.

## What Happens Behind the Scenes

1. Retool sends a webhook to n8n with the `member_id` and `email`
2. n8n calls the Supabase function `get_physical_report_data(member_id)` which returns all report data as JSON
3. n8n sends that JSON to the Railway-hosted PDF API (`/generate-report`)
4. The PDF API renders the HTML template with the member's data using Playwright/Chromium and returns the PDF
5. n8n emails the PDF to the specified address

## Report Contents

The PDF has three pages:

| Page | Content |
|------|---------|
| **Cover** | Hero image, member name, date |
| **Journey + Why Testing Matters** | The four Lockeroom stages (Reset → Baseline → Longevity → Performance) and why each pillar matters |
| **Physical Results** | Table with every test grouped by pillar, showing first / second most recent / most recent values with dates and stage highlighting |

### Tests Included

| Pillar | Tests |
|--------|-------|
| Health | InBody Points, Body Fat %, Body Weight |
| Fitness | VO2 Max, Push Ups, Chin Hold, Grip Strength |
| Strength (Power) | 4 Jump RSI, Cross Over Hop, Max Vertical Jump |

### RM (Results Manager)

The report displays the member's **effective coach** as RM, determined by `COALESCE(handoff_coach_id, coach_id)` from their active primary membership. If no active membership or coach is found, it shows "N/A".

### Data Sources

- **Health metrics** (Body Fat %, Body Weight): `member_health_metrics` table
- **All other tests**: `member_physicals_raw` table
- **Member info** (name, DOB, gender): `member_database` table
- **Coach/RM**: `member_memberships` + `staff_database` tables

## Common Mistakes

- **Member has no assessments** — The report will generate but all values will show "N/A". Check `member_physicals_raw` for the member first.
- **Wrong email** — Double-check the email before sending. There is no "unsend".
- **RM shows N/A** — The member either has no active primary membership or no coach assigned. Check `member_memberships` for an active row with `primary_membership_id IS NULL`.
- **Old data showing** — The report always pulls live data. If recent assessments aren't showing, confirm the data has been synced from TeamBuildr to `member_physicals_raw`.

## Troubleshooting

| Symptom | Check |
|---------|-------|
| Retool button spins forever | Is the n8n workflow active? Check n8n executions. |
| n8n shows "Internal Server Error" | Check Railway deployment logs. The PDF API may have crashed or restarted. |
| PDF arrives but data is wrong | Run `SELECT * FROM get_physical_report_data('member-uuid')` in Supabase to inspect the raw payload. |
| Email not received | Check spam/junk. Verify the email address. Check n8n execution logs for email node errors. |

## Related Rules

- Effective coach logic: `COALESCE(handoff_coach_id, coach_id)` — see schema rules
- Primary membership: row where `primary_membership_id IS NULL` and `status = 'active'`
- Physicals scoring: `physicals_scoring_lookup` table and `auto_calculate_physicals_scores` trigger
