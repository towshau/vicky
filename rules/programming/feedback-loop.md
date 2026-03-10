---
title: Feedback Loop
domain: programming
version: 1.0
effective_date: 2026-03-09
applies_to: [bligh, bridge, collins]
last_updated: 2026-03-11
updated_by: Shaun
status: active
replaces: null
tags: [feedback, coach, order, exclusions, normalization]
---

# Feedback Loop

## Summary

Coach feedback corrects exercise order, series assignments, and exclusions in `programming_normalized_programs`. Corrections are applied immediately and become the baseline for the next generation run.

## Rules

### Feedback Flow

1. Engine generates a program (or normalization tool processes TB export).
2. Coach reviews in Retool or TeamBuildr.
3. Coach can: approve as-is, modify exercise order/series, flag an exercise for exclusion, or flag a rule issue.

### Where Feedback Is Stored

- **Exercise order and series corrections** → update `programming_normalized_programs.payload` immediately (series_label, series_assignment fields).
- **Exercise exclusions** → insert into `programming_exercise_exclusions`.
- **Rule issues** → escalate to Head Coach / Programming Lead for `programming_rules` update.

### Sync With member_tbresults

- Weekly diff: compare latest TB data against `programming_normalized_programs`.
- Same exercises → update weights/reps, keep corrected order.
- Minor change (1–2 exercises swapped mid-program) → slot new exercise into same position.
- Full week change → new program detected; archive old record, create new entry, infer order from rules until coach corrects.

### Engine Does Not Self-Modify Rules

- Feedback is reviewed by Head Coach / Programming Lead before rule changes.
- Persistent issues lead to `programming_rules` updates (Supabase) and vicky rule file updates.

## Site Exceptions

> No site-specific exceptions currently.

## Examples

**Example 1: Coach reorders series**

Engine places Bicep Curl as B1 and Leg Curl as C1. Coach swaps them. Payload updated immediately — next run uses corrected order.

**Example 2: Exercise flagged for exclusion**

Coach removes Barbell Hip Thrust from C-series for a member. Entry added to `programming_exercise_exclusions`. Next run excludes it.

**Example 3: Systematic issue**

Multiple coaches report B-series is too long. Programming Lead updates `max_b_series_sets` in `programming_rules`.

## Changelog

| Date       | Version | Change          | By    |
|------------|---------|-----------------|-------|
| 2026-03-09 | 1.0     | Initial version | Shaun |
| 2026-03-11 | 1.1     | Added sync/diff detail and payload correction flow | Shaun |
