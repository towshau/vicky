# Systems — External System Integration Docs

How each tool in the Lockeroom stack connects. Use for integration logic and agent context.

## Documented Systems

| System | Doc | Purpose |
|--------|-----|---------|
| Physical Report Pipeline | [physical-report-pipeline.md](physical-report-pipeline.md) | On-demand PDF generation: Retool → n8n → Supabase → Railway → email |

## Systems to document

| System | Doc | Purpose |
|--------|-----|---------|
| Supabase | [supabase.md](supabase.md) | Project config, RLS, naming |
| Retool | [retool.md](retool.md) | Dashboards, key queries |
| n8n | [n8n.md](n8n.md) | Workflows, webhooks |
| HubSpot | [hubspot.md](hubspot.md) | Pipelines, contact sync |
| Stripe | [stripe.md](stripe.md) | Customer/invoice mapping |
| Slack | [slack.md](slack.md) | Channels, bots |
| Teambuildr | [teambuildr.md](teambuildr.md) | Data sync, exercise library |
| Google Workspace | [google-workspace.md](google-workspace.md) | Drive, Gmail, Calendar |

Create each `.md` file from `_templates/system.md` when ready.
