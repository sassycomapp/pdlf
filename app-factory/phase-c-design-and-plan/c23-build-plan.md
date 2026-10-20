---
title: "c23-build-plan"
doc-id: "mb-780ca546"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 23: Plan design review

**Must achieve:** Rates the chosen wireframes and `DESIGN.md` for usability and identifies gaps.

**Carried out by:** GStack, using `/plan-design-review`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/plan-design-review` (GStack) → the findings, which are the optimisation goal of Step 26.

**Testing:** every finding is either fixed at Step 26 or declined by the developer, and the review file records which.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design review
2. Invoke GStack `/plan-design-review` — Rates UX dimensions 0–10, identifies gaps
3. Verify outputs — GSTACK REVIEW REPORT appended to plan file; STOP if missing
4. Write Step 23 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-23-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue
