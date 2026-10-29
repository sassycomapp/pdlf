---
title: "a05-reference"
doc-id: "mb-beb2a975"
updated: "2026-10-29"
---
# Step 5 — Update to App 1: Reference

What the orchestrator does at Step 5, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a05-config|Step 5 Configuration]]](C:/pdlf/app-factory/phase-a-init/a05-config.md). It is carried out at item 8 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md), after the health check at item 7; that reference then completes the entry: the slug checks, the entry row, the receipt and the stop.

1. Ask David for the update in his own words and its short name.
2. Ask whether it changes what the app does. If it does, it is a feature: the route is Feature and the start step is 12. Otherwise the route is Update: ask David which step to start from.
3. Ask whether it corrects a fault. If it does, run `diagnosing-bugs` to find the root cause before any work, and save the diagnosis as `pdlf-outputs\a05\{slug}-a05-{run}-diagnosis.md`.
4. Run App 1's whole test suite once as the baseline (test PR-08), with the commands in the configuration. A failure is recorded in the checks file as a finding of the existing app.
5. Return to item 9 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md).
