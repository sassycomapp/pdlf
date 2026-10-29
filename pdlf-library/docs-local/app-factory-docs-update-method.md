---
title: "app-factory-docs-update-method"
updated: "2026-10-29"
doc-id: "mb-567f5152"
---
# App Factory Docs Update Method

## What this method is

This method brings each step's set of seven in the app factory up to date with its build plan. A step's build plan holds its design. The step's test specification, config, reference, explainer, decision tree and module are written from that build plan, in a fixed order, one suite at a time.

A suite is the set of seven of one step, named by its app-factory code (for example `a01`, `b12`, `c18`).

## How PDLF is completed

PDLF is completed phase by phase. Every phase goes through three stages, in this order:

1. **Built.** Every suite of the phase is brought up to date by the method below: the build plan is closed, and the test specification, config, reference, explainer and decision tree are written from it.
2. **Proven.** `mb-3-cs` runs through the phase. Whatever fails or is missing is corrected in PDLF, and the run continues from the step corrected.
3. **Finished.** The phase's modules are written from its proven suites.

The phases are taken in this order:

1. **Phase B is built.**
2. **Phase A is built for Phases A and B:** every entry point (Steps 2 to 10); the orchestrator (Step 1) as far as it runs Phases A and B; and the resume check, by which the orchestrator reads the ledger when it starts and offers to continue an unfinished run at the step where it stopped.
3. **Phases A and B are proven, then finished.** `mb-3-cs` runs through them by entry point 03. Step 11 makes `mb-3-cs` in a copy of the project template, `C:\dev\project-template\`, and the existing repositories of `mb-3-cs` are the context it brings.
4. **Phases C, D, E and F follow, one at a time.** For each: the phase is built; the orchestrator is extended to run it; the `mb-3-cs` run resumes at the step where it stopped, never from the start; the phase is proven, then finished.

An entry point is proven the first time a run takes it. A step is proven when `mb-3-cs` has run through it.

**Before every run, David backs up `mb-3-cs`.** Each time `mb-3-cs` runs through PDLF, David first copies its business folder, `C:\dev\dev-mb-3-cs\`, to his backup folder, so that a run that goes wrong can be undone.

## How it works

For each suite, in this order:

1. **Close the build plan.** Every item in the build plan's carried-over block, and every older review finding, is settled: what is still true is written into the step entry; what is not is removed. The block is then removed. The build plan holds no open item.
2. **Check the test specification** (`{suite}-test-spec.md`) against the closed build plan: every output the build plan names is proved by a test, every security review is proved by PR-04, and every test it names exists in the test suite. Correct it where the build plan changed.
3. **Write the config** (`{suite}-config.md`): the step's fixed values: inputs, outputs, file paths, skills, gate, BFT level and Sentinel scrutiny.
4. **Write the reference** (`{suite}-reference.md`): what the agent does, in order, with a link at each action to the system or source it uses.
5. **Write the explainer** (`{suite}-explainer.md`): what the step is, how it works, why it works that way and what has to happen.
6. **Generate the decision tree** (`{suite}-decision-tree.html`) from the reference, so that it matches the reference and cannot drift from it. Decision trees are HTML until PDLF switches to `mb-archify-scope` and Archify.
7. **Scan the files.** Every file is scanned before it is sent. A file is rejected if it holds a dead link, a dependency on an application's files, a term from the banned list below, or wording about what came before. A rejected file is corrected and scanned again.
8. **Send the files** to the developer, each with the path of the file it replaces.

The config, reference and explainer are written afresh from the closed build plan. The old text is source material only and is replaced completely. A fact lives in only one of the config, the reference and the explainer.

Each step's testing is its `{suite}-test-spec.md`, drawn from the test suite, which includes the testing and quality methodology.

**Banned terms:** `makepdlf`, `stepwise`, `mb-5-pdlf`, `mb5pdlf`, Daily Intentions Tracker, test application, staging, `develop` and `stable` branches, dev log, judgement trail, three levels of testing (the method is Levels 1, 2 and 3 of the test suite; use those names), `anvil db apply-schema` as an agent action.

## Why it works this way

- **The build plan first.** A config, reference or explainer written from a build plan that still holds open items inherits them. Closing the build plan first means each document is written once.
- **Phase by phase, each proven before the next is built.** A fault found by a real run in one phase is fixed before it is repeated in the next, and every later phase is built on steps that are known to work.
- **Phase B first, then Phase A.** Phase B is the most fully designed phase. The orchestrator can only be designed against steps that exist, so Phase A is built once Phase B is, and only as far as the phases built so far; it is extended with each later phase.
- **A run resumes, never restarts.** Each phase consumes what the phases before it produced. Resuming keeps the `mb-3-cs` outputs already proven, and proves the resume check itself on every phase.
- **A backup before every run.** A run writes to `mb-3-cs`'s repositories and to Anvil. The backup lets a failed run be undone without loss.
- **Written afresh, then scanned.** The old step documents hold outdated locations and methods. Writing from the build plan, and scanning before sending, keeps every one of them out of the finished documents.
- **The decision tree is generated.** A tree drawn by hand drifts from the reference it pictures; a tree generated from the reference does not (build plan rule 4.5).
- **Modules last in each phase.** A module is the finished step. It is written only once the step has been proven on `mb-3-cs`.

## What has to happen

- David backs up `mb-3-cs` before every run.
- The developer approves each suite's files before they are saved.
- The developer saves each file over the file it replaces and runs commit-all after each phase.
- User help documentation and video documentation are added to these documents when they are designed.
