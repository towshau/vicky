# programming_rules

> Deterministic rules the engine loads before generating a program. Nullable `gym` column: NULL = all gyms, non-null = gym-specific override. Higher priority overrides lower for the same rule_key.

## Quick Reference

- **Rows:** 15
- **Primary key:** `id` (uuid)
- **No FK to member tables** — rules are loaded by gym, not by member.

## Columns

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | uuid | NO | PK |
| gym | gym enum | YES | NULL = all gyms; non-null = gym-specific |
| name | text | YES | Human-readable label |
| category | text | YES | volume, progression, exercise_selection, structure, member_specific |
| rule_key | text | NO | Machine key for the engine |
| rule_value | jsonb | YES | Flexible payload (numbers, lists, objects) |
| priority | integer | NO | Higher overrides lower for same rule_key |
| active | boolean | NO | Only load where true |
| source | text | YES | Who/what created: 'manual', 'seed', later 'agent:slack_feedback' |
| source_ref | text | YES | Link to origin (Slack URL, coach note ID) |
| created_at | timestamptz | NO | |
| updated_at | timestamptz | NO | |

## Load Query

```sql
SELECT * FROM programming_rules
WHERE (gym = :gym OR gym IS NULL) AND active = true
ORDER BY priority DESC;
```

## Related Rules

- [Engine rules](../../rules/programming/engine-rules.md) — documents the logic.
- Narrative source: [programming-rules-source.md](https://github.com/towshau/programming_engine/blob/main/docs/programming-rules-source.md) in programming_engine repo.
