---
title: "f45-reference"
doc-id: "mb-eac0114b"
updated: "2026-11-13"
---
# Step 45 — Production Check: Reference

What the agent does at Step 45, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f45-config|Step 45 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f45-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 44 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. Hand David `mg-grant --path ~/.gstack --count 15` and wait until he confirms it ran ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2.8).
4. Run `/canary` against the baseline. Read every client's heartbeat in App 5. On a rollback trigger: give David the rollback instructions at once; stop and raise a deviation.
5. Run the post-release part of the assessment plan with `security-audit-methodology`, and schedule the periodic checks.
6. Write the production report. Run `mb-sentinel-review` for Step 45 at Medium scrutiny. On Flag or Escalate: stop and present it to David. Check the review's `triage_findings` row exists (test PR-04).
7. Record every test in the checks file, naming its evidence.
8. Run the Full BFT. Complete the Step 45 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
9. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
