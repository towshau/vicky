# programming_normalized_programs

> Enriched layer on top of member_tbresults. Adds series labels (A1, B1, C1), exercise order, and pairings missing from TeamBuildr exports. Updated by normalization tool and coach feedback. Engine reads this as the baseline for generating the next program.

## Quick Reference

- **Rows:** 8
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id

## Columns

| Column | Type | Nullable | Description |
|--------|------|----------|-------------|
| id | uuid | NO | PK |
| run_id | uuid | NO | Groups all members in one normalization run |
| member_id | uuid | NO | FK to member_database.id |
| assigned_to | uuid | YES | Optional coach filter |
| payload | jsonb | NO | Normalised program structure (see below) |
| created_at | timestamptz | NO | Record creation |
| updated_at | timestamptz | NO | Last update (sync or coach feedback) |

## Payload Structure

```json
{
  "sessions": [
    {
      "day": "2025-01-14",
      "assigned_date": "2025-01-14",
      "exercises": [
        {
          "series_label": "A1",
          "exercise_name": "Chin Up - Medium Grip",
          "exercise_id": "1200726784",
          "tags": "Vertical Pull",
          "series_assignment": ["A", "B"],
          "sets": [{"set_number": 1, "reps": 6, "result": "0"}]
        }
      ]
    }
  ]
}
```

**Key fields:** `series_label` (A1, A2, B1, C1, Warm Up) = order + series. `series_assignment` = pairing groups. `exercise_id` = TeamBuildr ID.

## Weekly Sync/Diff

1. Pull latest week from member_tbresults per active member.
2. Compare exercise lists against this table's payload.
3. Same exercises → update weights/reps, keep order.
4. Minor change → slot new exercise into same position.
5. Full week change → new program; archive old, create new, infer order from rules.

## Coach Feedback

Corrections to order or series update the payload immediately. Corrected version becomes the baseline for next generation.

## Related Rules

- [Feedback loop](../../rules/programming/feedback-loop.md), [Engine rules](../../rules/programming/engine-rules.md)
