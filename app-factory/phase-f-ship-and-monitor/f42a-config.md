---
title: "f42a-config"
doc-id: "mb-1de372f7"
updated: "2026-11-08"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 42A | Step 42A Release regression test | Skill | GStack/OpenCode — full integration/E2E suite | |

### Phase E — Ship & Monitor: phase notes

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see Run Plan.

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 42A | Release regression test | Skill/OpenCode | **Light** | Full integration/E2E suite against the test client instance — executes a locked test plan, not a design decision |
