---
title: "spec-skill-design"
doc-id: "mb-1202aaa9"
updated: "2026-10-13"
---
# PDLF Skill — Design Specification

**Why this exists:** this document states why PDLF's design choices were made — what was
considered, what was rejected, and what tradeoffs were accepted. It was originally written
alongside SKILL-v4.md (the implementation) and skill-workflow-table.md (the build spec) — the
three-document specification of the v4 era. Those two companions were retired 2026-07-19 and
absorbed into the stepwise files, which now carry the implementation.

---

## 1. Context

### 1.1 Target user

A **non-technical builder** using Anvil.works — someone who can read a PRD and judge whether a
feature works, but cannot personally verify every line of code. The agent is their consulting
architect; PDLF is the discipline that prevents the agent from making silent assumptions that
the developer cannot catch.

### 1.2 Success criteria (stated by the developer)

1. **Agent integrity** — the agent never runs off and explains itself afterward. Every decision
   has a traceable reason recorded at the time it was made.
2. **Build integrity** — what was built matches what was agreed. Scope doesn't drift silently.
3. **Continuity** — a session can stop at any step and resume later with zero context loss.
4. **Contiguity** — every step's output is the next step's input. No gaps where decisions fall
   through cracks.
5. **Ease of use for a non-technical developer** — the system works for someone who relies on
   the agent's technical judgment.

### 1.3 Platform constraint

PDLF targets **Anvil.works** applications exclusively. Anvil is a Python-based full-stack
platform with its own deployment model (named Deployment Environments, IDE-based publishing,
`anvil.yaml` for configuration). Many decisions below are shaped by Anvil's constraints.

---

## 2. Core Architecture — Decisions and Rationale

### 2.1 Postgres ledger replaces state file + devlog + completion report

**Decision:** All PDLF progress is recorded in a Postgres database (`pdlf`), not in markdown files.

**Why:**
- The v2 model had three files duplicating the same facts: `state.md` (snapshot), the retired `devlog.md`
  (audit trail), and per-step completion reports. They could silently disagree with each other.
- A database enforces referential integrity: step 19 literally cannot be recorded as complete if
  step 16 does not exist. A markdown file imposes no such constraint.
- The Step Receipt is generated from the ledger row just written — it IS the ledger row, formatted
  for reading. No narrative gloss can diverge from what actually happened. This is the direct
  answer to the developer's "black box" fear.

**Rejected:** Continuing with flat-file state management. Every previous version (state file,
devlog, completion report) was built and then fully retired when the ledger design proved
superior.

**Tradeoff:** Requires PostgreSQL to be running and accessible. For a non-technical user, this is
setup complexity. Accepted because the integrity guarantees justify it.

### 2.2 Progressive disclosure — lean SKILL.md, detailed reference files

**Decision:** SKILL.md contains only the step table and control loop. Detailed procedures
(testing, sanity audits, Anvil mechanics, screen production) live in separate files loaded
only at the step that needs them.

**Why:**
- A real project's build plan showed how long detail actually runs. Monolithic SKILL.md would
  be unreadable.
- This mirrors Matt Pocock's `writing-great-skills` guidance: a skill file should be scannable.
- New steps can be added by creating a new reference file and adding one row to the step table,
  without touching existing procedure docs.

**Rejected:** Monolithic SKILL.md with all procedures inlined. Every version prior to v4 had
procedures inlined, and every version grew unmanageably.

**Tradeoff:** Reference files must be kept in sync with the step table. The docmap and §0.2
reference table are the enforcement mechanism.

### 2.3 Skill-use principle — invoke only when it beats OpenCode directly

**Decision:** A GStack or Matt Pocock skill is invoked only when it performs a task better than
OpenCode could do directly with the model.

**Why:**
- Stated directly by the developer as a governing principle.
- Proven by example: the two sanity-audit gates (21, 34) don't need custom skills —
  cross-referencing markdown documents is well within OpenCode's native capability. They are
  documented procedures, not skills.
- Conversely, [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) is a skill because its six-question structured interview is
  genuinely better than OpenCode asking questions conversationally. [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md) is a skill because
  it drives a headless browser — something OpenCode cannot do at all.

**Rejected:** Invoking a skill at every step by default, regardless of whether it adds value.
The self-assessment document from July 2026 identified six specific mapping errors where skills
were prescribed for tasks they don't actually perform. A second review (2026-07-12) applied this
same principle retroactively and found two more: `to-spec` (formerly Step 13) had no confirmed
downstream consumer, and `prototype` (formerly Step 25) was optional and non-chained. Both removed.

**Tradeoff:** Requires the agent to read each skill's SKILL.md before invoking it, not just
trust the name. This rule has documented evidence of preventing real errors, most recently the
two removals above.

### 2.4 BFT at three levels — Full / Light / None

**Decision:** De Bono BODY Frame Thinking is not applied uniformly to every step. Full
six-question BFT runs on decision-heavy steps; Light (BONES + HEALTH only) on mostly-mechanical
steps following locked decisions; None on purely mechanical zero-judgment steps.

**Why:**
- Full BFT on "bump VERSION number" produces boilerplate — the exact rubber-stamping failure
  the developer's AGENTS.md warns against.
- The developer stated: "don't take the lazy route, don't rubber-stamp, don't make silly
  assumptions, remain fully diligent."
- The ratio ensures BFT attention is spent where judgment lives.

**Rejected:** Uniform Full BFT on all steps. Produces the rubber-stamping the system exists to
prevent.

**Tradeoff:** The Level assignment table ([[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|Bft Checkpoint Cheatsheet V2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md)) is itself a
decision that must be reviewed. A step's level may need adjustment after real-world use. As of
2026-07-12 this table has not yet been extended to cover the newly added lettered sub-steps
(35A, 38A, 40B, 42A) or the existing-project entry steps (2–3) — outstanding.

### 2.5 GStack and Matt Pocock skills are libraries, not pipelines

**Decision:** PDLF does not bridge two competing workflow pipelines. GStack provides review,
QA, and deployment skills. Matt Pocock provides domain modeling, ticket creation, and triage.
PDLF calls them selectively, in sequence — they are narrow libraries, not perpetual pipelines.

**Why:**
- The developer confirmed this reframing directly and asked whether it was feasible.
- Proven feasible by the self-assessment: real mapping corrections showed that individual
  skills need careful selection, not wholesale pipeline adoption.
- GStack's `/autoplan` (runs CEO/Eng/Design reviews all at once) is explicitly NOT used because
  PDLF runs those reviews at different stages for different reasons.
- A follow-up review confirmed GStack also ships its own native `/spec` skill, functionally
  overlapping with Matt's `to-spec`, and that GStack's own skills are not designed to consume
  Matt's skill outputs by default (verified directly against [[[pdlf:app-factory/phase-b-discover-and-define/b14-reference|Step 14 Plan Ceo Review]]](C:/pdlf/app-factory/phase-b-discover-and-define/b14-reference.md)'s GBrain query
  schema). This reinforced rather than contradicted the "libraries, not pipelines" framing —
  each skill's output must be deliberately routed to whatever consumes it; nothing is
  automatically wired together across the two toolsets.

**Rejected:** Treating GStack and Matt Pocock as competing pipeline orchestrators that need a
middleware bridge. The `gstack-matt-skills-handoff-guide.md` (now obsolete) was the exploratory
document that proved this approach correct — it identified bridge points, state management
patterns, and automation levels, all of which informed v4's execution discipline directly.

### 2.6 Seven gates — up from five in v2

**Decision:** Two new hard gates were added: `concept-locked` (Step 21) and `architecture-verified`
(Step 34). Plus `production-released` (Step 44) split from the original `released` gate.

**Why:**
- Both new gates were the developer's own additions, born from direct experience.
- `concept-locked`: before any wireframe work begins, a full cross-document coherence audit
  confirms the CEO review, Eng review, domain model, and design system all agree. After
  this gate, no new feature may be added without formal gate reopening — a hard scope freeze.
- `architecture-verified`: before any code-writing begins, the physical Anvil build (data tables,
  UI forms, scaffolding) is confirmed to match the locked architecture. This catches drift between
  plan and physical implementation before build effort is spent on a mismatched foundation.

**Rejected:** Trusting that the plan and the physical build will stay in sync without verification.

**Tradeoffs:** Adds two stops to the pipeline. The developer judged these stops worth their
cost, given prior experience of what breaks without them.

**Addendum (2026-07-12):** The `build-verified` gate (originally at Step 40) was found to sit
before the retest steps (36–38) that verify remediation applied at that same stage — meaning
shipped code could include unverified post-remediation changes. Moved to Step 39, after
retest and triage, so the gate genuinely reflects a verified state. See §2.8 addendum.

### 2.7 Anvil-specific release sequence replaces GStack's ship/land defaults

**Partially superseded 2026-07-18.** The staging/production environment model this section
justifies against GStack's defaults is itself now superseded by a further finding: this
platform's Five-App Structure means PDLF never needs a staging/production split at all —
see [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md). The comparison against
GStack's generic pipeline below remains accurate rationale for why Anvil needed *something*
different; it just doesn't yet reflect what that something now is. Steps 42–44 pending
rebuild.

**Decision (historical):** Steps 41–45 are rewritten for Anvil's deployment model. GStack's [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-reference|/ship]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-reference.md) (scope
narrowed: stops at push, no PR assumption) → manual Staging publish (42) → Staging smoke test
(43) → manual Production promotion (44) → Production canary (45).

**Why:**
- GStack assumes PR merge → CI pipeline → generic production URL. Anvil has none of these.
- Anvil deploys via named Deployment Environments, each with its own URL, code version, and
  database, switched by publishing in the IDE.
- Rollback is re-pointing an environment to a prior commit, not `git revert` (which doesn't
  un-publish an app).
- The Staging smoke test (43) catches problems on live infrastructure before promoting to
  Production — a safety net GStack's default flow doesn't provide for Anvil.

**Rejected:** GStack's default [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-reference|/ship]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-reference.md) → `/land-and-deploy` pipeline. Would require Anvil to
have a CI pipeline, which it doesn't.

**Note (2026-07-12):** A full integration/E2E step (42A) was added between the Staging publish
(42) and the smoke test (43) — the smoke test alone was assessed as too thin to be the only
verification step before Production promotion.

### 2.8 Feature-by-feature build loop

The build loop's design is held in Step 35's own build plan (`e35-build-plan.md`).

### 2.9 Test-mode with synthesized flag propagation

**Decision:** A `test` project mode shortens [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference|/design-consultation]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md) (Step 20). The
`synthesized = true` flag is recorded in the ledger and propagates forward — any step consuming
a synthesized artifact shows an INPUT NOTICE warning on its own receipt. Step 12 ([[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md))
is NOT test-mode-eligible — it is a simple yes/no decision gate.

**Why:**
- Full [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference|/design-consultation]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md) on a throwaway test project is tedium that produces no real value.
- The propagation rule ensures a shortcut at Step 20 is visible at Step 22 — a developer
  glancing at a later receipt should not have to remember that Step 20 was abbreviated.
- Step 12 was removed from test-mode eligibility because the yes/no gate is already the
  shortest possible path — the developer either runs the full skill or skips it.

**Rejected:** Either (a) no test-mode at all, which wastes time on throwaway projects, or
(b) a silent shortcut, which hides the quality compromise from downstream steps.

### 2.10 Two-repo separation — project-library vs code repo

**Decision:** Every PDLF project has two git repositories: `project-library` (docs, ADRs,
process artifacts) and the code repo (Anvil-connected app).

**Why:**
- Docs and process artifacts have a different lifecycle than code. They are queried, audited,
  and cross-referenced differently.
- The Anvil code repo contains `anvil.yaml` — a file PDLF must NEVER write to. Keeping docs
  in a separate repo eliminates any risk of touching it.
- GBrain indexes both as separate sources, enabling scoped queries.

### 2.11 Standards Library — extract general patterns, leave project specifics

**Decision:** Reusable Anvil/M3/testing knowledge is extracted from real projects (primarily
mb-3-cs) into a separate, project-agnostic Standards Library. Project-specific values stay in
their source documents.

**Why:**
- mb-3-cs contains genuinely reusable platform knowledge mixed with project-specific decisions.
- Reorganizing a working project's files is risky and explicitly prohibited by the developer.
- Extraction preserves the source project as-is while making the general knowledge available
  to all future projects.

**Status:** Design decided, implementation not yet complete.

### 2.12 Existing-project entry — disposition audit, not blind resume (new, 2026-07-12)

**Retired 2026-07-18 — kept as historical record, not current design.** The model
described below (Steps 2–3, SKIP/RE-RUN/RUN-AS-NEW disposition audit) was replaced by a
simpler principle: an existing project is redeveloped around its canonical concept, not
audited step-by-step. Every step always runs, for every project; what differs is only the
material a step starts from. See `[[12-office-hours]]` for where the distinction
actually lives now. The rationale below is retained the same way v1–v5 are retained in
the Evolution table — as a record of what was tried and why it was superseded, not as an
account of current behavior.

**Decision (historical):** An existing project entering PDLF does not resume at a single numeric step.
Steps 2–3 (`step-02-existing-registration.md`, `step-03-resume-point-audit.md`) run an
interactive, per-step audit assigning SKIP / RE-RUN / RUN-AS-NEW to every step from 12
through 34, plus a derived resume gate — all developer-approved before execution proceeds.

**Why:**
- Different parts of a real existing project (e.g. mb-3-cs) can genuinely be at different
  states of completion simultaneously — design done, code untouched, scaffold built but
  wireframes unconfirmed. No single step number can represent that state honestly.
- Evidence is classified into exactly two tiers — structural certainty (permits an
  unattended disposition) and everything else (always asks the developer) — deliberately
  rejecting a confidence-scoring model, which would itself be a hidden, unaccountable
  decision.
- Any contradiction between what OpenCode observes in the files and what the developer
  states is never silently accepted or merely logged — it is surfaced explicitly and routed
  through the existing `deviations` ledger table as a formal decision point.

**Rejected:** A single "resume at step N" answer, and any algorithmic confidence-scoring
approach to disposition.

**Tradeoff:** The audit adds an interactive question-and-answer pass before any planning or
build work resumes. Accepted because the alternative — guessing wrong on project state — is
a worse failure mode. **Status:** design complete, unvalidated against a real project run.

---

## 3. Evolution — How we got here

| Version | Model | State | Key change |
|---|---|---|---|
| v1 (pre-pdlf) | 17 stages | None | Original concept from initial.md |
| v2 | 24 steps + LEARN | State file + devlog + completion reports | First skill implementation. GStack and Matt Pocock skills mapped to each step. |
| v3 | 24 steps | Refined execution discipline | GBrain query/sync rules, deviation mechanism, BFT per step, output routing. |
| v4 | 36 steps (26 step numbers + 11 sub-steps) | Postgres ledger | Progressive disclosure, skill-use principle, two new gates, feature-by-feature build loop, Anvil-specific release sequence, test-mode propagation. |
| v5 | 36 steps (11-46, 10 reserved) | Stepwise decomposition | Monolith SKILL-v4.md absorbed into stepwise skill files + 5 shared references. YAML front matter, task execution order. Renumbered from 0-25/sub to 11-46. |
| v6 | Same numbering, revised value chain | Stepwise decomposition, corrected | `to-spec` (13) and `prototype` (25) removed on skill-use-principle grounds; `to-issues` renamed [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference\|Step 19 to Tickets]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md) (19); `build-verified` gate moved 40→39; lettered sub-steps 35A/38A/40B/42A added; existing-project entry branch defined (Steps 2–3); Step 37/38 artifact-persistence requirement added. |

Each version discarded prior work when a better design emerged. The state file, devlog file, and
completion report were all built in v2, then fully retired in v4 when the ledger proved superior.
The skill mapping was corrected multiple times across the July 2026 self-assessments, each time
after reading actual skill SKILL.md files revealed mapping errors. This is iterative by design.

---

## 4. Document Architecture — Stepwise Decomposition (v5)

The v4 three-document architecture (SKILL-v4.md, spec-skill-design.md, skill-workflow-table.md)
has been superseded by the v5 stepwise decomposition:

| Artifact | Purpose | Location |
|---|---|---|
| **Stepwise files** | Each step is a self-contained skill with YAML front matter, task execution order, inputs/outputs, and reference pointers | `app-factory/phase-{letter}-{name}/{NN}-{name}.md` (moved from `stepwise/` 2026-10-11) |
| **Shared references** | Single-source-of-truth procedures shared by all stepwise files | `[[spec-execution-discipline]]`, `[[spec-bft]]`, `[[spec-gate-procedure]]`, `[[step-mapping]]`, `[[run-plan]]` — `INDEX.md` was folded into `[[step-mapping]]` and the retired `sop-existing-project-resume-audit.md` was retired with the disposition-audit model, both 2026-07-18 |
| **spec-skill-design.md** (this file) | Why — design rationale, rejected alternatives, tradeoffs | `specifications-local/` |

The original three documents are retained in `obsolete/` for historical reference.
Supporting documents (policies, templates, ADRs) are loaded by the orchestrator as needed.

---

## 5. Binding Constraints

1. **Anvil.yaml is sacred.** Never written to by any agent. Read-only.
2. **The agent makes no decisions.** All decisions come from the developer. The agent executes,
   verifies, reports.
3. **No step is skipped without a deviation request.** The developer must explicitly authorize
   any deviation.
4. **The agent never commits or pushes.** Every step ends by asking the developer to run
   `/mb-close-out`; only the developer commits, with `commit-all`.
5. **A skill is never invoked without first reading its own SKILL.md.** Names mislead — the
   self-assessments have documented multiple real errors caused by trusting a skill name instead
   of its content.
6. **A disagreement between evidence and a developer's stated answer is never left unattended.**
   It is surfaced explicitly and resolved as a formal deviation, not silently deferred.

---

*Skill design specification version 3.0. Source material (retired files, no longer on disk — deleted
2026-07-19, commit eb26565, verified absent 2026-09-18): handover-document.md §4,
gstack-matt-skills-handoff-guide.md, SKILL-v4.md, skill-workflow-table.md, and
sop-existing-project-resume-audit.md (verified absent everywhere). Living source:
[[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md). Updated 2026-07-12 to reflect the v6 stepwise
value-chain review.*
