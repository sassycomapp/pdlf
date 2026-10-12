---
title: "step-43-staging-smoke-test"
doc-id: "mb-77e3b283"
updated: "2026-10-12"
---
## Task Execution Order

1. Run GStack [[[makepdlf-project-library:stepwise/step-38-qa|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) or `/canary` — retargeted at Staging URL from Step 42
2. Follow execution sequence in [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

QA or canary check retargeted at the Staging URL. Confirms the app works
on live infrastructure before promoting to Production.

## Inputs Required

- Staging URL from Step 42
- Test plan or canary configuration

## Outputs

- Smoke test report — pass/fail at Staging

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 43 | Skill (retargeted) | | GStack [[[makepdlf-project-library:stepwise/step-38-qa\|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) or `/canary`, at Staging URL |

## Reference Files

| [[[makepdlf-project-library:policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 41–45 (deployment) |

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
