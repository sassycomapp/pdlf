---
title: "step-30-pull-to-local"
doc-id: "mb-34a5bb8b"
updated: "2026-10-12"
---
## Task Execution Order

1. Pull the Anvil-connected code repo to local
2. Follow execution sequence in [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (None)

---

## Description

Pull the Anvil-connected code repo to local so the build loop has the real
component tree with Anvil AI's wiring.

## Outputs

- Updated local code repo with UI forms and wiring.

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 30 | Manual | | Pull to local |

## Reference Files

| [[[makepdlf-project-library:policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |

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
