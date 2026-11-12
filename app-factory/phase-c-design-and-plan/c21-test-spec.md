---
title: "c21-test-spec"
doc-id: "mb-e03e65ee"
updated: "2026-11-12"
---
# Step 21: Concept check — Test Specification

**Proves:** The concept has no contradictions, Steps 17 to 20 rest on passed tests, and `concept-locked` has David's approval.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c21\`; every result is recorded in `{slug}-c21-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 20 is complete or skipped. |
| DC-11 | Every pair of concept documents was checked and the report names each pair; every fixed check passed; no contradiction remains. |
| PR-05 | The receipts of Steps 17 to 20 match their evidence with `ts_report.py --check`. |
| PR-04 | Sentinel ran at Medium, and any Flag or Escalate has David's decision. |
| PR-03 | The `concept-locked` gate row was written by David's `pdlf-gate.sh`, with its time; the agent did not write it. |

**On failure:** Each failure is corrected at its source with David before the gate is offered.
