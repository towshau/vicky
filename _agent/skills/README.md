# Agent Skills — When to Use Which Capability

Skills are **reusable agent capabilities**: procedures and instructions for tasks like generating diagrams, importing data, or syncing config-driven views. They live here so any agent (Cursor, n8n, API) can discover and invoke them consistently.

## How skills are categorised

Skills are grouped by **capability type**, not by business domain:

| Type | Purpose | Examples |
|------|---------|----------|
| **reference** | Config-driven views; sync or render from a single source of truth (e.g. Supabase) | Client Journey diagram from `system_cj_config` |
| **data** | Ingest, transform, or sync bulk data into systems | Payroll hours, P&L/accounting uploads into Supabase |
| **generation** | Create artifacts: diagrams, images, documents | Excalidraw diagrams, Nano Banana 2 images |

Domain is in frontmatter (`domain: billing`, `domain: marketing`) so agents can filter by business area when needed. Use this README as the **index**: question/task → load the skill file(s) listed below.

---

## Quick lookup — Task / trigger → Skill

| User says / Task | Skill | File |
|------------------|--------|------|
| Client Journey, client journey diagram, sync resources from Supabase | Client Journey diagram | [reference/client-journey-diagram.md](reference/client-journey-diagram.md) |
| Payroll upload, payroll hours, Scendar payroll | Monthly import (payroll) | [data/monthly-import.md](data/monthly-import.md) |
| Account transactions, P&L upload, reconciled statement, monthly P&L | Monthly import (accounting) | [data/monthly-import.md](data/monthly-import.md) |
| Draw a diagram, Excalidraw, create editable diagram | Excalidraw diagram | [generation/excalidraw-diagram.md](generation/excalidraw-diagram.md) |
| Generate image, hyper-realistic image, Nano Banana, Kie.ai image | Nano Banana 2 images | [generation/nano-banana-images.md](generation/nano-banana-images.md) |

---

## By capability type

### reference/

Config-driven views; one source of truth (e.g. Supabase table), output is a diagram or structured view.

- [client-journey-diagram.md](reference/client-journey-diagram.md) — Sync Client Journey Excalidraw from `system_cj_config`.

### data/

Bulk ingest or sync into Lockeroom systems (Supabase, etc.).

- [monthly-import.md](data/monthly-import.md) — Payroll hours (CSV) and accounting/P&L (Excel or CSV) into `fin_payroll_hrs` and `fin_pandl`.

### generation/

Create new artifacts (diagrams, images, content).

- [excalidraw-diagram.md](generation/excalidraw-diagram.md) — Create or edit Excalidraw diagrams (editable .excalidraw JSON).
- [nano-banana-images.md](generation/nano-banana-images.md) — Hyper-realistic images via Nano Banana 2 (Gemini 3.1 Flash) / Kie.ai.

---

## How agents should use this folder

1. **Identify the task.** Use the quick lookup table above, or scan by capability type.
2. **Load the skill file.** Read the linked .md for that skill (progressive disclosure — don't load every skill).
3. **Follow the skill's "When to use" and steps.** Skills point to full instructions (e.g. Cursor global skills at `~/.cursor/skills/` or repo paths) where applicable.
4. **Respect frontmatter.** `status: active`, `applies_to` (gym/all), and `consumer` (cursor | n8n | api) where present.

When in doubt, prefer the **explicit rule in rules/** or **SOP in sops/** over a skill; skills are for capability invocation, not for overriding business rules.
