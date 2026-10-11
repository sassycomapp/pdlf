---
title: "README"
doc-id: "mb-5220bac9"
updated: "2026-10-11"
---
# PDLF Library

The PDLF library holds the shared machinery every module in `app-factory/` relies on: the decisions, specifications, policies, templates, explainers and working documents of the PDLF system. Knowledge and standards that are not specific to PDLF, Anvil knowledge included, live in `project-library-global`, not here.

## The intent comes first

[[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-intent|PDLF Intent]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-intent.md) is the single statement of what PDLF is meant to be. Where any document disagrees with it, the intent wins and the other document is corrected.

## Folders

| Folder | What it holds | The test for putting a document here |
|---|---|---|
| `pdlf-explainer-docs/` | Explainers, including `pdlf-intent.md` | It says what something is and why. It binds nobody. |
| `adr-local/` | Architecture decision records | It records a decision that was made, with its reasoning. |
| `specifications-local/` | Specifications (`spec-` prefix) | It states exact paths, rules and requirements the machinery must meet. |
| `policy-local/` | Policies (`pol-` prefix), listed in `pol-INDEX.md` | It is a rule the agent must obey. |
| `templates-local/` | Templates | It is a blank form a step fills in, such as a step receipt. |
| `docs-local/` | Working documents of the system | It tracks the system's state: configuration, build progress, run order, to-do list, judgement trail, reference material. |

## The documents that steer the build

- `app-factory/pdlf-build-plan.md`: the blueprint for building PDLF.
- `docs-local/pdlf-built-report.md`: what has been built.
- `docs-local/orchestrator-run-plan.md`: the order the orchestrator runs the steps.

## Finding documents

Documents are found by GBrain search (source `pdlf`).
