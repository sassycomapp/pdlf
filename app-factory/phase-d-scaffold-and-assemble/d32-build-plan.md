---
title: "d32-build-plan"
doc-id: "mb-b5303e24"
updated: "2026-11-12"
---
# Step 32 — Create the Scaffold: Build Plan

## Step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 32: Create the scaffold

**Must achieve:** every module and function `scaffold-spec.md` plans exists in the app as an empty stub, and nothing else is added, so that the build loop fills a structure that is already right; the scanner's settings match the plan; the stubs reach Anvil.

**Starts from:** `scaffold-spec.md` and the scanner settings from Step 31; for an existing app, the disposition list; the app's repository.

**Produces:** the missing modules and functions as stubs in the app's `client_code\` and `server_code\`; the app's `tests\ts-config.yaml` filled from the scanner settings; the stubs committed and pushed by David; in `pdlf-outputs\d32\`: the stub list, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with Anvil's `server-code` and `client-modules`. David commits and pushes the app.

**Must be built so that:**
- each planned module and function that does not yet exist is created exactly as `scaffold-spec.md` names it, with its access decorator, its rate-limit marker where planned, and a one-line docstring naming its behaviour and its test;
- every stub body raises `NotImplementedError`, so that no stub can pass a test or be called as if it worked;
- an existing module marked keep or rework is left as it is; nothing marked remove is removed in this step, because its ticket's build removes it;
- no module, function or file is created that `scaffold-spec.md` does not name; forms are not created here;
- the app's `tests\ts-config.yaml` is filled with the scanner settings, keeping its theme keys;
- every changed file passes `anvil --json validate`, and the scanner's structure check (ST-10) passes;
- David commits and pushes the app with `git pull` followed by `gcp`; the agent never commits;
- its ledger row is `step_type = 'skill'`, `skill_family = 'anvil'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 31.

**BFT level:** Light.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `server-code` and `client-modules` (Anvil): each stub written exactly as planned → David's push, then Step 33.

**Layers with no skill:** security (access decorators are placed as planned; Step 34 verifies them).

**Testing:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d32-test-spec|Step 32 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d32-test-spec.md): every planned stub exists and validates, nothing unplanned exists, and David pushed it.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2, 3 and 16.

## Why it is built this way

- **Exactly the plan.** Creating only what the plan names keeps the structure Step 34 verifies equal to the structure that was approved.
- **Stubs that cannot pass.** A stub that raises an error makes every test of an unbuilt function fail, so nothing looks finished before it is.
- **Existing code untouched.** Rework and removal happen with the ticket that needs them, so the app keeps working between features.
