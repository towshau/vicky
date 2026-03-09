# hr_direct_report

> Tracks HR direct report relationships between managers and coaches. Used for roll call, 1-on-1s, and org structure.

## Quick Reference

- **Rows:** ~14
- **Primary key:** `id` (uuid)
- **Key relationships:** `manager_id` → staff_database.id, `coach_id` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| manager_id | uuid | NO | | FK to staff_database (manager) |
| coach_id | uuid | NO | | FK to staff_database (coach) |
| coach_name | text | YES | | Denormalised |
| manager_name | text | YES | | Denormalised |
| submission_date | timestamp with time zone | YES | CURRENT_TIMESTAMP | |
| vibe_check | text | YES | | |
| personal_notes | text | YES | | |
| focus_areas | text | YES | | |
| system_updates | text | YES | | |
| manager_feedback | text | YES | | |
| performance_rating | numeric | YES | | |
| what_has_gone_wll | text | YES | | (typo in column name) |

## Business Context

Formal manager–coach reporting. staff_database.direct_report can mirror this; this table stores the relationship plus 1-on-1 / roll call notes. Used for org chart and roll call dependency (direct_report vs buddy).

## Related Rules

- [Direct reports](../../rules/hr/direct-reports.md), [Scheduling roll call](../../rules/scheduling/)

## Common Queries

```sql
-- All direct reports for a manager
SELECT coach_id, coach_name, manager_id, manager_name
FROM hr_direct_report
WHERE manager_id = :manager_id
ORDER BY coach_name;
```
