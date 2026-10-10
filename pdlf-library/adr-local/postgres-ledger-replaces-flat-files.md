---
title: "postgres-ledger-replaces-flat-files"
doc-id: "mb-bca36603"
updated: "2026-10-10"
---
# ADR — PostgreSQL Ledger Replaces Flat-File State Management

**Status:** Accepted

**Date:** 2026-07-10

---

## Context

The PDLF system needs to track project progress, step completion, gate approvals,
deviations, and BFT checkpoint results across sessions. Prior versions (v2, v3) used
flat markdown files: a state file (snapshot), a devlog (audit trail), and per-step
completion reports (detail). These three files duplicated the same facts and could
silently disagree with each other.

## Decision

All PDLF progress is recorded in a dedicated Postgres database (`pdlf`), accessed via
role `pdlf_agent`. Six tables: `projects`, `steps`, `gates`, `deviations`, `bft_records`,
and `isc` (Ideal State Criteria). The Step Receipt is generated directly from the ledger
row just written — it IS the ledger row, formatted for reading.

## Consequences

- Referential integrity is enforced at the database level: step 19 cannot be recorded
  as complete if step 16 does not exist.
- No narrative gloss can diverge from what actually happened. The receipt is a
  snapshot of the row, not a separately composed summary.
- Requires PostgreSQL to be running. This is setup complexity for a non-technical
  user, accepted because the integrity guarantees justify it.
- Flat-file state management (state file, devlog, completion report) was built in v2
  and fully retired when the ledger proved superior.
