---
title: "d29-build-plan"
doc-id: "mb-095646a3"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 29: Build UI forms

**Must achieve:** The forms are built in Anvil from the approved wireframes.

**Carried out by:** The developer with Anvil's AI, by hand in the Anvil editor.

**Skills.** Every skill's output is used by the step named after the arrow.
- `wizard` (Matt Pocock): the developer's instructions for each form: which wireframe HTML, screen HTML and screen PNG to give Anvil's AI, in what order, and the theme values from `DESIGN.md` (brand colour first in `theme/parameters.yaml`, the logo) → the forms, then Step 30.
- Anvil's AI in the Anvil editor builds each form from those three inputs and wires its components, using Anvil's own skills.

**Working with Anvil's AI.** Anvil's in-editor agent edits forms, components, client modules, server modules, the theme and CSS. It runs on the developer's own Claude account (connected under the agent's settings), cannot read Anvil Secrets, and commits its own changes automatically. For each form, the developer:
1. Starts a fresh conversation, names the form with `@` (for example `@CheckoutForm`), and attaches the screen PNG as an image (up to 10 MB).
2. Pastes the wireframe HTML and the screen HTML, states the goal in one sentence, names the M3 components and theme roles to use, and says what must not be touched: other forms, server modules, the schema.
3. Asks for a plan first, and approves or corrects it before any change is made.
4. Has the form built in small steps: layout, then components, then navigation and events. Each step is checked in the running app before the next.
5. Uses `/compact` when a conversation grows long, and a new conversation for each form.
6. Applies no schema change the agent proposes. The schema is fixed at Step 17; a proposed change goes back to Step 17.
7. Pulls the result locally at Step 30, where it is validated.

**Testing:** every approved screen has a form; every form validates (`anvil --json validate`); the UI conformance scans pass (Material 3 components only, no `HTMLTemplate`, no hard-coded colours, dark mode, no data rules or secrets in forms), as `d29-test-spec.md` sets out. **Layers with no skill:** security (forms hold no data rules; the scans check this here, Step 34 checks it for the whole app).

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) section 9, [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md), [[[default:specifications-global/spec-material-3-theme|Material 3 Theme]]](C:/dev/project-library-global/specifications-global/spec-material-3-theme.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to UI form construction
2. Developer + Anvil AI: Build UI forms in Anvil IDE — From approved wireframes and screens
3. Verify forms exist in Anvil IDE — STOP if missing
4. Write Step 29 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-29-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pdlf-phase-b-review.md`: finding 4.2

**4.2 Choose skills from the catalogue, deliberately.** For each step, read the catalogue and name the skill that best serves it, with the reason. Read that skill's own source before designing around it, and record what it really does in the build-plan entry. Phase C has clear candidates that were not used in Phase B: Anvil's `data-models`, `anvil-yaml` and `client-forms` for the tables and forms; `wizard`, which walks a person through steps only they can perform, for the manual steps in the Anvil editor (Steps 17, 29 and 32); and `writing-for-agents` whenever a step file is written, because step files are instructions for an agent.
