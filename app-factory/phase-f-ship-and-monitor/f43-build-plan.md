---
title: "f43-build-plan"
doc-id: "mb-7ecf0cbd"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). Steps 42 to 44 still describe a staging and production split that PDLF does not have; they are rebuilt around the `develop` → `stable` release.

#### Step 43: Staging smoke test

**Must achieve:** Still describes a smoke test on staging. To be rebuilt.

**Carried out by:** GStack, using `/qa` or `/canary`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to staging verification
2. Invoke GStack `/qa` or `/canary` — Retargeted at Staging URL from Step 42
3. Verify output — Smoke test report: pass/fail at Staging; STOP if failing
4. Write Step 43 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-43-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-anvil-platform.md`: release note

Steps 42 to 44 still model a staging and production split that Anvil, under the five-app structure, does not have; they are rebuilt around the `develop` → `stable` release in steps work. The reasoning is in [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md).

## From `pdlf-todo.md`: item A2

### A2. Rebuild Steps 42, 42A, 43, 44

These steps currently model a staging/production environment split that does not apply to this platform. Rebuild them around the actual publishing mechanism: a `develop` → `stable` GitHub merge, performed by the operator, outside PDLF's own pipeline. See [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md) for full reasoning. Deferred to Phase F.
