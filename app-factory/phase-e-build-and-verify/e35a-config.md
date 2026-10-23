---
title: "e35a-config"
doc-id: "mb-b18165ee"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 35A | Step 35A Testing | OpenCode | Local-scope `pip-audit` + broader testing | |

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
| 35A | Testing (local pip-audit + broader) | OpenCode | **Light** | Dev/test-tooling dependency scan + coverage — mechanical execution of a locked test plan, not a design decision |
