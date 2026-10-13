---
title: "c17-build-plan"
doc-id: "mb-2b6de0f2"
updated: "2026-10-13"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 17: Create Anvil data tables

**Must achieve:** The data tables are built in Anvil from the domain model and the ADRs.

**Carried out by:** The developer, by hand in the Anvil editor.

**Must be built so that:**
- Anvil's `anvil-yaml` skill is never used to write `anvil.yaml`, because no agent ever writes `anvil.yaml` (Anvil manages it); the tables are created by the developer in the Anvil editor, and the agent only reads `anvil.yaml` after it is pulled to local, to verify the tables exist.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to schema construction
2. Developer: Build data tables/schema in Anvil IDE — Per ADRs and authoritative schema from Steps 15–16
3. Verify tables exist — STOP if missing
4. Write Step 17 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-17-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pdlf-phase-b-review.md`: finding 4.2

**4.2 Choose skills from the catalogue, deliberately.** For each step, read the catalogue and name the skill that best serves it, with the reason. Read that skill's own source before designing around it, and record what it really does in the build-plan entry. Phase C has clear candidates that were not used in Phase B: Anvil's `data-models`, `anvil-yaml` and `client-forms` for the tables and forms; `wizard`, which walks a person through steps only they can perform, for the manual steps in the Anvil editor (Steps 17, 29 and 32); and `writing-for-agents` whenever a step file is written, because step files are instructions for an agent.
