---
title: "a04-reference"
doc-id: "mb-547ef812"
updated: "2026-10-29"
---
# Step 4 — Feature for App 1: Reference

What the orchestrator does at Step 4, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a04-config|Step 4 Configuration]]](C:/pdlf/app-factory/phase-a-init/a04-config.md). It is carried out at item 8 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md), after the health check at item 7; that reference then completes the entry: the slug checks, the entry row, the receipt and the stop.

1. Ask David for the feature in his own words, or the release specification in `docs-local\releases\v{n}\` that holds it.
2. Ask David for the feature's short name: lowercase, hyphens, unique in the business.
3. Check the application run `app1` has passed the gate `domain-locked`. If it has not: stop and raise a deviation, because a feature is described against an approved design.
4. Run App 1's whole test suite once as the baseline (test PR-08), with the commands in the configuration. A failure is recorded in the checks file as a finding of the existing app, not a reason to stop.
5. Return to item 9 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md).
