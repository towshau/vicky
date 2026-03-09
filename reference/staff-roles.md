# Staff Roles — From staff_database and staff_roles Enum

Refreshed from Supabase (see [MAINTENANCE.md](../MAINTENANCE.md)). Distinct role and employment_type for active staff; supplementary_roles in staff_roles enum.

## Role × Employment Type (active staff)

| Role | Employment type |
|------|------------------|
| Admin | FTE |
| Advanced Coach | FTE |
| Casual Coach | FTE |
| CEO | FTE |
| Coach | FTE, CASUAL |
| CRO | FTE |
| Gym Manager | FTE |
| Head Boxing Coach | FTE |
| Head of Exercise | FTE |
| Maintenance | FTE |
| Marketing Manager | FTE |
| Operations Manager | FTE |
| Physiotherapist | FTE |

## staff_roles enum (supplementary roles)

results_manager, programming_coach, sales_team, nutrition_team, human_resources

These can appear in staff_database.supplementary_roles array for a single staff member.
