---
title: "step-15-plan-eng-review"
doc-id: "mb-db592636"
updated: "2026-10-12"
---
## Task Execution Order

1. Query GBrain for context relevant to engineering review (automatic, read-only).
   Sources nominated explicitly: `{slug}`, `{slug}-project-library`,
   `project-library-global`.
2. Check Step 14's mode, recorded in the ledger, to determine which plan artifact
   exists: for SCOPE EXPANSION or SELECTIVE EXPANSION, a real GStack-native plan file
   exists at `~/.gstack/projects/{slug}/ceo-plans/{date}-{feature-slug}.md`; for HOLD
   SCOPE or SCOPE REDUCTION, no GStack-native file exists — only the stable copy at
   `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-14-ceo-plan.md`.
3. Assemble context: the plan artifact identified at item 2, `design-doc.md`,
   `design-doc-first-concept.md`, and the [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output file if it ran.
4. Local/global conflict check: compare anything in `{slug}-project-library` this
   review touches against `project-library-global`. Global wins by default. A real
   reason to diverge goes through a deviation request to the developer — same
   mechanism as Step 14's own conflict check; [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)'s `SKILL.md` has zero
   reference to `project-library-global`, confirming this is entirely OpenCode's own
   comparison, not something the skill surfaces on its own.
5. Invoke GStack [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md), pasting the full text of everything assembled at
   item 3 directly into the invocation prompt. State explicitly that a design doc
   already exists and is provided above — same preemption technique as Step 14, for
   the same reason: the skill runs its own design-doc glob regardless of what's
   pasted, and if it comes up empty, its own prerequisite offer would otherwise
   silently reopen a decision Step 12 already closed.
6. The skill runs its pre-review system audit (git history, TODOs, existing code, the
   design-doc glob, a handoff-note glob), then Step 0: **Scope Challenge** — genuinely
   different content from Step 14's Step 0 (mode selection). No SCOPE
   EXPANSION/EXPANSION/HOLD/REDUCTION framework here. Scope Challenge runs, in order:
   an existing-code-leverage check; a minimum-change check; a complexity trigger (8 or
   more files, or 2 or more new classes/services) — if triggered, STOP: mandatory
   `AskUserQuestion` proposing a minimal version; do NOT proceed to Section 1 until the
   developer responds; Search-Before-Building (Layer 1/2/3 plus EUREKA); a
   `TODOS.md` cross-reference; a completeness check; a distribution check (the
   build/publish pipeline for any genuinely new artifact type).
7. Section 1 — Architecture review, including a distribution-architecture sub-check.
   Each finding gets its own `AskUserQuestion` — never batched. STOP until the
   developer responds to each one individually.
8. Section 2 — Code Quality review. Same per-finding `AskUserQuestion` discipline.
9. Section 3 — Test review: coverage diagram, E2E decision matrix, and the
   REGRESSION RULE, which is mandatory and does not require an `AskUserQuestion`.
   During this section, the skill writes the ONE genuinely separate file this step
   produces: the Test Plan Artifact, at
   `~/.gstack/projects/{slug}/{user}-{branch}-eng-review-test-plan-{datetime}.md`.
   Same per-finding `AskUserQuestion` discipline applies to the rest of this section.
10. Section 4 — Performance review. Same per-finding `AskUserQuestion` discipline.
11. Required Outputs — written INTO the plan file itself, not as separate documents.
    **Confirmed directly against source, correcting an earlier draft's error: there is
    no five-document TDD cluster.** [[[mb-3-cs-project-library:docs-local/architecture|architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/architecture.md) (mb-3-cs project library), [[[mb-3-cs-project-library:docs-standard-local/integration-architecture|integration-architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/integration-architecture.md) (mb-3-cs project library),
    the retired `security-architecture-canonical.md`, [[[mb-3-cs-project-library:docs-standard-local/globals-contract|globals-contract]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/globals-contract.md) (mb-3-cs project library), and
    [[[mb-3-cs-project-library:docs-local/authoritative-schema|authoritative-schema]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/authoritative-schema.md) (mb-3-cs project library) do not exist anywhere in the skill's real source. The
    Required Outputs subsections, all landing in the same plan file: what is NOT in
    scope; what already exists; `TODOS.md` updates (each gets its own
    `AskUserQuestion`); diagrams (ASCII plus inline comment recommendations); failure
    modes; a worktree parallelization strategy.
12. Outside Voice — an independent AI-model review, default-on. Informational only; it
    never gates shipping. Any finding it raises needs an explicit accept or reject from
    the developer — never auto-incorporated.
13. The skill appends `## GSTACK REVIEW REPORT` to the same plan file (delete-then-
    append-at-end), ending with either `NO UNRESOLVED DECISIONS` or an explicit
    `**UNRESOLVED DECISIONS:**` block.
14. → Decision point: whether the skill's own append-in-place mechanic actually finds
    "the active plan file" inside an OpenCode invocation is not confirmed by source on
    either side ([[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)'s or OpenCode's). If it does not, the skill's file
    write may silently no-op. This does not block the step: the orchestrator captures
    the review's real findings directly from the skill's conversational output, and
    does not depend on the skill's own file-write having succeeded.
15. Capture the plan artifact (per item 14's outcome) and the Test Plan Artifact's real
    path.
16. Copy both to `dev-{slug}\{slug}-project-library\output-gstack\`:
    `makepdlf-step-15-eng-plan.md` and `makepdlf-step-15-test-plan.md`.
17. Verify both outputs exist. If either is missing: STOP, present a deviation request
    per [[[makepdlf-project-library:specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
18. Write Step 15 `steps` ledger row: `step_number = 15`, `type = 'SKILL'`,
    `status = 'complete'`, `synthesized = false`, `artifact_path` = the path captured
    at item 15.
19. Save Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-15-receipt.md`.
20. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at **Full**.
21. Ask separately: "Commit and push to GitHub?"
22. Ask separately: "Run the end-of-step memory sequence?" This is five actions, in
    order, every time: (1) invoke the `mb-submit-memory` skill, using the
    `pdlf_step_sync` credential — this is a PDLF step's own routine housekeeping, not a
    developer's independent, ad-hoc request — for
    `output-gstack\makepdlf-step-15-eng-plan.md` and for `output-gstack\makepdlf-step-15-test-plan.md`,
    each as its own separate submission; (2) run `gbrain dream` for real, NEVER
    `--dry-run`; (3) run `gbrain eval suspected-contradictions` immediately afterward;
    (4) read what it reports; (5) if anything is marked high-severity, STOP and
    present it to the developer before continuing.
23. Present the Step Receipt. Stop, wait for "continue."
24. Ask: "Continue to Step 16?"

---

## Description

Engineering review — locks in architecture, code quality, test coverage, and
performance, and produces the concrete test specification from the scope Step 14
identified. Where Step 14's Step 0 is mode selection, Step 15's own Step 0 is a
genuinely different procedure: **Scope Challenge** — an existing-code-leverage check,
a minimum-change check, a hard complexity trigger that can stop the review before it
even begins, Search-Before-Building, a `TODOS.md` cross-reference, a completeness
check, and a distribution check. No expansion/reduction framework exists here at all.

**Correction carried into this rebuild, not left as an open item:** every earlier draft
of this step, including one already marked complete elsewhere, assumed this skill
produces five separate documents ([[[mb-3-cs-project-library:docs-local/architecture|architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/architecture.md) (mb-3-cs project library), [[[mb-3-cs-project-library:docs-standard-local/integration-architecture|integration-architecture]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/integration-architecture.md) (mb-3-cs project library),
the retired `security-architecture-canonical.md`, [[[mb-3-cs-project-library:docs-standard-local/globals-contract|globals-contract]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-standard-local/globals-contract.md) (mb-3-cs project library), [[[mb-3-cs-project-library:docs-local/authoritative-schema|authoritative-schema]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/authoritative-schema.md) (mb-3-cs project library)).
Read directly against the skill's own 925-line source: none of these filenames appear
anywhere in it. The skill produces exactly one genuinely separate file — the Test Plan
Artifact — plus everything else landing inside the same plan file Step 14 already
produced: the four sections' findings, the Required Outputs subsections, and the
terminal `## GSTACK REVIEW REPORT`.

Steps 14 and 15 jointly produce the test plan consumed by Steps 35 and 38. Step 14
identifies what must be tested and why; Step 15 produces the concrete test
specification — happy-path E2E specs per critical flow, edge cases, error-path test
cases, and an access/RBAC coverage matrix.

## Local/Global Conflict Check

Same mechanics as Step 14, reconfirmed rather than assumed by symmetry:
[[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)'s `SKILL.md` has zero reference to `project-library-global`
anywhere in source. The conflict check is entirely OpenCode's own structured
comparison, run alongside the skill invocation.

## Inputs Required

- Step 14's plan artifact — the real GStack-native file for SCOPE EXPANSION/SELECTIVE
  EXPANSION, or the stable `output-gstack\makepdlf-step-14-ceo-plan.md` copy for HOLD
  SCOPE/SCOPE REDUCTION
- `dev-{slug}\{slug}-project-library\docs-local\design-doc.md`
- `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md`
- The [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output file, if it ran
- `project-library-global` content relevant to this review, for the local/global
  conflict check
- Developer's answers to each individual `AskUserQuestion` finding across all four
  review sections
- GBrain query at item 1 (automatic, read-only, sources explicitly nominated)

## Outputs

| Artifact | Location | Notes |
|---|---|---|
| Eng plan + review report (appended to Step 14's plan file) | Same file as Step 14's plan artifact | The living document — no five-document cluster |
| Test Plan Artifact | `~/.gstack/projects/{slug}/{user}-{branch}-eng-review-test-plan-{datetime}.md` | The one genuinely separate file this step produces |
| Eng plan (stable copy) | `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-15-eng-plan.md` | |
| Test plan (stable copy) | `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-15-test-plan.md` | |
| Step Receipt | `dev-{slug}\{slug}-project-library\pdlf\step-15-receipt.md` | |
| BFT record | — | Full |

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 15 | Skill | | GStack [[[makepdlf-project-library:stepwise/step-15-plan-eng-review\|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) |

---

## Handoff

Step 16 (domain modeling, gate `domain-locked`) needs the design doc plus the locked
architecture and test decisions produced here.

### Open, not yet decided

- **`TODOS.md` path unconfirmed.** Assumed `dev-{slug}\{slug}-project-library\TODOS.md`
  (root-of-docs-repo level), pending developer confirmation.
- **Plan file continuity.** Whether OpenCode's invocation of [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md)
  genuinely presents an "active plan file" in the sense item 14's append-in-place
  mechanic expects is not confirmed by either skill's source. Resolved for this step's
  own purposes per item 14 above — flagged here as something to watch on the first
  live run, not a blocker.

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode
directly.

For execution sequence: [[[makepdlf-project-library:specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[makepdlf-project-library:specifications-local/spec-bft|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at item 1. Getting new content into durable memory is
never auto-run — it is asked at item 22, through the `mb-submit-memory` skill and the
five-action sequence described there, never GStack `/sync-gbrain`. The two
housekeeping questions are asked separately, every step, never combined, never
auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail entries are the
complete checkpoint. No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to
`dev-{slug}\{slug}-project-library\pdlf\`.
