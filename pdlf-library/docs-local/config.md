---
title: "config"
doc-id: "mb-dea37a55"
updated: "2026-10-10"
---
# PDLF System Configuration

Non-secret reference for all PDLF system configuration. Secrets live in `.env` (git-ignored).

---

## PostgreSQL Ledger

| Setting | Value | Source |
|---|---|---|
| Host | `localhost` | `.env` |
| Port | `5433` | `.env` (`PGPORT`) |
| Database | `pdlf` | `.env` |
| Role | `pdlf_agent` | `.env` |
| Password | `PGPASSWORD` in `.env` | `.env` |
| Admin role | `postgres` | `.env` |
| Installation | `C:\Program Files\PostgreSQL\15\` (Windows) | On-disk |
| psql from WSL | `powershell.exe -Command '$env:PGPASSWORD="..."; & "C:\Program Files\PostgreSQL\15\bin\psql.exe" -h localhost -p 5433 -U pdlf_agent -d pdlf -c "..."'` | Verified 2026-07-09; port 5433 since 2026-10-05 |
| Tables | `projects`, `steps`, `gates`, `deviations`, `bft_records`, `isc`, `triage_findings` | Verified — all seven exist (schema detail: [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger\|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md); re-verified live 2026-09-05) |

## PDLF System Paths

| Setting | Path | Notes |
|---|---|---|
| PDLF system home | `/mnt/c/pdlf/` | Project-agnostic: skill, stepwise, registry, templates |
| System skill (active) | none — the deployed instance at `/mnt/c/pdlf/` was restructured; the `~/.config/opencode/skills/pdlf/` symlink no longer exists | Development consolidated in this repo (see Stepwise skills row). Verified 2026-09-18 |
| Slug → path resolution | GBrain search | The former `/mnt/c/pdlf/registry/projects.json` no longer exists — verified 2026-09-18 |
| Dev workspace | `/mnt/c/dev/dev-makepdlf/` | PDLF development project |
| Stepwise skills (source) | `/mnt/c/dev/dev-makepdlf/makepdlf-project-library/stepwise/` | 46 step skills + 5 shared references |
| Templates | `/mnt/c/dev/dev-makepdlf/makepdlf-project-library/templates-local/` | BFT cheatsheet, ISA template, receipt templates |
| Project template | `/mnt/c/dev/project-template/dev-(SLUG)/(slug)-project-library/` | Folder skeleton used at Step 11 init |
| Project library (global) | `/mnt/c/dev/project-library-global/` | Shared specs, ADRs, policies, SOPs, standards, templates — referenced directly, never copied

## OpenCode Configuration

| Setting | Value | Source |
|---|---|---|
| Config file | `/mnt/c/dev/dev-makepdlf/makepdlf-project-library/opencode.json` | Project-level |
| Default agent | `plan` | opencode.json |
| Permissions | edit=ask, webfetch=ask, bash=ask, external `C:\dev\**`=allow | opencode.json |

## GStack Configuration

| Setting | Value |
|---|---|
| Binary path | `/home/dev-p/.config/opencode/skills/gstack/bin/` |
| Project slug | `sassycomapp-dev-makepdlf` |
| GStack home | `~/.gstack/projects/sassycomapp-dev-makepdlf/` |

## GBrain Configuration

| Setting | Value |
|---|---|
| Source ID (this project) | `makepdlf-project-library` |
| Repo path | `/mnt/c/dev/dev-makepdlf/makepdlf-project-library` |
| Source ID (project-library-global) | `project-library-global` |
| Repo path | `/mnt/c/dev/project-library-global` |
| GitHub remote (project-library-global) | `https://github.com/sassycomapp/project-library-global` (public) |
| Brain type | PostgreSQL — WSL-native instance, `localhost:5432`, database `gbrain` (migrated from PGLite; verified 2026-09-05) |

`project-library-global` registration confirmed 2026-07-19 — real GitHub remote exists,
GBrain source registered. This is what makes
[[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md)'s discovery mechanism
actually usable, not just designed.

Every project PDLF builds also registers two further sources: `project-library-global`
(shared infrastructure, registered once, checked every Step 11 run — not per-project) and
`sassycomapp-{slug}-project-library` plus `{slug}-code` per project. All PDLF sources are
registered Isolated (`federated=false`); GBrain queries must explicitly nominate a source,
never unscoped. See [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md).

## WSL → Windows Bridge

PostgreSQL runs on Windows. OpenCode runs in WSL. Connection requires `powershell.exe`
to pass the `PGPASSWORD` environment variable into the Windows context.

Do NOT try `export PGPASSWORD=... && /mnt/c/.../psql.exe` — WSL's binfmt does not pass
Linux env vars to Windows executables. Use the PowerShell pattern:

```
powershell.exe -Command '$env:PGPASSWORD="..."; & "C:\Program Files\PostgreSQL\15\bin\psql.exe" -h localhost -p 5433 -U pdlf_agent -d pdlf -c "SQL HERE"'
```

| Role | Provider | Status |
|---|---|---|
| Embedding | OpenAI (text-embedding-3-large) | ✓ active |
| Chat / Expand | OpenAI (gpt-5.2) | ✓ active, will move to Anthropic |
| Reranker | ZeroEntropy | ✓ confirmed active |
---

*Config version 2.1. Last updated: 2026-09-18. Reflects v5 stepwise decomposition architecture.*
