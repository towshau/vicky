# member_memberships

> Tracks membership periods, stages, and staff assignments for each member. One row per membership period; primary/secondary via primary_membership_id.

## Quick Reference

- **Rows:** ~1596
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_type_id` → membership_types.id, `coach_id` / `programming_coach_id` / `handoff_coach_id` / `revenue_team_assignee` / `renewal_assignee` / `nutrition_lead` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| member_id | uuid | YES | | FK to member_database |
| membership_type_id | uuid | YES | | FK to membership_types |
| start_date | date | NO | | |
| end_date | date | NO | | |
| status | text | YES | 'pending' | |
| created_at | timestamp with time zone | YES | now() | |
| test_duration | text | YES | | |
| member_name | text | YES | | Denormalised |
| coach_id | uuid | YES | | RM / primary coach |
| salesperson_id | uuid | YES | | |
| membership_stage | text | YES | | |
| coach_name | text | YES | | Denormalised |
| newsale_metadata | uuid | YES | | FK to member_newsale_metadata |
| renewal_metadata | uuid | YES | | FK to member_renewal_meta |
| journey_stage | journey_stage_type | YES | | |
| gym | text | YES | | BLIGH, BRIDGE, COLLINS |
| programming_coach_id | uuid | YES | | |
| handoff_coach_id | uuid | YES | | |
| revenue_team_assignee | uuid | YES | | |
| renewal_assignee | uuid | YES | | |
| nutrition_lead | uuid | YES | | |
| pipeline_lost | pipelinelost_churnmarker | YES | | good_churn / bad_churn |
| membership_notes | text | YES | | |
| primary_membership_id | uuid | YES | | NULL = primary; non-NULL = secondary (FK to member_memberships) |
| check1 | boolean | YES | false | |
| check2 | boolean | YES | false | |
| check3 | boolean | YES | false | |
| renewal_date | date | YES | | |
| rm | boolean | NO | true | Is RM assigned |

## Business Context

One row per membership period (trial, new sale, renewal). Primary vs secondary: primary_membership_id IS NULL for the primary membership; secondaries reference their primary. Staff assignments (coach_id, programming_coach_id, renewal_assignee, etc.) drive who is responsible for the member during this period. Journey and membership_stage drive pipeline and reporting.

## Related Rules

- [Primary/secondary membership](../../rules/memberships/primary-secondary.md), [Renewals](../../rules/memberships/renewals.md), [New sale pipeline](../../rules/memberships/newsale-pipeline.md)

## Common Queries

```sql
-- Active memberships with coach
SELECT id, member_id, member_name, start_date, end_date, status, coach_id, coach_name, gym
FROM member_memberships
WHERE status = 'active' AND end_date >= CURRENT_DATE
ORDER BY end_date;
```
