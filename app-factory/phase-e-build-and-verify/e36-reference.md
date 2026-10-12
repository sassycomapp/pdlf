---
title: "e36-reference"
doc-id: "mb-60ebe004"
updated: "2026-10-12"
---

## From `36-design-review.md`

## Task Execution Order

1. Confirm Steps 35A, 40, and 40B (if applicable) have completed for this feature cycle.
2. Run GStack `/design-review` against the current state — including any remediation
   applied at Step 40B.
3. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
4. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full).

---

## Description

80-item live-site visual audit. Takes before/after screenshots, applies atomic fix
commits. Deliberately positioned after Step 40B, not directly after Step 35 — this
retests the feature as it will actually ship, including any architecture remediation,
rather than reviewing a build that's about to change again.

## Inputs Required

- Live target URL
- Step 20 DESIGN.md
- Clean git working tree
- Confirmation that 35A/40/40B have completed this cycle

## Outputs

- Structured design audit report
- Before/after screenshots
- One atomic git commit per fix

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 36 | Skill | | GStack `/design-review` |

---

## Reference

Position rationale — why this runs after remediation, not before: ADR-0007.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
