---
title: "c18-build-plan"
doc-id: "mb-1d6a836c"
updated: "2026-11-12"
---
# Step 18 — Pull to Local: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 18: Pull to local

**Must achieve:** David's local copy of the app holds exactly what Anvil holds, after work in the Anvil editor, so that the next step reads the real state of the app.

**Starts from:** the Step Receipt of the step before it (Step 17 here; Step 32 when Step 33 runs this procedure); the app's local repository.

**Produces:** The app's local repository brought level with GitHub; in `pdlf-outputs\c18\`: the test results and the Step Receipt; the ledger row.

**Carried out by:** David runs one command; OpenCode checks the result.

**Must be built so that:**
- David pulls the app with the one command in the configuration;
- the agent checks that the working tree is clean, that the local branch `master` equals `origin/master`, and that the change the step before it expects is present; for Step 17, `db_schema` in `anvil.yaml` equals the authoritative schema;
- the agent runs `anvil --json validate .` on the app and stops with a deviation on an error;
- any file changed that the step before it did not expect, apart from formatting Anvil itself applies, stops the step with a deviation;
- Step 33 runs this same procedure and does not repeat it; it names the change it expects;
- the Anvil CLI's `anvil watch` is not used, because it would send local edits to the app without David's push;
- its ledger row is `step_type = 'manual'`, `skill_family = 'manual'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 17.

**BFT level:** None.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** None. One command moves the code; the agent's checks are plain commands.

**Layers with no skill:** all; the step only moves code.

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c18-test-spec|Step 18 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-test-spec.md): only the expected change arrived, and the app validates.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md).

## Why it is built this way

- **One procedure for two steps.** Steps 18 and 33 do the same thing after work reaches Anvil, so they share one procedure and differ only in the change they expect.
- **The agent checks, David pulls.** Only David runs git; the agent proves the pull brought exactly what was expected and nothing else.
- **Validate on arrival.** A file Anvil cannot read is caught here, before any later step builds on it.
