---
title: "app-factory-explainer"
updated: "2026-10-11"
---
# PDLF — The App Factory

## What it is

The app factory (`C:\pdlf\app-factory\`) holds PDLF's build, one folder per phase: `phase-a-init`, `phase-b-discover-and-define`, `phase-c-design-and-plan`, `phase-d-scaffold-and-assemble`, `phase-e-build-and-verify` and `phase-f-ship-and-monitor`. Each phase folder holds its steps' files (`16-domain-modeling.md` and so on) and one module file per step (`16-module.md`). A module is one finished step, compiled into a single unit. When PDLF builds an application, the modules are what run.

The numbers follow the step numbers exactly, so module 16 is always Step 16. Module 01 is the orchestrator, which runs the others. Modules 02 to 10 are the entry points for work on existing applications (new features, updates, returning to another app of a five-app set). Modules 11 to 46 are the pipeline that builds an application. Numbers 13 and 25 are not used; their module files are kept. Inserted steps carry a lowercase letter: 35a, 38a, 40b and 42a.

## How it works

The orchestrator first establishes, by asking David, what kind of work this is. That decides the entry point, and so which modules run. It then runs those modules in order. Each module carries out its step through the same pattern (search, read, do, verify, think, record, explain and stop, close out), described in [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-explainer|PDLF Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-explainer.md).

Every module implements the shared rules in `pdlf-library`, above all [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md): pass prior outputs in full to the next skill, capture where the output was saved, confirm it exists, record it in the ledger, write the copy to `output/`, and stop with a deviation when something expected is missing. The decisions behind those rules are in [[[pdlf:pdlf-library/adr-local/artifact-saving-convention|ADR: Artifact Saving Convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md).

## Why it works this way

Keeping each step as its own module means a step can be built, tested and corrected on its own, without touching the others. Keeping the shared pattern in the orchestrator, rather than repeated in every module, means no module can skip it.

## What has to happen

A step is designed in its phase folder. When that design is finished and David instructs it, the step's files are compiled into its module file beside them. Until then the module file stays a placeholder (rule 2 of `C:\pdlf\AGENTS.md`). Modules are built one at a time, not in bulk.
