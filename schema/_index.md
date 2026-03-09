# Schema Index — All Tables

One line per table. Category: **core** (detailed doc in [core/](core/)) or **supporting** (listed here only). Row counts and comments from Supabase; refresh weekly (see [MAINTENANCE.md](../../MAINTENANCE.md)).

| Table | Category | Rows | Description |
|-------|----------|------|-------------|
| coach_session_actual | core | 956 | completed sessions |
| hr_direct_report | core | 14 | Tracks HR direct report relationships between managers and coaches |
| member_daily_sessions_attended | core | 1385 | |
| member_database | core | 782 | Master for all Members (Past & Present) |
| member_holds | core | 740 | |
| member_lcns | core | 1065 | |
| member_memberships | core | 1596 | Tracks membership periods, stages, and staff assignments for each member. |
| member_physicals_raw | core | 535 | |
| member_programs | core | 461 | |
| membership_types | core | 63 | HIGH LEVEL - Non changing identities. Do not change pricing, T&Cs etc. |
| membership_versions | core | 0 | ADD NEW ROWS FOR CHANGES TO POLICIES, PRICES ETC. Change old version to 'inactive' and the new version will automatically be set to 'active' |
| payment_success_tracker | core | 148 | |
| staff_database | core | 39 | Master Database for all base information |
| stripe_invoices | core | 5111 | |
| _schedule_preferences_backup | supporting | 0 | |
| admin_onboarding_tasks | supporting | 53 | Tracks onboarding tasks for staff members |
| admin_roles | supporting | 1 | Configuration table for admin role assignments |
| admin_sop | supporting | 0 | |
| admin_tickets | supporting | 99 | |
| allcontacts_hubspot | supporting | 139 | |
| audit_revenue_team_updates | supporting | 0 | |
| biomap_measurement_dimensions | supporting | 0 | Core dimension types for measurements (e.g., concentration, ratio, activity) |
| biomap_measurement_types | supporting | 0 | Biomarker definitions with canonical units |
| biomap_measurement_unit_conversions | supporting | 0 | Conversion formulas between units |
| biomap_reference_ranges | supporting | 0 | Reference ranges by measurement type, unit, sex, and age |
| biomap_responses | supporting | 1 | BIOMAP Client Questionnaire responses |
| biomap_supplements | supporting | 0 | |
| biomap_unit_aliases | supporting | 0 | Normalized text aliases enabling flexible unit text matching |
| biomap_units | supporting | 0 | Canonical unit definitions linked to dimensions |
| call_links | supporting | 0 | Tidycal or Booking Links |
| call_types | supporting | 0 | Externals Calls to Members |
| cardio_workouts | supporting | 0 | |
| coach_3month_review | supporting | 0 | |
| coach_core_product_survey | supporting | 0 | |
| coach_monthly_report | supporting | 0 | |
| coach_perf_reviews | supporting | 0 | |
| coach_pr_report | supporting | 0 | |
| coach_rm_intensives | supporting | 0 | |
| coach_session_expectation_log | supporting | 38 | |
| coach_slack_channel_map | supporting | 0 | |
| coach_survey | supporting | 0 | |
| coach_tech_intensives | supporting | 15 | |
| coach_wcr_logging | supporting | 0 | |
| coach_weekly_hours_snapshot | supporting | 19 | |
| exercise_library | supporting | 820 | Unique exercises from member_tbhealthmax with names and tags from member_tbresults. |
| feedback_cleaning | supporting | 4 | Stores survey responses for Gym Cleanliness & Maintenance. |
| fin_pandl | supporting | 0 | Unified P&L transactions by gym and category from accountant exports |
| fin_payroll_hrs | supporting | 2463 | Payroll hours from Scendar Payroll Activity Details export |
| google_reviews | supporting | 0 | |
| holds_policies | supporting | 0 | |
| hubspot_created_reco | supporting | 522 | |
| lead_referral | supporting | 2 | |
| management_velocity_board | supporting | 0 | |
| manual_first_vo2_boxing | supporting | 0 | Manual entries for first VO2 boxing (trials/non-members) |
| member_addons | supporting | 8 | |
| member_batch_attendance | supporting | 0 | |
| member_biomap | supporting | 0 | |
| member_biomap_results | supporting | 0 | Fact table storing all measurements with both raw and normalized values |
| member_biomap_unit_review_queue | supporting | 0 | Queue for handling unrecognized units requiring manual review |
| member_boxing_list | supporting | 0 | |
| member_boxing_physicals | supporting | 0 | Stores physical performance data submissions for boxing clients |
| member_call_status | supporting | 27 | |
| member_cardio_time_trials | supporting | 0 | Stores cardio time trial test results for members with coach tracking |
| member_cardio_workout_log | supporting | 9 | |
| member_coach_notes | supporting | 33 | |
| member_gym_flags | supporting | 0 | |
| member_health_metrics | supporting | 121 | |
| member_holds_backup_20251124 | supporting | 0 | |
| member_holds_staging | supporting | 0 | |
| member_memberhealth | supporting | 0 | |
| member_myzone | supporting | 10 | |
| member_newsale_metadata | supporting | 10 | Stores metadata for newly sold memberships |
| member_not_renewing | supporting | 8 | |
| member_parking_incident_log | supporting | 0 | |
| member_parking_registration | supporting | 0 | |
| member_physicals_vo2_raw | supporting | 3 | VO2-only physicals for Craftmypdf |
| member_priority_booking | supporting | 0 | |
| member_renewal_meta | supporting | 13 | Stores metadata for renewed memberships |
| member_staging | supporting | 0 | |
| member_tbhealthmax | supporting | 4473 | |
| member_tbresults | supporting | 13821 | |
| member_vo2_milestones | supporting | 17 | |
| member_vo2credits | supporting | 0 | |
| member_weekly_attendance_dd | supporting | 0 | |
| membership_addons | supporting | 0 | |
| membership_holds_tracker | supporting | 0 | |
| ops_cleaning_sop | supporting | 136 | |
| ops_consumables | supporting | 31 | |
| payment_statuses | supporting | 0 | |
| physicals_config | supporting | 0 | Stores VO2 threshold values by gender and age category |
| physicals_quarterly_cycles | supporting | 0 | Stores quarterly cycle definitions for physical assessments |
| physicals_scoring_lookup | supporting | 0 | Lookup for converting raw physical test values to standardized scores |
| physicals_stages_config | supporting | 228 | Stage thresholds (1–4) for physicals tests by age bracket and gender |
| programming_concept2 | supporting | 0 | |
| programming_exercise_exclusions | supporting | 0 | Exercises to exclude per member; engine never assigns these |
| programming_feedback | supporting | 0 | Coach feedback on generated programs |
| programming_generated | supporting | 2 | Generated program per member per run |
| programming_past_programs_staging | supporting | 8 | Normalised past program per member per run |
| programming_progression_schemes | supporting | 12 | Config for rep-range progression |
| programming_removal_requests | supporting | 0 | Admin reports exercise no longer exists |
| programming_rules | supporting | 15 | Engine rules: load where gym = :gym or gym is null, active = true |
| renewal_reminders_log | supporting | 0 | |
| rolling_schedule_preferences | supporting | 1171 | |
| sale_types | supporting | 0 | |
| sales_schedule | supporting | 0 | |
| schedule_audit_log | supporting | 0 | |
| schedule_block_config | supporting | 0 | |
| schedule_block_metadata | supporting | 0 | |
| schedule_block_weight_config | supporting | 0 | |
| schedule_calendar_blocks | supporting | 0 | |
| schedule_day_open_config | supporting | 0 | |
| schedule_final | supporting | 0 | |
| schedule_periods | supporting | 2 | |
| schedule_preferences | supporting | 0 | |
| schedule_proposed | supporting | 0 | |
| session_forecast_next_14_days | supporting | 27336 | Stores 14-day ahead forecasts for session attendance |
| staff_leave_confirmed | supporting | 27 | |
| staff_leave_requests | supporting | 4 | |
| staff_onboarding | supporting | 307 | Individual onboarding tasks for staff members |
| staff_personal_vision | supporting | 2 | Stores personal vision form submissions from staff members |
| staff_supplementary_additional_hours | supporting | 4 | |
| staff_supplementary_default_hours | supporting | 0 | |
| stg_member_health_metrics | supporting | 0 | |
| stripe_customers | supporting | 0 | |
| stripe_customers_staging | supporting | 0 | |
| stripe_transactions | supporting | 0 | |
| survey_newclient_nps | supporting | 0 | |
| system_bracket_policy_rules | supporting | 0 | |
| system_cj_config | supporting | 26 | Config for Lockerroom client journey diagram |
| system_config | supporting | 0 | |
| system_member_health_config | supporting | 0 | |
| teambuildr_completion_dd | supporting | 0 | |
| tech_docs | supporting | 0 | |
| unpaid_sessions | supporting | 0 | Operational tracking for unpaid member sessions |
| webhook_error_log | supporting | 0 | |
| work_calendar | supporting | 0 | |
| work_estimations | supporting | 0 | |
