---
title: "step-31-scaffold-planning"
doc-id: "mb-2b25e3a2"
updated: "2026-10-10"
---
## Task Execution Order

1. Review Step 15/16 architecture and domain model (TDD cluster, CONTEXT.md, ADRs)
2. Review Step 30 pulled UI form structure
3. Review Step 21 concept audit report
4. Plan module/function structure — determine what stubs to create
5. Write `scaffold-plan.md` saved to `<project-library>/`
6. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
7. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Plans the module/function structure for the codebase — what stubs to create
before the build loop fills them in.

## Inputs Required

- Step 15/16 architecture and domain model (TDD cluster, CONTEXT.md, ADRs)
- Step 30 pulled UI form structure
- Step 21 concept audit report

## Outputs

- `scaffold-plan.md` saved to `<project-library>/`

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 31 | OpenCode-native | | Scaffold Planning |

## Artifact Routing

| Scaffold plan | `<project-library>/` (Step 31's output) |

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
