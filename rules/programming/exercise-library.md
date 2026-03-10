---
title: Exercise Library
domain: programming
version: 1.0
effective_date: 2026-03-09
applies_to: [bligh, bridge, collins]
last_updated: 2026-03-09
updated_by: Shaun
status: active
replaces: null
tags: [exercise-library, approval, exclusions]
---

# Exercise Library

## Summary

Rules governing which exercises are available, how new exercises are approved, and which exercises should be avoided.

## Rules

### No New Exercises Without Approval

- Any new exercise must be:
  1. Posted in the Programming Slack channel, **and**
  2. Approved by Head Coach or Programming Lead
- Only then can it be added to programs.

### Exercises to Leave Out When Possible

- Walking lunges.
- Farmer carries.

### Exercise Library Source

- The `exercise_library` table in Supabase is the single source of truth (exercise_id, exercise_name, tags).
- It is built by a trigger from `member_tbhealthmax` and `member_tbresults`.
- The library is synced weekly to a Google Sheet for coach reference.

## Site Exceptions

> No site-specific exceptions currently.

## Examples

**Example 1: Coach wants to add a new exercise**

Coach posts "Nordic Hamstring Curl" in the Programming Slack channel. Head Coach approves. Exercise is then added to the library and can be used in programs.

**Example 2: Engine generating a program**

Engine checks `exercise_library` for available exercises. Walking lunges and farmer carries are deprioritised / excluded by default unless specifically overridden.

## Changelog

| Date       | Version | Change          | By    |
|------------|---------|-----------------|-------|
| 2026-03-09 | 1.0     | Initial version | Shaun |
