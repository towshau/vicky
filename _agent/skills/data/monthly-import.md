---
name: monthly-import
description: Process monthly Scendar payroll hours or accounting (P&L) statement uploads into Supabase.
status: active
applies_to: all
domain: billing
consumer: cursor
---

# Monthly data import

**Use when** the user mentions uploading payroll, payroll hours, account transactions, reconciled statements, or monthly P&L data.

## Summary

- **Repo:** [helm_p-l](https://github.com/towshau/helm_p-l). Scripts run from that repo; ensure it is cloned and deps installed.
- **Payroll (CSV):** Columns Employee, Pay Item Type, Pay Item, Date, Units → `scripts/load_payroll_hrs.py` → table `fin_payroll_hrs`.
- **Accounting (Excel/CSV):** Scendar Account Transactions or per-category CSVs → `scripts/load_fin_pandl.py` → table `fin_pandl`.
- **Before load:** Check for existing data for that month in the target table; warn and confirm if duplicates would result.
- **Env:** `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`.

## Full instructions

For Cursor agents: use the **monthly-import** skill. Full steps (dedup check, entity/gym mapping, dry run, reporting) are in:

`~/.cursor/skills/monthly-import/SKILL.md`
