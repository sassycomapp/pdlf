---
title: "README"
doc-id: "mb-5220bac9"
updated: "2026-10-01"
---
# PDLF Library

The canonical technical documentation home of the PDLF system — the running
Project Development Lifecycle Framework — living in the PDLF environment
(`C:\pdlf`). The makePDLF development project (`C:\dev\dev-makepdlf\`)
builds the system; this library documents it. Decisions, specifications, and
explainers that are canonical to the PDLF system live here once they are
settled.

## Folder map

| Folder | Holds | The one-line test |
|---|---|---|
| `pdlf-adr/` | Architecture decision records | A decision that was made, with its reasoning |
| `pdlf-specifications/` | Technical specifications | The binding truth: exact paths, exact rules, checkable requirements |
| `pdlf-policy/` | Policies | Rules agents must obey — enforced, not explained |
| `pdlf-processes/` | Procedures | A procedure someone follows, in order |
| `pdlf-explainer-docs/` | Explainers | What something is, what role it plays, why it is this way — binds nobody |
| `pdlf-explainer-docs/pdlf-stepwise/` | Per-step explainers | One folder per step (1–46), filled as each step is finalized |
| `pdlf-register/` The use of registers has been discontinued. Please review | The register | One row per document in this library |

Explainers make you understand; specifications make the machine behave;
policies forbid; ADRs record why; processes walk through doing.

## Naming rules

- Every filename carries the library and type prefix: `pdlf-adr-`,
  `pdlf-spec-`, `pdlf-pol-`, `pdlf-proc-`, `pdlf-expl-`. A document's
  identity (its filename) is therefore unique across the whole corpus by
  construction.
- Files are named descriptively, without sequence numbers. Two standing
  exceptions are inherently ordinal: the stepwise material and the
  app-factory modules.
- Full naming rules, including the project-slug rules that keep every
  artifact name unambiguous: `pdlf-specifications/pdlf-spec-nomenclature.md`.

## What is here now, and what is deferred

Present: the artifact-saving convention ADR, the artifact-and-handover
specification, the nomenclature specification, three explainers (orchestrator
agent, artifact lifecycle, app-factory), the objective review. The
environment explainer and system explainer were returned to
`C:\mybizz\mybizz-os-docs\` on 2026-09-19 per developer instruction; the
objective review was moved here from `C:\mybizz\mybizz-os-docs\` on
2026-09-11 (moved, not copied — sole homes, no duplicates).

Deliberately deferred to the makePDLF environment until makePDLF completes:
the per-step explainers (`pdlf-stepwise/` — folders exist, empty), the
stepwise gating policy, and the stepwise closeout process. These describe
machinery still being built and reworked; they will migrate here with the
app-factory modules when the system is complete.

## Relationship to its neighbours

- **The makePDLF development project** builds the system and holds its own
  in-development step files, policies, and procedures. This library holds
  what is settled and canonical to the finished system.
- **[[[mybizz-os-docs:os-reference-docs/pdlf-explainer]]](C:/mybizz/mybizz-os-docs/os-reference-docs/pdlf-explainer.md)** (now `pdlf-explainer.md` in `C:\mybizz\mybizz-os-docs\`,
  returned 2026-09-19) is the full
  general explainer of PDLF, moved here from `C:\mybizz\mybizz-os-docs\` on
  2026-09-11 — this is its sole home; no duplicate exists elsewhere.
- **[[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-objective-review]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-objective-review.md)** assesses PDLF against the comparable
  frameworks in the field.
- **The app-factory** (`C:\pdlf\app-factory\`) is the machinery this library
  documents; its modules implement the conventions specified here.

## Register The use of registers has been discontinued. Please review

`pdlf-register/pdlf-register.md` The use of registers has been discontinued. Please review — one row per document, maintained as
documents land. Nothing exists in this library that is not registered.

---

*End of README — PDLF Library*