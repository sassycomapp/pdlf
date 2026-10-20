---
title: "f46-build-plan"
doc-id: "mb-9d39104e"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is the clone of App 1's approved code into App 2, `master_template`, which every client instance depends on.

#### Step 46: Learning

**Must achieve:** The retrospective: what this build taught is captured and written into the sources the next build reads.

**Carried out by:** OpenCode.

**Gate:** `released`: the build cycle closes.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/retro` (GStack): what the build taught, from its history → the lessons.
- `/learn` (GStack): exports what GStack's own skills learned during this build → the lessons.
- `mb-submit-memory`: each approved lesson, once written into the source the next build reads, is submitted as a governed fact → GBrain, for the next build.

**Not used:** GStack `/context-save`; the ledger already records where a build stands.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to retrospective and learning
2. Invoke GStack `/retro` — Retrospective report
3. Invoke GStack `/learn` — Capture learnings
4. Invoke GStack `/context-save` — Persist working state
5. Update ISA — Fill Verification section, update Changelog
6. Update registry — `current_step: 46`, `last_gate: "released"`, `active: false`
7. Sync and embed GBrain — Learnings now searchable for next project
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `released` (jointly with Step 45) — Full BFT, gate summary, developer approval required to close the project cycle
10. Write Step 46 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-46-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop
