---
title: "pol-skill-invocation"
doc-id: "mb-507292ab"
updated: "2026-10-10"
---
# PDLF Policy — Skill Invocation

**Binding.** The agent must comply whenever a PDLF step involves work that a skill covers.

---

## What

1. **Skills take precedence.** When a skill in PDLF's library covers a task, the agent uses that skill. It never improvises the task itself, and never does a skill's job by hand.
2. **A skill earns its place.** A skill joins the library only if it serves PDLF's objectives better than any alternative. The library holds nothing superfluous and lacks nothing needed. The skills catalog in mybizz-os ([[[mybizz-os-docs:os-reference-docs/skills-catalog|Skills Catalog]]](C:/mybizz/mybizz-os-docs/os-reference-docs/skills-catalog.md)) is the single register of installed skills; which skill each step uses is set in that step's design.
3. **Read before invoking.** Before invoking a skill, the agent reads the skill's own file to confirm it is the right tool and how it behaves. A skill's name is never trusted on its own.
4. **User-invoked skills are asked for.** When a skill can only be started by the user, the agent asks David to start it. It never simulates the skill.
5. **When a skill cannot run.** If the prescribed skill cannot be invoked, the agent raises a deviation ([[[pdlf:pdlf-library/policy-local/pol-sequential-enforcement-and-deviation|Policy: Sequential Enforcement and Deviation]]](C:/pdlf/pdlf-library/policy-local/pol-sequential-enforcement-and-deviation.md)). It does not quietly do the work another way.
6. **Outputs.** A skill saves where it is designed to save. The orchestrator does not change that; it captures the location, records it, and writes the copy to `output/` ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md)).
7. **Lean orchestrator.** The orchestrator holds only the step pattern and the step order. Each step's detail lives in its own step file and module, loaded when that step runs.

---

## Why

A skill in the library has been chosen because it does its task well and in a known way. If the agent improvises instead, the result depends on the agent's judgement in that moment, which is exactly what David cannot check. Using the skill every time makes the work repeatable and its quality known.

A skill's name is an unreliable guide to what it does. Reading the skill's own file is the only way to know.

---

## Where

Every step whose task a skill covers. The invocation procedure is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
