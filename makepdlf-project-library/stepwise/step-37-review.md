---
title: "step-37-review"
doc-id: "mb-bb95a7ee"
updated: "2026-10-09"
---
## Task Execution Order

1. Run GStack `/review`, Standards axis pointed at `specifications-global/`
   (particularly `[[spec-security]]`, `[[spec-regulatory-compliance-baseline]]`, and, once
   written, the retired `spec-coding-standards.md`), Spec axis against the originating ticket/plan.
2. Regardless of outcome, write findings to
   `<project-library>/pdlf/outputs/step-37-findings.md`. If there are no findings, the
   file must still be written, stating explicitly "no findings, clean pass."
3. → Verification point: OpenCode confirms the file exists and is non-empty before this
   step is marked complete. Absence is always a step failure — never a silent pass.
4. Follow execution sequence in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
5. Apply BFT per [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (Full).

---

## Description

Pre-landing code review — finds bugs that pass CI but would break in production.
Auto-fixes the obvious ones. This step's findings are the primary input to Step 39
([[[pdlf:makepdlf-project-library/stepwise/step-39-triage|triage]]](C:/pdlf/makepdlf-project-library/stepwise/step-39-triage.md)); because GStack's own repository states its skills' persistence behavior is
unverified even by the maintainer, this step cannot be trusted to have written anything
down without an explicit check.

## Inputs Required

- Current branch's git diff against base branch
- Plan file / originating ticket (for Plan Completion Audit)
- `specifications-global/` (Standards axis reference)
- Optional PR description and TODOS.md

## Outputs

- Review report (Plan Completion Audit, Scope Drift check, specialist findings)
- One AUTO-FIXED commit per mechanical fix
- `<project-library>/pdlf/outputs/step-37-findings.md` — mandatory, non-empty, present
  even on a clean pass

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 37 | Skill | | GStack `/review` |

---

## Reference

Artifact-persistence requirement rationale: ADR-0009.
Standards axis pointed at global specs, not a separate CI system: ADR-0012.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
