---
title: "stepwise-decomposition-model"
doc-id: "mb-bd17f7b3"
updated: "2026-10-11"
---
# ADR — Stepwise Decomposition Model

**Status:** Accepted

**Date:** 2026-07-10

---

## Context

SKILL-v4 was a monolith skill — a single 492-line file containing the step table,
execution discipline, gate procedure, BFT rules, and all operational content. The
developer's stated intent is for the final PDLF skill to be broken into 46 separate
skills, each a complete self-contained entity, with an orchestrator that glues them
together.

## Decision

Each numbered step (11–46) becomes its own stepwise skill file in `stepwise/` (since 2026-10-11: its own step file in its phase folder in `app-factory/`). Five
shared reference documents ([[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec Bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md),
[[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), `INDEX.md`, [[[pdlf:pdlf-library/docs-local/orchestrator-run-plan|Run Plan]]](C:/pdlf/pdlf-library/docs-local/orchestrator-run-plan.md)) provide single-source-of-truth
procedures that individual stepwise files reference via context pointers. This follows
the `writing-great-skills` information hierarchy: push shared material to disclosed
reference, keep step-specific content in-skill.

## Consequences

- SKILL-v4.md is absorbed and no longer exists as a standalone file.
- The `skill-workflow-table.md` is absorbed and no longer exists.
- The 5 shared reference files eliminate duplication — the execution sequence, BFT
  questions, and gate ceremony are defined once, referenced 36+ times.
- Each stepwise file is independently loadable and understandable.
- Renumbering starts at 11; slots 1 and 4–10 remain reserved for future steps, slots
  2–3 are now defined as the existing-project entry branch (see
  the retired `sop-existing-project-resume-audit.md`).
- The orchestrator (SKILL-v5) loads stepwise files in execution order per [[[pdlf:pdlf-library/docs-local/orchestrator-run-plan|Run Plan]]](C:/pdlf/pdlf-library/docs-local/orchestrator-run-plan.md),
  not numerical sequence.
- The clean 11–46 numbering has since been extended with lettered sub-steps for
in-loop insertions (`35A`, `38A`, `40B`, `42A`) rather than further renumbering —
    see the superseding note on [[[pdlf:pdlf-library/adr-local/renumbering-11-to-46|Renumbering 11 to 46]]](C:/pdlf/pdlf-library/adr-local/renumbering-11-to-46.md).
