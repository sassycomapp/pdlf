---
title: "adr-global-content-discovery-and-application-discipline"
doc-id: "mb-c0174316"
updated: "2026-10-23"
---
# ADR — Global Content Discovery and Application Discipline

**Status:** Accepted

---

## Context

Every application PDLF builds draws on `project-library-global`'s specifications, ADRs, policies and procedures. PDLF's steps and skills are how a building agent meets that content. Two problems arise:

1. **Discovery** — how a step or skill knows which global files are relevant to its task.
2. **Application** — a GBrain result is an indication of a source, not the source itself. The dangerous failure is an agent acting on a snippet, its own paraphrase, or a specification it invented because the real one was never read. It looks like compliance (a query ran, a decision was made) while the result never conformed to the real standard.

## Decision

**Discovery is a GBrain search, not a hand-maintained map.** Every step starts with a GBrain search across the federated documentation sources, which include `project-library-global` (source `default`) and the project's own library ([[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md)). A static map from steps to global files would be a second source of truth to keep in step, and would not scale.

**Application follows query → indication → fetch → apply, never query → paraphrase.** For any step whose work touches global content:

1. The task begins.
2. GBrain is searched across the federated documentation sources.
3. GBrain returns indications: which files are relevant, not their authoritative content.
4. The agent reads the indicated files in full.
5. The agent applies what those files actually say.

Step 3 is never treated as step 5. A GBrain snippet is a pointer for finding the source, not a substitute for reading it. This is the same discipline as [[[pdlf:pdlf-library/policy-local/pol-skill-invocation|Policy: Skill Invocation]]](C:/pdlf/pdlf-library/policy-local/pol-skill-invocation.md)'s "read before invoke" rule for skills.

**Enforcement, not just instruction.** The step cites which global files it read and applied, in its Step Receipt or BFT record. A claim of compliance is trusted only once it can be checked.

## Consequences

- [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md) carries the five-step sequence and the citation requirement as a binding rule.
- Every step whose work touches global content builds the sequence into its own reference when the step is written.
