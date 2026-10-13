---
title: "b11-config"
doc-id: "mb-ea7e8074"
updated: "2026-10-13"
---
# Step 11 — Init: Configuration

The fixed values of Step 11. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-b-discover-and-define/b11-reference|Step 11 Reference]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-reference.md). What the step is and why: [[[pdlf:app-factory/phase-b-discover-and-define/b11-explainer|Step 11 Explainer]]](C:/pdlf/app-factory/phase-b-discover-and-define/b11-explainer.md).

## Identity

| Item | Value |
|---|---|
| Step | 11, Init |
| Phase | B, Discover and Define |
| Carried out by | OpenCode |
| Entry points that run it | 02 (route A), 03 (route B), 07 and 08 (route C) |
| Next step | 12, except entry 07 (App 3), which ends Phase B here |
| Gate | None |
| BFT level | Full |

## Inputs

| Input | Where |
|---|---|
| Entry record | From the orchestrator (build plan section 4) |
| Project template | `C:\dev\project-template\dev-(SLUG)\` |
| Blank pre-project files | `C:\pdlf\pdlf-library\templates-local\pre-project\` |
| Anvil's `AGENTS.md` template and skills | `C:\mybizz\anvil-agent-references\` |
| The ledger | Database `pdlf`, port 5433, through the PowerShell bridge ([[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)) |

## Outputs

| Output | Where |
|---|---|
| Business folder | `C:\dev\dev-{slug}\` |
| App folders | `C:\dev\dev-{slug}\{slug}-app1`, `-app2`, `-app3`, `-app5` |
| Project library | `C:\dev\dev-{slug}\{slug}-project-library\`, private GitHub repository `sassycomapp/{slug}-project-library` |
| GBrain source | `{slug}-project-library`, federated |
| Ledger | the `projects` row; the Step 11 `steps` row; its BFT record; its `triage_findings` row |
| Step Receipt | `{slug}-project-library\pdlf-outputs\b11\{slug}-b11-app-receipt.md` |

## Skills and tools

| Skill or tool | Used for |
|---|---|
| `wizard` | David's exact instructions for creating an app in Anvil |
| `setup-matt-pocock-skills` | The Matt Pocock configuration in `docs\agents\` |
| `mb-sentinel-review` | Security review, High scrutiny |
| [[[pdlf:pdlf-library/operating-procedures/sop-health-check\|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) | The closing self-audit |

## Fixed answers for the Matt Pocock setup

| Question | Answer |
|---|---|
| Issue tracker | Local markdown files in `pdlf-tickets\` |
| Triage labels | `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix` |
| Domain documents | Single context: `docs-local\CONTEXT.md` and `adr-local\` |
| `CLAUDE.md` | Never created |

## Foundation checks

| Check | Pass when |
|---|---|
| Ledger | Port 5433 answers; seven tables exist |
| GBrain | It answers; sources `default` and `pdlf` are registered |
| Anvil's skills | `C:\mybizz\anvil-agent-references` exists |
| Skills | `office-hours`, `plan-ceo-review`, `plan-eng-review`, `grilling`, `grill-with-docs`, `domain-modeling`, `setup-matt-pocock-skills`, `data-models`, `secure-software-engineering`, `mb-sentinel-review` and `wizard` are installed |

## App `.gitignore` baseline

`.env`, `.env.*`, credentials, `__pycache__/`, `*.pyc`, test output, `.venv/`, `.opencode/`, `.gstack/`.

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `11` |
| `step_type` | `skill` |
| `skill_family` | `opencode` |
| `run` | `app` |
| `app_number` | 1 for routes A and B; 3 or 5 for route C |
