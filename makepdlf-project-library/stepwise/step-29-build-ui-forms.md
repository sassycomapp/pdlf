---
title: "step-29-build-ui-forms"
doc-id: "mb-08047605"
updated: "2026-10-09"
---
## Task Execution Order

1. Developer + Anvil AI: Build UI forms in the Anvil IDE from approved wireframes and screens
2. Follow execution sequence in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (Light)

---

## Description

Developer + Anvil AI builds UI forms in the Anvil IDE. Anvil AI wires
components to their code-behind functions during this step.

## Inputs Required

- Wireframe HTML from Step 22/26
- Screen HTML from Step 27
- Screen PNG from Step 28

## Outputs

- Live UI forms in the Anvil IDE (not local files)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 29 | Manual | | Developer + Anvil AI, in Anvil IDE |

## Reference Files

| [[[pdlf:makepdlf-project-library/policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/pdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 17/29/32 (platform) |

Anvil integration is governed by [[[pdlf:makepdlf-project-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) in full — the detailed reference (the earlier `stepwise/step-6-24-anvil-integration.md` pointer was retired 2026-07-18: the file was never created; its intended content lives in the policy).

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
