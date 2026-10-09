---
title: "dev-makepdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-10-09"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

> **Review note (2026-10-08):** This list merges the earlier and the revised versions of this file into one, grouped by subject. It was written before many later decisions, so each item carries a note where a later system, method or decision has made part or all of it obsolete. Notes marked **Superseded** mean that part no longer applies. Notes marked **Changed since** mean the item still stands but must be re-planned against the newer setup. Items with no note are still current as written. Section E holds items that are fully superseded and leave nothing to do. This file is to be resolved when makePDLF planning resumes.

---

## A. Rebuilding the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 (excluding 42/42A/43/44, see A2) are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16.

> **Changed since:** This was previously listed as "deferred by explicit agreement, not tracked as an action item." It is the main makePDLF task and is now an action item. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`.

### A2. Rebuild Steps 42, 42A, 43, 44

These steps currently model a staging/production environment split that does not apply to this platform. Rebuild them around the actual publishing mechanism: a `develop` → `stable` GitHub merge, performed by the operator, outside PDLF's own pipeline. See [[[pdlf:makepdlf-project-library/adr-local/adr-no-staging-environment-five-app-isolation|ADR No Staging Environment Five App Isolation]]](C:/pdlf/makepdlf-project-library/adr-local/adr-no-staging-environment-five-app-isolation.md) for full reasoning. Deferred to Phase E.

---

## B. Rules for building every step

### B1. Global-content query-fetch-apply sequence

Rule and enforcement mechanism decided 2026-07-19 — see
[[[pdlf:makepdlf-project-library/adr-local/adr-global-content-discovery-and-application-discipline|ADR Global Content Discovery and Application Discipline]]](C:/pdlf/makepdlf-project-library/adr-local/adr-global-content-discovery-and-application-discipline.md) and
[[[pdlf:makepdlf-project-library/policy-local/pol-memory-and-knowledge|Pol Memory and Knowledge]]](C:/pdlf/makepdlf-project-library/policy-local/pol-memory-and-knowledge.md). `project-library-global`'s GBrain registration is confirmed
working, so the mechanism is usable, not just designed. Remaining work: build the
five-step sequence and citation requirement into each relevant step file (17, 20, 22, 26,
27, 35, 35A, 37, 38, 41–45 at minimum) as that step is written or rebuilt. Deferred to
Phase B onward, same treatment as A2.

> **Changed since:** This is a rule for building each step, not a separate task; it is applied as part of A1. Since it was written, GBrain was upgraded to 0.59.18.0, every documentation repository became a federated source so one search covers everything, and cross-repository links now use the standard form `[[[source-id:slug]]](C:/full/path.md)`, written by agents as `[[name]]` and converted by the `mb-doc-check` commit hook. The five-step sequence must be checked against that setup before it is built into any step.

### B2. End-of-step housekeeping: governed memory writes, dream cycle, commit and push

Original rule: two related, recurring per-step items, applied together as each new step file is built:

- **Governed memory writes.** Every step's own housekeeping question ("sync/embed GBrain?") must invoke the real, governed pipeline (`mb-submit-memory`, using the `pdlf_step_sync` credential) rather than the older, ungoverned raw sync. Already applied to Steps 11, 12, 14, 15, 16. Needs applying to every step from 17 through 46 (excluding the retired Step 13) as each is actually built.
- **Dream-cycle discipline.** At the end of every step, after the governed memory-write sequence, run: `gbrain dream` for real (never `--dry-run`), then `gbrain eval suspected-contradictions` immediately afterward (does not run automatically), then review the findings. Already applied to the same five steps (11, 12, 14, 15, 16). Same remaining scope: Steps 17–46 as each is built.

> **Superseded — governed memory writes:** End-of-step housekeeping is now the OpenCode skill `/mb-close-out`, which the developer runs on demand after every makePDLF step. It saves governed memory, processes the memory governor's review queue and updates the project documents through `mb-project-docs`, using the existing scripts and skills. Steps no longer carry their own memory-write sequence; each step ends by telling the developer to run `/mb-close-out`.
>
> **Superseded — dream cycle:** The dream cycle never runs by itself and is not run at the end of a step. The developer runs it during Sunday maintenance, prompted by the 9 a.m. Google Calendar reminder that lists every maintenance task in order.
>
> **Superseded — commit and push inside steps:** Agents never commit or push to Git, and no Git grant exists (global `AGENTS.md`). The developer runs `commit-all.sh` in the WSL terminal, which commits every documentation repository, updates GBrain and pushes.

### B3. Remove obsolete housekeeping from the steps already built

> **Changed since:** Follows from B2. The dream-cycle instructions written into Steps 11, 12, 14, 15 and 16 must be removed. The commit-and-push questions in Step 11 (items 18 and 22) and in the other built steps must be removed. Each of these steps must instead end by telling the developer to run `/mb-close-out`.

### B4. End-to-end proof of the governed memory pipeline

The final, real end-to-end proof that the governed memory pipeline works together in practice requires PDLF itself to be a real, running system before it can be tested. It was previously tracked in Deferred and Unresolved Matters, Entry 2.

> **Changed since:** The one-time live test still stands. Its natural setting is the first real step run on `mb5pdlf`, the test project for makePDLF and PDLF.

---

## C. Testing

### C1. Integrate Suite A and Suite B into Steps 35A, 36, 37, 38, 39, and relook the testing suite

Both testing checklists ([[[pdlf:makepdlf-project-library/checklists-local/chk-pdlf-self-test|Chk Pdlf Self Test]]](C:/pdlf/makepdlf-project-library/checklists-local/chk-pdlf-self-test.md) exists; the earlier
`chk-anvil-app-testing.md` was retired and is no longer on disk anywhere —
verified 2026-09-18) are referenced from [[[pdlf:makepdlf-project-library/policy-local/pol-testing-and-quality|pol-testing-and-quality]]](C:/pdlf/makepdlf-project-library/policy-local/pol-testing-and-quality.md), but
their checks are not yet built into the actual stepwise files that do
testing work. Deferred to Phase D, when those step files are rebuilt.

The testing suite implemented in PDLF is to be relooked at the same time, not separately. Real, preserved seed material exists from an earlier MB-3-CS testing iteration (test taxonomy, a working Anvil-context test technique, real Anvil/M3-specific pass/fail criteria) — see [[[pdlf:makepdlf-project-library/docs-local/pdlf-testing-seed-material/pdlf-testing-seed-material-readme|Seed Material (from MB-3-CS)]]](C:/pdlf/makepdlf-project-library/docs-local/pdlf-testing-seed-material/pdlf-testing-seed-material-README.md) in `makepdlf-project-library` for what's there and how to use it when this work is actually picked up.

> **Changed since:** The earlier lists carried the Suite A/B integration and the testing relook as two separate items; they are one job and are merged here.

---

## D. Code checking

### D1. Deterministic server-code dependency checker — hard gate

`GBrain`'s own symbol resolution only resolves same-file references by design — it cannot trace cross-file calls, the majority case in any real codebase. Decision already made: implement via `Graphify`, scoped to `server_code/` only (`client_code/` explicitly out of scope — Anvil's RPC/event-handler wiring is string-based and invisible to any static analyzer regardless). Build as a standing gate inside the existing `code-plan-build` workflow's "Mandatory checks before edits" step, authored once in PDLF so every future PDLF-managed project inherits it automatically. Not yet done: actual gate implementation and wiring into PDLF's step/gate definitions.

> **Changed since:** The developer has since stated doubt about Graphify's benefit, and the decision is deferred. He also takes the view that code sources should not be in GBrain. The "decision already made" above no longer stands as settled and must be reopened before any gate is built.

---

## E. Superseded — nothing left to do

### E1. Step 11 — include Cupcake setup for new projects

Step 11 (project init) needs a real addition: running the appropriate `cupcake init` sequence as part of setting up a new project, matching the real, live pattern already established for `makepdlf-project-library`. Applies once a new PDLF-managed project actually starts — see [[[mybizz-config-docs:cupcake/cupcake-config|Cupcake Configuration]]](C:/mybizz/mybizz-config-docs/cupcake/cupcake-config.md) for current project-init scope and status.

> **Superseded:** Cupcake enforces its rules globally. Every rule lives in `~/.config/cupcake/policies`, and a global fallback setup in `~/.config/cupcake/fallback` covers any folder with no Cupcake setup of its own (checked 2026-10-08). The `.cupcake` folder in `makepdlf-project-library` holds only the standard setup files and no rules of its own. The Cupcake exam of 2026-10-04 confirmed that writes are blocked in a session opened in a folder without its own setup. A new project is therefore protected automatically, and Step 11 needs no Cupcake action. Agents needing access outside their project hand the developer an `mg-grant` or `net-grant` line, per the global `AGENTS.md`.

### E2. Build out `Instructions.md` files

Approximately 20 placeholder files in `C:\dev\project-template\`. Confirmed non-blocking and low priority — these files have no functional role in PDLF's operation. Revisit when convenient.

> **Superseded:** The project template at `C:\dev\project-template` is no longer a GitHub repository and is applied by hand when needed. The placeholder files do nothing, and Step 11 already freezes the creation of further `Instructions.md` files.

### E3. Define a recheck cadence for `project-library-global`

Only one file ([[[default:specifications-global/spec-testing-methodology-standards|Testing Methodology]]](C:/dev/project-library-global/specifications-global/spec-testing-methodology-standards.md)) has been reviewed out of 98. Confirmed mostly out of scope for dev-makepdlf's own housekeeping — most of it concerns the Anvil application brand, not PDLF. No action planned unless a specific need surfaces (e.g., building Suite B's next iteration, or a step file that references a specific global file).

> **Superseded:** The item itself says no action is planned, so it is not a task. Since it was written, `project-library-global` was made private, is a federated GBrain source covered by the same single search as every other documentation repository, and is defined as the definitive library of specifications, ADRs and standards for every app PDLF builds. Its README and guides/standards sections are still work in progress, but that work belongs to `project-library-global`, not to makePDLF.

### E4. Full cross-document consistency pass

Complete for everything in its defined scope (stepwise shared references, specs, policies, docs-local, root config, templates). Not extended to `project-library-global` or Steps 17–46, both deliberately out of scope at the time.

> **Superseded:** The global `AGENTS.md` now requires any agent that changes a fact to update every document stating it in the same task, and the `mb-doc-check` commit hook keeps links live at every commit. A separate consistency pass is no longer needed.
