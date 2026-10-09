---
title: "system-description"
doc-id: "mb-dd5b5693"
updated: "2026-10-09"
---
# makePDLF Workshop — System Description

## What this document covers

This document describes the makePDLF workshop: the place where PDLF is designed, built and tested before it is deployed. It says where each part of PDLF is defined, how the workshop is laid out, and what state the build is in.

It does not explain PDLF itself. What PDLF is, why it exists and how it works are covered in [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-explainer|PDLF Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-explainer.md). The two documents are kept separate so that each has one job: the explainer describes the system, and this document describes the workshop that builds it.

---

## Where each part of PDLF is defined

PDLF is built as many small files rather than one large one. Each part of the system has exactly one file that defines it, so that two documents can never disagree about the same fact. The table below says which file that is.

| Part of PDLF | Defining file |
|---|---|
| Execution order, branching and dependencies between steps | [[[pdlf:makepdlf-project-library/stepwise/run-plan\|Run Plan]]](C:/pdlf/makepdlf-project-library/stepwise/run-plan.md) |
| What each step number is and who handles it (a lookup table only, with no say over order) | [[[pdlf:makepdlf-project-library/stepwise/step-mapping\|Step Mapping]]](C:/pdlf/makepdlf-project-library/stepwise/step-mapping.md) |
| Each step's own procedure, inputs and outputs | One file per step in `stepwise/`, named `step-{NN}-{name}.md` |
| The execution sequence every step follows | [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md) |
| BFT definitions and the rules against rubber-stamping | [[[pdlf:makepdlf-project-library/specifications-local/spec-bft\|Spec: BFT]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md) |
| The BFT level assigned to each step (currently 27 Full, 7 Light, 6 None, 40 steps in total) | [[[pdlf:makepdlf-project-library/templates-local/bft-checkpoint-cheatsheet-v2\|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/makepdlf-project-library/templates-local/bft-checkpoint-cheatsheet-v2.md) |
| The sections of the Ideal State Artifact | [[[pdlf:makepdlf-project-library/templates-local/isa-template-v2\|ISA Template v2]]](C:/pdlf/makepdlf-project-library/templates-local/isa-template-v2.md) |
| The Postgres ledger and the WSL-to-Windows bridge used to reach it | [[[pdlf:makepdlf-project-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-postgres-ledger.md) |
| Skill design decisions | [[[pdlf:makepdlf-project-library/specifications-local/spec-skill-design\|Spec: Skill Design]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-skill-design.md) |
| Test-mode project branching (defined, but not yet reconciled with the rest of PDLF's testing design) | [[[pdlf:makepdlf-project-library/policy-local/step-conditional-state-policy\|Step Conditional State Policy]]](C:/pdlf/makepdlf-project-library/policy-local/step-conditional-state-policy.md) |
| PDLF's internal architecture decisions | `adr-local/` |

---

## How the workshop is laid out

The workshop is `C:\dev\dev-makepdlf\`. PDLF's own documentation and step files live in its documentation repository, `makepdlf-project-library`:

```
C:\dev\dev-makepdlf\makepdlf-project-library\
├── stepwise/                     ← step files, build notes, decision trees, shared references
│   └── skill-source-reference/   ← external skill source kept as verification evidence
├── specifications-local/         ← binding specifications
├── policy-local/                 ← binding PDLF policies
├── templates-local/              ← runtime templates
├── docs-local/                   ← documentation, including this file and the docmap
├── adr-local/                    ← PDLF internal ADRs
├── agents/                       ← Matt Pocock skills configuration for the workshop itself
├── pre-project/
├── Standard-operating-procedures-local/
├── obsolete/                     ← retired files
├── wip/                          ← active work in progress, including the makePDLF to-do list
├── AGENTS.md
├── opencode.json
└── README.md
```

The full map, including empty and reserved folders, is [[[pdlf:makepdlf-project-library/docs-local/docmap|Docmap]]](C:/pdlf/makepdlf-project-library/docs-local/docmap.md). It is the one canonical map and is not repeated here.

### What the workshop builds against

PDLF applies a shared library to every project it builds. That library is not part of the workshop, but the workshop's steps refer to it:

```
C:\dev\project-library-global\
├── specifications-global/
├── adr-global/
├── policy-global/
├── standard-operating-procedures-global/
├── checklists-global/
├── docs-standard-global/
└── templates-global/
```

### What the workshop produces for each project

When PDLF runs a project, Step 11 sets up that project's folders. For a new project it copies the template at `C:\dev\project-template\dev-(SLUG)\` and replaces the slug throughout. For an existing project it checks the folders already there and creates only those that are missing, never overwriting anything. Each project has two repositories: the documentation repository at `dev-{slug}\{slug}-project-library\`, and the Anvil-connected code repository at `dev-{slug}\{slug}\`. `anvil.yaml` is never written to.

---

## State of the build

PDLF is being built in the workshop and has not yet been deployed. Nothing has been placed in `C:\pdlf\` as a running system. Deployment is a separate, later phase; how it is done is set out in [[[pdlf:makepdlf-project-library/docs-local/deployment-procedure|Deployment Procedure]]](C:/pdlf/makepdlf-project-library/docs-local/deployment-procedure.md).

Steps 11, 12, 14, 15 and 16 have been rebuilt. Steps 17 to 46 are rebuilt one at a time as each phase is reached. Steps 42, 42A, 43 and 44 are flagged for rebuild, because they model a staging and production split that this platform does not have; see [[[pdlf:makepdlf-project-library/adr-local/adr-no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/makepdlf-project-library/adr-local/adr-no-staging-environment-five-app-isolation.md). Open work is tracked in the makePDLF to-do list in `wip/`.
