# member_physicals_raw

> Raw and scored physical assessment data per member per submission (grip, push-ups, VO2, vertical jump, chin hold, RSI, COH, InBody, Concept2, etc.).

## Quick Reference

- **Rows:** ~535
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_id` → member_memberships.id, `coach_id` → staff_database.id, `quarter_cycle_id` → physicals_quarterly_cycles

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| coach_id | uuid | YES | | |
| member_id | uuid | NO | | |
| created_at | timestamp with time zone | NO | now() | |
| updated_at | timestamp with time zone | NO | now() | |
| submission_date | date | YES | CURRENT_DATE | |
| membership_id | uuid | YES | | |
| age_at_assessment | integer | YES | | |
| grip_strength_value | numeric | YES | | |
| push_ups_value | numeric | YES | | |
| vo2_value | numeric(2,0) | YES | | |
| vertical_jump_value | numeric | YES | | |
| chin_hold_value | numeric | YES | | |
| rsi_value | numeric | YES | | |
| coh_value | numeric | YES | | |
| inbody_value | numeric | YES | | |
| concept2_value | numeric | YES | | |
| grip_strength_score | numeric | YES | | 0–10 etc. |
| push_ups_score | numeric | YES | | |
| vo2_score | numeric | YES | | |
| vertical_jump_score | numeric | YES | | |
| chin_hold_score | numeric | YES | | |
| rsi_score | numeric | YES | | |
| coh_score | numeric | YES | | |
| inbody_score | numeric | YES | | |
| concept2_score | numeric | YES | | |
| quarter_cycle_id | uuid | YES | | |
| goals | text | YES | | |
| injuries | text | YES | | |
| focus_program | text | YES | | |
| exercise_avoid | text | YES | | |
| hinge | text | YES | | |
| shoulder_flexion | text | YES | | |
| toe_touch | text | YES | | |
| squat | text | YES | | |
| program_notes | text | YES | | |
| pushups_complete | text | YES | | |
| chinhold_complete | text | YES | | |
| grip_strength_left | numeric | YES | | |
| grip_strength_right | numeric | YES | | |
| lateral_hop_complete | text | YES | | |
| left_lateral_hop | numeric | YES | | |
| right_lateral_hop | numeric | YES | | |
| picked_cardio | text | YES | | |
| bike_test_avg_watt | numeric | YES | | |
| member_name | text | YES | | Denormalised |
| source | text | NO | 'form' | |
| run_test_meters | numeric | YES | | |

## Business Context

One row per physicals submission. Raw values and scores (from physicals_scoring_lookup / physicals_stages_config) support reporting and VO2 milestones. member_database.last_physicals_date is derived from submission_date.

## Related Rules

- [Physicals scoring](../../rules/physicals/scoring.md), [Quarterly cycles](../../rules/physicals/quarterly-cycles.md), [VO2 milestones](../../rules/physicals/vo2-milestones.md)

## Common Queries

```sql
-- Latest physicals per member
SELECT DISTINCT ON (member_id) member_id, member_name, submission_date, vo2_value, vo2_score
FROM member_physicals_raw
ORDER BY member_id, submission_date DESC;
```
