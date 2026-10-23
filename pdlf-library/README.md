---
title: "README"
doc-id: "mb-2c28aeef"
updated: "2026-10-23"
---
# PDLF Library

The PDLF library holds how PDLF itself works: the machinery every step relies on. What a good Mybizz application is lives in `project-library-global`; what is true of one application lives in that application's own project library.

## Folders

| Folder | What it holds |
|---|---|
| `adr-local/` | PDLF's own decisions and why they were made. |
| `specifications-local/` | What must be true of PDLF: execution discipline, gates, BFT, the ledger, artifact handover, the skill context pack, and PDLF's process tests. |
| `policy-local/` | How PDLF makes decisions and works; `pol-INDEX.md` lists them. |
| `operating-procedures/` | PDLF's repeatable procedures, such as the health check. |
| `templates-local/` | Blank forms PDLF fills in: the Step Receipt, the ISA, the self-test checklist and the pre-project files. |
| `pdlf-explainer-docs/` | What PDLF, the app factory and PDLF's testing are, how they work and why. |
| `docs-local/` | PDLF's working documents: the to-do list, the update method, the skills scoping strategy, the built report and the configuration. |
| `wip/` | Working files of the moment. Not part of PDLF. |

## Rules

- A fact lives in one document; every other document links to it.
- No project data is kept here. A step's outputs for a project go to that project library's `pdlf-outputs\{step}\` folder.
