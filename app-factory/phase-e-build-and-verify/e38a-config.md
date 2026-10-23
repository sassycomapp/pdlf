---
title: "e38a-config"
doc-id: "mb-fe48d787"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 38A | Step 38A Dependency Scan Confirm | OpenCode | Capture Anvil's native `pip-audit` result | |

### Phase D — Build & Verify (per-feature loop): phase notes

Repeats once per feature/package from Step 19's ticket list, until every feature has
individually reached `build-verified`. For the loop's actual order and dependencies, see
Run Plan, "Step 35 Feature Loop."


Exit gate: `build-verified`, evaluated per feature. For entry condition and dependencies,
see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase E — Build & Verify (Steps 35–40)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 38A | Dependency scan confirm | OpenCode (per feature cycle) | **None** | Records Anvil's own native pip-audit result — capture only, no judgment |
