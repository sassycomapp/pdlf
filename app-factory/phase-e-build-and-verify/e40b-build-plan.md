---
title: "e40b-build-plan"
doc-id: "mb-b74e415a"
updated: "2026-11-13"
---
# Step 40B — Approved Fixes: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 40B: Approved fixes

**Must achieve:** only the fixes David approved at Step 40 applied, with every test of the feature passing again; skipped when Step 40 did not run or David approved nothing.

**Starts from:** the scan report of Step 40; the feature's code and tests.

**Produces:** the approved fixes in the app; in `pdlf-outputs\e40b\`: the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with the skills below. David commits.

**Must be built so that:**
- only the fixes David approved are applied, within `scaffold-spec.md`'s modules, with `codebase-design` and the Anvil skill for each part of the code touched;
- every test of the feature, and the whole suite, runs again and passes; no test is weakened;
- David commits the app with `git pull` followed by `gcp`;
- its ledger row carries the ticket, with `step_type = 'optional'`, `skill_family = 'opencode'`, `synthesized = false`, and `inputs_used` naming Step 40.

**BFT level:** Light.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `codebase-design` (Matt Pocock): each fix kept within the planned modules → Step 37.
- `server-code`, `client-modules`, `client-forms` and `data-models` (Anvil): each fix in the part of the code it touches → Step 37.
- `tdd` (Matt Pocock): every test run again → Step 36.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e40b-test-spec|Step 40B Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40b-test-spec.md).

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md).

## Why it is built this way

- **Only what was approved.** A fix David did not approve is never made.
- **Everything retested.** A structural fix can break what worked, so every test runs again.
