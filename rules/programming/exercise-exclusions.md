---
title: Exercise Exclusions
domain: programming
version: 1.0
effective_date: 2026-03-09
applies_to: [bligh, bridge, collins]
last_updated: 2026-03-09
updated_by: Shaun
status: active
replaces: null
tags: [exclusions, injuries, contraindications, member-specific]
---

# Exercise Exclusions

## Summary

Member-specific exercise exclusions based on injuries, contraindications, preferences, or coach feedback. The engine must never assign an excluded exercise.

## Rules

### Exclusion Sources

- **member_database columns:** `injuries`, `goals`, `medications`, `contraindications` — free-text fields on the member record.
- **programming_exercise_exclusions table:** Structured per-member exclusions (member_id, exercise_id, reason, added_by, created_at).
- **Coach feedback:** Coaches can flag exercises to exclude via the feedback loop; these get added to exclusions.

### Engine Behaviour

- Before assigning any exercise, the engine checks the member's exclusion list.
- Excluded exercises are **never** assigned, regardless of rule priority.
- If an exclusion removes a core movement pattern, the engine should substitute with an appropriate alternative from the same tag/category in `exercise_library`.

### Global Exclusions

- Walking lunges and farmer carries should be left out when possible (soft exclusion — can be overridden by coach).

## Site Exceptions

> No site-specific exceptions currently.

## Examples

**Example 1: Member with knee injury**

Member has "ACL reconstruction" in injuries. `programming_exercise_exclusions` lists Barbell Squat and Leg Extension. Engine substitutes with Leg Press (if allowed) or Goblet Squat.

**Example 2: Coach feedback exclusion**

Coach flags "Lat Pulldown causes shoulder pain for this member." Entry added to `programming_exercise_exclusions`. Next program generation excludes it automatically.

## Changelog

| Date       | Version | Change          | By    |
|------------|---------|-----------------|-------|
| 2026-03-09 | 1.0     | Initial version | Shaun |
