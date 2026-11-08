---
title: "f45-config"
doc-id: "mb-165902b2"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 45 | `f45-build-plan` | Skill | GStack `/canary` at the test client instance; App 5 heartbeats | |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 45 | /canary and heartbeats | Skill | **Full** | Post-release monitoring loop — production health decisions |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `released` | 45 + 46 | Every client instance on the release, initial canary passed, LEARN complete, ISA Verification/Changelog updated. Cycle closed. |
