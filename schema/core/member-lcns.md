# member_lcns

> Late cancels and no shows: one row per member per date with counts per coach. Used for LC/NS policy and reporting.

## Quick Reference

- **Rows:** ~1065
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `coach_id` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| created_at | timestamp with time zone | NO | now() | |
| member_id | uuid | YES | | |
| member_name | text | YES | | Denormalised |
| date | date | NO | | CURRENT_DATE default |
| coach_id | uuid | YES | | |
| coach_name | text | YES | | Denormalised |
| late_cancel | integer | NO | 0 | |
| no_show | integer | NO | 0 | |
| entry_seq | integer | YES | | |

## Business Context

Records late cancels and no shows at member–date–coach level. Policy (e.g. 10hr before noon, 4hr after) is in rules/coaching/late-cancel-noshow.md. Aggregated in coach_session_actual for coach-level counts.

## Related Rules

- [Late cancel / no show](../../rules/coaching/late-cancel-noshow.md)

## Common Queries

```sql
-- LC/NS in last 30 days by member
SELECT member_id, member_name, date, coach_name, late_cancel, no_show
FROM member_lcns
WHERE date >= CURRENT_DATE - INTERVAL '30 days'
  AND (late_cancel > 0 OR no_show > 0)
ORDER BY date DESC, member_name;
```
