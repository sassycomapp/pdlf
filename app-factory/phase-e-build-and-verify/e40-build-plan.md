---
title: "e40-build-plan"
doc-id: "mb-71500d0b"
updated: "2026-11-13"
---
# Step 40 — Architecture Scan: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 40: Architecture scan

**Must achieve:** an optional, read-only scan of the feature's code for places where the architecture could be deeper or cleaner, so that David can approve the fixes worth making before the feature is reviewed; David decides for each ticket whether it runs.

**Starts from:** the feature as tested at Step 35A; `scaffold-spec.md`; the code graph from Step 34.

**Produces:** the scan report, when it runs; David's decision on each finding; in `pdlf-outputs\e40\`: the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with Matt Pocock's `improve-codebase-architecture` and `graphify`. David decides whether the scan runs and which findings are fixed.

**Must be built so that:**
- David is asked whether the scan runs for this ticket; on no, the step is recorded `skipped`;
- `graphify` refreshes the code graph for the feature, as the evidence of coupling;
- `improve-codebase-architecture` runs read-only against `scaffold-spec.md`'s modules and seams, and changes nothing;
- David approves or declines each finding; only approved findings go to Step 40B;
- its ledger row carries the ticket, with `step_type = 'optional'`, `skill_family = 'matt-skills'`, `synthesized = false`, and `inputs_used` naming Step 35A.

**BFT level:** Light.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Policy: Step Conditional State]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `improve-codebase-architecture` (Matt Pocock), read-only → the findings, then Step 40B.
- `graphify`: the refreshed code graph → the findings' evidence.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e40-test-spec|Step 40 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-test-spec.md).

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2, 3 and 16.

## Why it is built this way

- **Before review, not after.** Fixes made here are reviewed at Steps 36 to 38 with the rest of the feature.
- **David chooses.** The scan is advice; only fixes he approves are made.
