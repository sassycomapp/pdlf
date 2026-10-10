---
title: "pol-INDEX"
doc-id: "mb-65973e87"
updated: "2026-10-10"
---
# PDLF Policy Index

Internal policies governing the development and operation of the PDLF system. These are
**binding constraints** — not guidelines, not recommendations. The agent must comply; the
developer must be informed of any conflict.

PDLF is an internal system. It is never public-facing. These policies govern how PDLF
behaves, how it must be developed, and how it must be used.

| Policy | Concern | Source authority |
|---|---|---|
| [[[pdlf:pdlf-library/policy-local/pol-bft-discipline\|Policy: BFT Discipline]]](C:/pdlf/pdlf-library/policy-local/pol-bft-discipline.md) | BFT application rules — Full/Light/None assignment, gate rule, anti-rubber-stamping | [[[pdlf:pdlf-library/specifications-local/spec-bft\|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) |
| [[[pdlf:pdlf-library/policy-local/pol-sequential-enforcement-and-deviation\|Policy: Sequential Enforcement and Deviation]]](C:/pdlf/pdlf-library/policy-local/pol-sequential-enforcement-and-deviation.md) | Step execution discipline, gate procedure, deviation mechanism | [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md), [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) |
| [[[pdlf:pdlf-library/policy-local/pol-anvil-platform\|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) | anvil.yaml protection, deployment model, pull-to-local junctures, two-repo separation | This policy is self-contained — no separate mechanics file |
| [[[pdlf:pdlf-library/policy-local/pol-testing-and-quality\|Policy: Testing and Quality]]](C:/pdlf/pdlf-library/policy-local/pol-testing-and-quality.md) | Three-level testing, backup discipline, feature signoff, Uplink rules, full per-feature verification loop | This policy is self-contained — no separate mechanics file |
| [[[pdlf:pdlf-library/policy-local/pol-skill-invocation\|Policy: Skill Invocation]]](C:/pdlf/pdlf-library/policy-local/pol-skill-invocation.md) | Skill-use principle, read-before-invoke, progressive disclosure | [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) |
| [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge\|Policy: Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md) | GBrain query/sync boundary, cross-contamination discipline, ISA lifecycle | [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline\|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) |
| [[[pdlf:pdlf-library/docs-local/stepwise-development-process\|Policy: Stepwise]]](C:/pdlf/pdlf-library/docs-local/stepwise-development-process.md) | Working process for developing stepwise files — discussion discipline, file identity, numbering convention, skill ecosystem | [[[pdlf:pdlf-library/specifications-local/spec-skill-design\|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md), `specifications-local/spec-architecture.md` |

Note: `[[pol-stepwise]]` is a **living working document**, not a binding policy in the same
sense as the other six — it is included here for discoverability since it governs how the
stepwise files themselves are developed, but see its own header for that distinction.

Each policy states:
- **What** the policy is (the binding rule)
- **Why** it exists (the reason, with evidence)
- **Where** it applies (which steps or situations)

---

*Policy Index version 1.1. Updated 2026-07-12: added missing row for `[[pol-stepwise]]`,
which existed on disk but was absent from this index.*
