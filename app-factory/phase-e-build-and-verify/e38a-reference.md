---
title: "e38a-reference"
doc-id: "mb-ee5b1678"
updated: "2026-10-12"
---

## From `38a-dependency-scan-confirm.md`

## Task Execution Order

1. Confirm whether this feature's work has caused an Anvil server-environment rebuild
   (e.g., via a package registered through the IDE, or an Uplink-triggered build).
2. → Decision point: if no rebuild occurred this cycle, record "no new native scan this
   cycle" and proceed — this is not a failure.
3. If a rebuild occurred: locate Anvil's native `pip-audit` result in the IDE's Build
   Output panel.
4. Record the result (pass, or vulnerabilities found) in the ledger. If vulnerabilities
   are found, present as a deviation request — developer decides whether to address
   before continuing.
5. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
6. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Anvil already runs `pip-audit` automatically on every server-environment build, covering
every package registered through the IDE's Package section. PDLF does not duplicate this
check — this step's entire job is making sure that native result actually gets looked at
and recorded, since nothing currently captures it automatically. This is the app-level
half of the dual-scope dependency scan (see ADR-0011); Step 35A covers the other half
(local dev/test tooling, which Anvil structurally cannot see).

## Inputs Required

- Feature build state from Steps 35–40B
- Anvil IDE Build Output panel, if a rebuild occurred this cycle

## Outputs

- Ledger record of Anvil's native `pip-audit` result, or confirmation that no rebuild
  occurred this cycle
- Deviation request, if vulnerabilities were found and require developer decision

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 38A | OpenCode (per feature cycle) | | OpenCode |

---

## Handoff to Step 39

Step 39 ([[[pdlf:app-factory/phase-e-build-and-verify/e39-reference|triage]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-reference.md)) is not blocked by this step's outcome unless a deviation is raised and
left unresolved.

---

## Reference

Design rationale and scope boundary vs. Step 35A: ADR-0011.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
