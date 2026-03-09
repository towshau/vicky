# member_programs

> Programming pipeline: member–programming coach assignment, due date, completion weeks, and stage (new_member, update_stage, awaiting_program, upload_required, complete, inactive).

## Quick Reference

- **Rows:** ~461
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_id` → member_memberships.id, `programming_coach_id` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| member_id | uuid | YES | | |
| membership_id | uuid | YES | | |
| programming_coach_id | uuid | YES | | |
| due_date | date | YES | | |
| weeks_completed | text | YES | | |
| completion_weeks_addition | text | YES | | |
| completion_bucket | text | YES | | |
| created_at | timestamp with time zone | YES | now() | |
| updated_at | timestamp with time zone | YES | now() | |
| programming_stage | programming_stage | YES | | new_member, update_stage, awaiting_program, upload_required, complete, inactive |
| membership_expiry_date | date | YES | | Denormalised |
| member_name | text | YES | | Denormalised |
| member_notes | text | YES | | |

## Business Context

Tracks who has programming, who it’s with, and pipeline stage. Feeds program generation and handoff; programming_stage drives Retool and reporting.

## Related Rules

- [Coach assignments](../../rules/coaching/coach-assignments.md), [Programming handoff](../../rules/programming/) (engine rules, exclusions)

## Common Queries

```sql
-- Members awaiting program
SELECT member_id, member_name, programming_coach_id, programming_stage, due_date
FROM member_programs
WHERE programming_stage = 'awaiting_program'
ORDER BY due_date;
```
