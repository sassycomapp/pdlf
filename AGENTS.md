---
title: "AGENTS"
doc-id: "mb-a65c6e3a"
updated: "2026-10-10"
---
# AGENTS.md — PDLF

## What this location is

`C:\pdlf` is the PDLF system: the framework that builds Anvil applications step by step, with gates, reviews, QA and verification. PDLF is a system, not a project, and has no code repository. All work on PDLF happens here.

The global `AGENTS.md` (`~/.config/opencode/AGENTS.md`) governs everything this file does not cover, including Git, grants, credentials, links and close-out.

## Structure

| Folder | What it holds |
|---|---|
| `app-factory/` | One module per pipeline step number; placeholders until each step is built. See `app-factory/README.md`. |
| `stepwise/` | The step design, `run-plan.md`, `step-mapping.md` and `workflow.md`. |
| `pdlf-library/` | The shared machinery: ADRs, specifications, policies, processes, templates, explainers. See `pdlf-library/README.md`. |
| `output/` | Temporary artifact copies for the project currently in the pipeline, by producing tool: `output-gstack/`, `output-opencode/`, `output-pocock/`. Not version-controlled. |
| `desktop/` | The developer's working documents. |
| `obsolete/` | Retired files. |

## Standing rules

1. All PDLF work happens in `C:\pdlf`. There is no other workshop or copy of PDLF.
2. `stepwise/` is read-only. Do not edit, move or delete anything in it until the developer states that step design has resumed. It holds the designed steps, which are protected while the rest of PDLF is restructured.
3. Do not touch the `app-factory/` placeholders. A module is written only when its step has been built, and only on the developer's instruction.
4. `output/` serves one project at a time, the one in PDLF's pipeline. Copy each artifact into that project's folders, verify the copy, then clear it from `output/`. See [[[pdlf:pdlf-library/adr-local/artifact-saving-convention|Artifact Saving Convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md).
