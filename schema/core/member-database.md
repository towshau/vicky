# member_database

> Master record for all members (past and present). Single source of identity and contact; membership periods live in member_memberships.

## Quick Reference

- **Rows:** ~782
- **Primary key:** `id` (uuid)
- **Key relationships:** `coach_id` → staff_database.id, `salesperson` → staff_database.id, `referrer_id` → member_database.id (self), `stripe_primary_fk` → Stripe

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| created_at | timestamp with time zone | NO | now() | |
| coach_id | uuid | YES | | FK to staff_database |
| first_name | text | YES | | |
| last_name | text | YES | | |
| email | text | YES | '' | |
| phone | bigint | YES | | |
| dob | date | YES | | |
| referral_source_name | text | YES | | |
| current_status | membership_status | YES | 'active' | |
| member_name | text | YES | | Denormalised display name |
| linkedin_url | text | YES | | |
| company_name | text | YES | | |
| gender | gender | YES | | |
| initial_weight | numeric | YES | | |
| initial_bf_percentage | numeric | YES | | |
| height | numeric | YES | | in cm |
| lifestyle_grouping | text | YES | | rate of progress field |
| personality_archetype | text | YES | | |
| address | text | YES | | |
| gym_string | text | YES | | |
| salesperson | uuid | YES | | FK to staff_database |
| referral_source_email | text | YES | | |
| coach_name | text | YES | | Denormalised |
| gr_bligh | boolean | YES | false | Google Review flag |
| gr_bridge | boolean | YES | false | |
| injuries | text | YES | | |
| goals | text | YES | | |
| medications | text | YES | | |
| contraindications | text | YES | | |
| stripe_primary_fk | uuid | YES | | |
| test_account | boolean | NO | false | |
| gr_collin | boolean | YES | false | |
| last_physicals_date | date | YES | | Most recent physicals from member_physicals_raw |
| referrer_id | uuid | YES | | Member who referred this member (self-reference) |

## Business Context

The single source of truth for who a member is. All membership periods, holds, sessions, and payments reference `member_id` → this table. Denormalised fields (member_name, coach_name) support display and reporting; for canonical data use the FKs. Current_status is derived/updated from membership state.

## Related Rules

- [Primary/secondary membership](../../rules/memberships/primary-secondary.md), [Holds policy](../../rules/memberships/holds-policy.md)

## Common Queries

```sql
-- Active members with current coach
SELECT id, member_name, coach_id, coach_name, current_status
FROM member_database
WHERE current_status = 'active'
ORDER BY member_name;
```
