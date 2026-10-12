---
title: "step-32-physical-scaffold-build"
doc-id: "mb-13fb6825"
updated: "2026-10-12"
---
## Task Execution Order

1. Developer: Create empty client-code modules and server modules/functions in Anvil IDE per scaffold-plan.md
2. Follow execution sequence in [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (Light)

---

## Description

Developer creates empty client-code modules and server modules/functions in
Anvil IDE, following the scaffold plan from Step 31.

## Outputs

- Empty stubs in the Anvil app — modules, server functions, form code-behind shells

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 32 | Manual | | Physical scaffold build, in Anvil IDE |

## Reference Files

| [[[makepdlf-project-library:policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 17/29/32 (platform) |

Anvil integration is governed by [[[makepdlf-project-library:policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) in full — the detailed reference (the earlier `stepwise/step-6-24-anvil-integration.md` pointer was retired 2026-07-18: the file was never created; its intended content lives in the policy).

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
