---
title: "e36-build-plan"
doc-id: "mb-06eb6076"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 36: Design review

**Must achieve:** A visual audit of the feature as it will ship, after any fixes from Step 40B.

**Carried out by:** OpenCode, with GStack `browse`.

**Runs:** once per feature.

**Skills.** Every skill's output is used by the step named after the arrow.
- `browse` (GStack): screenshots of the feature as it runs → compared with the approved screen PNG from Step 28 and stage 2 of the two-stage check in the screen and wireframe production standards → `step-36-findings.md`, including a clean-pass statement, then Step 39.

**Not used:** GStack `/design-review`, because it commits each fix itself; agents never commit.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to visual audit
2. Invoke GStack `/design-review` — 80-item live-site visual audit; before/after screenshots, atomic fix commits
3. Verify outputs — Design audit report, screenshots, fix commits; STOP if missing
4. Write Step 36 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-36-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-testing-and-quality.md`: code review and QA

### Code review and QA (Steps 36–38)

Every feature cycle goes through `/design-review` (visual), `/review` (structural), and [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md)
(functional + regression) before its `build-verified` gate. These are GStack skills — they
drive a headless browser for live-site testing, which OpenCode cannot do directly.

This step's testing is its test specification, drawn from the test suite in `C:\dev\project-library-global\test-suite\`.
