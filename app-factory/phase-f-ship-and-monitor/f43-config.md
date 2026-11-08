---
title: "f43-config"
doc-id: "mb-c55a9572"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 43 | `f43-build-plan` | Skill | GStack /qa or `/canary` — smoke test | |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 43 | /qa or /canary at the test client instance | Skill | **Full** | Smoke test against the test client instance — verification decisions before the Release action |
