---
title: "app-factory-docs-update-method"
updated: "2026-10-23"
doc-id: "mb-567f5152"
---
# App Factory Docs Update Method

## What this method is

This method brings each step's set of seven in the app factory up to date with its build plan. A step's build plan holds its design. The step's test specification, config, reference, explainer, decision tree and module are written from that build plan, in a fixed order, one suite at a time.

A suite is the set of seven of one step, named by its app-factory code (for example `a01`, `b12`, `c18`).

PDLF is completed in three passes:

1. **Pass 1, the documents.** Every suite, phase by phase, in the order B, C, D, E, F, then A: the build plan is closed, and the test specification, config, reference, explainer and decision tree are written from it. Modules are not written.
2. **Pass 2, the pressure test.** `mb-3-cs` is pulled through PDLF from beginning to end, after David has backed it up. Whatever fails or is missing is corrected in PDLF.
3. **Pass 3, the modules.** A phase's modules are written once `mb-3-cs` has run through that phase in Pass 2.

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

**Banned terms:** `makepdlf`, `stepwise`, `mb-5-pdlf`, `mb5pdlf`, Daily Intentions Tracker, test application, staging, `develop` and `stable` branches, dev log, judgement trail, three levels of testing, `anvil db apply-schema` as an agent action.

## Why it works this way

- **The build plan first.** A config, reference or explainer written from a build plan that still holds open items inherits them. Closing the build plan first means each document is written once.
- **Phase by phase.** A fault found in one phase is fixed before it is repeated in the next.
- **Phase B first.** Phase B is the most fully designed phase and the first `mb-3-cs` runs through.
- **Written afresh, then scanned.** The old step documents hold outdated locations and methods. Writing from the build plan, and scanning before sending, keeps every one of them out of the finished documents.
- **The decision tree is generated.** A tree drawn by hand drifts from the reference it pictures; a tree generated from the reference does not (build plan rule 4.5).
- **Modules last.** A module is the finished step. It is written only once the step has been proven on `mb-3-cs`.

## What has to happen

- The developer approves each suite's files before they are saved.
- The developer saves each file over the file it replaces and runs commit-all after each phase.
- User help documentation and video documentation are added to these documents when they are designed.
