---
title: "a01-test-spec"
updated: "2026-10-23"
doc-id: "mb-6e7ca43f"
---
# Step 1: Orchestrator — Test Specification

**Proves:** The orchestrator routes each entry to its step, runs steps only when their dependencies are complete, and cannot pass a gate without the developer.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a01\`.

| Test | Applied here |
|---|---|
| PR-01 | Each entry point, run in test mode, joins at the step the build plan names; a step with an incomplete dependency is refused. |
| PR-03 | An agent's attempt to pass each gate is blocked; a failed gate stops the pipeline. |

**On failure:** PDLF is not used until the orchestrator passes.
