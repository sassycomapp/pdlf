---
title: "e38a-test-spec"
doc-id: "mb-c66ffc80"
updated: "2026-11-13"
---
# Step 38A: Package Check — Test Specification

**Proves:** Anvil's package report is recorded and agrees with `pip-audit`, or each difference is a finding.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e38a\`; every result is recorded in `{slug}-e38a-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 38 is complete for the ticket. |
| ST-13 | Anvil's package report agrees with `pip-audit`; findings recorded. |

**On failure:** Each finding goes to Step 39.
