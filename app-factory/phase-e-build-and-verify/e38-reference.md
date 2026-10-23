---
title: "e38-reference"
doc-id: "mb-1c768333"
updated: "2026-10-23"
---

## From `38-qa.md`

## Task Execution Order

1. Run GStack [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md) against the live/local URL, covering cross-feature flows and
   regression testing against everything built before this feature — not limited to the
   single feature just built (that narrower check is Step 35's Level 3).
2. Regardless of outcome, write findings to
   `<project-library>/pdlf/outputs/step-38-findings.md`. If there are no findings, the
   file must still be written, stating explicitly "no findings, clean pass."
3. → Verification point: OpenCode confirms the file exists and is non-empty before this
   step is marked complete. Absence is always a step failure — never a silent pass.
4. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
5. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full).

---

## Description

Systematic QA testing and bug fixing. Generates regression tests. Deliberately broader in
scope than Step 35's Level 3 check — Level 3 verifies the single feature just built; this
step verifies that feature against everything else in the application (see ADR-0010).
Like Step 37, its findings feed Step 39 ([[[pdlf:app-factory/phase-e-build-and-verify/e39-reference|triage]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-reference.md)) directly, so persistence is mandatory,
not assumed.

## Inputs Required

- Live/local URL
- Project-scoped test plan (from Steps 14–15)
- Clean working tree
- Prior features' state, for regression coverage

## Outputs

- Structured QA report with before/after screenshots
- One atomic fix commit per verified bug
- Auto-generated regression test files committed to codebase
- `<project-library>/pdlf/outputs/step-38-findings.md` — mandatory, non-empty, present
  even on a clean pass

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 38 | Skill | | GStack [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference\|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md) |

## Reference Files

| [[[pdlf:pdlf-library/templates-local/isa-template\|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template.md) | Steps 26, 35, 39, 46 |

---

## Reference

Artifact-persistence requirement rationale: ADR-0009.
Scope distinction vs. Step 35 Level 3: ADR-0010.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
