---
title: "f45-config"
doc-id: "mb-165902b2"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 45 | `[[step-45-canary-production]]` | Skill | GStack `/canary` at Production | |

### Phase E — Ship & Monitor: phase notes

**Note:** Steps 42, 42A, 43, and 44 are flagged for rebuild — see `ToDo.md` item 2. They
currently model a staging/production environment split that does not apply to this
platform (see `[[adr-no-staging-environment-five-app-isolation]]`). Listed here as
currently defined; not yet corrected.


Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 45 | /canary at Production | Skill | **Full** | Post-deploy monitoring loop — production health decisions |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `released` | 45 + 46 | Production deployed, initial canary passed, LEARN complete, ISA Verification/Changelog updated. Cycle closed. |
