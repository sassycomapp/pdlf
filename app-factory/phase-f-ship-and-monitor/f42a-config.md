---
title: "f42a-config"
doc-id: "mb-1de372f7"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 42A | Step 42A Staging Integration E2E | Skill | GStack/OpenCode — full integration/E2E suite | |

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
| 42A | Staging integration/E2E | Skill/OpenCode | **Light** | Full integration/E2E suite against staging — executes a locked test plan, not a design decision |
