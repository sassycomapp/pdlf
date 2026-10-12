---
title: "d32-build-plan"
doc-id: "mb-b5303e24"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 32: Physical scaffold build

**Must achieve:** The empty modules and functions are created in Anvil from the scaffold plan.

**Carried out by:** The developer, by hand in the Anvil editor.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to scaffold construction
2. Developer: Create empty client-code modules and server modules/functions in Anvil IDE — Per `scaffold-plan.md`
3. Verify stubs exist in Anvil IDE — STOP if missing
4. Write Step 32 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-32-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pdlf-phase-b-review.md`: finding 4.2

**4.2 Choose skills from the catalogue, deliberately.** For each step, read the catalogue and name the skill that best serves it, with the reason. Read that skill's own source before designing around it, and record what it really does in the build-plan entry. Phase C has clear candidates that were not used in Phase B: Anvil's `data-models`, `anvil-yaml` and `client-forms` for the tables and forms; `wizard`, which walks a person through steps only they can perform, for the manual steps in the Anvil editor (Steps 17, 29 and 32); and `writing-for-agents` whenever a step file is written, because step files are instructions for an agent.
