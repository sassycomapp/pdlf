---
title: "f44-build-plan"
doc-id: "mb-c7cb929d"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is the clone of App 1's approved code into App 2, `master_template`, which every client instance depends on.

#### Step 44: Release

**Must achieve:** The developer confirms the release, on the results of Steps 41 to 43.

**Carried out by:** The developer, at the gate.

**Gate:** `production-released`: the application is released.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** None: the gate reads the results of Steps 41, 42A and 43 and the open findings in `triage_findings`; an open finding blocks it.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to production deployment
2. Developer: Promote the same reviewed commit from Staging to Production in Anvil IDE — Rollback is re-pointing, not `git revert`
3. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
4. Gate: `production-released` — Full BFT, gate summary, developer approval required; app is now live
5. Write Step 44 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-44-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-anvil-platform.md`: release note

Steps 42 to 44 still model a staging and production split that Anvil, under the five-app structure, does not have; they are rebuilt around the `develop` → `stable` release in steps work. The reasoning is in [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md).

## From `pdlf-todo.md`: item A2

### A2. Rebuild Steps 42, 42A, 43, 44

These steps currently model a staging/production environment split that does not apply to this platform. Rebuild them around the actual publishing mechanism: a `develop` → `stable` GitHub merge, performed by the operator, outside PDLF's own pipeline. See [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md) for full reasoning. Deferred to Phase F.
