---
title: "step-44-promote-to-production"
doc-id: "mb-e537cc77"
updated: "2026-10-10"
---
## Task Execution Order

1. Developer: Promote the same reviewed commit from Staging to Production in the Anvil IDE
2. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
3. → GATE: `production-released` — developer approval required. App is now live.
4. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
5. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

Developer promotes the same reviewed commit to Production. Rollback is
re-pointing the environment, not `git revert`.

## Inputs Required

- Passing smoke test from Step 43

## Outputs

- App running at Production URL
- GATE `production-released` — Full BFT, gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 44 | Manual | **GATE** `production-released` | Promote to Production |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `production-released` | 44 | Staging smoke test passed, same commit promoted to Production, databases confirmed separate. App is live. |

## Reference Files

| [[[pdlf:pdlf-library/policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 41–45 (deployment) |

Anvil integration is governed by [[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) in full — the detailed reference (the earlier `stepwise/step-6-24-anvil-integration.md` pointer was retired 2026-07-18: the file was never created; its intended content lives in the policy).

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
