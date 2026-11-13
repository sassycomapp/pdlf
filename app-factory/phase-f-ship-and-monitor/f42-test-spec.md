---
title: "f42-test-spec"
doc-id: "mb-60334d81"
updated: "2026-11-13"
---
# Step 42: Release to App 2 — Test Specification

**Proves:** Every client is backed up, App 2 equals the release tag, the image is built, scanned and signed, and the test client instance runs it by digest.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f42\`; every result is recorded in `{slug}-f42-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 41 is complete. |
| RL-02 | Every client backed up before the release. |
| RL-03 | Schema changes are safe. |
| RL-04 | App 2 is exactly the release; the image holds App 2, App 3 and `m3` at the release. |
| RL-19 | Only signed images run. |
| RL-05 | The test client instance runs the release correctly. |
| PR-08 | The suite passes on the image. |
| PR-06 | David committed and pushed each repository. |

**On failure:** Any failure stops the release; after the test client instance has moved, it is rolled back.
