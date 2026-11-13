---
title: "e40-test-spec"
doc-id: "mb-57eabeaa"
updated: "2026-11-13"
---
# Step 40: Architecture Scan — Test Specification

**Proves:** The scan, when it runs, changed nothing, and every finding has David's decision.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e40\`; every result is recorded in `{slug}-e40-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 35A is complete for the ticket. |
| ST-10 | The code still matches its structure rules; the scan changed no file. |

**On failure:** A finding without a decision is put to David before the step ends.
