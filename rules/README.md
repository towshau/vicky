# Rules — Business Rules by Domain

Business rules are the "law" of how Lockeroom operates. They are grouped by **domain** (what area of the business), not by department. Start here to see what domains exist; then open a domain folder and read its README before loading specific rule files.

## Domains

| Domain | Folder | Description |
|--------|--------|-------------|
| Memberships | [memberships/](memberships/) | Lifecycle, primary/secondary, pricing, holds, renewals, cancellations, new sale, add-ons |
| Coaching | [coaching/](coaching/) | Session expectations, brackets, RM ceiling, late cancel/no show, reviews, WCR, coach assignments |
| Billing | [billing/](billing/) | Payment plans, Stripe reconciliation, unpaid sessions, payroll |
| Scheduling | [scheduling/](scheduling/) | Block preferences, day config, proposed-to-final schedule flow |
| Programming | [programming/](programming/) | Progression schemes, exclusions, engine rules, feedback, exercise library |
| Physicals | [physicals/](physicals/) | Scoring, quarterly cycles, VO2 milestones |
| Sales | [sales/](sales/) | HubSpot pipelines, lead referral, trial conversion |
| HR | [hr/](hr/) | Onboarding, leave, direct reports, personal vision, supplementary roles |
| Operations | [operations/](operations/) | Cleaning SOP rules, parking, member health scoring, Google reviews |

## Rule file format

Rule files use YAML frontmatter (`title`, `domain`, `version`, `effective_date`, `applies_to`, `last_updated`, `status`, `tags`). Use `_templates/rule.md` when creating new rules. Only apply rules where `status: active` and `effective_date` is in the past.
