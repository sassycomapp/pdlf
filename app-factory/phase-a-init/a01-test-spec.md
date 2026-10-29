---
title: "a01-test-spec"
doc-id: "mb-6e7ca43f"
updated: "2026-10-29"
---
# Step 1: Orchestrator — Test Specification

**Proves:** The orchestrator resumes a run where it stopped, routes each entry to its step, runs a step only when its dependencies are complete and its phase is built, and cannot pass a gate without the developer.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a01\`; every result is recorded in `{slug}-a01-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Each entry point joins its route at the step the configuration names; a step whose dependency is not complete, or whose gate before it has not passed, is refused. |
| PR-11 | Started again on the business, the orchestrator offers the unfinished run at its first step that is not complete or skipped, runs no complete step again, and reports the run as paused at the first step of a phase not yet built. |
| PR-03 | The agent's attempt to run `pdlf-gate.sh` and to write the `gates` table is blocked by Cupcake; the run passes `domain-locked` only after David's `pdlf-gate.sh` row exists. |

**On failure:** The run stops; the orchestrator is corrected before the run continues.
