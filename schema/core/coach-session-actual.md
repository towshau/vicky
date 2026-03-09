# coach_session_actual

> Completed sessions: one row per coach per week with session counts, late cancels, no shows, covered, missed.

## Quick Reference

- **Rows:** ~956
- **Primary key:** `id` (uuid)
- **Key relationships:** `staff_id` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| staff_id | uuid | YES | | FK to staff_database |
| session_time | time without time zone | YES | | |
| session_name | text | YES | | |
| coach_name | text | YES | | Denormalised |
| date_added | timestamp with time zone | YES | now() | |
| session_date | date | YES | | |
| sessions_attended | integer | YES | | |
| late_cancels | integer | YES | | |
| no_shows | integer | YES | | |
| sessions_covered | integer | YES | | |
| sessions_missed | integer | YES | | |
| notes | text | YES | | |
| week_start | date | YES | | Week start for aggregation |

## Business Context

Source of truth for coach session delivery. Used for session expectations (vs target from hours), WCR, and performance reporting. Late cancels and no shows are also recorded in member_lcns at member level.

## Related Rules

- [Session expectations](../../rules/coaching/session-expectations.md), [Late cancel / no show](../../rules/coaching/late-cancel-noshow.md), [WCR](../../rules/coaching/wcr.md)

## Common Queries

```sql
-- Sessions by coach for a week
SELECT staff_id, coach_name, week_start, sessions_attended, late_cancels, no_shows
FROM coach_session_actual
WHERE week_start = DATE_TRUNC('week', CURRENT_DATE)::date
ORDER BY coach_name;
```
