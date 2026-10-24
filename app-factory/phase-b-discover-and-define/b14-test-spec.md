---
title: "b14-test-spec"
updated: "2026-10-24"
doc-id: "mb-b0c6e8a1"
---
# Step 14: CEO review — Test Specification

**Proves:** The run's scope, data, legal position, client exit and Hobby fit are settled, testable and approved by David.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b14\`; every result is recorded in `{slug}-b14-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 12 is complete, with its design doc approved. |
| DC-03 | The Scope section states goals and non-goals and the review's NOT in scope section gives every exclusion its reason; every kind of data in the Data Inventory has its owner, readers, writers, protection level and retention; the Regulatory Position decides POPIA, GDPR and PCI DSS SAQ A; the Client Exit section names the handover package; the Hobby Fit section shows a typical client within the Hobby limits. |
| DC-01 | Every requirement and acceptance criterion the review added is testable: no vague term, no bundled needs. |
| PR-06 | No secret is in the reviewed plan, any ADR written or any copy in `pdlf-outputs\b14\` (gitleaks on the project library's working tree). |
| PR-04 | Sentinel ran at Medium. |

**On failure:** The plan is corrected with David and checked again; a secret found is removed before the step ends.
