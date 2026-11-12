---
title: "c19-test-spec"
doc-id: "mb-c29931ed"
updated: "2026-11-12"
---
# Step 19: Tickets — Test Specification

**Proves:** The tickets cover the plan, in a buildable order, each with its forms, functions, tables and tests.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c19\`; every result is recorded in `{slug}-c19-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 18 is complete. |
| DC-10 | No cycle in the order; every feature has a ticket and every ticket a feature; shared components first; each ticket names its acceptance and security tests by ID, and its forms by module path. |
| PR-04 | Sentinel ran at Medium, and any Flag or Escalate has David's decision. |

**On failure:** Each failure is corrected in the tickets and checked again before the step ends.
