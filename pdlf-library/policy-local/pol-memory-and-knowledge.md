---
title: "pol-memory-and-knowledge"
doc-id: "mb-d07a9e52"
updated: "2026-10-10"
---
# PDLF Policy — Memory and Knowledge Management

**Binding.** The agent must comply at every step. No exceptions.

---

## What

### GBrain querying is automatic (read-only)

Every step starts with a GBrain query relevant to that step's domain. This is substep 1 of
the 13-point execution sequence. Querying is read-only — it has no side effects on any
database, is equivalent to reading a project file, and runs automatically.

### GBrain syncing is asked (write operation)

`gbrain sync` + `gbrain embed` are write operations that modify the brain's index. They are
asked as part of the two housekeeping questions at substep 10 of every step — separately,
never combined with other questions, never auto-run.

### GBrain results are indications, not sources — mandatory query-fetch-apply sequence

A GBrain query result is a pointer to a source, not the source itself — the same category
of thing a search-result snippet is. This applies with particular force to
`project-library-global` content: a step whose domain touches global specs, ADRs,
policies, or SOPs must follow this exact sequence, never collapse it:

1. Task begins.
2. GBrain query, scoped to `project-library-global` (and the project's own sources).
3. GBrain returns indications — which files are relevant, not their authoritative content.
4. The agent fetches and reads the actual indicated file(s) in full.
5. The agent applies what those real files actually say to the current task.

Step 3 is never treated as step 5. Acting on a GBrain snippet, a paraphrase, or an assumed
recollection of a global file's content — instead of the file itself — is not compliance
with this policy, regardless of whether a GBrain query technically ran.

**Enforcement, not just instruction.** A step whose domain touches `project-library-global`
must cite which specific global file(s) it fetched and applied — visible in that step's
Step Receipt or BFT answer, not merely implied. This mirrors the artifact-persistence
requirement already binding on Steps 37/38 (write findings to a named path, verified by
OpenCode, not assumed as a side effect): a claim of standards compliance is only trusted
once it's checkable. The specific danger this closes: an agent silently generating its own
specification or standard, in place of the real global one, while a GBrain query still
technically fired — this looks like compliance and isn't.

Full rationale: [[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR: Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md).
Per-step implementation is built into each relevant step file (Steps 17, 20, 22, 26, 27,
35, 35A, 37, 38, 41–45 at minimum) as that step is written or rebuilt — not retrofitted in
bulk now.

### Sync cadence

| Trigger | Action |
|---|---|
| Every step that produces artifacts | GBrain sync + embed asked |
| Every gate | Full maintenance: git push (library + code repos) + GBrain sync + embed |
| After LEARN junction (Step 46) | GBrain sync + embed (learnings are now searchable for the next project) |

### Cross-contamination discipline

1. Always tag GBrain results with source project.
2. Cross-project learnings are WELCOME (advisory).
3. Cross-project decisions are NOT transferable (confirm with developer).
4. Scope queries where possible (`--source <slug>`).
5. Never auto-apply a cross-project decision.

### ISA lifecycle (Ideal State Artifact)

The ISA is the living done-definition for a project. It is:

- **Created** at Step 16 (domain model locked)
- **Updated** at Steps 26 (wireframes approved), 35 (build complete), 39 (build-verified gate
  passed for this feature), 46 (released)
- **Queried** at Step 11 of the next initiative (resume context)

The ISA's Criteria and Verification sections are generated from the `isc` table in the ledger.
Do not hand-edit ISC entries — the ledger is the source of truth.

### Step Receipt preservation

Every step produces a Step Receipt saved to `dev-{slug}\{slug}-project-library\pdlf\step-{N}-receipt.md`.
The receipt is generated from the ledger row just written — it IS the ledger row, formatted
for reading. Never compose a receipt separately; a separate composition could diverge from
what actually happened.

### Devlog Index and Judgement Trail

- `devlog-index.md`: reverse-chronological index of every Step Receipt. Regenerated after
  each step.
- `judgement-trail.md`: per-step decisions, flags, deviations. Extracted from each Step
  Receipt at write time, not reconstructed afterward.

Both live at `dev-{slug}\{slug}-project-library\pdlf\` and are generated from ledger rows.

---

## Why

The developer is a non-technical builder who cannot personally verify every decision an
agent makes across a multi-session project. GBrain provides the persistent memory layer that
enables continuity. The cross-contamination discipline prevents a pattern from one project
being silently applied to another where it doesn't belong. The ISA and Step Receipt create
a verifiable trail from idea to production.

---

## Where

Every step in the PDLF pipeline. GBrain integration mechanics at [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
ISA lifecycle at [[[pdlf:pdlf-library/templates-local/isa-template-v2|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md). Cross-contamination discipline
defined in this policy.

**Source:** [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), [[[pdlf:pdlf-library/templates-local/isa-template-v2|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md),
[[[pdlf:pdlf-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md) §2.1.

---

*Updated 2026-07-12: ISA update point moved from Step 38 to Step 39. With the build/verify
loop reordered (35 → 35A → 40 → 40B → 36 → 37 → 38 → 38A → 39 → gate), Step 38 ("QA passed")
is no longer near the end of verification for a feature — Steps 38A, 39, and the
`build-verified` gate all follow it. Step 39 is where the feature's verification actually
concludes for this cycle.*
