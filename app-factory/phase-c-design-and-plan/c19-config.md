---
title: "c19-config"
doc-id: "mb-5e1eb893"
updated: "2026-11-12"
---
# Step 19 — Tickets: Configuration

The fixed values of Step 19. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-c-design-and-plan/c19-reference|Step 19 Reference]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-reference.md). What the step is and why: [[[pdlf:app-factory/phase-c-design-and-plan/c19-explainer|Step 19 Explainer]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-explainer.md). What it must prove: [[[pdlf:app-factory/phase-c-design-and-plan/c19-test-spec|Step 19 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 19, Tickets |
| Phase | C, Design and Plan |
| Carried out by | OpenCode, with the skills below; David approves the ticket list |
| Runs for | App 1 and App 5 as a whole application; every feature |
| Previous step | 18 |
| Next step | 20 |
| Gate | None |
| BFT level | Full |
| Sentinel scrutiny | Medium |
| Conditional | No |

## Inputs

| Input | Where |
|---|---|
| Reviewed plan, with the data design | `{slug}-project-library\docs-local\design\{run}\design-doc.md` |
| Test plan | `{slug}-project-library\docs-local\design\{run}\test-plan.md` |
| Glossary and ADRs | `{slug}-project-library\docs-local\GLOSSARY.md`; `adr-local\` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| User flows, when they exist | `{slug}-project-library\docs-local\user-flows.md` |
| Packages | `{slug}-project-library\ui\README.md` |
| Ticket format and labels | `{slug}-project-library\docs\agents\issue-tracker.md`; `triage-labels.md` |
| Context pack | [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack\|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md) |

## Outputs

| Output | Where |
|---|---|
| Tickets | `pdlf-tickets\{run}\{ticket-slug}.md`, one per feature |
| Ticket list | `pdlf-outputs\c19\{slug}-c19-{run}-ticket-list.md`: every ticket in build order, with its forms |
| Flow diagrams | `pdlf-outputs\c19\{slug}-c19-{run}-flow-{name}.*`, written by `archify` |
| Test results | `pdlf-outputs\c19\{slug}-c19-{run}-checks.xml` |
| Step Receipt | `pdlf-outputs\c19\{slug}-c19-{run}-receipt.md` |
| Ledger | the Step 19 `steps` row; its BFT record; its `triage_findings` row |

All paths are inside `{slug}-project-library\`.

## Ticket contents

| Section | Holds |
|---|---|
| Feature | The feature of the plan the ticket builds |
| Forms | Each form, by module path `<package path>.<FormName>` |
| Server functions | Each server function, by name |
| Tables | Each table read or written, by its name in the authoritative schema |
| Acceptance tests | The test plan's IDs |
| Security criteria | From Step 15's threat model |
| Depends on | The tickets that must be built first |

## Build order

| Order | Tickets |
|---|---|
| 1 | `layouts` and `shared`, including every shared custom component |
| 2 | `auth` |
| 3 | Every other feature, in the order its dependencies allow |

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `to-tickets` | The tickets in dependency order |
| `secure-software-engineering` | Security acceptance criteria |
| `mb-archify-scope`, then `archify` | The user flows and the multi-form feature flows |
| `mb-sentinel-review` | Security review, Medium scrutiny |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `19` |
| `step_type` | `skill` |
| `skill_family` | `matt-skills` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after David approves the ticket list |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-tickets\{run}\` |
| `inputs_used` | Steps 16 and 17 |
