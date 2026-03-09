# member_daily_sessions_attended

> Daily attendance: one row per member per session date with session name, coach, time, and membership context.

## Quick Reference

- **Rows:** ~1385
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| created_at | timestamp with time zone | NO | now() | |
| session_name | text | YES | | |
| session_date | date | YES | | |
| coach_name | text | YES | | |
| session_start | time without time zone | YES | | |
| session_end | time without time zone | YES | | |
| member_name | text | YES | | |
| email | text | YES | | |
| phone | text | YES | | |
| client_id | text | YES | | |
| membership_type | text | YES | | |
| expiry | text | YES | | |
| remaining_visits | text | YES | | |
| member_id | uuid | YES | | |
| gym | text | YES | | |
| class_type | text | YES | | |

## Business Context

Source of attendance for “who attended when.” Used with coach_session_actual and member_lcns for session counts and LC/NS. Denormalised fields support display without joining.

## Related Rules

- [Session expectations](../../rules/coaching/session-expectations.md), [Late cancel / no show](../../rules/coaching/late-cancel-noshow.md)

## Common Queries

```sql
-- Attendance for a member in a date range
SELECT session_date, session_name, coach_name, session_start, session_end
FROM member_daily_sessions_attended
WHERE member_id = :member_id
  AND session_date BETWEEN :start AND :end
ORDER BY session_date, session_start;
```
