---
title: "README"
doc-id: "README"
---
# pdlf — The PDLF Environment

The home of the PDLF system — the Project Development Lifecycle Framework —
scaffolded 2026-09-11 per developer instruction.

## What lives here

| Path | What it is |
|---|---|
| `pdlf-library\` | Canonical technical documentation: ADRs, specifications, explainers, and the register. See `pdlf-library\README.md`. |
| `app-factory\` | The system's machinery — 46 modules, one per pipeline step (placeholders today; populated by makePDLF, migrated here once when all steps are complete). See `app-factory\README.md`. |
| `output\` | The producer-routed artifact safety net (transient — copied into the shipping project's folders, then cleared). Not version-controlled. |

## Connections (live as of 2026-09-11)

- **GitHub:** `sassycomapp/pdlf` (private), branch `main` — initial scaffold pushed 2026-09-11.
- **GBrain:** source `pdlf` (federated) — registered and synced 2026-09-11; 59 pages, 54 chunks embedded.
- **Config register:** `pdlf-config.yaml` is registered in
  `C:\mybizz\mybizz-config-docs\projects-config-register.md`.

## What deliberately waits

Nothing executes in this location yet. The machinery arrives with the
app-factory migration when makePDLF completes all 46 steps; the OpenCode
configuration and agent role files are built at that deployment, not before.
Until then, the system is developed in the makePDLF environment
(`C:\dev\dev-makepdlf\makepdlf-project-library`).

See `AGENTS.md` for the standing rules for this location, and
`pdlf-config.yaml` for the exact current state.
