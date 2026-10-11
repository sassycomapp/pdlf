---
title: "AGENTS"
doc-id: "mb-a65c6e3a"
updated: "2026-10-11"
---
# AGENTS.md — PDLF

## What this location is

`C:\pdlf` is the PDLF system: the framework that builds Anvil applications step by step, with gates, reviews, QA and verification. PDLF is a system, not a project, and has no code repository. All work on PDLF happens here.

The global `AGENTS.md` (`~/.config/opencode/AGENTS.md`) governs everything this file does not cover, including Git, grants, credentials, links and close-out.

## Structure

| Folder | What it holds |
|---|---|
| `app-factory/` | The build, one folder per phase (`phase-a-init` to `phase-f-ship-and-monitor`). Each holds its numbered step files (`11-init.md`, `11-build-notes.md` and so on) and one module file per step (`11-module.md`), plus `pdlf-build-plan.md` at the top. See `app-factory/README.md`. |
| `pdlf-library/` | The shared machinery: ADRs, specifications, policies, processes, templates, explainers. See `pdlf-library/README.md`. |
| `output/` | Temporary artifact copies for the project currently in the pipeline, by producing tool: `output-gstack/`, `output-opencode/`, `output-pocock/`. Not version-controlled. |
| `desktop/` | The developer's working documents. |
| `obsolete/` | Retired files. |

## Standing rules

1. All PDLF work happens in `C:\pdlf`. There is no other workshop or copy of PDLF.
2. A module file (`NN-module.md`) is written only by compiling its step's files, and only on the developer's instruction.
3. `output/` serves one project at a time, the one in PDLF's pipeline. Copy each artifact into that project's folders, verify the copy, then clear it from `output/`. See [[[pdlf:pdlf-library/adr-local/artifact-saving-convention|Artifact Saving Convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md).
