# stripe_invoices

> Payment records synced from Stripe. One row per invoice; links to member and membership for reconciliation.

## Quick Reference

- **Rows:** ~5111
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_id` → member_memberships.id; stripe_invoice_id / stripe_customer_id are Stripe IDs

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| stripe_invoice_id | text | NO | | Stripe invoice ID |
| stripe_customer_id | text | YES | | |
| member_id | uuid | YES | | |
| membership_id | uuid | YES | | |
| status | text | NO | | draft, open, paid, void, uncollectible, failed |
| payment_method | text | YES | | |
| payment_date | timestamp with time zone | YES | | |
| amount_due | numeric | YES | | |
| currency | text | YES | 'aud' | |
| attempt_count | integer | YES | 0 | |
| next_payment_attempt | timestamp with time zone | YES | | |
| collection_method | text | YES | | |
| invoice_number | text | YES | | |
| hosted_invoice_url | text | YES | | |
| invoice_pdf_url | text | YES | | |
| created_at | timestamp with time zone | YES | now() | |
| updated_at | timestamp with time zone | YES | now() | |
| description | text | YES | | |
| customer_email | text | YES | | |
| amount_paid | numeric | YES | | |
| customer_name | text | YES | | |
| billing_name | text | YES | | |
| raw_event | jsonb | YES | | |
| stripe_subscription_id | text | YES | | |
| last_4_digits | text | YES | | |
| stripe_object_id | text | YES | | |
| stripe_event_id | text | YES | | |
| brand | text | YES | | |
| network | text | YES | | |
| invoice_id | text | YES | | |
| payment_intent_id | text | YES | | |
| charge_id | text | YES | | |
| invoice_item_id | text | YES | | |
| stripe_event_type | text | YES | | |
| due_date | text | YES | | |

## Business Context

Synced from Stripe via webhooks. Used for reconciliation with member_memberships and payment_success_tracker. status and payment_date drive “paid vs outstanding” reporting.

## Related Rules

- [Stripe reconciliation](../../rules/billing/stripe-reconciliation.md), [Payment plans](../../rules/billing/payment-plans.md)

## Common Queries

```sql
-- Paid invoices in last 30 days
SELECT member_id, customer_name, amount_paid, payment_date, status
FROM stripe_invoices
WHERE status = 'paid' AND payment_date >= CURRENT_DATE - INTERVAL '30 days'
ORDER BY payment_date DESC;
```
