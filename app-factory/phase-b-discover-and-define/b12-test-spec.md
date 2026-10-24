---
title: "b12-test-spec"
updated: "2026-10-24"
doc-id: "mb-8ab64548"
---
# Step 12: Office hours — Test Specification

**Proves:** The design doc of the run is complete, measurable, bound by the platform's facts and the common aspects, approved by David and free of anything secret.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b12\`; the DC results are written to `{slug}-b12-{run}-dc-checks.md`, each with the section of the design doc that shows it.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 11 is complete for the app worked on. |
| DC-01 | Every success criterion has a metric, a threshold and a method; no requirement uses a vague term or bundles two needs. |
| DC-02 | Every section of the fixed structure is present, in order; the Constraints section states one app and one database per client, server authority, public client code, the Hobby plan and POPIA; the 14 common aspects are each listed as shared or deviating with its reason; when a reference platform is used, its analysis is checked against its primary sources and only its domain and workflows are taken. |
| PR-06 | No secret is in the design docs, the research file or any copy in `pdlf-outputs\b12\` (gitleaks on the project library's working tree). |
| PR-04 | Sentinel ran at Medium. |

**On failure:** The design doc is corrected with David and checked again; a secret found is removed before the step ends.
