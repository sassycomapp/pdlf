---
title: "d30-build-plan"
doc-id: "mb-0bbaa200"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 30: Pull to local

**Must achieve:** The code repository is pulled to local after the forms are built.

**Carried out by:** The developer, by hand.

**Skills.** Every skill's output is used by the step named after the arrow.
- The shared pull procedure of Step 18.
- `client-forms` (Anvil): validates every pulled form with `anvil --json validate` → Step 31.

**Testing:** every form validates, and every approved screen has its form locally.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Component tree with Anvil AI's wiring
3. Verify local repo updated — STOP if UI forms not present
4. Write Step 30 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-30-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pdlf-phase-b-review.md`: finding 4.7

**4.7 Fit for purpose before thoroughness.** For each step, ask whether it earns its place. Phase C has three near-identical "pull to local" steps (18, 30 and 33): one shared procedure may serve all three. For each review, ask what only it covers, so that the developer is never asked the same question twice.

## From `pol-anvil-platform.md`: pull to local

| Pull | After |
|---|---|
| Step 30 | UI forms built in Anvil at Step 29. |
