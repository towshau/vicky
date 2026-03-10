# programming_generated

> Engine output: one generated program per member per run. Contains the canonical program JSON with series labels, prescribed rep ranges, and metadata. Coach reviews in Retool; approved version feeds back into programming_normalized_programs as the new baseline.

## Quick Reference

- **Rows:** 2
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `run_id` groups all members in one generation run

## Columns

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | uuid | NO | PK |
| run_id | uuid | NO | Groups all members in one generation run |
| member_id | uuid | NO | FK to member_database.id |
| assigned_to | uuid | YES | Coach assignment for filter/export |
| sessions_per_week | integer | NO | 2, 3, or 4 |
| duration_weeks | integer | NO | Default 6; first program = 4 |
| phase_number | integer | YES | Phase in progression cycle (1–4) |
| scheme_name | text | YES | GPP, Hypertrophy, Strength, etc. |
| rep_range | text | YES | e.g. "10-12", "4-6" |
| changes_summary | text | YES | Human-readable diff from last phase |
| rules_applied | jsonb | YES | Array of rule_keys used during generation |
| payload | jsonb | NO | Canonical program JSON |
| created_at | timestamptz | NO | |
| updated_at | timestamptz | NO | |

## Payload Shape

```json
{
  "metadata": {
    "scheme": "GPP",
    "confidence": "high",
    "phase_order": 4,
    "current_rep_range": "6-8",
    "next_rep_range": "4-6",
    "exercise_behavior": "same_exercises"
  },
  "sessions": [
    {
      "day": 1,
      "exercises": [
        {
          "series_label": "A1",
          "exercise_name": "Press - Flat - Dumbbell",
          "exercise_id": "1182509177",
          "tags": "Horizontal Press",
          "sets": [{"set_number": 1, "reps": "4-6"}]
        }
      ]
    }
  ]
}
```

Same exercise shape as `programming_normalized_programs` but with prescribed rep ranges (string) instead of completed weights/reps. After member completes the program and TB exports results, the generated output becomes the basis for the next normalized record.

## Related Rules

- [Engine rules](../../rules/programming/engine-rules.md), [Progression schemes](../../rules/programming/progression-schemes.md), [Feedback loop](../../rules/programming/feedback-loop.md)
