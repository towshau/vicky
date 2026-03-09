# Domain Map — Question Type → Files to Load

Flat lookup for agents: given a question type or topic, which files should be loaded? Expand this as rule files are added.

---

## Memberships

| Question type | Load first | Then if needed |
|---------------|------------|----------------|
| Holds (eligibility, duration, credits) | rules/memberships/README.md | rules/memberships/holds-policy.md, schema/core/member-holds.md |
| Primary/secondary structure | rules/memberships/README.md | rules/memberships/primary-secondary.md, schema/core/member-memberships.md |
| Pricing, discounts, payment plans | rules/memberships/README.md | rules/memberships/pricing.md, rules/billing/payment-plans.md |
| Renewals (stages, assignee) | rules/memberships/README.md | rules/memberships/renewals.md |
| Cancellations, not renewing | rules/memberships/README.md | rules/memberships/cancellations.md |
| New sale pipeline | rules/memberships/README.md | rules/memberships/newsale-pipeline.md |
| Add-ons (VO2, boxing) | rules/memberships/README.md | rules/memberships/addons.md |

## Coaching

| Question type | Load first | Then if needed |
|---------------|------------|----------------|
| Session expectations from hours | rules/coaching/README.md | rules/coaching/session-expectations.md |
| Session brackets, scoring | rules/coaching/README.md | rules/coaching/session-brackets.md |
| RM client cap | rules/coaching/README.md | rules/coaching/rm-ceiling.md |
| Late cancel / no show | rules/coaching/README.md | rules/coaching/late-cancel-noshow.md, schema/core/member-lcns.md |
| Performance reviews | rules/coaching/README.md | rules/coaching/performance-reviews.md |
| WCR points | rules/coaching/README.md | rules/coaching/wcr.md |
| Coach assignments (RM, programming, handoff) | rules/coaching/README.md | rules/coaching/coach-assignments.md |

## Billing

| Question type | Load first | Then if needed |
|---------------|------------|----------------|
| Payment plans, split payments | rules/billing/README.md | rules/billing/payment-plans.md, schema/core/payment-success-tracker.md |
| Stripe reconciliation | rules/billing/README.md | rules/billing/stripe-reconciliation.md, schema/core/stripe-invoices.md |
| Unpaid sessions | rules/billing/README.md | rules/billing/unpaid-sessions.md |
| Payroll (Scendar, FTE/PTE) | rules/billing/README.md | rules/billing/payroll.md |

## Scheduling, Programming, Physicals, Sales, HR, Operations

*Add rows as rule files are created. Pattern: README first, then specific rule file and schema doc if needed.*
