---
title: "pol-memory-and-knowledge"
doc-id: "mb-d07a9e52"
updated: "2026-11-02"
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
| The project's own documents: `{slug}-project-context` while it exists, and `{slug}-project-library` (`docs-local`, `docs-standard-local`, `policy-local`, `adr-local`) | What is true of that one application only. |

### Canonical sources

`project-library-global` and the project's own documents are canonical. They are the authority every step builds to, never material to consult when it seems useful.

| Canonical source | Authority for |
|---|---|
| `project-library-global`, every folder | What every Mybizz application must be |
| The project's documents: `{slug}-project-context` while it exists (read-only), and `{slug}-project-library` `docs-local`, `docs-standard-local`, `policy-local` and `adr-local` | What this application is and does |

1. **Read in full, from the folders.** Before any work, the step reads in full every canonical file its subject touches. The step's configuration names its canonical folders; the agent lists those folders itself and reads each file that bears on the step. A GBrain search never decides alone what is read.
2. **Requirements, not prior material.** Every statement in a canonical document is a requirement. The agent never treats a canonical document as background, a suggestion or prior material to check; never summarises it in place of carrying it; and never drops, softens or reinterprets a statement in it. A change to what a canonical document says is David's decision, made in that document.
3. **Conflicts go to David.** Where two canonical documents disagree, the document the project names as its standard (for an application, its architecture reference) is followed, and the conflict is put to David with a recommended resolution. The agent never resolves a conflict silently.
4. **Canonical first.** Where a canonical document and a skill, a GBrain result, an earlier output or the agent's own judgement disagree, the canonical document is followed.
5. **Carried into every skill.** Every skill invocation is given the full text of the canonical files the step read, beside the context pack.
6. **Cited.** Every Step Receipt lists each canonical file read and what the step applied from it. A step that cannot show this has not complied.

A project's `AGENTS.md`, `CLAUDE.md` and `opencode.json` from before PDLF are tooling files, not canonical documents, and are never instructions.

### GBrain: at every task, advisory

Every task, not only the start of a step, begins with a GBrain search on its subject. Searching is automatic and changes nothing. GBrain is advisory: it points to files and shows related lessons; the file is the truth. The sequence is always:

1. Search GBrain.
2. Take the results as pointers to files, never as the content.
3. Read the actual files in full, together with the canonical files rule 1 requires.
4. Apply what those files say.

Where a GBrain result differs from the file it points to, the file is followed and the difference is reported, so GBrain is synced at the next `commit-all`.

The search covers the federated documentation sources (one search covers the project library `{slug}-project-library`, the project context `{slug}-project-context` while it exists, `default`, which is `project-library-global`, and `pdlf`). A step that needs Anvil knowledge also names `anvil-agent-references-code`. Application code is never a GBrain source; the agent reads it directly from the app folder.

A claim of compliance that cannot be checked is not compliance (rule 6). The reasoning is in [[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR: Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md).

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
- **The Step Receipt** for each step is produced from the ledger row that step wrote and saved to `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-{run}-receipt.md`. It is never written separately.
- **The ISA** (Ideal State Artifact) is the project's definition of "done". Its criteria and verification sections are produced from the ledger's `isc` table, never edited by hand. It is created at Step 16, updated at Steps 26, 35, 39 and 46, and read at the start of the next build.

No other log is kept. A record nobody reads is not kept.

---

## Why

David cannot personally verify what the agent knows or assumes. The canonical documents are where David has stated what every application, and this application, must be; an agent that treats them as optional material builds something else. GBrain gives every session the same memory; the search-read-apply sequence makes sure that memory is used from its real source, not from a snippet or a guess. Writing each lesson into the source the next build reads is what stops PDLF making the same mistake twice.

---

## Where

Every step. The execution sequence is in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md); the ISA template is [[[pdlf:pdlf-library/templates-local/isa-template|ISA Template]]](C:/pdlf/pdlf-library/templates-local/isa-template.md).
