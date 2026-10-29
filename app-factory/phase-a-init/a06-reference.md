---
title: "a06-reference"
doc-id: "mb-b1325604"
updated: "2026-10-29"
---
# Step 6 — Release into App 2: Reference

What the orchestrator does at Step 6, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a06-config|Step 6 Configuration]]](C:/pdlf/app-factory/phase-a-init/a06-config.md). It is carried out at item 8 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md), after the health check at item 7; that reference then completes the entry: the slug checks, the entry row, the receipt and the stop.

1. Ask David to confirm that App 1's approved work is to be released into App 2, which every client instance depends on.
2. Run App 1's whole test suite (test PR-08), with the commands in the configuration. A failure stops the entry: a release starts only from a passing App 1.
3. Return to item 9 of [[[pdlf:app-factory/phase-a-init/a01-reference|Step 1 Reference]]](C:/pdlf/app-factory/phase-a-init/a01-reference.md).
