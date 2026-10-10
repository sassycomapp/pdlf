---
title: "domain"
doc-id: "mb-19ac844a"
updated: "2026-10-10"
---
# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

## PDLF's own domain (dev-makepdlf workspace)

- **`docs-local/`** — System description, scaffold plan, design specs, docmap, nomenclature.
- **`adr-local/`** — ADRs for PDLF's own development decisions (postgres-ledger, stepwise decomposition, renumbering, etc.).
- **`policy-local/`** — Binding PDLF policies (BFT discipline, sequential enforcement, Anvil platform rules, etc.).
- **`specifications-local/`** — PDLF-specific specifications.
- **`docs-standard-local/`** — Standard document templates.

## When PDLF runs a project

- **`CONTEXT.md`** at the project-library root — domain glossary (from domain-modeling). When working on a PDLF-managed project, read this first.
- **`adr-local/`** — Project-specific architecture decisions.
- **`policy-local/`** — Project-specific binding policies.
- **`specifications-local/`** — Project-specific specifications.
- **`C:\dev\project-library-global\adr-global\`** — Global architecture decisions (42 ADRs) that apply across all Anvil.works projects. Read ADRs that touch the area you're about to work in.
- **`C:\dev\project-library-global\specifications-global\`** — Binding global specifications (25 files: Anvil platform, M3 design, testing, security, deployment, etc.).

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

## File structure (per project, when PDLF runs)

```
<project-library>/
├── CONTEXT.md                            ← Domain glossary
├── adr-local/                            ← Project ADRs
├── docs-local/                           ← Project-specific docs
├── specifications-local/                 ← Project specifications
├── policy-local/                         ← Project policies
└── ...

C:\dev\project-library-global\
├── adr-global/                           ← Cross-project ADRs (42+ files)
├── specifications-global/                ← Cross-project specs (25 files)
├── policy-global/                        ← Cross-project policies
└── ...
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in `CONTEXT.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal — either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md)).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders) — but worth reopening because…_
