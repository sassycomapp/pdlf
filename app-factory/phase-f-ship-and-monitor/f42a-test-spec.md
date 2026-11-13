---
title: "f42a-test-spec"
doc-id: "mb-1d651bfe"
updated: "2026-11-13"
---
# Step 42A: Release Regression — Test Specification

**Proves:** Every feature works on the release image in three browsers, and the release's dynamic scan is clean.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f42a\`; every result is recorded in `{slug}-f42a-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 42 is complete. |
| RL-06 | Every feature's flows pass on the release image in Chrome, Firefox and Safari. |
| SC-18 | The dynamic scan leaves no high or medium alert open. |
| SC-09 | Nothing sensitive in addresses or browser storage. |

**On failure:** A failure moves the test client instance back and stops the release.
