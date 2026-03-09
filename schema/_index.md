| Table | Schema | Row count | Comment |
|-------|--------|-----------|---------|
| public._schedule_preferences_backup |  | 0 |  |
| public.admin_onboarding_tasks |  | 53 | Tracks onboarding tasks for staff members |
| public.admin_roles |  | 1 | Configuration table for admin role assignments |
| public.admin_sop |  | 0 |  |
| public.admin_tickets |  | 100 |  |
| public.allcontacts_hubspot |  | 142 |  |
| public.audit_revenue_team_updates |  | 0 |  |
| public.biomap_measurement_dimensions |  | 0 | Core dimension types for measurements (e.g., concentration, ratio, activity) |
| public.biomap_measurement_types |  | 0 | Biomarker definitions with canonical units |
| public.biomap_measurement_unit_conversions |  | 0 | Conversion formulas between units: normalized = raw × multiplier + offset |
| public.biomap_reference_ranges |  | 0 | Reference ranges by measurement type, unit, sex, and age |
| public.biomap_responses |  | 1 | BIOMAP Client Questionnaire responses |
| public.biomap_supplements |  | 0 |  |
| public.biomap_unit_aliases |  | 0 | Normalized text aliases enabling flexible unit text matching |
| public.biomap_units |  | 0 | Canonical unit definitions linked to dimensions |
| public.call_links |  | 0 | Tidycal or Booking Links |
| public.call_types |  | 0 | Externals Calls to Members |
| public.cardio_workouts |  | 0 |  |
| public.coach_3month_review |  | 0 |  |
| public.coach_core_product_survey |  | 0 |  |
| public.coach_monthly_report |  | 0 |  |
| public.coach_perf_reviews |  | 0 |  |
| public.coach_pr_report |  | 0 |  |
| public.coach_rm_intensives |  | 0 |  |
| public.coach_session_actual |  | 956 | completed sessions |
| public.coach_session_expectation_log |  | 38 |  |
| public.coach_slack_channel_map |  | 0 |  |
| public.coach_survey |  | 0 |  |
| public.coach_tech_intensives |  | 15 |  |
| public.coach_wcr_logging |  | 0 |  |
| public.coach_weekly_hours_snapshot |  | 19 |  |
| public.exercise_library |  | 820 | Unique exercises from member_tbhealthmax with names and tags from member_tbresults. |
| public.feedback_cleaning |  | 4 | Stores survey responses for Gym Cleanliness & Maintenance. |
| public.fin_pandl |  | 0 | Unified P&L transactions by gym and category from accountant exports |
| public.fin_payroll_hrs |  | 2463 | Payroll hours from Scendar Payroll Activity Details export; date column used with inclusive range for cumulative hours query. |
| public.google_reviews |  | 0 |  |
| public.holds_policies |  | 0 |  |
| public.hr_direct_report |  | 14 | Tracks HR direct report relationships between managers and coaches |
| public.hubspot_created_reco |  | 522 |  |
| public.lead_referral |  | 2 |  |
| public.management_velocity_board |  | 0 |  |
| public.manual_first_vo2_boxing |  | 0 | Manual entries for first VO2 boxing (trials/non-members) so they appear in the report without a membership. |
| public.member_addons |  | 8 |  |
| public.member_batch_attendance |  | 0 |  |
| public.member_biomap |  | 0 |  |
| public.member_biomap_results |  | 0 | Fact table storing all measurements with both raw and normalized values |
| public.member_biomap_unit_review_queue |  | 0 | Queue for handling unrecognized units requiring manual review |
| public.member_boxing_list |  | 0 |  |
| public.member_boxing_physicals |  | 0 | Stores physical performance data submissions for boxing clients |
| public.member_call_status |  | 27 |  |
| public.member_cardio_time_trials |  | 0 | Stores cardio time trial test results for members with coach tracking |
| public.member_cardio_workout_log |  | 9 |  |
| public.member_coach_notes |  | 37 |  |
| public.member_daily_sessions_attended |  | 1385 |  |
| public.member_database |  | 782 | Master for all Members (Past & Present) |
| public.member_gym_flags |  | 0 |  |
| public.member_health_metrics |  | 124 |  |
| public.member_holds |  | 740 |  |
| public.member_holds_backup_20251124 |  | 0 |  |
| public.member_holds_staging |  | 0 |  |
| public.member_lcns |  | 1065 |  |
| public.member_memberhealth |  | 0 |  |
| public.member_memberships |  | 1598 | Tracks membership periods, stages, and staff assignments for each member. |
| public.member_myzone |  | 10 |  |
| public.member_newsale_metadata |  | 10 | Stores metadata for newly sold memberships, including financials, duration, sessions, and staff assignments. |
| public.member_not_renewing |  | 8 |  |
| public.member_parking_incident_log |  | 0 |  |
| public.member_parking_registration |  | 0 |  |
| public.member_physicals_raw |  | 535 |  |
| public.member_physicals_vo2_raw |  | 3 | VO2-only physicals for Craftmypdf; vo2_value from view_cardio_vo2_scores. |
| public.member_priority_booking |  | 0 |  |
| public.member_programs |  | 461 |  |
| public.member_renewal_meta |  | 15 | Stores metadata for renewed memberships, including financials, duration, sessions, and staff assignments. |
| public.member_staging |  | 0 |  |
| public.member_tbhealthmax |  | 4473 |  |
| public.member_tbresults |  | 13821 |  |
| public.member_vo2_milestones |  | 17 |  |
| public.member_vo2_session_summary |  | 780 |  |
| public.member_vo2credits |  | 0 |  |
| public.member_weekly_attendance_dd |  | 0 |  |
| public.membership_addons |  | 0 |  |
| public.membership_holds_tracker |  | 0 |  |
| public.membership_types |  | 63 | HIGH LEVEL - Non changing identities. Do not change pricing, T&Cs etc. |
| public.membership_versions |  | 0 | ADD NEW ROWS FOR CHANGES TO POLICIES, PRICES ETC. Change old version to 'inactive' and the new version will automatically be set to 'active' |
| public.ops_cleaning_sop |  | 136 |  |
| public.ops_consumables |  | 31 |  |
| public.payment_statuses |  | 0 |  |
| public.payment_success_tracker |  | 150 |  |
| public.physicals_config |  | 0 | Stores VO2 threshold values by gender and age category for physical assessments |
| public.physicals_quarterly_cycles |  | 0 | Stores quarterly cycle definitions for physical assessments |
| public.physicals_scoring_lookup |  | 0 | Lookup table for converting raw physical test values to standardized scores (0-10) based on test type, gender, and age group |
| public.physicals_stages_config |  | 228 | Stage thresholds (1–4) for physicals tests by age bracket and gender. Lower stage = worse, higher = better. |
| public.programming_concept2 |  | 0 |  |
| public.programming_exercise_exclusions |  | 0 | Exercises to exclude per member (injury, preference, etc.); engine never assigns these. |
| public.programming_feedback |  | 0 | Coach feedback on generated programs; feeds back into exclusions and rule tuning. |
| public.programming_generated |  | 2 | Generated program per member per run; view in Retool, PDF export on demand. |
| public.programming_past_programs_staging |  | 8 | Normalised past program per member per run; view in Retool, optional PDF export. |
| public.programming_progression_schemes |  | 12 | Config for rep-range progression; engine picks rows by gym/name/goal. |
| public.programming_removal_requests |  | 0 | Admin reports exercise no longer exists; senior coach approves/rejects before any delete. |
| public.programming_rules |  | 15 | Engine rules: load where gym = :gym or gym is null, active = true; higher priority overrides. |
| public.renewal_reminders_log |  | 0 |  |
| public.rolling_schedule_preferences |  | 1171 |  |
| public.sale_types |  | 0 |  |
| public.sales_schedule |  | 0 |  |
| public.schedule_audit_log |  | 0 |  |
| public.schedule_block_config |  | 0 |  |
| public.schedule_block_metadata |  | 0 |  |
| public.schedule_block_weight_config |  | 0 |  |
| public.schedule_calendar_blocks |  | 0 |  |
| public.schedule_day_open_config |  | 0 |  |
| public.schedule_final |  | 0 |  |
| public.schedule_periods |  | 2 |  |
| public.schedule_preferences |  | 0 |  |
| public.schedule_proposed |  | 0 |  |
| public.session_forecast_next_14_days |  | 27336 | Stores 14-day ahead forecasts for session attendance with capacity utilization and risk flags |
| public.staff_database |  | 39 | Master Database for all base information |
| public.staff_leave_confirmed |  | 27 |  |
| public.staff_leave_requests |  | 4 |  |
| public.staff_onboarding |  | 307 | Individual onboarding tasks for staff members, copied from admin_onboarding_tasks templates |
| public.staff_personal_vision |  | 2 | Stores personal vision form submissions from staff members |
| public.staff_supplementary_additional_hours |  | 4 |  |
| public.staff_supplementary_default_hours |  | 0 |  |
| public.stg_member_health_metrics |  | 0 |  |
| public.stripe_customers |  | 0 |  |
| public.stripe_customers_staging |  | 0 |  |
| public.stripe_invoices |  | 5111 |  |
| public.stripe_transactions |  | 0 |  |
| public.survey_newclient_nps |  | 0 |  |
| public.system_bracket_policy_rules |  | 0 |  |
| public.system_cj_config |  | 26 | Config for Lockerroom client journey diagram: resources and staff per stage. Sync to Excalidraw via Client Journey skill. |
| public.system_config |  | 0 |  |
| public.system_member_health_config |  | 0 |  |
| public.teambuildr_completion_dd |  | 0 |  |
| public.tech_docs |  | 0 |  |
| public.unpaid_sessions |  | 0 | Operational tracking table for unpaid member sessions. Used by Admin to identify, review, and resolve sessions that were attended but not charged. Supports follow-ups, payment recovery workflows, and Retool reporting. |
| public.view_attendance_weekly_26_mvp_csu |  | 90 |  |
| public.view_data_attendance_26_mvp_csu |  | 384 |  |
| public.webhook_error_log |  | 0 |  |
| public.work_calendar |  | 0 |  |
| public.work_estimations |  | 0 |  |
