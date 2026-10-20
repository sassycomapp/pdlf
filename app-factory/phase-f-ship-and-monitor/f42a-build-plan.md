---
title: "f42a-build-plan"
doc-id: "mb-f3b31ed1"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is the clone of App 1's approved code into App 2, `master_template`, which every client instance depends on.

#### Step 42A: Release regression test

**Must achieve:** Every feature is tested on App 2 as released.

**Carried out by:** GStack, using `/qa-only`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack): tests every feature on App 2 in a real browser, report only → `f42a` findings, then Step 43; a failure is rolled back at Step 42.

## From `pol-anvil-platform.md`: release note

Steps 42 to 44 still model a staging and production split that Anvil, under the five-app structure, does not have; they are rebuilt around the `develop` → `stable` release in steps work. The reasoning is in [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md).

## From `pdlf-todo.md`: item A2

### A2. Rebuild Steps 42, 42A, 43, 44

These steps currently model a staging/production environment split that does not apply to this platform. Rebuild them around the actual publishing mechanism: a `develop` → `stable` GitHub merge, performed by the operator, outside PDLF's own pipeline. See [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md) for full reasoning. Deferred to Phase F.
