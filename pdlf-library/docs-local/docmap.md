---
title: "docmap"
doc-id: "mb-73c01a09"
updated: "2026-10-10"
---
# PDLF System Document Map

**Purpose:** Single canonical navigation map for the whole PDLF system — where every file
lives, what it is for, and how to find it. This replaces two prior competing versions
(one at `docs-local\docmap.md` itself, one at the project root). The root-level copy
should be deleted once this version is confirmed in place. The version in `obsolete\` is
older still and requires no further action.

**Date:** 2026-07-18

---

## Dev Workspace — `C:\dev\dev-makepdlf\`

Where PDLF itself is developed. Project-agnostic — this is the factory, not the product.

```
C:\dev\dev-makepdlf\
├── stepwise/
│   ├── step-01-orchestrator.md
│   ├── step-04-undefined.md                  ← Reserved
│   ├── step-05-undefined.md                  ← Reserved
│   ├── step-06-undefined.md                  ← Reserved
│   ├── step-07-undefined.md                  ← Reserved
│   ├── step-08-undefined.md                  ← Reserved
│   ├── step-09-undefined.md                  ← Reserved
│   ├── step-10-undefined.md                  ← Reserved
│   ├── step-11-init.md
│   ├── step-11-build-notes.md
│   ├── step-11-decision-tree-v2.html
│   ├── step-11-project-inventory-build-notes.md
│   ├── step-12-office-hours.md
│   ├── step-12-build-notes.md
│   ├── step-12-decision-tree.html
│   ├── step-14-plan-ceo-review.md
│   ├── step-14-build-notes.md
│   ├── step-14-decision-tree.html
│   ├── step-15-plan-eng-review.md
│   ├── step-15-build-notes.md
│   ├── step-15-decision-tree.html
│   ├── skill-source-reference/               ← New: external skill source kept as
│   │   │                                         verification evidence, not PDLF's own
│   │   ├── plan-eng-review-manifest.json
│   │   └── plan-eng-review-review-sections.md
│   ├── step-16-domain-modeling.md               ← GATE domain-locked
│   ├── step-17-create-anvil-data-tables.md
│   ├── step-18-pull-to-local.md
│   ├── step-19-to-tickets.md
│   ├── step-20-design-consultation.md
│   ├── step-21-concept-sanity-audit.md          ← GATE concept-locked
│   ├── step-22-wireframe-phase-1.md
│   ├── step-23-plan-design-review.md
│   ├── step-24-plan-devex-review.md
│   ├── step-26-wireframe-phase-2.md             ← GATE wireframes-approved
│   ├── step-27-screen-production.md
│   ├── step-28-screen-to-png.md
│   ├── step-29-build-ui-forms.md
│   ├── step-30-pull-to-local.md
│   ├── step-31-scaffold-planning.md
│   ├── step-32-physical-scaffold-build.md
│   ├── step-33-pull-to-local.md
│   ├── step-34-architectural-sanity-audit.md    ← GATE architecture-verified
│   ├── step-35-build-loop.md
│   ├── step-35A-testing.md
│   ├── step-36-design-review.md
│   ├── step-37-review.md
│   ├── step-38-qa.md
│   ├── step-38A-dependency-scan-confirm.md
│   ├── step-39-triage.md                        ← GATE build-verified
│   ├── step-40-improve-codebase-architecture.md
│   ├── step-40B-remediation.md
│   ├── step-41-ship.md
│   ├── step-42-publish-to-staging.md            ← Needs rebuild — ToDo item 2
│   ├── step-42A-staging-integration-e2e.md      ← Needs rebuild — ToDo item 2
│   ├── step-43-staging-smoke-test.md            ← Needs rebuild — ToDo item 2
│   ├── step-44-promote-to-production.md         ← GATE production-released, needs rebuild
│   ├── step-45-canary-production.md
│   ├── step-46-LEARN-junction.md                ← GATE released
│   ├── INDEX.md                                 ← Router: step number → file path
│   ├── run-plan.md
│   ├── step-mapping.md                          ← Step number → file → handler → gate lookup
│   ├── step-16-build-notes.md
│   ├── step-16-decision-tree.html
├── specifications-local/                     ← Binding specifications
│   ├── spec-nomenclature.md                  ← Terminology and naming standard, actively maintained
│   ├── spec-bft.md                           ← BFT questions, levels, gate rule
│   ├── spec-execution-discipline.md          ← 13-point execution sequence
│   ├── spec-gate-procedure.md                ← Gate ceremony, maintenance, approval
│   ├── spec-postgres-ledger.md               ← Postgres ledger schema, role, connection
│   └── spec-skill-design.md                  ← Design rationale & tradeoffs
├── policy-local/                             ← Binding PDLF policies — top-level folder,
│   │                                            not nested under docs-local
│   ├── pol-INDEX.md
│   ├── pol-bft-discipline.md                 ← Corrected 2026-07-18: 27 Full / 7 Light / 6 None, 40 steps
│   ├── pol-sequential-enforcement-and-deviation.md
│   ├── pol-anvil-platform.md
│   ├── pol-testing-and-quality.md
│   ├── pol-skill-invocation.md
│   ├── pol-memory-and-knowledge.md
│   ├── pol-stepwise.md
│   └── step-conditional-state-policy.md
├── adr-local/                                ← PDLF internal ADRs
│   ├── postgres-ledger-replaces-flat-files.md
│   ├── stepwise-decomposition-model.md
│   ├── renumbering-11-to-46.md
│   ├── skill-use-principle.md
│   ├── two-gate-extension.md
│   ├── project-library-global-registration.md
│   ├── adr-no-staging-environment-five-app-isolation.md   ← Added 2026-07-18
│   └── adr-global-content-discovery-and-application-discipline.md
├── templates-local/                          ← Runtime templates
│   ├── bft-checkpoint-cheatsheet-v2.md       ← Corrected 2026-07-18
│   ├── isa-template-v2.md
│   ├── step-receipt-template.md
│   ├── devlog-index-template.md
│   └── judgement-trail-template.md
├── docs-local/                                ← Top-level, not the parent of policy-local
│   ├── system-description.md                 ← User reference
│   ├── config.md
│   ├── deployment-procedure.md                ← Corrected 2026-07-18: filename fix, retired-file cleanup
│   ├── docmap.md                              ← This file
│   ├── bft-system-derived.md
│   ├── matt-pocock-skills-local-reference.md
│   └── matt-pocock-skills-pdlf-compliance.md
├── pre-project/                               ← Pre-project thinking templates
│   ├── 01-project-brief.md
│   ├── 02-scoping-ideas.md
│   └── 03-constraints-and-notes.md
├── Standard-operating-procedures-local/       ← Top-level, currently empty or near-empty
├── agents/                                    ← Matt Pocock skills config for dev-makepdlf itself
│   ├── domain.md
│   ├── issue-tracker.md
│   ├── triage-labels.md
│   └── instructions.md
├── checklists-local/                          ← chk-pdlf-self-test.md (added 2026-07-18)
├── docs-standard-local/                       ← Empty, populated as needed
├── output-gstack/                             ← Empty, populated at runtime
├── output-opencode/                           ← Empty, populated at runtime
├── output-matt-skills/                        ← Empty, populated at runtime
├── workspace/                                 ← Agent workspace scratch
├── wip/                                       ← Active work in progress (dev-makepdlf\wip\)
│   ├── Active-non-PDLF-ToDo-List.md
│   ├── dev-makepdlf-todo.md                   ← Active PDLF-relevant to-do list, actively maintained
│   ├── workflow.md                            ← Execution order decision tree (registered: makepdlf-0106)
│   └── Active PDF To Do List has been save.txt
├── pdlf/
│   ├── devlog-index.md                        ← Audit trail (AGENTS.md rule 13)
│   └── judgement-trail.md                     ← Audit trail (AGENTS.md rule 13)
├── obsolete/                                  ← Superseded files — holds retired content
│   │                                             (including the prior docmap.md versions and the v1
│   │                                             BFT cheatsheet) and other retired files
│   └── ...
├── .scratch/
├── .out-of-scope/
├── AGENTS.md                                  ← Project-level agent rules
├── INDEX.md                                   ← Workspace index
├── instructions.md
├── opencode.json
├── .gbrain-source                             ← GBrain source binding
├── .env
├── .gitignore
├── output-staging/                            ← Producer-output staging area
├── register-local/                            ← Append-only document register
├── pdlf-temp/                                 ← Transient working state (scope scaffold exception)
└── README.md
```

---

## Project Library Global — `C:\dev\project-library-global\`

Shared resources that apply across all Anvil.works projects. Never cleared between
projects. Never copied into a project — always referenced in place.

```
C:\dev\project-library-global\
├── specifications-global/                    ← Binding specifications
│   ├── spec-anvil-platform-standards.md
│   ├── spec-m3-design-standards.md
│   ├── spec-testing-methodology-standards.md
│   ├── spec-screen-and-wireframe-production-standards.md
│   ├── spec-five-app-architecture-model.md   ← Governs the ADR on staging/production, added 2026-07-18
│   ├── spec-deployment.md
│   ├── spec-integration.md
│   ├── spec-security.md
│   ├── spec-security-architecture.md
│   ├── spec-nomenclature.md
│   └── ...
├── adr-global/                                ← Global architecture decisions
│   ├── adr-client-instance-architecture.md
│   ├── adr-client-instance-readme-five-app-system.md   ← Source for the Five-App Structure
│   └── ...
├── policy-global/                             ← Binding policies
│   ├── pol-anvil-first-development.md
│   ├── pol-documentation-and-decisions.md
│   ├── pol-security-and-data-governance.md
│   └── pol-testing-and-quality.md
├── standard-operating-procedures-global/      ← Global SOPs + topic subfolders
│   ├── Agent readiness/
│   ├── uplink-kickstart/
│   ├── sop-deployment-procedures.md
│   ├── sop-offboarding.md
│   └── sop-vault-totp-recovery.md
├── anvil-docs/
├── docs-standard-global/
├── guides-global/
├── register-global/
├── rules-cupcake-global/
├── security-global/
├── sessions/
├── quarantine/                                ← Quarantine lane — never referenced as live corpus
├── templates-global/                          ← tmp- prefixed
├── README.md
└── project-library-global-config.yaml
```

---

## PDLF System Home — `C:\pdlf\`

The home of the PDLF system, scaffolded live 2026-09-11. **This is the deployment target; the machinery is built in
the makePDLF environment (`C:\dev\dev-makepdlf\`) and migrates here.**

```
C:\pdlf\
├── pdlf-library/                             ← Canonical technical documentation (ADRs, specs, policies, explainers, register)
├── app-factory/                              ← Machinery — one module per pipeline step (populated by makePDLF)
├── output/                                   ← Producer-routed artifact safety net (transient)
├── AGENTS.md                                 ← Standing rules for this location
├── pdlf-config.yaml                          ← Config file
└── README.md
```

**Housekeeping note:** `C:\pdlf\` was scaffolded live 2026-09-11 (pdlf-library, app-factory
machinery, output area, GitHub repo re-established). Development continues in the workshop
(`C:\dev\dev-makepdlf\`); deployment to `C:\pdlf\` is a distinct, later phase.

---

## GStack Project Home

```
~/.gstack/projects/<slug>/
```

GStack skills save their outputs here per project — e.g. `ceo-plans/`,
`*-design-*.md`, `*-eng-review-test-plan-*.md`. Confirmed against real skill source during
Steps 14–15's rebuild, not assumed.

---

## Postgres Ledger — Database `pdlf`

Single source of truth for all PDLF run-time progress. Seven tables, referentially
enforced (confirmed against [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md), corrected from an earlier "six
tables" claim — `triage_findings` was missing from that count).

```
Database: pdlf
Role: pdlf_agent
Host: localhost:5433 (Windows PostgreSQL 15, reached from WSL via powershell.exe bridge; WSL's own PostgreSQL 16 keeps port 5432)

Tables:
├── projects          ← slug, name, mode, paths, GBrain sources, is_active
├── steps              ← step_number, type, status, synthesized, artifact_path, next_action
├── gates               ← gate_name, passed, approved_at
├── deviations           ← description, options_presented, decision
├── bft_records            ← level, bones..health
├── isc                     ← isc_number, description, verify_method, status, evidence
└── triage_findings          ← id, step_id, finding_id, source_step, triage_label,
                                 resolution_note, resolved_by, resolved_at, created_at
```

---

## Per-Project Structure — When PDLF Runs a Project

Created at Step 11 for each project. Two repos: docs (project-library) and code.

```
dev-{slug}\{slug}-project-library\           ← Docs repo
├── AGENTS.md
├── CONTEXT.md                               ← Domain glossary, from Step 16
├── DESIGN.md                                ← From Step 20 (/design-consultation)
├── pre-project\                             ← Developer's first-thoughts templates
├── docs-local\
│   ├── design-doc.md
│   └── design-doc-first-concept.md
├── docs-standard-local\
├── specifications-local\
├── policy-local\
├── adr-local\                               ← Project-specific ADRs, e.g. from Step 16
├── pdlf\                                    ← PDLF process artifacts, no "outputs" subfolder
│   ├── step-{N}-receipt.md
│   ├── devlog-index.md
│   └── judgement-trail.md
├── output-gstack\                           ← Stable copies of GStack-native artifacts
├── output-opencode\
├── output-matt-skills\
├── wireframes\
├── screens\
├── workspace\
├── wip\
├── checklists-local\
└── templates-local\

dev-{slug}\{slug}\                           ← Anvil-connected code repo
├── anvil.yaml                               ← NEVER WRITE TO THIS
├── client_code\
├── server_code\
└── theme\
```

---

## Project Template — `C:\dev\project-template\`

Source template copied at Step 11 (new-project entry) to create a new project's folder
structure. Contains a placeholder `Instructions.md` in each folder (~20 files),
explaining that folder's purpose to a human. These files are not part of PDLF's
operation — no step reads, writes, or depends on them. They may be built out, left as
placeholders, or deleted at any time with no functional impact. Resolved 2026-07-18;
not tracked as an open action item.

---

## Anomalies Found — Not Yet Resolved

Found while updating this file's `stepwise/` listing against the developer's confirmed
current folder contents (2026-07-18):

All previously flagged anomalies are resolved as of this version. [[[pdlf:stepwise/step-15-build-notes|Step 15 Build Notes]]](C:/pdlf/stepwise/step-15-build-notes.md)
replaces the old-named [[[pdlf:stepwise/step-15-build-notes|Step 15 Build Notes]]](C:/pdlf/stepwise/step-15-build-notes.md). `plan-eng-review-manifest.json`
and [[[pdlf:stepwise/skill-source-reference/plan-eng-review-review-sections|Plan: Eng Review Sections]]](C:/pdlf/stepwise/skill-source-reference/plan-eng-review-review-sections.md) relocate to the new `skill-source-reference/`
folder below. `todo-stepwise-development).md` and both `PDLF-*-Mapping.md` files have
moved to `obsolete/`.

## Housekeeping Status (as of this version)

Reflects the developer's Active-PDLF ToDo list as of 2026-07-18. Full detail there, not
duplicated here. Retired since the prior docmap versions: `bft-checkpoint-cheatsheet.md` v1
(no longer present anywhere — verified absent system-wide 2026-09-23), `step-13-to-spec.md`
(confirmed non-existent anywhere). Corrected since the
prior docmap versions: [[[pdlf:pdlf-library/policy-local/pol-bft-discipline|Policy: BFT Discipline]]](C:/pdlf/pdlf-library/policy-local/pol-bft-discipline.md),
[[[pdlf:pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2|BFT Checkpoint Cheatsheet v2]]](C:/pdlf/pdlf-library/templates-local/bft-checkpoint-cheatsheet-v2.md), [[[pdlf:pdlf-library/docs-local/deployment-procedure|Deployment Procedure]]](C:/pdlf/pdlf-library/docs-local/deployment-procedure.md), [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md)
(a Stepwise File Naming section and two tables migrated from the retired
architecture documentation). Steps 11, 14, 15, 16 rebuilt and verified against real skill
source. Two testing checklists added 2026-07-18: [[[pdlf:pdlf-library/templates-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/pdlf-library/templates-local/chk-pdlf-self-test.md) (local, tests
PDLF's own orchestration) and a global Anvil-app test checklist — both referenced from
[[[pdlf:pdlf-library/policy-local/pol-testing-and-quality|Policy: Testing and Quality]]](C:/pdlf/pdlf-library/policy-local/pol-testing-and-quality.md). Their integration into
Steps 35A/36–39 is deferred to Phase D. Steps 17–46 exist as files but have not been
individually verified against
real skill source this session — verification status is per-step, not assumed uniform.
verified: 2026-09-23
