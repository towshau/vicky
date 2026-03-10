# member_tbresults

> Raw exercise data from TeamBuildr export. One row = one set of one exercise. Source of truth for what was assigned and completed; does NOT contain exercise order or series assignments.

## Quick Reference

- **Rows:** ~13,821
- **Primary key:** `id` (bigint, auto-increment)
- **Key relationships:** `member_id` → member_database.id

## Columns

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | bigint | NO | PK (auto-increment) |
| member_id | uuid | YES | FK to member_database.id |
| member_name | text | YES | Denormalised |
| exercise_name | text | NO | Full exercise name |
| assigned_date | date | YES | Date workout was assigned; identifies the training day |
| completed_date | date | YES | Date member completed it |
| set_number | numeric | YES | Set within this exercise (1, 2, 3…) |
| result | text | YES | Weight or value achieved |
| reps | numeric | YES | Reps performed |
| workout_id | numeric | YES | TeamBuildr workout ID; one per exercise per day |
| tags | text | YES | Exercise tag (e.g. "Vertical Press", "Horizontal Pull") |

## Grain

One row per **set** per exercise per day per member. A 3-set exercise = 3 rows. Unilateral exercises may double (left + right).

## Missing From TB Export

- Exercise order / sequence within a session
- Series assignment (A, B, C)
- Pairing information (which exercises are supersetted)

These are inferred by the normalization tool and stored in `programming_normalized_programs`.

## Program Detection

- No phase or program_id column.
- Same exercises repeat for 4–6 weeks = same program.
- Full week's exercises change = new program.
- Mid-week 1–2 exercise swaps = adjustment, not new program.
- Group by `member_id` + `assigned_date` to identify one training day.
- A 3D member has 3 distinct assigned_dates per week.

## Related Rules

- [Engine rules](../../rules/programming/engine-rules.md), [Feedback loop](../../rules/programming/feedback-loop.md)

## Common Queries

```sql
-- Latest week of training for a member
SELECT exercise_name, assigned_date, set_number, reps, result, tags
FROM member_tbresults
WHERE member_id = :id AND assigned_date >= current_date - interval '7 days'
ORDER BY assigned_date, workout_id, exercise_name, set_number::int;
```
