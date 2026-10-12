---
title: "AGENTS"
doc-id: "mb-a65c6e3a"
updated: "2026-10-12"
---
# AGENTS.md — PDLF

## What this location is

`C:\pdlf` is the PDLF system: the framework that builds Anvil applications step by step, with gates, reviews, QA and verification. PDLF is a system, not a project, and has no code repository. All work on PDLF happens here.

The global `AGENTS.md` (`~/.config/opencode/AGENTS.md`) governs everything this file does not cover, including Git, grants, credentials, links and close-out.

## Structure

| Folder | What it holds |
|---|---|
| `app-factory/` | The build, one folder per phase (`phase-a-init` to `phase-f-ship-and-monitor`). Each holds the set of six for every step (for example `b11-build-plan.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md`, `b11-decision-tree.html` and `b11-module.md`), plus the older step files and build notes kept as source material; `pdlf-build-plan.md` sits at the top. See `app-factory/README.md`. |
| `pdlf-library/` | The shared machinery: ADRs, specifications, policies, templates, explainers and working documents. See `pdlf-library/README.md`. |
| `desktop/` | The developer's working documents. |
| `obsolete/` | Retired files. |

## Standing rules

1. All PDLF work happens in `C:\pdlf`. There is no other workshop or copy of PDLF.
2. A module file (for example `b11-module.md`) is written only by compiling its step's files, and only on the developer's instruction.
3. No project data is kept in `C:\pdlf`. Each step's outputs for a project go to that project library's step folder, `{slug}-project-library\pdlf-outputs\{step}\`.
