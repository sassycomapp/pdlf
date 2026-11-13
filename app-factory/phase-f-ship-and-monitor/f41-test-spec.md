---
title: "f41-test-spec"
doc-id: "mb-8fd2257d"
updated: "2026-11-13"
---
# Step 41: Release Readiness — Test Specification

**Proves:** The app is ready to release: every feature verified, every test and release test passing, the security assessment clean, and the release documented.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f41\`; every result is recorded in `{slug}-f41-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The last ticket's Step 39 is complete. |
| RL-01 | Every feature passed `build-verified`; the suite passes; no high or critical finding is open. |
| Release tests | Every release test the app's test plan names passes. |
| RL-02 | Backups restore in a drill, before the first release. |
| RL-07 | Rollback works. |
| RL-08 | Exit export, first release and each schema change. |
| SC-16 | Penetration test passed before the first public launch. |
| SC-17 | The threat model is current. |
| SC-18 | The dynamic scan of hosted App 1 is clean. |
| DC-14 | Release notes, migration plan, and the legal documents before a first release. |
| BR-06 | The performance baseline is recorded. |
| PR-06 | David committed, tagged and pushed. |

**On failure:** A failing test or open high finding returns its feature to Step 35.
