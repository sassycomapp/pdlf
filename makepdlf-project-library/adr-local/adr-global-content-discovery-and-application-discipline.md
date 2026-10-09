---
title: "adr-global-content-discovery-and-application-discipline"
doc-id: "mb-c0174316"
updated: "2026-10-09"
---
# ADR — Global Content Discovery and Application Discipline

**Status:** Accepted

**Date:** 2026-07-19

---

## Context

Every project PDLF builds needs to draw on `project-library-global`'s specs, ADRs, and
(eventually) policies and SOPs — this is company-wide Anvil-application content, not
PDLF's own concern, but PDLF's steps and skills are the mechanism by which a building
agent encounters it. Two problems needed solving, not one:

1. **Discovery** — how does a step or skill know which global files are relevant to its
   current task? No systematic mechanism existed; the only routing found was a small,
incomplete step-to-spec table migrated into [[[pdlf:makepdlf-project-library/specifications-local/spec-nomenclature|Spec: Nomenclature]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-nomenclature.md) from the retired
    `spec-architecture.md`.

2. **Application, and the sharper risk underneath it** — even once GBrain returns relevant
   results, a query result is an *indication of a source*, not the source itself. Nothing
   previously stated that an agent must fetch and apply the actual file content GBrain
   points to, rather than acting on the GBrain snippet, its own paraphrase, or — worst
   case — silently generating its own specification when the real one wasn't actually
   read. This last failure mode is the dangerous one: it looks like compliance
   (a GBrain query ran, a decision got made) while producing content that never actually
   conformed to the real standard.

## Decision

**Discovery mechanism: GBrain semantic query, scoped to `project-library-global`, not a
hand-maintained static map.** [[[pdlf:makepdlf-project-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/makepdlf-project-library/policy-local/pol-memory-and-knowledge.md)'s existing scoping rule already
requires every GBrain query to nominate `project-library-global` as a source — this ADR
confirms that scoped query is the intended discovery path, not a rejected half-measure. A
static per-step map (the kind partially built in `spec-nomenclature.md`) does not scale to
98 files across 7 folders and would itself become a second source of truth to keep in sync
— the same duplication failure found and corrected repeatedly elsewhere in this document
set (two [[[pdlf:makepdlf-project-library/docs-local/docmap|Docmap]]](C:/pdlf/makepdlf-project-library/docs-local/docmap.md)s, two todo lists, `ADR-0007` vs. real filenames). GBrain queried live,
at the point of need, avoids that.

**Application discipline: query → indication → fetch → apply. Never query → paraphrase.**
The full required sequence for any step whose domain touches `project-library-global`:

1. Task begins.
2. GBrain query, scoped to `project-library-global` (and the project's own sources, per
   existing policy).
3. GBrain returns indications — which global files are relevant, not their authoritative
   content.
4. The agent fetches and reads the actual indicated file(s) in full.
5. The agent applies what those real files actually say to the current task.

Step 3 is never treated as step 5. A GBrain snippet is a pointer, exactly the same
category of thing a search-result snippet is — useful for finding the source, not a
substitute for reading it. This mirrors a principle already binding elsewhere in PDLF:
[[[pdlf:makepdlf-project-library/policy-local/pol-skill-invocation|Policy: Skill Invocation]]](C:/pdlf/makepdlf-project-library/policy-local/pol-skill-invocation.md)'s "read before invoke" rule for skills — never trust a name or
summary, read the actual source. This ADR applies the identical discipline to global
content instead of skills.

**Enforcement, not just instruction.** An instruction to "apply the real standard" with no
check is exactly the gap that produces silent non-conformance. The step or skill must cite
which specific global file(s) it fetched and applied — visible in the Step Receipt or BFT
answer for that step, not merely implied. This is the same pattern already used for Steps
37/38's artifact-persistence requirement (write findings to a named path, verified by
OpenCode, not assumed as a side effect) — a claim of compliance is only trusted once it's
checkable, not merely stated.

## Consequences

- [[[pdlf:makepdlf-project-library/policy-local/pol-memory-and-knowledge|Policy: Memory and Knowledge]]](C:/pdlf/makepdlf-project-library/policy-local/pol-memory-and-knowledge.md) gains a new binding subsection formalizing the five-step
  sequence and the citation requirement. See that policy for the operational rule this ADR
  authorizes.
- Every step file built from Phase B onward whose domain touches global content (Steps 17,
  20, 22, 26, 27, 35, 35A, 37, 38, 41–45 at minimum, per the existing partial mapping in
   [[[pdlf:makepdlf-project-library/specifications-local/spec-nomenclature|Spec: Nomenclature]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-nomenclature.md)) must build this sequence into its own procedure when it is
  written or rebuilt — not retrofitted in bulk now. This is deferred work, consistent with
  the existing agreement to handle Steps 17–46 one at a time as each phase is reached. This
  ADR exists so that deferred work has a defined target to build toward, not so the target
  itself gets built today.
- `project-library-global`'s own discovery-side gaps (an ADR index organized by
  status/date rather than topic, two empty policy/SOP index folders) are not fixed by this
  ADR — they're a separate, `project-library-global`-side concern, out of scope for a
  dev-makepdlf ADR. If GBrain semantic search proves an adequate substitute for a
  topic-organized static index, that gap may never need closing; if it doesn't, that's a
  finding for later, not assumed now.
- Registration dependency: **resolved 2026-07-19.** `project-library-global` has a real
  GitHub remote (`https://github.com/sassycomapp/project-library-global`, public) and is
  registered as a GBrain source (`project-library-global` →
  `/mnt/c/dev/project-library-global`). The mechanism this ADR describes is now actually
  usable, not just designed.
