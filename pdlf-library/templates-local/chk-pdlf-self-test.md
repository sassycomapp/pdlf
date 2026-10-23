---
title: "chk-pdlf-self-test"
doc-id: "mb-afcdd367"
updated: "2026-10-23"
---
# Checklist — PDLF Self-Test

**Scope:** tests PDLF itself, the orchestration system in `C:\pdlf`. It does not test the applications PDLF builds; they are tested by the test suite in `C:\dev\project-library-global\test-suite\`.

**Why this is local:** it checks PDLF's own mechanics — the ledger schema, the execution sequence, the gate ceremony and PDLF's own step documents. None of it applies outside PDLF.

**Cadence:** continuous. The relevant sections are run again whenever a step document, policy or specification changes.

**How to use:** each item is a pass or fail check with a stated method. Run it against its target (a step's documents, a live run, the ledger) and report the result to the developer; an action that follows goes on `pdlf-todo.md`.

---

## 1. Execution Discipline Conformance

Run per step file, or against a live step execution.

| # | Check | Method |
|---|---|---|
| 1.1 | GBrain query fires automatically at substep 1, read-only | Read the step's reference; confirm item 1 is a GBrain query with no side effects |
| 1.2 | Step type correctly routed (SKILL / MANUAL / OPTIONAL / GATE) | Compare the step file's own type declaration against [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)'s Step-Type Routing section |
| 1.3 | Skill's real `SKILL.md` read before invocation, not trusted by name | Confirm the step's build plan or reference cites verification against actual skill source, not an assumed behavior |
| 1.4 | Expected output existence verified before the step is marked complete | Confirm a verification substep exists, not just an invocation substep |
| 1.5 | BFT run at the step's assigned level, with non-boilerplate answers | Cross-check the level set in the step's config; for a live run, confirm each answer is specific to the step, not generic |
| 1.6 | Ledger row matches [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)'s schema exactly | Compare the step's ledger-write substep against the real `steps` table columns |
| 1.7 | Step Receipt generated from the ledger row, not composed separately | Confirm the receipt substep says "generate from the row just written," not "write a summary" |
| 1.8 | The step ends by asking the developer to run `/mb-close-out`, and never commits, pushes or writes memory itself | Confirm the last substeps are explain, stop and the request for `/mb-close-out`, with no commit, push, memory or dream-cycle action |
| 1.9 | The step stops and waits for "continue" | Confirm the final substep is a stop, not an automatic advance |

## 2. Gate Integrity

Run per gate (`domain-locked`, `concept-locked`, `wireframes-approved`,
`architecture-verified`, `build-verified`, `production-released`, `released`).

| # | Check | Method |
|---|---|---|
| 2.1 | Full BFT applies regardless of the step's assigned level | Confirm the gate step's file explicitly overrides to Full |
| 2.2 | The gate commits, pushes and syncs nothing | Confirm the gate procedure has no commit, push or GBrain sync, and ends with the request for `/mb-close-out` |
| 2.3 | Gate summary block matches the format in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) | Compare presented output against the template |
| 2.4 | Developer approval required before advancing | Confirm no path exists from gate to next step without an explicit yes |
| 2.5 | A failed gate blocks the pipeline, not just that one step | Confirm the "No" branch stops and records a blocker, not a silent retry |
| 2.6 | A passed gate cannot be silently unwound | Confirm reopening requires a formal deviation request, not a direct edit |

## 3. Ledger Schema Conformance

Run against the live database. Items 3.1, 3.3 and 3.4 need database access and are run by OpenCode with the instruction below; items 3.2 and 3.5 are document checks.

| # | Check | Method |
|---|---|---|
| 3.1 | All seven tables exist: `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`, `triage_findings` | `\dt` against the live database |
| 3.2 | Step order is enforced by the orchestrator against its run order ([[[pdlf:app-factory/phase-a-init/a01-build-plan\|Run Plan]]](C:/pdlf/app-factory/phase-a-init/a01-build-plan.md)), not by the database | Confirm no step's reference writes a ledger row without first checking the run order |
| 3.3 | The `build-verified` query on `triage_findings` returns the right pass or fail | Seed a feature's findings with `wontfix`, resolved and open rows; confirm the gate query matches [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)'s stated logic |
| 3.4 | `deviations` captures the description, the options presented and the decision | Seed a deviation; confirm all three fields are populated |
| 3.5 | No document states a table count other than seven | Search every document for another count |

## 4. Skill Invocation Correctness

Run whenever a step's documents are written or reviewed.

| # | Check | Method |
|---|---|---|
| 4.1 | Every skill named in a step exists at its claimed source, under that name | Read the skill's `SKILL.md` at its pinned version |
| 4.2 | The skill is invocable the way the step assumes (user-invoked or model-invoked, standalone or wrapped) | Read the skill's own description and frontmatter; never infer from its name |
| 4.3 | If the skill is a thin wrapper, every skill it delegates to is accounted for | Read the wrapper's body in full |
| 4.4 | The step was designed from the skill's pinned version | Compare against the pinned version; a skill is rechecked whenever a step that uses it is written, and whenever its pinned version changes |

## 5. Documentation Consistency

| # | Check | Method |
|---|---|---|
| 5.1 | No broken or doubled file paths | Search for repeated path segments (for example `specifications-local/specifications-local/`) |
| 5.2 | No two documents claim to be the source of truth for the same fact | Check for competing maps, indexes and sources of truth |
| 5.3 | No dead reference to a file that does not exist | Check every cited path against the repositories |
| 5.4 | Names match [[[default:specifications-global/spec-nomenclature\|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) | Check file and folder names against it |
| 5.5 | No document describes an outdated mechanism as current, and none holds history | Run the scan of banned terms in the update method |

## 6. Deviation Mechanism

Run against a live or seeded deviation.

| # | Check | Method |
|---|---|---|
| 6.1 | The deviation request has the form set in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) | Compare the presented request with it |
| 6.2 | The agent never decides | Confirm the flow always stops for the developer, with no default path |
| 6.3 | The deviation is recorded in the `deviations` table, not only narrated | Query the table after the event |

---

## OpenCode Instruction — Section 3

Run in **build mode**: it writes and removes test rows.

**TASK: run checks 3.1, 3.3 and 3.4 against the live `pdlf` database.**

Use the WSL to Windows PowerShell bridge in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). Do not touch any real project's rows: use the dummy `project_slug` `_selftest` only.

1. **Check 3.1:** run `\dt` against `pdlf`. Report which of the seven tables exist, pass or fail per table.
2. **Check 3.3:** for `project_slug = '_selftest'`, seed three `triage_findings` rows for one feature's `step_id`: one `wontfix`, one with `resolved_at` set, one `needs-triage` with `resolved_at` empty. Run the `build-verified` query from the ledger specification; it must not pass. Resolve the third row and run it again; it must pass. Report both results.
3. **Check 3.4:** insert a `deviations` row with a description, an `options_presented` JSON object and a decision. Read it back. Report whether all three fields return correctly.
4. Remove every `_selftest` row.

**Report:** pass or fail for each check, with the raw query results for 3.3. If a check fails, stop and report; do not change the schema without the developer's authorization.
