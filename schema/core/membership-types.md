# membership_types

> High-level membership identities (e.g. 2x/week, 3x/week). Do not change pricing or T&Cs here; use membership_versions for that.

## Quick Reference

- **Rows:** ~63
- **Primary key:** `id` (uuid)
- **Key relationships:** Referenced by member_memberships.membership_type_id and membership_versions.membership_type_id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| name | text | YES | | Display name |
| session_frequency_per_week | integer | YES | | |
| session_total | integer | YES | | |
| category | membership_category_enum | YES | | all_inclusive, boxing_only, etc. |
| created_at | timestamp without time zone | YES | now() | |
| sort_order | integer | YES | | |
| tod_category | tod_category_enum | YES | | on_peak, off_peak, online |

## Business Context

Stable identity for a membership “product” (e.g. “2x per week”). Pricing, duration, and terms are versioned in membership_versions. Reference data for dropdowns and reporting; see reference/membership-types.md for full list.

## Related Rules

- [Pricing](../../rules/memberships/pricing.md), [Add-ons](../../rules/memberships/addons.md)

## Common Queries

```sql
SELECT id, name, session_frequency_per_week, session_total, category, tod_category
FROM membership_types
ORDER BY sort_order, name;
```
