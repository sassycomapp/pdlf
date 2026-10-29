---
title: "a10-reference"
doc-id: "mb-e1131122"
updated: "2026-10-29"
---
# Step 10 — Update to App 3 or App 5: Reference

What the orchestrator does at Step 10, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a10-config|Step 10 Configuration]]](C:/pdlf/app-factory/phase-a-init/a10-config.md). It is carried out at item 8 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md), after the health check at item 7; that reference then completes the entry: the slug checks, the entry row, the receipt and the stop.

1. Ask David which app the update is for: App 3 or App 5.
2. Ask David for the update in his own words and its short name.
3. Ask whether it changes what the app does. If it does, the route is Feature and the start step is 12. Otherwise the route is Update: ask David which step to start from.
4. Ask whether it corrects a fault. If it does, run `diagnosing-bugs` to find the root cause before any work, and save the diagnosis as `pdlf-outputs\a10\{slug}-a10-{run}-diagnosis.md`.
5. For App 5: run its whole test suite once as the baseline (test PR-08), with the commands in the configuration. App 3 holds no code and has no suite.
6. Return to item 9 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md).
