---
title: "chk-pdlf-self-test"
doc-id: "mb-afcdd367"
updated: "2026-10-13"
---
# Checklist — PDLF Self-Test Suite

**Location:** `checklists-local\chk-pdlf-self-test.md`

**Scope:** Tests `C:\pdlf` per se — the orchestration
system itself. Does not test any Anvil application PDLF builds. For that, see
the retired `chk-anvil-app-testing.md` (global, `specifications-global\`).

**Why this is local, not global:** this checklist verifies PDLF's own internal mechanics
— the ledger schema, the execution sequence, the gate ceremony, the specific step files in
this repo. None of it is reusable outside PDLF itself, unlike the Anvil-testing standard,
which applies to any Anvil project regardless of whether PDLF built it.

**Cadence:** continuous, not one-time. Re-run relevant sections whenever a step file,
policy, or spec changes — not just at a scheduled interval. This document itself should be
revisited as PDLF's design evolves; a stale checklist is a failure condition, same as any
other PDLF document.

**How to use:** each item is a pass/fail check with a stated method. Run against a specific
target (a step file, a live run, the ledger schema) and record findings — this checklist
does not prescribe where findings get recorded; use the developer's standing process
(currently: report back directly, log to `wip\ToDo.md` if it becomes an action item).

---

## 1. Execution Discipline Conformance

Run per step file, or against a live step execution.

| # | Check | Method |
|---|---|---|
| 1.1 | GBrain query fires automatically at substep 1, read-only | Read the step file's Task Execution Order; confirm item 1 is a GBrain query with no side effects |
| 1.2 | Step type correctly routed (SKILL / MANUAL / OPTIONAL / GATE) | Compare the step file's own type declaration against [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)'s Step-Type Routing section |
| 1.3 | Skill's real `SKILL.md` read before invocation, not trusted by name | Confirm the step file or its build notes cite verification against actual skill source, not an assumed behavior |
| 1.4 | Expected output existence verified before the step is marked complete | Confirm a verification substep exists, not just an invocation substep |
| 1.5 | BFT run at the step's assigned level, with non-boilerplate answers | Cross-check [[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2\|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md)'s assigned level; for a live run, confirm each answer is specific to the step, not generic |
| 1.6 | Ledger row matches [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)'s schema exactly | Compare the step's ledger-write substep against the real `steps` table columns |
| 1.7 | Step Receipt generated from the ledger row, not composed separately | Confirm the receipt substep says "generate from the row just written," not "write a summary" |
| 1.8 | The step ends by asking the developer to run `/mb-close-out`, and never commits, pushes or writes memory itself | Confirm the last substeps are explain, stop and the request for `/mb-close-out`, with no commit, push, memory or dream-cycle action |
| 1.9 | The step stops and waits for "continue" | Confirm the final substep is a stop, not an automatic advance |

## 2. Gate Integrity

Run per gate (`domain-locked`, `concept-locked`, `wireframes-approved`,
`architecture-verified`, `build-verified`, `production-released`, `released`).

| # | Check | Method |
|---|---|---|
| 2.1 | Full BFT applies regardless of the step's assigned level in the cheatsheet | Confirm the gate step's file explicitly overrides to Full |
| 2.2 | The gate commits, pushes and syncs nothing | Confirm the gate procedure has no commit, push or GBrain sync, and ends with the request for `/mb-close-out` |
| 2.3 | Gate summary block matches the format in [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) | Compare presented output against the template |
| 2.4 | Developer approval required before advancing | Confirm no path exists from gate to next step without an explicit yes |
| 2.5 | A failed gate blocks the pipeline, not just that one step | Confirm the "No" branch stops and records a blocker, not a silent retry |
| 2.6 | A passed gate cannot be silently unwound | Confirm reopening requires a formal deviation request, not a direct edit |

## 3. Ledger Schema Conformance

Run against the live Postgres schema, or against [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md) as the source of
truth if the database isn't reachable.

**Execution note:** items 3.1–3.4 require live database access, which Claude does not have.
These are handed off to OpenCode as a standing instruction — see § OpenCode Instruction —
Section 3 Execution, below. Item 3.5 is a document-grep and stays with Claude.

| # | Check | Method |
|---|---|---|
| 3.1 | All seven tables exist: `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`, `triage_findings` | `\dt` or equivalent against the live database |
| 3.2 | Sequencing is enforced by the orchestrator against [[[pdlf:app-factory/phase-a-init/a01-build-plan\|Run Plan]]](C:/pdlf/app-factory/phase-a-init/a01-build-plan.md)'s dependency table, not by a database FK — confirmed 2026-07-18 there is no inter-step constraint at the schema level, by design. Verify OpenCode actually checks dependencies before writing a step's ledger row | Attempt a real or simulated out-of-order step invocation through the normal PDLF flow (not a raw insert); confirm OpenCode blocks or flags it before writing |
| 3.3 | `build-verified`'s `triage_findings` query returns correct pass/fail | Seed a feature's findings with a mix of `wontfix`/resolved/open rows; confirm the gate query matches [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)'s stated logic exactly |
| 3.4 | `deviations` captures description, options presented, and decision correctly | Trigger a real or seeded deviation; confirm all three fields are populated, not just the decision |
| 3.5 | No document anywhere states a table count other than seven | Grep the live document set for "six tables" — this exact error has recurred three times already this session |

## 4. Skill Invocation Correctness

Run whenever a step file is built, rebuilt, or reviewed — not a one-time pass.

| # | Check | Method |
|---|---|---|
| 4.1 | Every skill name in the step file exists at its claimed source, under that name | Fetch the real `SKILL.md` (GStack or Matt Pocock) and confirm |
| 4.2 | The skill is actually invocable the way the step file assumes (user-invoked vs. model-invoked, standalone vs. wrapped) | Read the skill's own description/frontmatter — do not infer from its name, per the [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference\|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md)/`grill-with-docs` precedent |
| 4.3 | If the skill is a thin wrapper, every skill it delegates to is also accounted for | Read the wrapper's body in full |
| 4.4 | Recheck cadence: skills are copied files, not a live plugin — upstream changes don't propagate automatically | Periodic manual diff against upstream `main` for every skill PDLF depends on; no fixed interval defined yet, needs a decision |

## 5. Documentation Consistency

The exact class of check this housekeeping session has been running manually. Continuous,
per your explicit instruction — not a one-time pass.

| # | Check | Method |
|---|---|---|
| 5.1 | No broken or doubled file paths | Grep for repeated path segments (e.g. `specifications-local/specifications-local/`) |
| 5.2 | No two files claim the same canonical status for the same information | Check for competing "this is the map/index/source of truth" documents |
| 5.3 | No dead references to retired or non-existent files | Cross-check every file path cited in every document against what actually exists |
| 5.4 | Naming matches [[[default:specifications-global/spec-nomenclature\|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) | Check filenames against its Stepwise File Naming and Repo & Path Conventions tables |
| 5.5 | No document describes a retired mechanism as current | Check for the disposition-audit model, Steps 2–3, `to-prd`/`to-spec` as live, the old staging/production model — the recurring classes of staleness found this session |
| 5.6 | Cross-references are bidirectional where the relationship warrants it | Check that a file frequently pointed to also points back where useful (e.g. [[[pdlf:app-factory/phase-a-init/a01-build-plan\|Run Plan]]](C:/pdlf/app-factory/phase-a-init/a01-build-plan.md) ↔ [[[pdlf:pdlf-library/docs-local/pdlf-built-report\|Step Mapping]]](C:/pdlf/pdlf-library/docs-local/pdlf-built-report.md)) |

## 6. Deviation Mechanism

Run against a live or seeded deviation event.

| # | Check | Method |
|---|---|---|
| 6.1 | Exactly three options presented (Authorize / Do not authorize / Skip) | Compare against the template in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) |
| 6.2 | The agent never decides unilaterally | Confirm the flow always stops for developer input, no default path taken automatically |
| 6.3 | The deviation is recorded in the `deviations` table, not just narrated in chat | Query the table after the event |

---

## OpenCode Instruction — Section 3 Execution

**TASK: Execute Ledger Schema Conformance checks 3.1–3.4 against the live `pdlf` database.**

Use the WSL→Windows PowerShell bridge per [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md).
Do not modify any real project's data. Use a disposable test/seed context for 3.2–3.4 —
create and drop test rows scoped to a dummy `project_slug` (e.g. `_selftest`), never touch
a real project's rows.

1. **Check 3.1:** Run `\dt` against the `pdlf` database. Report which of the seven expected
   tables (`projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`,
   `triage_findings`) exist. Report pass/fail per table.

2. **Check 3.2, corrected 2026-07-18:** No inter-step FK exists at the database level, by
   design — confirmed via live test, see [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md) Principle 2. This check
   no longer tests a raw insert. Instead: confirm [[[pdlf:app-factory/phase-a-init/a01-build-plan|Run Plan]]](C:/pdlf/app-factory/phase-a-init/a01-build-plan.md)'s Step Dependencies table
   is the sole enforcement mechanism, and that no step file's own procedure attempts to
   write a ledger row without first consulting it. This is a documentation/procedure check,
   not a database check — reassign to Section 5 (Documentation Consistency) on this
   checklist's next revision.

3. **Check 3.3:** For `project_slug = '_selftest'`, seed three `triage_findings` rows for one
   feature's `step_id`: one `wontfix`, one with a non-null `resolved_at`, one with
   `triage_label = 'needs-triage'` and `resolved_at IS NULL`. Run the `build-verified` gate
   query as defined in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md). Expected result: gate does NOT pass (one
   open finding remains). Then resolve the third row and re-run — expected result: gate
   passes. Report both outcomes.

4. **Check 3.4:** Insert a `deviations` row with a description, a populated
   `options_presented` JSON object, and a decision. Query it back. Report whether all three
   fields round-trip correctly.

5. Clean up all `_selftest`-scoped rows after the run.

**Report back:** pass/fail for each of 3.1–3.4, plus the raw query results for 3.3's
before/after gate check. If any check fails, stop and report — do not attempt to fix the
schema without developer authorization.

---

## Decisions Closed

**4.4 — recheck cadence for upstream skill drift, resolved:** a skill is rechecked against
its real upstream source (a) every time a step file using that skill is built or rebuilt —
already the standing practice since Steps 14/15/16 — and (b) at the start of every
housekeeping pass, as a standard first step, not an occasional extra. No separate fixed
calendar interval — cadence is tied to activity, not a clock, consistent with how this
whole document treats "continuous" testing.

**Checklist not yet run end-to-end, resolved:** Sections 1, 2, 4, 5, 6 have all been
implicitly exercised during this session's work (Steps 11/12/14/15/16 rebuild, the
cross-document audit, the skill-source verification passes) — that constitutes the first
real run, just not one that was tracked against this document as the instrument at the
time. Section 3 completes the first full run once OpenCode returns the report requested
above. No further open point remains — the first full pass is in progress, not undefined.

---

*chk-pdlf-self-test.md v1.1. Created 2026-07-18 as part of the testing-strategy
housekeeping pass. Updated same day: Section 3 handed off to OpenCode as a standing
instruction; both prior open items resolved with concrete decisions. Companion document:
the retired `chk-anvil-app-testing.md` (global, not yet built).*
