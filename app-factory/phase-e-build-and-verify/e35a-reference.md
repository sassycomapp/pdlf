---
title: "e35a-reference"
doc-id: "mb-ca3e2562"
updated: "2026-11-13"
---
# Step 35A — Testing: Reference

What the agent does at Step 35A, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e35a-config|Step 35A Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 35 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. With `tdd`, add every edge-case, integration and security test the test plan names for the ticket. Run them. On a failure: return the feature to Step 35 as a deviation.
4. Run `test-audit` on the feature's tests. Present each weak or duplicate test to David with the correction; apply it on his approval. Weaken no test.
5. Run `pip-audit` and `/cso --supply-chain`. Write every finding to `triage_findings`.
6. Record every test in the checks file, naming its evidence.
7. Run the Light BFT. Complete the Step 35A `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
8. Explain what was done. Present the Step Receipt and stop.
