---
title: "pol-memory-and-knowledge"
doc-id: "mb-d07a9e52"
updated: "2026-10-13"
---
# PDLF Policy — Memory and Knowledge

**Binding.** The agent must comply at every step.

---

## What

### Three homes for knowledge

Each fact lives in exactly one place:

| Home | Holds |
|---|---|
| `C:\pdlf\pdlf-library` | How PDLF works. |
| `project-library-global` | What a good application is: standards, specifications and decisions that apply to every application, Anvil knowledge included. Project-agnostic. |
| The project's own `project-library`, `docs-local` | What is true of that one application only. |

### Searching: search, read, apply

Every step starts with a GBrain search on its subject. Searching is automatic and changes nothing. The sequence is always:

1. Search GBrain.
2. Take the results as pointers to files, never as the content.
3. Read the actual files in full.
4. Apply what those files say.

The search covers the federated documentation sources (one search covers the project library `{slug}-project-library`, `default`, which is `project-library-global`, and `pdlf`). A step that needs Anvil knowledge also names `anvil-agent-references-code`. Application code is never a GBrain source; the agent reads it directly from the app folder.

A step that applies a `project-library-global` standard names the file it read and applied, in its Step Receipt or thinking checkpoint. A claim of compliance that cannot be checked is not compliance. The reasoning is in [[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR: Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md).

### Writing to memory

New knowledge enters GBrain only through close-out (`/mb-close-out`) and `mb-submit-memory`, with David's approval. No step writes to GBrain directly, and no step syncs GBrain itself; David's `commit-all` updates GBrain.

### Learning

Each lesson is written once, into the source the next build will read:

- a lesson about Anvil, or about what a good application is, goes into `project-library-global`;
- a lesson about how PDLF works goes into the module, rule or specification concerned in `pdlf-library`;
- a lesson about one application goes into that application's `docs-local`.

A lesson that belongs to one application never goes into `project-library-global`.

### Self-healing

When a step fails, or David corrects something, the agent proposes the fix to the source that caused the problem, before the step stops. It names the lesson and its home (`project-library-global`, the PDLF step, rule or specification concerned, or the application's `docs-local`). David approves or rejects it. An approved fix is made in that source, and the fact is recorded in GBrain through `mb-submit-memory` at close-out.

### Other projects

1. A GBrain result from another project is labelled with its project.
2. Lessons from other projects are welcome as advice.
3. Decisions from other projects are not transferred; the agent asks David before applying one.

### Records each build keeps

- **The ledger** (database `pdlf`) records every step, gate, deviation and thinking checkpoint. It is how the orchestrator enforces order and how a build resumes.
- **The Step Receipt** for each step is produced from the ledger row that step wrote and saved to `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-receipt.md`. It is never written separately.
- **The ISA** (Ideal State Artifact) is the project's definition of "done". Its criteria and verification sections are produced from the ledger's `isc` table, never edited by hand. It is created at Step 16, updated at Steps 26, 35, 39 and 46, and read at the start of the next build.

No other log is kept. A record nobody reads is not kept.

---

## Why

David cannot personally verify what the agent knows or assumes. GBrain gives every session the same memory; the search-read-apply sequence makes sure that memory is used from its real source, not from a snippet or a guess. Writing each lesson into the source the next build reads is what stops PDLF making the same mistake twice.

---

## Where

Every step. The execution sequence is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md); the ISA template is [[[pdlf:pdlf-library/templates-local/isa-template-v2|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md).
