---
title: "pol-skill-invocation"
doc-id: "mb-507292ab"
updated: "2026-10-09"
---
# PDLF Policy — Skill Invocation

**Binding.** The agent must comply whenever a skill is invoked during the pipeline.

---

## What

### Skill-use principle

A GStack or Matt Pocock skill is invoked **only** when it performs a task better than OpenCode
could do directly with the model. If a task is simple enough that OpenCode can do it natively,
no skill is invoked — the orchestrator just does the work.

Every skill named in the Step Table is there because it was checked against this principle and
found to add real, unique value. A skill's presence in the table must always be justified, not
assumed.

### Read before invoke

Before invoking any skill, the agent reads that skill's own SKILL.md to confirm it is the right
tool. **Never trust a skill name alone.** Two rounds of self-assessment have documented real
mapping errors caused by trusting a skill name instead of reading its content:

**July 2026 (v5):**
- `/autoplan` is a pipeline orchestrator, not a standalone tool — using it AND individual reviews
  is redundant
- `/spec` creates GitHub issues, not project framing
- `/design-review` needs a live URL — it cannot run before the app is running
- `/grill-me` is stateless `/grill-with-docs` — redundant if `/grill-with-docs` already ran
- `/codebase-design` is reference vocabulary, not a file-producing skill

**July 2026 (v6, this pass):**
- `to-prd`/`to-spec` (formerly Step 13) had no confirmed downstream consumer — verified
  directly against [[[pdlf:makepdlf-project-library/stepwise/step-14-plan-ceo-review|Step 14 Plan Ceo Review]]](C:/pdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md)'s GBrain query schema, which does not reference an
  issue-tracker or spec artifact at all. Removed.
- `prototype` (formerly Step 25) was optional and non-chained, with no consumer anywhere
  downstream. Removed.
- `/review` and [[[pdlf:makepdlf-project-library/stepwise/step-38-qa|/qa]]](C:/pdlf/makepdlf-project-library/stepwise/step-38-qa.md) (Steps 37, 38) were assumed to persist their findings for [[[pdlf:makepdlf-project-library/stepwise/step-39-triage|triage]]](C:/pdlf/makepdlf-project-library/stepwise/step-39-triage.md)
  (Step 39) to act on. GStack's own repository states this behavior is unverified even by
  the maintainer. Both steps now explicitly require writing findings to a specified artifact
  path, verified by OpenCode before the step is marked complete — the assumption is no longer
  trusted un-checked.

These errors were only caught by reading the actual skill files, not by trusting what a skill's
name or reputation implied. The rule is not optional.

### Progressive disclosure

The PDLF orchestrator skill is deliberately lean — step table and control loop only. Detailed
procedures (testing, sanity audits, Anvil mechanics, execution discipline, BFT reference,
gate procedure) live in separate stepwise files loaded at the step that needs them. Do not
inline reference file content into the orchestrator.

### Agent never does a skill's job manually

If the Step Table prescribes a skill, the agent invokes it. If the skill cannot be invoked,
the agent presents a deviation request — it does not silently do the work manually. The
developer decides whether the manual alternative is acceptable.

### Output routing

Skills save where they are designed. The orchestrator does not override a skill's default
save location. The project's AGENTS.md governs where copies of each producer's output are
stored.

---

## Why

Stated directly by the developer. Proven by documented errors across two review passes. The
skill-use principle retroactively simplified an entire sub-project: the two sanity-audit gates
don't need custom skills — cross-referencing markdown documents is well within OpenCode's
native capability. They are documented procedures, not skills, saving development effort and
avoiding unnecessary tool dependencies. The same principle, applied a second time in July 2026,
removed two more skills from the live pipeline.

---

## Where

Every step in the pipeline where the Step Table names a skill. Invocation procedure at
[[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).

**Source:** [[[pdlf:makepdlf-project-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-skill-design.md) §2.3, §2.5, §2.12, [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md),
`skill/agents-self-assessment-20260701.md` (retired, verified absent).

---

*Updated 2026-07-12: removed stale references to `to-prd` and `/prototype` as live examples
(both now removed from the pipeline); added the v6 self-assessment findings.*
