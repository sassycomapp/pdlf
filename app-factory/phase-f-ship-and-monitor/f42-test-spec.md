---
title: "f42-test-spec"
updated: "2026-10-23"
doc-id: "mb-60334d81"
---
# Step 42: Release to App 2 — Test Specification

**Proves:** Clients are protected before the release and correct after it.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f42\`.

| Test | Applied here |
|---|---|
| RL-02 | Every client backed up first. |
| RL-03 | Migration tested on the test client; App 3's schema equals App 1's. |
| RL-04 | App 2 equals the tag. |
| RL-05 | Every instance reports the release and schema. |
| PR-06 | The developer pushed App 2. |

**On failure:** Corrected at once, or rolled back to the last good tag.
