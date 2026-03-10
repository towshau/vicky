# programming_exercise_exclusions

> Per-member exercises the engine must never assign. Sourced from injuries, contraindications, and coach feedback.

## Quick Reference

- **Rows:** 0 (populated as coaches flag exclusions)
- **Primary key:** `id`
- **Key relationships:** `member_id` → member_database.id

## Business Context

Before assigning any exercise, the engine checks this table. Excluded exercises are never assigned regardless of rule priority. If an exclusion removes a core movement pattern, the engine substitutes from the same tag/category in exercise_library.

Global soft exclusions (walking lunges, farmer carries) are handled in programming_rules, not here.

## Related Rules

- [Exercise exclusions](../../rules/programming/exercise-exclusions.md), [Feedback loop](../../rules/programming/feedback-loop.md)
