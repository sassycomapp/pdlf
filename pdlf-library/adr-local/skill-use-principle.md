---
title: "skill-use-principle"
doc-id: "mb-5a21b240"
updated: "2026-10-11"
---
# ADR — Skill-Use Principle

**Status:** Accepted

**Date:** 2026-07-10

---

## Context

The PDLF pipeline invokes external skills (GStack, Matt Pocock, Claude Wireframe)
at specific steps. A v2 self-assessment in July 2026 identified six specific mapping
errors where skills were prescribed for tasks they did not actually perform. The
developer stated explicitly that the orchestrator should not invoke a skill by default
— it should invoke a skill only when that skill genuinely adds value over what OpenCode
can do directly.

## Decision

A skill is invoked only when it performs a task better than OpenCode could do directly
with the model. A skill's presence in the Step Table must always be justified, not
assumed. Before invoking any skill, the agent reads that skill's own SKILL.md to
confirm it is the right tool. Never trust a skill name alone.

## Consequences

- The two sanity-audit gates (Steps 21 and 34) are OpenCode-native procedures, not
  custom skills — cross-referencing markdown documents is well within OpenCode's
  native capability.
- Conversely, [[[pdlf:app-factory/phase-e-build-and-verify/38-qa|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/38-qa.md) IS a skill because it drives a headless browser — something
  OpenCode cannot do at all. [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md) IS a skill because its six-question
  structured interview is better than conversational questioning.
- The "read before invoke" rule has documented evidence of preventing real errors.
- The GStack `/autoplan` (runs CEO/Eng/Design reviews all at once) is explicitly NOT
  used because PDLF runs those reviews at different stages for different reasons.
