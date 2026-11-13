---
title: "f41-reference"
doc-id: "mb-638f4cb1"
updated: "2026-11-13"
---
# Step 41 — Release Readiness: Reference

What the agent does at Step 41, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-config|Step 41 Configuration]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-config.md). The pattern every step follows (search, read, verify, BFT, ledger row, receipt, explain, stop, close-out) is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) and is not repeated here. Every skill is invoked with the handover material and the context pack, in full ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2).

1. Read the entry record and the ledger row of Step 39 for this run. Check it is complete or skipped (test PR-01). If not: stop and raise a deviation.
2. Carry forward every input notice to this step's receipt, and read every input in the configuration.
3. Check every ticket of the run has passed `build-verified`. If not: stop and raise a deviation.
4. With `tdd`, run the whole suite at Levels 1 and 2, and every release test the test plan names for the app. On a failure: return its feature to Step 35.
5. Run the pre-release part of the assessment plan with `security-audit-methodology`, and a full static scan with `/cso`. Every high or critical finding returns its feature to Step 35.
6. Record the performance baseline with `benchmark`.
7. For a schema change: check it only adds tables and nullable columns, and write its migration plan and rollback into the schema migration log.
8. Write the release notes.
9. At a first release: run every first-release check in the configuration.
10. Write the readiness report. Give David the command in the configuration, written with `wizard`, and wait until he confirms it ran.
11. Record every test in the checks file, naming its evidence.
12. Run the Full BFT. Complete the Step 41 `steps` row with the ledger values in the configuration, and write the BFT record and the Step Receipt, from the [[[pdlf:pdlf-library/templates-local/step-receipt-template|Step Receipt Template]]](C:/pdlf/pdlf-library/templates-local/step-receipt-template.md).
13. Explain what was done. Present the Step Receipt, stop, and ask David to run `/mb-close-out`.
