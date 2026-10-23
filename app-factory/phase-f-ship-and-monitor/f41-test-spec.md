---
title: "f41-test-spec"
updated: "2026-10-23"
doc-id: "mb-8fd2257d"
---
# Step 41: Release readiness — Test Specification

**Proves:** The release is ready and every security and data proof is in place.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f41\`.

| Test | Applied here |
|---|---|
| RL-01 | All features signed off, whole suite passes, no serious finding open, ASVS evidence complete. |
| SC-17 | The threat model covers changed trust boundaries. |
| SC-18 | Every threat model attack run; ZAP passive scan clean. |
| SC-16 | Before the first public launch, yearly and before an enterprise sale: penetration test passed. |
| DC-14 | Release notes, migration plan, legal documents. |
| RL-02 | Restore drill (first release). |
| RL-07 | Rollback drill (first release). |
| RL-08 | Exit export proven (first release and schema changes). |
| BR-06 | Performance baseline recorded. |
| PR-06 | The developer tagged and pushed App 1. |

**On failure:** A failure returns its feature to Step 35; a missing first-release proof blocks the release.
