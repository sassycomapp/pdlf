---
title: "e38-reference"
doc-id: "mb-1c768333"
updated: "2026-11-13"
---
# Step 38 — Quality Testing: Reference

What the agent does at Step 38, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e38-config|Step 38 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 37 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
4. Run `/qa-only` on every action of every spec sheet of the feature, as each role and signed out, with `TEST_` data only. Then run every flow of every earlier signed-off feature again. Test payments end to end in test mode when the feature touches them.
5. Run `benchmark` on each of the feature's pages.
6. Write every finding with its evidence and severity; with none, write the clean-pass statement. Fix nothing. Remove the `TEST_` data.
7. Run `mb-sentinel-review` for Step 38 at High scrutiny on the findings. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).
8. Record every test in the checks file, naming its evidence.
9. Run the Full BFT. Complete the Step 38 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
10. Explain what was done. Present the Step Receipt and stop.
