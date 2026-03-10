# Vicky — Lockeroom Second Brain

> **Repo:** [github.com/towshau/vicky](https://github.com/towshau/vicky)  
> **Codename:** Vicky  
> **Primary consumer:** Claude AI agents (n8n / API), with human readability  
> **Scope:** All of Lockeroom Gym — operations, coaching, sales, finance, HR, marketing  
> **Format:** Markdown with YAML frontmatter on rule files; plain markdown for reference docs

## Who Vicky Is

Vicky is the operational intelligence behind Lockeroom Gym. She lives in the systems — Slack, dashboards, automations, reports — and knows the business inside out. Her personality and behavioural rules are defined in [SOUL.md](SOUL.md). AI agents that answer questions or perform tasks as Vicky should read SOUL.md first.

## How to Navigate This Repo

- **Start here** — You're in the right place. This README is the entry point.
- **Rules** — Business rules (the "law" of how Lockeroom operates) live in [rules/](rules/). Each domain (memberships, coaching, billing, etc.) has a README that indexes its rule files.
- **Schema** — Database table and view documentation in [schema/](schema/). [schema/_index.md](schema/_index.md) lists every table; [schema/core/](schema/core/) has detailed docs for the 14 core tables.
- **SOPs** — Standard operating procedures (how to do things) in [sops/](sops/), grouped by role (coaching, sales, admin, management).
- **Reference** — Static lookup data (membership types, enums, site config) in [reference/](reference/).
- **Agent instructions** — How AI agents should use this repo: [_agent/AGENT_INSTRUCTIONS.md](_agent/AGENT_INSTRUCTIONS.md) and [_agent/domain-map.md](_agent/domain-map.md).
- **Skills** — Reusable agent capabilities (diagrams, imports, image generation) in [_agent/skills/](_agent/skills/). See [_agent/skills/README.md](_agent/skills/README.md) for when to use which skill.

## Key Files at Root

| File | Purpose |
|------|---------|
| [SOUL.md](SOUL.md) | Vicky's identity, personality, communication style |
| [CHANGELOG.md](CHANGELOG.md) | Chronological log of rule/SOP/schema changes |
| [GLOSSARY.md](GLOSSARY.md) | Lockeroom-specific terminology |
| [MAINTENANCE.md](MAINTENANCE.md) | How to keep the second brain current (automation, review cadence) |

## Design Philosophy

The structure is organised by **knowledge type** (rules vs schema vs SOPs) and then by **domain** (memberships, coaching, billing, etc.), not by department. That way an agent answering "can this member go on hold?" can pull from memberships + billing + scheduling rules without wondering which department owns the answer.

Progressive disclosure: read folder READMEs first, then load only the specific rule/schema/SOP files needed. Don't pull the entire brain into context.
