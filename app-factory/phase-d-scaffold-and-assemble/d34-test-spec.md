---
title: "d34-test-spec"
doc-id: "mb-97443c97"
updated: "2026-11-12"
---
# Step 34: Architecture audit — Test Specification

**Proves:** The skeleton passes every static check, traces to the locked decisions, implements the threat model's controls, and `architecture-verified` has David's approval.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d34\`; every result is recorded in `{slug}-d34-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 33 is complete. |
| ST-01 | The whole app validates. |
| ST-02 to ST-12 | Each passes, or each failure in existing code is on the rework list with its ticket. |
| ST-13 | bandit, pip-audit and `/cso` are clean, or each finding in existing code is on the rework list. |
| Structure | Every module and function traces to `scaffold-spec.md`; nothing unplanned exists; every server function a screen requirement names exists with its access rule. |
| DC-06 | Every trust boundary's control exists in the skeleton. |
| DC-08 | The skeleton obeys the common aspects; App 3 needs no code. |
| PR-05 | The receipts of Steps 31 to 33 match their evidence. |
| PR-04 | Sentinel ran at Very High; no finding is open. |
| PR-03 | The `architecture-verified` gate row was written by David's `pdlf-gate.sh`; the agent did not write it. |

**On failure:** Any failure blocks the gate; a fault in what PDLF built is corrected at its step and Step 34 runs again.
