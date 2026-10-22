---
title: "app-factory-docs-update-method"
updated: "2026-10-22"
doc-id: "mb-567f5152"
---
# App Factory Docs Update Method

## What this method is

This method brings each step's set of seven in the app factory up to date with its build plan. A step's build plan holds its design. The step's test specification, config, reference, explainer, decision tree and module are written from that build plan, in a fixed order, one suite at a time.

A suite is the set of seven of one step, named by its app-factory code (for example `a01`, `b12`, `c18`).

## How it works

Suites are worked phase by phase, starting with Phase B, then C, D, E, F and A.

For each suite, in this order:

1. **Close the build plan.** Every item in the build plan's "Carried over from the old workflow" block, and every older review finding, is settled: what is still true is written into the step entry; what is not is removed. The block is then removed. The build plan holds no open item.
2. **Check the test specification** (`{suite}-test-spec.md`) against the closed build plan: every output the build plan names is proved by a test, every security review is proved by PR-04, and every test it names exists in the test suite. Correct it where the build plan changed.
3. **Write the config** (`{suite}-config.md`): the step's fixed values: inputs, outputs, file paths, skills, gate, BFT level and Sentinel scrutiny.
4. **Write the reference** (`{suite}-reference.md`): what the agent does, in order.
5. **Write the explainer** (`{suite}-explainer.md`): what the step is, how it works, why it works that way and what has to happen.
6. **Generate the decision tree** (`{suite}-decision-tree.html`) from the reference, so that it matches the reference and cannot drift from it. Decision trees are HTML until PDLF switches to `mb-archify-scope` and Archify.
7. **Send the files** to the developer, each with the path of the file it replaces.

A fact lives in only one of the config, the reference and the explainer.

The module (`{suite}-module.md`) is not written in this pass. A phase's modules are compiled once that phase has run on the test application, `mb-5-pdlf`.

## Why it works this way

- **The build plan first.** A config, reference or explainer written from a build plan that still holds open items inherits them. Closing the build plan first means each document is written once.
- **Phase by phase.** A phase is run on the test application as soon as its steps are written (build plan rule 4.8). A fault found in one phase is fixed before it is repeated in the next.
- **Phase B first.** Phase B is the most fully designed phase and the first the test application runs.
- **The decision tree is generated.** A tree drawn by hand drifts from the reference it pictures; a tree generated from the reference does not (build plan rule 4.5).
- **Modules last.** A module is the finished step. It is compiled only once the step has been proven on the test application.

## What has to happen

- The developer approves each suite's files before they are saved.
- The developer saves each file over the file it replaces and runs commit-all after each phase.
- The testing scheme, user help documentation and video documentation (Pass 3 of the skills scoping strategy) are added to these documents when they are designed. Until then each step's documents carry the light testing element its build plan names.
