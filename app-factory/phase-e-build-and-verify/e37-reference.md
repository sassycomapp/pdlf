---
title: "e37-reference"
doc-id: "mb-7004c91f"
updated: "2026-11-13"
---
# Step 37 — Code Review: Reference

What the agent does at Step 37, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-e-build-and-verify/e37-config|Step 37 Configuration]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 36 for this ticket. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Read the ticket, and every input in the configuration.
3. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
4. In its own session, run `code-review` on the feature's changes with the review standards in the configuration. Check each form and spec sheet against its approved screen requirement, and that Anvil's agent changed only handler bodies.
5. Run `ts_scan.py` on the app.
6. In its own session, run `/cso --diff` on the feature's changes.
7. In its own session, run `mb-sentinel-review` for Step 37 at Very High scrutiny. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).
8. Write every finding with its file, line and severity; with none, write the clean-pass statement. Fix nothing.
9. Record every test in the checks file, naming its evidence.
10. Run the Full BFT. Complete the Step 37 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
11. Explain what was done. Present the Step Receipt and stop.
