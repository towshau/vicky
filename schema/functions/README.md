# Schema — Functions

Index of RPC functions and triggers in the public schema. Many are from Postgres extensions (btree_gist, pg_trgm, pg_net, etc.); application functions are listed below. No individual function docs yet.

## Application functions (selected)

- **Member / membership:** fn_resolve_member_and_membership, fuzzy_find_member_id_from_fullname, auto_populate_member_id, auto_populate_membership_id, propagate_member_name_change, set_member_fullname, sync_member_status_on_change, sync_member_coach_from_handoff_coach, sync_membership_gym_from_member
- **Stripe:** backfill_stripe_customers_member_id, backfill_stripe_invoices_member_id, trg_stripe_invoices_auto_assign_member_id, trg_stripe_customers_auto_assign_member_id, populate_stripe_non_money_events_billing_name
- **Holds / renewals:** set_hold_version_from_membership, set_holds_policy_from_agreement_newsale, set_holds_policy_from_agreement_renewal, set_good_bad_from_membership, calculate_member_not_renewing_dates, recalc_member_newsale_metadata_totals, recalc_member_renewal_meta_totals
- **Physicals / VO2:** auto_calculate_physicals_scores, get_physicals_score, get_quarter_cycle_for_date, get_vo2_report_payload, check_vo2_milestones, mark_vo2_notification_sent, sync_last_physicals_date, sync_tb_physicals_to_member_physicals_raw
- **Coaching / schedule:** coach_session_tracker_fill_staff_id, run_coach_weekly_snapshot, get_role_hours_for_week, get_staff_sup_hours_for_week, refresh_sb_recommended_perform, sync_to_rolling, auto_extend_preferences
- **Onboarding / HR:** create_onboarding_tasks_for_staff, create_staff_onboarding_tasks, sync_staff_onboarding_from_template, expand_staff_leave_requests, expand_leave_request_to_confirmed
- **Admin / tickets:** auto_populate_assignee_from_department, fire_webhook_on_admin_ticket_status, fire_webhook_on_admin_ticket_priority
- **Other:** set_payment_status_from_paid_through, set_gym_flags, update_gr_flag, find_docs_for_object, get_docs_needing_review

## Triggers (trg_*)

Trigger functions fire on table insert/update/delete. Examples: trg_member_holds_autofill_end_date, trg_member_journey_stage_webhook, trg_member_renewal_complete, trg_stripe_invoices_set_updated_at.

## Adding function docs

Create a new `.md` file in this folder describing purpose, arguments, return value, and when it’s called (trigger or RPC).
