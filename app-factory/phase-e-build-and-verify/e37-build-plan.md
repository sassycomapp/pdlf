---
title: "e37-build-plan"
doc-id: "mb-78301dea"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 37: Code review

**Must achieve:** Reviews the feature's code for bugs that would break in use. Findings are written to `step-37-findings.md`, including a clean-pass statement.

**Carried out by:** Matt Pocock, using `code-review`, with GStack `/cso`.

**Runs:** once per feature.

**Skills.** Every skill's output is used by the step named after the arrow.
- `code-review` (Matt Pocock): reviews the feature's changes against the project's standards (the Anvil standards in `project-library-global` and the Anvil skills' rules) and against its ticket → `step-37-findings.md`, then Step 39.
- `/cso --diff` (GStack): a security review of this feature's changes only → `step-37-findings.md`.
- `mb-sentinel-review`, Very High → `triage_findings`.

**Not used:** GStack `/review`, because it applies fixes itself; fixes are decided at Step 39 and made at Step 35.

**Must be built so that:**
- `code-review` also checks the code against [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md);

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to pre-landing code review
2. Invoke GStack `/review` — Finds bugs that pass CI but would break in production; auto-fixes obvious ones
3. Verify outputs — Review report, AUTO-FIXED commits; STOP if missing
4. Write Step 37 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-37-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-testing-and-quality.md`: code review and QA

### Code review and QA (Steps 36–38)

Every feature cycle goes through `/design-review` (visual), `/review` (structural), and [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md)
(functional + regression) before its `build-verified` gate. These are GStack skills — they
drive a headless browser for live-site testing, which OpenCode cannot do directly.

This step's testing is its test specification, drawn from the test suite in `C:\dev\project-library-global\test-suite\`.
