---
title: "step-35A-testing"
doc-id: "mb-d4e34b00"
updated: "2026-10-12"
---
## Task Execution Order

1. Run `pip-audit` against the local development/test environment only —
   test frameworks, `anvil-uplink`, and any other tooling installed locally
   that is never registered through Anvil's IDE Package section.
2. Run any additional local test coverage beyond Step 35's Levels 1–3, if applicable
   to this feature.
3. Record findings. If `pip-audit` reports vulnerabilities, present as a deviation
   request — developer decides whether to address before continuing.
4. Follow execution sequence in [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
5. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

The first of two dependency-scan touchpoints in the per-feature loop (see ADR-0011). This
step covers only what Anvil's own native scan structurally cannot see: local development
and test tooling that never gets registered in the Anvil IDE. It does not audit the app's
own third-party dependencies — those are Anvil's responsibility, captured at Step 38A, not
duplicated here.

## Inputs Required

- Local development/test Python environment for this feature cycle
- Feature build output from Step 35

## Outputs

- `pip-audit` result for the local dev/test environment
- Any additional local test coverage results

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 35A | OpenCode (per feature cycle) | | OpenCode |

---

## Handoff to Step 40

Proceeds to Step 40 (architecture scan, optional) regardless of `pip-audit` result, unless
a vulnerability finding is escalated as a deviation requiring resolution first.

---

## Reference

Design rationale and scope boundary vs. Anvil's native scan: ADR-0011.
`pip-audit` installed via `pipx install pip-audit`.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
