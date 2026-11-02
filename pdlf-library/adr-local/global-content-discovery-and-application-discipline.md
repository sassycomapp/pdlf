---
title: "adr-global-content-discovery-and-application-discipline"
doc-id: "mb-c0174316"
updated: "2026-11-02"
---
# ADR — Canonical Sources: Discovery and Application Discipline

**Status:** Accepted

---

## Context

Every application PDLF builds is bound by two bodies of documents:

- `project-library-global`: what every Mybizz application must be.
- The project's own documents (`{slug}-project-context` while it exists, and `{slug}-project-library`): what this one application is and does, as David has stated it.

PDLF's steps and skills are how a building agent meets these documents. Two failures follow when nothing forces the agent to them:

1. **Discovery left to chance.** A step that reads only what a GBrain search happens to return misses documents the search did not rank. The agent never knows what it did not read.
2. **Canonical documents treated as optional.** An agent that regards the project's documents as prior material to check, or squeezes them into a summary, replaces David's stated specification with its own reading of it. It looks like compliance (a search ran, a document was cited) while the result never conformed to what the documents say.

## Decision

**Both bodies of documents are canonical.** They are the authority every step builds to. The binding rules are in [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md), Canonical sources.

**Discovery is the canonical folders, read in full, plus GBrain.**

1. Each step's configuration names its canonical folders: the `project-library-global` folders and the project's folders its subject touches. The configuration names folders, never a list of files, so nothing needs to be kept in step when a document is added.
2. The agent lists those folders itself and reads in full each file that bears on the step.
3. GBrain is searched at every task across the federated sources. Its results are advisory pointers: each file it points to is read in full, and anything it finds outside the canonical folders is read as well.

**Application follows read → apply, never read → paraphrase.**

1. Every statement in a canonical document is a requirement, applied as written.
2. A canonical document is never summarised in place of being carried. A step's output names the document and section it applies, and the document stays the authority.
3. A conflict between canonical documents, or between a canonical document and anything else, is put to David with a recommended resolution. Only David changes what a canonical document says, and he changes it in that document.

**Enforcement, not just instruction.** Every Step Receipt lists each canonical file read and what the step applied from it, and every skill invocation is given the full text of those files. A claim of compliance is trusted only once it can be checked.

## Consequences

- [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), substep 1, carries the sequence for every step.
- Every step's configuration has a Canonical folders table, written when the step is built or rebuilt.
- Step 12 carries the project's canonical documents into the design doc by name, in its Specification and Canonical Sources sections, so every later step builds to the same documents.
- GBrain stays in every task, and a stale GBrain result can never override a file.
