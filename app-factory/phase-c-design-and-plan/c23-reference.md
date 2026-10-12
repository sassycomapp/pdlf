---
title: "c23-reference"
doc-id: "mb-9de2903a"
updated: "2026-10-12"
---

## From `23-plan-design-review.md`

## Task Execution Order

1. Run GStack [[[pdlf:app-factory/phase-c-design-and-plan/c23-reference|/plan-design-review]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-reference.md)
2. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Rates the plan's UX dimensions 0–10 and identifies gaps.

## Inputs Required

- Plan file (updated through Steps 19/22)
- Step 20 DESIGN.md
- Step 22 wireframes

## Outputs

- GSTACK REVIEW REPORT appended to the plan file (7 design passes, 0–10 ratings)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 23 | Skill | | GStack [[[pdlf:app-factory/phase-c-design-and-plan/c23-reference\|/plan-design-review]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-reference.md) |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
