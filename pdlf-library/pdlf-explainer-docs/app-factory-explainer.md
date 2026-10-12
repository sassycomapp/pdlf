---
title: "app-factory-explainer"
doc-id: "mb-bcfa10bb"
updated: "2026-10-12"
---
# PDLF — The App Factory

## What it is

The app factory (`C:\pdlf\app-factory\`) holds PDLF's build, one folder per phase: `phase-a-init`, `phase-b-discover-and-define`, `phase-c-design-and-plan`, `phase-d-scaffold-and-assemble`, `phase-e-build-and-verify` and `phase-f-ship-and-monitor`. Each phase folder holds the set of six for each of its steps: its build plan, config, reference, explainer, decision tree and module (`b16-build-plan.md` to `b16-module.md`). A module is one finished step, compiled into a single unit. When PDLF builds an application, the modules are what run.

Each name is the phase letter followed by the step number, so `b16-module.md` is always Step 16. Module `a01` is the orchestrator, which runs the others. Modules 02 to 10 are the entry points for work on existing applications (new features, updates, returning to another app of a five-app set). Modules 11 to 46 are the pipeline that builds an application. Numbers 13 and 25 are not used; each keeps a placeholder file. Inserted steps carry a lowercase letter after the number, only to keep the files in order: 35a, 38a, 40b and 42a.

## How it works

The orchestrator first establishes, by asking David, what kind of work this is. That decides the entry point, and so which modules run. It then runs those modules in order. Each module carries out its step through the same pattern (search, read, do, verify, think, record, explain and stop, close out), described in [[[pdlf:pdlf-library/pdlf-explainer-docs/pdlf-explainer|PDLF Explainer]]](C:/pdlf/pdlf-library/pdlf-explainer-docs/pdlf-explainer.md).

Every module implements the shared rules in `pdlf-library`, above all [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md): pass prior outputs in full to the next skill, capture where the output was saved, confirm it exists, record it in the ledger, write the copy to `output/`, and stop with a deviation when something expected is missing. The decisions behind those rules are in [[[pdlf:pdlf-library/adr-local/artifact-saving-convention|ADR: Artifact Saving Convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md).

## Why it works this way

Keeping each step as its own module means a step can be built, tested and corrected on its own, without touching the others. Keeping the shared pattern in the orchestrator, rather than repeated in every module, means no module can skip it.

## What has to happen

A step is designed in its phase folder. When that design is finished and David instructs it, its config, reference, explainer and decision tree are compiled into its module beside them. Until then the module is empty (rule 2 of `C:\pdlf\AGENTS.md`). Modules are built one at a time, not in bulk.
