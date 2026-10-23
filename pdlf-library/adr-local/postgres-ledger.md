---
title: "postgres-ledger"
doc-id: "mb-bca36603"
updated: "2026-10-23"
---
# ADR — The PostgreSQL Ledger Is PDLF's Only Register

**Status:** Accepted

---

## Context

PDLF must track every project's progress, step completions, gate approvals, deviations, BFT checkpoints and triage findings across sessions. Separate files for the same facts (a state snapshot, a log, per-step reports) duplicate one another and silently disagree.

## Decision

All PDLF progress is recorded in one PostgreSQL database, `pdlf`, reached through the role `pdlf_agent`, with seven tables: `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc` (Ideal State Criteria) and `triage_findings`. There is no other register: no dev log, no state file, no judgement trail. The Step Receipt is generated from the ledger row just written; it is that row, formatted for reading. Detail: [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md).

## Consequences

- Step order is enforced by the orchestrator against its run order before a row is written; the database links every step to its project.
- No narrative can diverge from what happened: the receipt is a snapshot of the row, not a separately written summary.
- PostgreSQL must be running. This is setup complexity for a non-technical user, accepted because the integrity guarantees justify it.
