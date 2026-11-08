---
title: "f41-config"
doc-id: "mb-dccc0401"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 41 | `[[step-41-ship]]` | Skill | GStack /ship | |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 41 | /ship (scope narrowed) | Skill | **Light** | Version bump, CHANGELOG, commit, push. Mostly mechanical but CHANGELOG writing has judgment. |
