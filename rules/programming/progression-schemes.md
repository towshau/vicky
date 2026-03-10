---
title: Progression Schemes
domain: programming
version: 1.0
effective_date: 2026-03-09
applies_to: [bligh, bridge, collins]
last_updated: 2026-03-09
updated_by: Shaun
status: active
replaces: null
tags: [progression, rep-ranges, phases, duration]
---

# Progression Schemes

## Summary

Defines how rep ranges progress between program phases and how long each program lasts. The default progression is the same for all members unless overridden by goals, injuries, or strength phases.

## Rules

### Default Rep Progression

- Standard Lockeroom progression across phases: **10–12 → 8–10 → 6–8 → 4–6**.
- May be adjusted based on goals, injuries, or strength phases.
- First program starting reps are chosen from: 10–12 (most common), 8–10, 6–8, or 4–6.

### Program Duration

- **Standard program duration:** 6 weeks.
- **First program (new members only):** 4 weeks (earlier check-in).
- **Adjustable:** 4 to 6 weeks depending on the member.
- Admin extends the program at the end of the week based on the coach's selection.

### Sessions Per Week

- Next phase = same number of sessions per week (2D, 3D, 4D) as the previous program.
- No member-level master config; inherit from last program.
- First program fallback: determined at onboarding (2D, 3D, or 4D base program loaded).

## Site Exceptions

> No site-specific exceptions currently.

## Examples

**Example 1: Standard progression**

Member finishes Phase 1 at 10–12 reps. Phase 2 moves to 8–10 reps. Phase 3 to 6–8. Phase 4 to 4–6. Then cycle restarts or adjusts.

**Example 2: First program**

New member receives physicals data. Coach loads 3D base program at 10–12 reps, sets completion weeks to 4. After first program, subsequent programs default to 6 weeks.

## Changelog

| Date       | Version | Change          | By    |
|------------|---------|-----------------|-------|
| 2026-03-09 | 1.0     | Initial version | Shaun |
