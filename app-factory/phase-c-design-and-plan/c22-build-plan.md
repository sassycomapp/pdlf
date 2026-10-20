---
title: "c22-build-plan"
doc-id: "mb-70132173"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 22: Wireframes, phase 1

**Must achieve:** Produces the wireframes for every screen the tickets need: five options per screen, in black and white with Clean and Polished colour variants. The developer chooses one option per screen.

**Carried out by:** The Magdoub wireframe skill.

**Skills.** Every skill's output is used by the step named after the arrow.
- `wireframe` (Magdoub), scope "wireframes and visuals", one run per screen, from the tickets, the flows and `design-context.md` → the developer's choice of option, then Steps 23 and 26.
- The skill writes to `wireframe\` in the project library, its canonical place; a copy goes to `pdlf-outputs\c22\`.

**Testing:** stage 1 of the two-stage check (wireframe fidelity) in the screen and wireframe production standards.

**Standards:** [[[default:specifications-global/spec-screen-and-wireframe-production-standards|Screen and Wireframe Production Standards]]](C:/dev/project-library-global/specifications-global/spec-screen-and-wireframe-production-standards.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe generation
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 1: 5 B&W UX wireframe approaches
3. Verify outputs — `wireframe/brain/design-context.md`, `design-taste.md`, `wireframe/DDMM-{feature}/index.html` + `styles.css`; STOP if missing
4. Write Step 22 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-22-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue
