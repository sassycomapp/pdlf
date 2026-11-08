---
title: "f44-config"
doc-id: "mb-1edd98fd"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 44 | `f44-build-plan` | Manual + GATE | Release to every client instance | `production-released` |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

### Gate Summary

`build-verified` sits at Step 39 (triage), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see Run Plan for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `production-released` | 44 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 44 | Release | Manual + GATE | **Full** | GATE `production-released`. Commits the release to real users. Full BFT mandatory. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `production-released` | 44 | Test client instance passed on the release image; every client instance moved to it by App 5's Release action. |
