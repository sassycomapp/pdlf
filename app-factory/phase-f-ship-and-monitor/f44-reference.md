---
title: "f44-reference"
doc-id: "mb-ac475804"
updated: "2026-11-08"
---

## Release

## Task Execution Order

1. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
2. → GATE: `production-released` — developer approval required.
3. App 5's Release action moves every client instance to the release image, staged where the release is high-risk.
4. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
5. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

The developer approves the release, and App 5 moves every client instance to the
release image. Rollback moves client instances back to the previous release image,
not `git revert`.

## Inputs Required

- Passing smoke test from Step 43

## Outputs

- Every client instance running the release image
- GATE `production-released` — Full BFT, gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 44 | Manual | **GATE** `production-released` | Release to every client instance |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `production-released` | 44 | Test client instance passed on the release image; every client instance moved to it by App 5's Release action. |

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
