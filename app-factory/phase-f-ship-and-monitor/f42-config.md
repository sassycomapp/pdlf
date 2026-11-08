---
title: "f42-config"
doc-id: "mb-ae23ef5b"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 42 | `f42-build-plan` | Manual | Release to App 2 and build the release image | |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 42 | Release to App 2 | Manual | **None** | Push, build and check follow fixed procedures. Zero judgment. |
