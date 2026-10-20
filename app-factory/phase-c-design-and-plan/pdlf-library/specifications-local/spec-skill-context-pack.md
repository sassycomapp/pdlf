---
title: "spec-skill-context-pack"
updated: "2026-10-20"
doc-id: "mb-ff7aa34c"
---
# PDLF — Skill Context Pack (Specification)

## What it is

The context pack is the set of platform rules every skill must know before it shapes an application. It is a list of files, nothing more. Each fact keeps its one home; this document only names the files.

## How it is used

At every skill invocation, the orchestrator pastes the full text of every file listed below into the invocation prompt, after the step's own handoff material ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact and Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 2). It never pastes a summary, and never only a path.

## The pack

1. [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md): the five apps, why each exists, and the rule never to add forms or server modules to a client instance.
2. [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md) and [[[default:security-global/threat-models/sec-multi-tenant-assumption-leakage|Threat Model: Multi-Tenant Assumption Leakage]]](C:/dev/project-library-global/security-global/threat-models/sec-multi-tenant-assumption-leakage.md): no shared database, no tenant column, no tenant filter, ever.
3. [[[default:policy-global/pol-anvil-first-development|Policy: Anvil-First Development]]](C:/dev/project-library-global/policy-global/pol-anvil-first-development.md): use Anvil's own facility first.
4. [[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md): `anvil.yaml` is changed only through Anvil's `anvil-yaml` skill; `client_code` and `theme/assets` are public; what goes to Anvil.
5. [[[default:specifications-global/spec-anvil-platform-standards|Spec: Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) and [[[default:adr-global/adr-anvil-platform-constraints|ADR: Anvil Platform Constraints]]](C:/dev/project-library-global/adr-global/adr-anvil-platform-constraints.md): what Anvil can and cannot do.
6. The defaults of Anvil's `data-models` skill, `C:\mybizz\anvil-agent-references\skills\data-models\SKILL.md`: tables default to no client access; data rules live in model classes and server code; the server holds authority over identity and ownership.
7. [[[default:specifications-global/spec-m3-design-standards|Spec: M3 Design Standards]]](C:/dev/project-library-global/specifications-global/spec-m3-design-standards.md): every application uses Anvil's Material 3 theme.

## Not applicable to an Anvil application

The pack ends with this instruction, pasted with it:

> Some parts of this review do not apply to an Anvil application. Record each of them as "not applicable: Anvil application" and do not put a question to the developer about it:
> - the distribution check and distribution architecture (an Anvil app has no build or publish pipeline of its own);
> - the worktree parallelisation strategy;
> - test-framework detection (PDLF states its own test method);
> - pull-request and CI/CD assumptions.

When a step finds another part of a skill that does not apply to Anvil, the step proposes adding it to this list, as a lesson, before it stops.

## Why

Most skills PDLF uses were written for ordinary web development. Left to themselves, they propose what Anvil forbids or PDLF never allows, such as a shared database with a tenant column, or a build pipeline Anvil does not have. A mistake made while the application is being defined is built into every later step. Giving every skill the same rules, in full, every time, stops that mistake at its source. Marking the parts that do not apply saves David from questions that cannot matter, so his attention goes to the ones that do.
