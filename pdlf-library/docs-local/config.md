---
title: "config"
doc-id: "mb-dea37a55"
updated: "2026-10-23"
---
# PDLF System Configuration

The non-secret configuration of PDLF. Secrets live in `C:\pdlf\.env`, which Git never tracks.

---

## PostgreSQL Ledger

Database `pdlf` on the Windows PostgreSQL 15 server, port 5433, role `pdlf_agent`, password in `.env`. Its connection method, the WSL bridge and its seven tables are set in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md).

## Paths

| Setting | Path | Notes |
|---|---|---|
| PDLF home | `/mnt/c/pdlf/` | The app factory and the PDLF library |
| App factory | `/mnt/c/pdlf/app-factory/` | One folder per phase; each step's set of seven |
| Templates | `/mnt/c/pdlf/pdlf-library/templates-local/` | Step Receipt, ISA, BFT checkpoint, self-test checklist, pre-project files |
| Project template | `/mnt/c/dev/project-template/dev-(SLUG)/` | The scaffold Step 11 copies for a new business |
| Global library | `/mnt/c/dev/project-library-global/` | Read directly, never copied |

## OpenCode

| Setting | Value |
|---|---|
| Project configuration | `C:\pdlf\opencode.json` is written when the orchestrator is designed; until then the global OpenCode configuration applies |

## GStack

| Setting | Value |
|---|---|
| Binary path | `/home/dev-p/.config/opencode/skills/gstack/bin/` |
| Project name | `sassycomapp-pdlf`, from the GitHub repository |
| GStack home | `~/.gstack/projects/sassycomapp-pdlf/` |

## GBrain

| Setting | Value |
|---|---|
| PDLF's source | `pdlf`, covering `/mnt/c/pdlf` |
| The global library's source | `default`, covering `/mnt/c/dev/project-library-global` |
| Each business's source | `{slug}-project-library`, covering its project library |
| Federation | Every documentation source is federated, so one search covers all of them |
| Application code | Never a GBrain source; agents read it directly, and Graphify answers questions about it |
| Database | GBrain's own PostgreSQL in WSL, `localhost:5432`, database `gbrain` |

The list of every repository and its GBrain source is [[[mybizz-os-docs:os-reference-docs/repo-organization|Repo Organization]]](C:/mybizz/mybizz-os-docs/os-reference-docs/repo-organization.md).
