---
title: "c26-build-plan"
doc-id: "mb-220a58b2"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 26: Wireframes, phase 2

**Must achieve:** Produces the approved wireframe of every screen: the chosen option, refined with the findings of Step 23.

**Carried out by:** The Magdoub wireframe skill.

**Gate:** `wireframes-approved`: the wireframes are approved and Phase C ends.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `wireframe` (Magdoub), run again per screen, with the chosen option recorded in `design-context.md` so that its safe option extends it, and the Step 23 findings as the optimisation goal → the gate, then Steps 27 and 29.
- The Clean variant is the visual reference for screens. A Polished effect that breaks the M3 standards is not carried into screens.

**Testing:** stage 1 of the two-stage check again, against the approved option.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to wireframe refinement
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 2: Clean + Polished color variants
3. Verify outputs — `styles-opt1.css` through `styles-opt5.css`; STOP if missing
4. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
5. Gate: `wireframes-approved` — Full BFT, gate summary, developer approval required to proceed beyond Phase C
6. Write Step 26 ledger row — `completed_at`
7. Generate Step Receipt — `<project-library>/pdlf/outputs/step-26-receipt.md`
8. Apply BFT — Full (gate override)
9. Follow execution sequence — Housekeeping, stop, wait for continue
