---
title: "skill-use-principle"
doc-id: "mb-5a21b240"
updated: "2026-10-23"
---
# ADR — Skill-Use Principle

**Status:** Accepted


---

## Context

PDLF builds Anvil.works applications through steps that use installed skills from Anvil, GStack, Matt Pocock, Magnus919, Magdoub, Archify and MyBizz. A skill carries a tested method that the agent working alone does not reliably reproduce. A skill's name does not reliably say what it does.

## Decision

1. A skill takes precedence over OpenCode doing the work itself. When a skill covers a task, the step uses it and the agent never improvises that task.
2. Before a skill is chosen, its own `SKILL.md` is read, and what it really does is recorded in the step's build plan.
3. Every skill a step runs produces an output that a named later step, or the developer at a gate, uses. A skill whose output nothing uses is not run.
4. Skills that overlap are compared on what each one actually does. Each is used where it serves best, and both may run in one step.
5. Skill sets are libraries, not pipelines. No skill's output is assumed to reach another skill on its own; each step routes every output deliberately to the step that uses it.
6. Skills are chosen per step by the method in [[[pdlf:pdlf-library/docs-local/pdlf-skills-scoping-strategy|PDLF Skills Scoping Strategy]]](C:/pdlf/pdlf-library/docs-local/pdlf-skills-scoping-strategy.md).

## Consequences

- Every step's build plan lists its skills, what each produces and which step uses it.
- The skills catalog's PDLF Steps column mirrors the step build plans.
- GStack `/autoplan` is not used: PDLF runs the CEO, engineering and design reviews at different steps for different reasons.
