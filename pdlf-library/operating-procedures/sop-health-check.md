---
title: "sop-health-check"
updated: "2026-10-24"
doc-id: "mb-af372f72"
---
# SOP: Health Check

The one procedure that checks a business's setup is sound before PDLF works on it. Agent-facing.

## When it runs

- At the start of entry points 04 to 10, before any other work.
- At the end of Step 11, as its self-audit.

Both use this procedure unchanged, so there is only one idea of what "a sound setup" means.

## What it checks

Run every check, in this order, for the business `{slug}` and every app folder it has. Never stop at the first failure: run them all, then report.

1. **The ledger is reachable.** Connect to database `pdlf` on port 5433 through the PowerShell bridge in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). All seven tables exist: `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`, `triage_findings`.
2. **The business row matches the disk.** The `projects` row for `{slug}` exists, and every path and GBrain source name it records exists on disk and in GBrain under that name.
3. **Each app folder is a linked Anvil app.** For each of `{slug}-app1`, `{slug}-app2`, `{slug}-app3` and `{slug}-app5` that has been created (an app folder holding only the template's placeholder is an app not yet created, and is skipped): it is a Git repository, its remote is `https://github.com/sassycomapp/{slug}-app{n}`, and it holds `anvil.yaml`.
4. **Each app folder is up to date.** After `git fetch`, the folder is not behind GitHub, so nothing made in the Anvil editor is waiting to be pulled.
5. **Each app folder keeps secrets out.** Its `.gitignore` excludes `.env`, credentials and test output.
6. **The project library is sound.** `C:\dev\dev-{slug}\{slug}-project-library` is a Git repository linked to `https://github.com/sassycomapp/{slug}-project-library`, has every folder of the project template (`C:\dev\project-template\dev-(SLUG)\(slug)-project-library\`), including `pdlf-tickets\` and `pdlf-outputs\` with one folder per step.
7. **The project library is registered and committed.** It is the GBrain source `{slug}-project-library`, it has the commit hook, and it is on the `commit-all` list.
8. **The Matt Pocock configuration is right.** The project's Matt Pocock skills configuration points to the project library's `docs-local\GLOSSARY.md` and `adr-local`.
9. **The Anvil command-line tool answers.** `anvil version` runs, because every Anvil skill validates its work with `anvil --json validate`.

## What it reports

- One line per check: `PASS` or `FAIL`, with the reason for every failure.
- A last line: `ALL PASS` or `NOT READY`.

## What happens after

- If every check passes, the work continues.
- If any check fails, the agent stops. It fixes nothing without David's permission. It sets out each failure as a deviation, with its options, and David decides. Work does not start until every check passes.

## Why

A broken setup found late costs far more than one found first: work done on an unlinked folder or an unregistered library is lost or invisible. Checking everything, every time, means PDLF never builds on a foundation it has not verified.
