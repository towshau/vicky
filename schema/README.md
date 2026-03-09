# Schema — Database Documentation

Documentation for the Lockeroom Supabase database. Structure:

- **[ _index.md](_index.md)** — One-line listing of every table (name, category, row count, comment). Auto-refreshed from Supabase when automation is built (see [MAINTENANCE.md](../../MAINTENANCE.md)).
- **core/** — Detailed docs for the 14 core tables (member_database, staff_database, member_memberships, etc.). Each file has columns, relationships, business context, and common queries.
- **supporting/** — Other tables are listed in _index.md only; add individual docs here as needed.
- **views/** — Index of database views (see README in that folder).
- **functions/** — Index of RPC functions and triggers (see README in that folder).
- **enums/** — Index of custom enum types (see README in that folder).

## Naming conventions

- Table and column names: `snake_case`
- Denormalised names (e.g. `member_name` on a child table) are intentional for display and reporting; the source of truth is the referenced table.

## Core tables (documented in core/)

| Table | Doc file | Purpose |
|-------|----------|---------|
| member_database | [member-database.md](core/member-database.md) | Master member record |
| staff_database | [staff-database.md](core/staff-database.md) | Master staff record |
| member_memberships | [member-memberships.md](core/member-memberships.md) | Membership periods & stages |
| membership_types | [membership-types.md](core/membership-types.md) | High-level membership identities |
| membership_versions | [membership-versions.md](core/membership-versions.md) | Versioned pricing & T&Cs |
| member_holds | [member-holds.md](core/member-holds.md) | Hold periods and credits |
| stripe_invoices | [stripe-invoices.md](core/stripe-invoices.md) | Payment records |
| payment_success_tracker | [payment-success-tracker.md](core/payment-success-tracker.md) | Payment plan tracking |
| coach_session_actual | [coach-session-actual.md](core/coach-session-actual.md) | Completed sessions |
| member_programs | [member-programs.md](core/member-programs.md) | Programming pipeline |
| member_physicals_raw | [member-physicals-raw.md](core/member-physicals-raw.md) | Physical assessment data |
| member_daily_sessions_attended | [member-daily-sessions.md](core/member-daily-sessions.md) | Attendance |
| member_lcns | [member-lcns.md](core/member-lcns.md) | Late cancels and no shows |
| hr_direct_report | [hr-direct-report.md](core/hr-direct-report.md) | Manager/coach relationships |
