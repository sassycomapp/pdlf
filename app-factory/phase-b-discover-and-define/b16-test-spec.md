---
title: "b16-test-spec"
updated: "2026-10-29"
doc-id: "mb-7808f2ff"
---
# Step 16: Domain modeling — Test Specification

**Proves:** The vocabulary is sound and agrees with the data design, Phase B of the run is complete, tested and approved, and the `domain-locked` gate has David's approval.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b16\`; every result is recorded in `{slug}-b16-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 15 is complete, with its outputs approved. |
| DC-09 | Every term in `GLOSSARY.md` has one meaning; every entity has an owner and a place in the data design; shared terms match `spec-nomenclature`; "multi-tenant" is never used for the five-app model. |
| PR-05 | Every Phase B receipt of the run (b11 for a whole application, b12, b14, b15) matches its evidence with `ts_report.py --check`. |
| PR-06 | No secret is in the glossary, any ADR or any copy in `pdlf-outputs\b16\` (gitleaks on the project library's working tree). |
| PR-04 | Sentinel ran at Low/Medium, and every Sentinel finding of the run's Phase B steps has David's decision. |
| PR-03 | The `domain-locked` gate row was written by David's `pdlf-gate.sh`, with its time; the agent did not write it. |

**On failure:** Each failure is corrected with David before the gate is offered; a secret found is removed before the step ends.
