---
title: "c27-build-plan"
doc-id: "mb-868a7285"
updated: "2026-10-21"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 27: Screen production

**Must achieve:** Produces the screen HTML of every approved wireframe, to the project's screen production standard. Step 29 needs it.

**Carried out by:** OpenCode.

**Skills.** No installed skill produces screens to the project's screen standard; OpenCode produces them as the screen and wireframe production standards require. Every output is used by the step named after the arrow.
- The screen design comes from the approved Magdoub wireframe (Clean variant).
- `client-forms` (Anvil) M3 references and `C:\mybizz\anvil-agent-references\docs\m3`: every element maps to an Anvil M3 component → Step 29.
- The fixed pre-work reading list of the screen and wireframe production standards is read in full first.

**Testing:** both stages of the two-stage check (wireframe fidelity, then standard compliance).

**Standards:** [[[default:specifications-global/spec-screen-and-wireframe-production-standards|Screen and Wireframe Production Standards]]](C:/dev/project-library-global/specifications-global/spec-screen-and-wireframe-production-standards.md), [[[default:specifications-global/spec-screen-production-standard|Screen Production Standard]]](C:/dev/project-library-global/specifications-global/spec-screen-production-standard.md), [[[default:specifications-global/spec-m3_component_mapping|M3 Component Mapping]]](C:/dev/project-library-global/specifications-global/spec-m3_component_mapping.md).

**Must be built so that:**
- no screen uses a component that `DESIGN.md` excludes;

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen production
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Produce screen HTML from approved wireframe (Step 26)
4. Apply wireframe fidelity checklist
5. Apply screen standard compliance checklist
6. Verify outputs — Screen HTML, both checklists; STOP if missing
7. Write Step 27 ledger row — `completed_at` (or `deferred`)
8. Generate Step Receipt — `<project-library>/pdlf/outputs/step-27-receipt.md`
9. Apply BFT — Full level (if active)
10. Follow execution sequence — Housekeeping, stop, wait for continue
