---
title: "c17-build-plan"
doc-id: "mb-2b6de0f2"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 17: Create Anvil data tables

**Must achieve:** The data tables are built in Anvil from the domain model and the ADRs.

**Carried out by:** OpenCode writes the schema; the developer applies it in the Anvil editor.

**Must be built so that:**
- the agent writes the tables into `db_schema` in App 1's `anvil.yaml` only through Anvil's `anvil-yaml` skill, from the data design locked at Step 16, and validates the file with `anvil --json validate anvil.yaml`;
- every new table defaults to `client: none`, as `data-models` and `anvil-yaml` require;
- the developer pushes the change and applies the schema in Anvil's Data Tables view, following numbered instructions the agent writes with `wizard`;
- after Step 18, the agent compares the tables in `anvil.yaml` with the data design and stops with a deviation on any difference.

**Skills.** Every skill's output is used by the step named after the arrow.
- `data-models` (Anvil): table ownership, model classes and client access → the schema, then Steps 29, 31 and 35.
- `anvil-yaml` (Anvil): writes `db_schema` and validates it → the developer's apply in the Anvil editor, then Step 18.
- `wizard` (Matt Pocock): the developer's instructions for pushing and applying the schema → Step 18.
- `secure-software-engineering` (Magnus919): checks every table's access against the trust boundaries from Step 15 → the schema.
- `mb-sentinel-review`, High → `triage_findings`.

**Testing:** `anvil --json validate` passes, and the pulled tables match the data design. **Layers with no skill:** display, documentation (the schema is its own record).

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) section 10 (access rules), [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).

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
