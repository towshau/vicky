---
name: client-journey-diagram
description: Sync the Lockeroom Client Journey Excalidraw diagram from Supabase system_cj_config.
status: active
applies_to: all
domain: marketing
consumer: cursor
---

# Client Journey diagram

**Use only when** the user says "Client Journey" (or explicitly refers to the client journey diagram). Do not activate on "Lockeroom", "Excalidraw", or "resource links" alone.

## Summary

- **Source of truth:** Supabase table `system_cj_config` (journey_type, state, stage_name, resource_name, resource_link, staff_responsible_id).
- **Output:** Excalidraw file (e.g. `locker-room-client-journey.excalidraw`) in workspace or [client-journey repo](https://github.com/towshau/client-journey).
- **Sync:** Fetch rows from `system_cj_config`, map stage_name → element IDs (res1-1, mel-res1-1, etc.), update Resources (and optionally staff) bubbles in the .excalidraw JSON.

## Full instructions

For Cursor agents: use the **Client Journey** skill. Full step-by-step and stage→element mapping are in:

`~/.cursor/skills/client-journey-diagram/SKILL.md`

(Or the repo that contains the diagram; the skill may be loaded from the Cursor global skills directory.)
