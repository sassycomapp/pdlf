---
title: "e35a-build-plan"
doc-id: "mb-cc2d83a1"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 35A: Testing

**Must achieve:** Broader testing of the feature, and a security check of the development and test tools (`pip-audit`).

**Carried out by:** OpenCode.

**Runs:** once per feature.

**Skills.** Every skill's output is used by the step named after the arrow.
- `tdd` (Matt Pocock): extends the feature's tests to the edge cases in Step 15's test plan → Step 38.
- `pip-audit` (a tool, not a skill) checks the development and test tools → `triage_findings`.
- `/cso --supply-chain` (GStack): checks the feature's dependencies and tooling for supply-chain risk → `triage_findings`.

This step's testing is its test specification, drawn from the test suite in `C:\dev\project-library-global\test-suite\`.
