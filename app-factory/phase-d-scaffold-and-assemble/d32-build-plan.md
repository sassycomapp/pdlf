---
title: "d32-build-plan"
doc-id: "mb-b5303e24"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 32: Physical scaffold build

**Must achieve:** The empty modules and functions are created from the scaffold plan and reach Anvil.

**Carried out by:** OpenCode writes the empty modules locally; the developer commits and pushes App 1.

**Skills.** Every skill's output is used by the step named after the arrow.
- `server-code` and `client-modules` (Anvil): write each empty module and function exactly as `scaffold-plan.md` names it, and validate each with `anvil --json validate` → the push, then Step 33.
- `wizard` (Matt Pocock): the developer's instructions for committing and pushing App 1 → Step 33.

**Testing:** every stub in `scaffold-plan.md` exists and validates; nothing exists that the plan does not name.

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
