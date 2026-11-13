---
title: "e40b-reference"
doc-id: "mb-7cc93d36"
updated: "2026-11-13"
---
# Step 40B — Approved Fixes: Reference

What the agent does at Step 40B, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e40b-config|Step 40B Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 40 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. If Step 40 was skipped or David approved no fix: record the step `skipped`, write the receipt, stop.
4. Apply each approved fix with `codebase-design` and the Anvil skill for the code it touches. Apply nothing else.
5. Run every test of the feature and the whole suite. On a failure: find its root cause with `diagnosing-bugs`, fix it, run again. Weaken no test.
6. Give David the commit command and wait until he confirms it ran.
7. Run the Light BFT. Complete the Step 40B `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
8. Explain what was done. Present the Step Receipt and stop.
