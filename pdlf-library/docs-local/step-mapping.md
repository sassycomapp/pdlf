---
title: "step-mapping"
doc-id: "mb-77c13555"
updated: "2026-10-12"
---
# PDLF Step Mapping

**Purpose:** This file answers one question — "what is Step N, and who handles it?" It
maps every step number to its file, phase, type, handler, and gate status. It is a
reference table, not a run order. Steps are listed in numerical order for
findability only; numerical order is not execution order.

**This file does not define sequence, dependencies, or branching, in any form.** That is
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md)'s job exclusively. A step number's position in this file's tables carries
no meaning about when that step runs relative to any other. Two documents claiming
jurisdiction over sequencing is a planning defect, not a stylistic choice — this file
stays out of that territory entirely, including in earlier drafts of itself that carried
an "Execution Order" column. That column has been removed.

**This replaces two previously separate documents:** `step-mapping.md` and `INDEX.md`.
Both mapped step numbers to files; `INDEX.md` had gone stale (still listed the retired
Steps 2–3, the retired `sop-existing-project-resume-audit.md`, and `step-11-output.md` as live) while
`step-mapping.md` stayed current. Merged into one file rather than maintaining two.

**This also replaces the two prior `PDLF-`-prefixed mapping documents** (one for new
projects, one for existing projects). They are gone because the distinction they existed
to capture no longer exists: every step always runs, in full, for every project,
regardless of entry mode. What differs for an existing project is only the material a
step starts from — never whether it runs. See [[[makepdlf-project-library:stepwise/step-12-office-hours|Step 12: Office Hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) for where that
distinction actually lives.

Steps marked `(loop)` are part of the per-feature build/test/review loop. This block
repeats once per feature/package until every feature has individually passed through it.
For the loop's actual order, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md), "Step 35 Feature Loop" — not this file.

---

## Reserved

Steps 4–10 are reserved and undefined. There is no existing-project registration/audit
branch at Steps 2–3 — that model (disposition audit, SKIP/RE-RUN/RUN-AS-NEW) is retired
entirely. Existing-project entry is handled inside Step 11 itself; see [[[makepdlf-project-library:stepwise/step-11-init|Step 11: Init]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-11-init.md).

| Step | File | Status |
|---|---|---|
| 1 | [[[makepdlf-project-library:stepwise/step-01-orchestrator\|Step 01: Orchestrator]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-01-orchestrator.md) | Orchestrator — defined |
| 4–10 | `step-{N}-undefined.md` | Reserved — not yet defined |

---

## Phase A — Discover & Define

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 11 | `[[step-11-init]]` | OpenCode | Init — foundation checks, folder structure, registration | |
| 12 | `[[step-12-office-hours]]` | Skill (conditional) | GStack [[[makepdlf-project-library:stepwise/step-12-office-hours\|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) | |
| 14 | `[[step-14-plan-ceo-review]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review\|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) | |
| 15 | `[[step-15-plan-eng-review]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-15-plan-eng-review\|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) | |
| 16 | `[[step-16-domain-modeling]]` | Skill + GATE | `/grill-with-docs` (using [[[makepdlf-project-library:stepwise/step-16-domain-modeling\|/domain-modeling]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-16-domain-modeling.md)) | `domain-locked` |

Exit gate: `domain-locked` (Step 16). For entry condition and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## Phase B — Design & Plan

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 17 | `[[step-17-create-anvil-data-tables]]` | Manual | Developer, Anvil IDE | |
| 18 | `[[step-18-pull-to-local]]` | Manual | Pull to local | |
| 19 | ``[[step-19-to-tickets]]`` | Skill | Matt [[[makepdlf-project-library:stepwise/step-19-to-tickets\|Step 19 to Tickets]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-19-to-tickets.md) | |
| 20 | `[[step-20-design-consultation]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-20-design-consultation\|/design-consultation]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-20-design-consultation.md) | |
| 21 | `[[step-21-concept-sanity-audit]]` | Gate | OpenCode | `concept-locked` |
| 22 | `[[step-22-wireframe-phase-1]]` | Tool | Wireframe skill (Magdoub) — B&W | |
| 23 | `[[step-23-plan-design-review]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-23-plan-design-review\|/plan-design-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-23-plan-design-review.md) | |
| 24 | `[[step-24-plan-devex-review]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-24-plan-devex-review\|/plan-devex-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-24-plan-devex-review.md) | |
| 26 | `[[step-26-wireframe-phase-2]]` | Tool + GATE | Wireframe skill (Magdoub) — Clean/Polished | `wireframes-approved` |
| 27 | `[[step-27-screen-production]]` | OpenCode (deferred) | Screen production | |
| 28 | `[[step-28-screen-to-png]]` | External (deferred) | Screen → PNG | |

Exit gates: `concept-locked` (Step 21), `wireframes-approved` (Step 26). For entry
condition and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## Phase C — Scaffold & Assemble

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 29 | `[[step-29-build-ui-forms]]` | Manual | Developer + Anvil AI, Anvil IDE | |
| 30 | `[[step-30-pull-to-local]]` | Manual | Pull to local | |
| 31 | `[[step-31-scaffold-planning]]` | OpenCode | Scaffold planning | |
| 32 | `[[step-32-physical-scaffold-build]]` | Manual | Anvil IDE | |
| 33 | `[[step-33-pull-to-local]]` | Manual | Pull to local | |
| 34 | `[[step-34-architectural-sanity-audit]]` | Gate | OpenCode | `architecture-verified` |

Exit gate: `architecture-verified` (Step 34). For entry condition and dependencies, see
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## Phase D — Build & Verify (per-feature loop)

Repeats once per feature/package from Step 19's ticket list, until every feature has
individually reached `build-verified`. For the loop's actual order and dependencies, see
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md), "Step 35 Feature Loop."

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 35 | `[[step-35-build-loop]]` | Agent loop | OpenCode, feature-by-feature | |
| 35A | [[[makepdlf-project-library:stepwise/step-35a-testing\|Step 35A Testing]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-35A-testing.md) | OpenCode | Local-scope `pip-audit` + broader testing | |
| 36 | `[[step-36-design-review]]` | Skill | GStack `/design-review` — retest, post-remediation | |
| 37 | `[[step-37-review]]` | Skill | GStack `/review` | |
| 38 | `[[step-38-qa]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-38-qa\|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) | |
| 38A | [[[makepdlf-project-library:stepwise/step-38a-dependency-scan-confirm\|Step 38A Dependency Scan Confirm]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38A-dependency-scan-confirm.md) | OpenCode | Capture Anvil's native `pip-audit` result | |
| 39 | `[[step-39-triage]]` | Skill + GATE | Matt [[[makepdlf-project-library:stepwise/step-39-triage\|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md) | `build-verified` |
| 40 | ``[[step-40-improve-codebase-architecture]]`` | Skill (optional) | Matt [[[makepdlf-project-library:stepwise/step-40-improve-codebase-architecture\|Step 40 Improve Codebase Architecture]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md) — read-only | |
| 40B | [[[makepdlf-project-library:stepwise/step-40b-remediation\|Step 40B Remediation]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-40B-remediation.md) | OpenCode (conditional) | Apply developer-approved fixes from Step 40 | |

Exit gate: `build-verified`, evaluated per feature. For entry condition and dependencies,
see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## Phase E — Ship & Monitor

**Note:** Steps 42, 42A, 43, and 44 are flagged for rebuild — see `ToDo.md` item 2. They
currently model a staging/production environment split that does not apply to this
platform (see `[[adr-no-staging-environment-five-app-isolation]]`). Listed here as
currently defined; not yet corrected.

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 41 | `[[step-41-ship]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-41-ship\|/ship]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-41-ship.md) | |
| 42 | `[[step-42-publish-to-staging]]` | Manual | Publish to Staging | |
| 42A | [[[makepdlf-project-library:stepwise/step-42a-staging-integration-e2e\|Step 42A Staging Integration E2E]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-42A-staging-integration-e2e.md) | Skill | GStack/OpenCode — full integration/E2E suite | |
| 43 | `[[step-43-staging-smoke-test]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-38-qa\|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) or `/canary` — smoke test | |
| 44 | `[[step-44-promote-to-production]]` | Manual + GATE | Promote to Production | `production-released` |
| 45 | `[[step-45-canary-production]]` | Skill | GStack `/canary` at Production | |
| 46 | [[[makepdlf-project-library:stepwise/step-46-learn-junction\|Step 46 Learn Junction]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-46-LEARN-junction.md) | LEARN + GATE | OpenCode | `released` |

Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

---

## Reference Files

| File | Applies To | Content |
|---|---|---|
| [[[makepdlf-project-library:stepwise/run-plan\|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) | Orchestrator | **Execution order, branching, dependencies — the sole authority on sequence.** |
| [[[makepdlf-project-library:specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md) | Every step | 13-point execution sequence, step-type routing, deviation mechanism |
| [[[makepdlf-project-library:specifications-local/spec-bft\|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) | Every step | BFT questions, levels, gate rule, anti-rubber-stamping |
| [[[makepdlf-project-library:specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-gate-procedure.md) | Gate steps (16, 21, 26, 34, 39, 44, 46) | Gate ceremony, full maintenance, ledger integrity check, approval flow |
| [[[makepdlf-project-library:policy-local/step-conditional-state-policy\|Step Conditional State Policy]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/step-conditional-state-policy.md) | Step 12 | Conditional step states (complete / skipped), downstream propagation |
| [[[makepdlf-project-library:specifications-local/spec-nomenclature\|Spec: Nomenclature]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-nomenclature.md) | Every step | Naming and path conventions, authoritative |

---

## Gate Summary

`build-verified` sits at Step 39 ([[[makepdlf-project-library:stepwise/step-39-triage|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md)), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `domain-locked` | 16 |
| `concept-locked` | 21 |
| `wireframes-approved` | 26 |
| `architecture-verified` | 34 |
| `build-verified` | 39 (per feature) |
| `production-released` | 44 |
| `released` | 46 |
