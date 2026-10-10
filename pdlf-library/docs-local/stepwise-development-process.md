---
title: "stepwise-development-process"
doc-id: "mb-311cf022"
updated: "2026-10-10"
---
# Stepwise Working Document

**Purpose:** Defines the working process for developing the PDLF stepwise skill files.
This is a process definition document, not a binding policy. Updated incrementally as
decisions are made.

**Status:** Living working document. Last revised: 2026-07-12.

---

## A. Discussion and Collaboration

- Discussion is incremental — do not discuss the entire skill at once. Work one topic at a time.
- The developer leads the process. The agent advises, proposes, and discusses, but does not run ahead and develop.
- The agent's proposals are advisory. All decisions rest with the developer.
- Do not assume the developer's intent. Wait for direction.
- Apply recommended solutions with options presented for developer decision.

## B. Stepwise File Identity

- Every stepwise file is a complete, standalone skill with YAML front matter.
- The PDLF orchestrator skill (SKILL-v5) glues the stepwise skills together in execution order.
- Stepwise files must be short, concise, and highly focused. They are skills, not discussion or descriptive documents.
- No rationale. No design discussion. Cross-references only when necessary.
- Each file follows the `writing-great-skills` information hierarchy: steps first, reference second.
- `disable-model-invocation: true` — these are orchestrator-invoked skills.
- The exact number of stepwise files needed is unknown at this stage — do not assume a fixed count.

## C. Numbering

**Superseded 2026-07-12** — see note at end of this section. Original text retained below for
history:

- ~~Renumbering starts from 11, leaving slots 1–10 open for future expansion.~~
- ~~Numbering is fluid and NOT locked during development.~~
- ~~Do not hard-code or assume any numbering scheme at this stage.~~

**Current convention:** Canonical step numbers are now fixed identifiers and are no longer
fluid. They never indicate execution order — execution order lives exclusively in [[[pdlf:stepwise/run-plan|Run Plan]]](C:/pdlf/stepwise/run-plan.md). New steps inserted between existing canonical numbers use a letter suffix
on the nearest preceding number (e.g., `35A`, `40B`) rather than renumbering. Slots 1 and
4–10 remain reserved. Slots 2–3 were briefly defined for an existing-project
registration/audit branch, then retired 2026-07-18 along with the disposition-audit model
they implemented — existing-project entry is handled inside Step 11 itself.

## D. Template

- All stepwise files share a common template (to be defined).
- The template starts blank and is built and edited as progress is made.

## E. Source Documents

- `skill/SKILL-v4.md` — absorbed into stepwise files. No longer exists as standalone.
- `docs-local/skill-workflow-table.md` — absorbed into stepwise files. No longer exists as standalone.
- `policy-local/pol-stepwise.md` — this file. Working document defining the stepwise process.
- [[[pdlf:pdlf-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md) — design rationale (reference only, not runtime). `spec-architecture.md`, formerly listed here, was retired 2026-07-18 — its accurate content was migrated into [[[pdlf:pdlf-library/specifications-local/spec-nomenclature|Spec: Nomenclature]]](C:/pdlf/pdlf-library/specifications-local/spec-nomenclature.md).

## F. Shared Reference Documents

- [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) — 13-point execution sequence, step-type routing, deviation mechanism.
- [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) — Six BFT questions, levels, gate rule, anti-rubber-stamping.
- [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) — Gate ceremony, seven gates, approval flow.
- [[[pdlf:stepwise/step-mapping|Step Mapping]]](C:/pdlf/stepwise/step-mapping.md) — Step number → file → phase → handler → gate lookup. Folded in what used to be a separate `INDEX.md`, 2026-07-18.
- [[[pdlf:stepwise/run-plan|Run Plan]]](C:/pdlf/stepwise/run-plan.md) — Execution order decision tree; the sole authority on sequence.

## G. Skill Ecosystem

**Corrected 2026-07-12:**

- **GStack skills:** office-hours, plan-ceo-review, plan-eng-review, design-consultation,
  plan-design-review, plan-devex-review, design-review, review, qa, ship, canary.
- **Matt Pocock skills:** [[[pdlf:stepwise/step-16-domain-modeling|Step 16 Domain Modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) (invoked via `/grill-with-docs`, not directly —
  [[[pdlf:stepwise/step-16-domain-modeling|Step 16 Domain Modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) is an inline discipline, not a standalone runnable session, confirmed
  against its real skill source 2026-07-18), [[[pdlf:stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/stepwise/step-19-to-tickets.md), `triage`,
  [[[pdlf:stepwise/step-40-improve-codebase-architecture|Step 40 Improve Codebase Architecture]]](C:/pdlf/stepwise/step-40-improve-codebase-architecture.md).
  `to-prd`/`to-spec` and `prototype` are **removed** from the pipeline — not part of the
  active skill ecosystem. `to-issues` is renamed [[[pdlf:stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/stepwise/step-19-to-tickets.md).
- **Magdoub:** Claude Wireframe Skill (Steps 22, 26).
- **OpenCode-native (new):** the lettered sub-steps (35A testing, 38A CI confirmation, 40B
  remediation, 42A staging integration/E2E) and the existing-project entry steps (2, 3) are
  OpenCode-native procedures, not third-party skills.

## H. Reference Patterns

- Shared procedure: one-line context pointer (e.g., "Follow the execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)")
- Policy: `policy-local/pol-*.md`
- Template: `templates-local/*.md`
- Global spec: `C:\dev\project-library-global\specifications-global\spec-*.md`
- Global ADR: `C:\dev\project-library-global\adr-global\*.md`
- No placeholder path convention — literal paths throughout (`<pdlf-home>` and
  `<project-library>` were retired 2026-07-18; `spec-architecture.md`, which originally
  defined their resolution, is itself retired)
