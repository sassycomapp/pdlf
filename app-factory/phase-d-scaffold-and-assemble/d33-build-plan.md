---
title: "d33-build-plan"
doc-id: "mb-b57f0c0c"
updated: "2026-11-12"
---
# Step 33 — Pull to Local: Build Plan

## Step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 33: Pull to local

**Must achieve:** David's local copy of the app holds exactly what Anvil holds after the scaffold was pushed, so that Step 34 audits the real state of the app.

**Starts from:** Step 32's receipt and stub list; the app's local repository.

**Produces:** the app's local repository level with GitHub; in `pdlf-outputs\d33\`: the test results and the Step Receipt; the ledger row.

**Carried out by:** David runs one command; OpenCode checks the result.

**Must be built so that:**
- the step runs Step 18's pull procedure ([[[pdlf:app-factory/phase-c-design-and-plan/c18-reference|Step 18 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-reference.md)); the change it expects is every module and function on Step 32's stub list, and the filled `tests\ts-config.yaml`;
- any other change, apart from formatting Anvil itself applies, stops the step with a deviation;
- its ledger row is `step_type = 'manual'`, `skill_family = 'manual'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 32.

**BFT level:** None.

**Gate:** none.

**References:** [[[pdlf:app-factory/phase-c-design-and-plan/c18-reference|Step 18 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-reference.md); [[[pdlf:app-factory/phase-c-design-and-plan/c18-config|Step 18 Configuration]]](C:/pdlf/app-factory/phase-c-design-and-plan/c18-config.md).

**Skills.** None; Step 18's procedure is plain commands.

**Layers with no skill:** all; the step only moves code.

**Testing:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d33-test-spec|Step 33 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d33-test-spec.md): only the expected change arrived, and the app validates.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md).

## Why it is built this way

- **One procedure.** The pull and its checks are written once, at Step 18; this step names only the change it expects.
- **Audit the real app.** Step 34 must audit what Anvil holds, including any formatting Anvil applied on the push.
