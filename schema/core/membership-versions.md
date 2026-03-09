# membership_versions

> Versioned pricing, duration, and T&Cs for each membership type. Add new rows for changes; set old version to inactive.

## Quick Reference

- **Rows:** ~0 (populate when versions are used)
- **Primary key:** `id` (uuid)
- **Key relationships:** `membership_type_id` → membership_types.id, `created_by` → staff_database.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| created_at | timestamp with time zone | NO | now() | |
| base_price | numeric | YES | | |
| sessions_per_week | smallint | YES | | |
| price_per_session | numeric | YES | | |
| cancellation_policy | text | YES | | |
| created_by | uuid | YES | | |
| holds_policy | text | YES | | |
| internal_notes | text | YES | | |
| is_active_version | boolean | YES | true | |
| membership_name | text | YES | | |
| inclusions | text | YES | | |
| updated_at | timestamp with time zone | YES | now() | |
| duration_weeks | smallint | YES | | |
| membership_duration | membership_duration_months_enum | YES | | |
| sessions_total | smallint | YES | | |
| membership_type_id | uuid | YES | | |
| sort_order | integer | YES | | |
| newsale_price_adjusted | numeric | YES | | |
| renewal_price_adjusted | numeric | YES | | |
| version_number | integer | NO | nextval(...) | |

## Business Context

When pricing or terms change, add a new row and set the previous row’s is_active_version to false. Do not edit pricing/T&Cs on existing rows. Automation (see MAINTENANCE.md) can flag new versions so rules/memberships/pricing.md can be updated.

## Related Rules

- [Pricing](../../rules/memberships/pricing.md), [Holds policy](../../rules/memberships/holds-policy.md)

## Common Queries

```sql
-- Active version per membership type
SELECT * FROM membership_versions
WHERE is_active_version = true
ORDER BY membership_type_id, version_number DESC;
```
