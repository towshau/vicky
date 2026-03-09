# payment_success_tracker

> Tracks payment plans (split payments): agreed price, due dates, amounts per instalment, and paid-through date.

## Quick Reference

- **Rows:** ~148
- **Primary key:** `id` (uuid)
- **Key relationships:** `member_id` → member_database.id, `membership_type_id` → membership_types.id

## Columns

| Column | Type | Nullable | Default | Description |
|--------|------|----------|--------|-------------|
| id | uuid | NO | gen_random_uuid() | Primary key |
| member_id | uuid | NO | | |
| membership_type_id | uuid | YES | | |
| payment_date | text | YES | | First payment date |
| amount | numeric(10,2) | NO | | Total or first amount |
| sale_type | text | YES | | |
| payment_status | text | NO | 'Awaiting payment' | |
| payment_method | text | NO | | |
| product_description | text | YES | | |
| notes | text | YES | | |
| created_at | timestamp with time zone | NO | now() | |
| payment_plan_label | text | YES | | |
| payment_date_2 … payment_date_12 | text | YES | | Instalment dates |
| amount_2 … amount_12 | numeric | YES | | Instalment amounts |
| price_agreed | numeric | YES | | |
| gym | text | YES | | |
| member_firstname | text | YES | | |
| member_lastname | text | YES | | |
| start_date | date | YES | | |
| end_date | date | YES | | |
| paid_through_date | date | YES | | Last date paid through |
| paid_through_updated_at | timestamp with time zone | YES | now() | |

## Business Context

Used for multi-instalment payment plans. payment_date_2..12 and amount_2..12 hold the schedule; paid_through_date is updated as payments are received. Links to Stripe and member_memberships for reconciliation.

## Related Rules

- [Payment plans](../../rules/billing/payment-plans.md)

## Common Queries

```sql
-- Plans with upcoming or overdue payments
SELECT member_id, member_firstname, member_lastname, payment_status, paid_through_date, start_date, end_date
FROM payment_success_tracker
WHERE payment_status != 'Paid' AND end_date >= CURRENT_DATE;
```
