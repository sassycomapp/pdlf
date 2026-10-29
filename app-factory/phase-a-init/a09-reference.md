---
title: "a09-reference"
doc-id: "mb-5f062048"
updated: "2026-10-29"
---
# Step 9 — Feature for App 3 or App 5: Reference

What the orchestrator does at Step 9, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a09-config|Step 9 Configuration]]](C:/pdlf/app-factory/phase-a-init/a09-config.md). It is carried out at item 8 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md), after the health check at item 7; that reference then completes the entry: the slug checks, the entry row, the receipt and the stop.

1. Ask David which app the feature is for: App 3 or App 5.
2. Ask David for the feature in his own words, and its short name.
3. Check the app's run `app{n}` has passed the gate `domain-locked`, for App 5, or is complete at Step 11, for App 3. If not: stop and raise a deviation.
4. For App 5: run its whole test suite once as the baseline (test PR-08), with the commands in the configuration. A failure is recorded as a finding of the existing app. App 3 holds no code and has no suite.
5. Return to item 9 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md).
