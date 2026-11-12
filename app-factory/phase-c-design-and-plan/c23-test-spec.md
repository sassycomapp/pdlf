---
title: "c23-test-spec"
doc-id: "mb-dc5cd8dc"
updated: "2026-11-12"
---
# Step 23: Design review — Test Specification

**Proves:** Every screen requirement was reviewed for usability, theme usage, accessibility and the always-available controls, and every finding is recorded with its severity.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c23\`; every result is recorded in `{slug}-c23-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 22 is complete. |
| DC-16 | Theme usage: every element of every screen requirement was compared with the whole inventory, and each better-fitting component found is a high finding. |
| Review complete | Every screen requirement in the index has its review entry; every finding has its element, proposed correction and severity. |

**On failure:** The missing review entries are written before the step ends.
