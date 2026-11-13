---
title: "e39-test-spec"
doc-id: "mb-0bff5864"
updated: "2026-11-13"
---
# Step 39: Triage — Test Specification

**Proves:** Every finding is decided, the whole suite passes, the receipts match their evidence, and `build-verified` has David's approval for the ticket.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e39\`; every result is recorded in `{slug}-e39-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 38A is complete or skipped for the ticket. |
| PR-04 | Every finding of 35A to 38A is in `triage_findings`, resolved or declined. |
| LG-07 | Every fixed finding has its test. |
| PR-08 | The whole suite passes. |
| PR-05 | The receipts of Steps 35 to 38A match their evidence. |
| PR-03 | The `build-verified` gate row for the ticket was written by David's `pdlf-gate.sh`; the agent did not write it. |

**On failure:** A fix returns the feature to Step 35; the gate is offered only when nothing is open.
