---
title: "c26-test-spec"
doc-id: "mb-cd8a0cae"
updated: "2026-11-12"
---
# Step 26: Screens approved — Test Specification

**Proves:** Every finding of Step 23 is closed, every screen requirement passes DC-16 and is approved, and `screens-approved` has David's approval.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c26\`; every result is recorded in `{slug}-c26-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 23 is complete. |
| DC-16 | After the corrections, every screen requirement passes in full, including theme usage. |
| Findings closed | Every finding of Step 23 is corrected or, for a medium or low finding, declined by David with his reason; no theme-usage finding is declined. |
| Approved | Every screen requirement in the index has `status: approved`. |
| PR-05 | The receipts of Steps 21 to 23 match their evidence with `ts_report.py --check`. |
| PR-03 | The `screens-approved` gate row was written by David's `pdlf-gate.sh`, with its time; the agent did not write it. |

**On failure:** Each failure is corrected before the gate is offered.
