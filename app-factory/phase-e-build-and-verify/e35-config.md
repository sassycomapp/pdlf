---
title: "e35-config"
doc-id: "mb-d062d332"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 35 | `[[step-35-build-loop]]` | Agent loop | OpenCode, feature-by-feature | |

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
| 35.N | Build feature N | Agent loop (each issue) | **Full** | Writes production code — every feature cycle has logic, integration, and verification decisions |
