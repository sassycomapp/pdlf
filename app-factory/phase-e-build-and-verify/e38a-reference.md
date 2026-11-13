---
title: "e38a-reference"
doc-id: "mb-ee5b1678"
updated: "2026-11-13"
---
# Step 38A — Package Check: Reference

What the agent does at Step 38A, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e38a-config|Step 38A Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 38 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. If the feature did not rebuild the server environment: record the step `skipped`, write the receipt, stop.
4. Give David instructions to copy Anvil's package report from the Anvil editor into the step folder, and wait until he confirms.
5. Compare the report with Step 35A's `pip-audit` result. Write every finding to `triage_findings`.
6. Complete the Step 38A `steps` row with the ledger values in the configuration, and write the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
7. Explain what was done. Present the Step Receipt and stop.
