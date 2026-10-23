---
title: "f46-config"
doc-id: "mb-652cce5f"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 46 | Step 46 Learn Junction | LEARN + GATE | OpenCode | `released` |

### Phase E — Ship & Monitor: phase notes

**Note:** Steps 42, 42A, 43, and 44 are flagged for rebuild — see `ToDo.md` item 2. They
currently model a staging/production environment split that does not apply to this
platform (see `[[adr-no-staging-environment-five-app-isolation]]`). Listed here as
currently defined; not yet corrected.


Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

### Gate Summary

`build-verified` sits at Step 39 (triage), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see Run Plan for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `released` | 46 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 46 | LEARN junction | OpenCode + GATE | **Full** | Retrospective, learnings, ISA update. GATE `released` (jointly with 45). Full BFT — last checkpoint of the cycle. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `released` | 45 + 46 | Production deployed, initial canary passed, LEARN complete, ISA Verification/Changelog updated. Cycle closed. |
