---
title: "e38-build-plan"
doc-id: "mb-8b5ce355"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 38: Quality testing

**Must achieve:** Tests the feature, and checks that earlier features still work. Findings are written to `step-38-findings.md`, including a clean-pass statement.

**Carried out by:** GStack, using `/qa-only`.

**Runs:** once per feature.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack): tests the feature and every earlier feature in a real browser, report only → `step-38-findings.md`, including a clean-pass statement, then Step 39.
- `mb-sentinel-review`, High → `triage_findings`.

**Not used:** GStack `/qa`, because it commits its own fixes; agents never commit.

**Must be built so that:**
- `/qa-only` tests the public pages signed out as well as the admin pages signed in;

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to QA testing
2. Invoke GStack `/qa` — Systematic QA testing; bug fixing; generates regression tests
3. Verify outputs — QA report with before/after screenshots, fix commits, regression test files; STOP if missing
4. Write Step 38 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-38-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-testing-and-quality.md`: code review and QA

### Code review and QA (Steps 36–38)

Every feature cycle goes through `/design-review` (visual), `/review` (structural), and [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md)
(functional + regression) before its `build-verified` gate. These are GStack skills — they
drive a headless browser for live-site testing, which OpenCode cannot do directly.

This step's testing is its test specification, drawn from the test suite in `C:\dev\project-library-global\test-suite\`.
