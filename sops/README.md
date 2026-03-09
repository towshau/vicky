# SOPs — Standard Operating Procedures

Human-facing procedures: how to do specific tasks. Grouped by **role** (coaching, sales, admin, management). The `admin_sop` table in Supabase tracks task scheduling; this folder holds the actual procedure content. Use `_templates/sop.md` when creating new SOPs.

## By role

| Role | Folder | Description |
|------|--------|-------------|
| Coaching | [coaching/](coaching/) | Renewal conversation, new client onboarding, cancellation, hold request, programming handoff, physicals |
| Sales | [sales/](sales/) | Lead follow-up, trial booking, new sale data entry |
| Admin | [admin/](admin/) | Daily tasks, Stripe payment follow-up, member data entry, ticket management |
| Management | [management/](management/) | Weekly review, monthly reporting, velocity board |

## SOP file format

Plain markdown with a header block: Role, Frequency, Estimated time, Systems used. Then Prerequisites, Steps, Common Mistakes, Related Rules.
