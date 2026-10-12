---
title: "c24-reference"
doc-id: "mb-f40c61dc"
updated: "2026-10-12"
---

## From `24-plan-devex-review.md`

## Task Execution Order

1. Run GStack [[[pdlf:app-factory/phase-c-design-and-plan/c24-reference|/plan-devex-review]]](C:/pdlf/app-factory/phase-c-design-and-plan/c24-reference.md)
2. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Reviews API/CLI/SDK friction points and onboarding time before building.

## Inputs Required

- Plan file (updated through Step 23)
- API/CLI/SDK surfaces described in the plan

## Outputs

- DX scorecard appended to the plan file (TTHW target, Getting Started, API,
  Error Messages, Docs)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 24 | Skill | | GStack [[[pdlf:app-factory/phase-c-design-and-plan/c24-reference\|/plan-devex-review]]](C:/pdlf/app-factory/phase-c-design-and-plan/c24-reference.md) |

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
