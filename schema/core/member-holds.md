# member_holds

> Tracks hold periods for members with financial and session credits. Holds are full-week (Monday–Friday); policy and credits are stored here.

## Quick Reference

- **Rows:** ~740
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_id` → member_memberships.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| member_id | uuid | YES | | FK to member_database |
| member_name | text | YES | | Denormalised |
| membership_id | uuid | YES | | FK to member_memberships |
| hold_start | date | NO | | Start date of hold |
| hold_end | date | YES | | End date of hold |
| full_hold_week | integer | YES | | Full weeks in hold |
| policy_applied | text | YES | | |
| hold_notes | text | YES | | |
| created_at | timestamp with time zone | YES | now() | |
| financial_hold_credit | numeric | YES | | Dollar value credited back |
| email | text | YES | | Denormalised |
| session_account_credit | numeric | YES | | Session credits applied |
| RM | text | YES | | Denormalised RM name |
| travel_programming_notes | text | YES | | |

## Business Context

Source of truth for all member holds. Holds start and end on full weeks (Mon–Fri). financial_hold_credit and session_account_credit record what was credited; policy logic is documented in rules/memberships/holds-policy.md.

## Related Rules

- [Holds policy](../../rules/memberships/holds-policy.md)

## Common Queries

```sql
-- Active holds
SELECT * FROM member_holds
WHERE hold_start <= CURRENT_DATE AND (hold_end IS NULL OR hold_end >= CURRENT_DATE);
```
