# staff_database

> Master record for all staff (coaches, sales, admin). Base information for scheduling, assignments, and HR.

## Quick Reference

- **Rows:** ~39
- **Primary key:** `id` (uuid)
- **Key relationships:** `direct_report` → staff_database.id (manager), `buddy_coach` → staff_database.id, `session_bracket_fk` → session bracket config

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| first_name | text | NO | | |
| last_name | text | YES | | |
| dob | date | YES | | |
| lockeroom_email | text | YES | | |
| personal_email | text | YES | | |
| mobile_number | text | YES | | |
| client_drive_link | text | YES | | |
| workbook_id | text | YES | | |
| raw_data_code | text | YES | | |
| coach_name | text | YES | | Denormalised |
| role | text | YES | | e.g. results_manager, programming_coach |
| slack_channel_id | text | YES | | |
| staff_status | active_inactive | YES | 'active' | |
| style_relator | integer | YES | | |
| style_transformer | integer | YES | | |
| style_snc | integer | YES | | |
| style_specialist | integer | YES | | |
| style_wellness | integer | YES | | |
| home_gym | text | YES | | |
| tod_coaching | text | YES | | |
| rm_ceiling | numeric | YES | | Results manager client cap |
| supplementary_roles | text[] | YES | | e.g. nutrition_team, revenue_team |
| clientworkbook_links | text | YES | | |
| roles_ldp | text | YES | | |
| direct_report | uuid | YES | | Manager (FK to staff_database) |
| session_bracket_fk | uuid | YES | | |
| sb_selector | session_bracket_enum | YES | | |
| sb_recommended | session_bracket_enum | YES | | |
| kpi | text | YES | | |
| slack_prg_id | text | YES | | |
| employment_type | text | YES | 'FTE' | FTE, PTE, CASUAL etc. |
| updated_at | timestamp with time zone | YES | now() | |
| cpr_perform | numeric | YES | | |
| cpr_box | numeric | YES | | |
| slack_member_id | text | YES | | |
| state | text | YES | 'NSW' | NSW, VIC, etc. |
| buddy_coach | uuid | YES | | FK to staff_database |
| rgb_colour | text | YES | | |
| executive | boolean | YES | false | |

## Business Context

Source of truth for staff identity, role, employment type, and reporting (direct_report). Used for coach assignments on memberships, session expectations, scheduling, and org structure. hr_direct_report stores the formal manager–coach relationship; direct_report here is the same concept.

## Related Rules

- [Coach assignments](../../rules/coaching/coach-assignments.md), [RM ceiling](../../rules/coaching/rm-ceiling.md), [Direct reports](../../rules/hr/direct-reports.md)

## Common Queries

```sql
-- Active coaches with manager
SELECT id, coach_name, role, direct_report, employment_type
FROM staff_database
WHERE staff_status = 'active'
ORDER BY coach_name;
```
