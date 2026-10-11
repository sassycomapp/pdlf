---
title: "40b-remediation"
doc-id: "mb-e424b8ca"
updated: "2026-10-11"
---
## Task Execution Order

1. → Decision point: if Step 40 was skipped, or produced no findings, or the developer
   declined all findings: skip this step entirely, no artifact produced.
2. If findings were approved: OpenCode applies only the specific, developer-approved
   fixes from Step 40's report. No fix is applied that was not explicitly approved.
3. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
4. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Direct code remediation of findings surfaced by Step 40's read-only architecture scan.
This is the only point in the loop where architecture-scan findings become actual code
changes — Step 40 itself never touches code. Exists specifically so that any such change
is retested by Steps 36–38 before the `build-verified` gate, not shipped unverified (see
ADR-0007).

## Inputs Required

- Step 40's architecture report
- Developer's specific approval of which findings to act on

## Outputs

- Code changes, scoped exactly to approved findings
- Nothing, if Step 40 was skipped or all findings were declined

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 40B | OpenCode (per feature cycle, conditional) | | OpenCode |

---

## Handoff to Step 36

Step 36 (`/design-review`) runs next and explicitly retests this step's output, not just
Step 35's original build. If this step produced no changes, Step 36 still runs as normal.

---

## Reference

Design rationale — why the `build-verified` gate sits after this step's retest, not before
Step 40: ADR-0007.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
