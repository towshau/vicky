# [table_name]

> One-line description of what this table stores and why it exists.

## Quick Reference

- **Rows:** ~[approximate count]
- **Primary key:** `[pk_column]` ([type])
- **Key relationships:** `[fk_column]` → [referenced table], …

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| … | … | … | … | … |

## Business Context

[Why this table exists, how it's used in the business, source of truth for what.]

## Related Rules

- [Rule or SOP that uses this table]

## Common Queries

```sql
-- [Short description of query]
SELECT ...
FROM [table_name]
WHERE ...;
```
