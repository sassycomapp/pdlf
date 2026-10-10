---
title: "pol-anvil-platform"
doc-id: "mb-f219a912"
updated: "2026-10-10"
---
# PDLF Policy — Anvil Platform

**Binding.** The agent must comply whenever interacting with an Anvil-connected project. No
exceptions — platform constraints are hard.

---

## What

### anvil.yaml is sacred

Never write to `anvil.yaml`. Never. It is Anvil-managed configuration. Any task that appears
to require editing it must stop and request explicit developer authorization. This includes:
create, edit, reformat, regenerate, normalize, merge-edit, patch, or include in bulk refactors.

### Two-repo separation

Every PDLF-managed Anvil project has two git repositories:
- **Project-library repo:** docs, ADRs, process artifacts, templates, outputs. The agent's
  working home for all documentation and PDLF ceremony.
- **Code repo:** The Anvil-connected app. Contains `anvil.yaml`, `client_code/`,
  `server_code/`, `theme/`.

The two repos are never mixed. Docs never go in the code repo. Code never goes in the
library repo.

### Deployment is manual and environment-scoped

**Flagged for rebuild, 2026-07-18:** the release sequence below models a staging/production
environment split that does not apply to this platform. The platform uses the Five-App
Structure — PDLF operates entirely within the development-workspace app, which is
structurally never a dependency for any live client instance. Real publishing happens via
a `develop` → `stable` GitHub merge, performed by the operator, outside PDLF's own
pipeline. Full reasoning: [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md). The
sequence below is not yet corrected — treat as pending, not authoritative.

Anvil deploys via named Deployment Environments, each with its own URL, branch/commit pointer,
database, and Uplink keys. Publishing is a deliberate human action in the Anvil IDE — there
is no auto-publish on git push.

**Release sequence (Steps 41–45):**
1. [[[pdlf:stepwise/step-41-ship|/ship]]](C:/pdlf/stepwise/step-41-ship.md) pushes code to the branch. Stops there.
2. Manual: developer publishes to Staging environment only.
3. Full integration/E2E suite run against Staging (Step 42A) — verifies cross-feature behavior
   before the smoke test, which alone was assessed as too thin a check before Production.
4. Staging smoke test.
5. Manual: developer promotes to Production.
6. Production canary.

**Rollback** is re-pointing an environment to a prior commit — not `git revert` (which doesn't
un-publish an app).

### Pull-to-local junctures

The Anvil-connected code repo is pulled to local after every point where physical Anvil-side
work occurred and local work depends on it:

| After Step | Trigger |
|---|---|
| 18 | Data tables created in Anvil |
| 30 | UI forms built in Anvil |
| 33 | Scaffolding built in Anvil |
| Per feature cycle (Step 35) | Each Level 2 test pass |

### Environment-aware code

Code branches on `anvil.app.environment.name` to run identically across environments without
per-deploy edits. Staging and Production use separate databases confirmed by environment check.

---

## Why

These are not negotiable platform constraints — they reflect how Anvil.works actually works.
The deployment model (manual publish, per-environment configuration, environment-aware code)
is Anvil's native mechanic. GStack's default [[[pdlf:stepwise/step-41-ship|/ship]]](C:/pdlf/stepwise/step-41-ship.md) → `/land-and-deploy` pipeline assumes a
CI/CD model Anvil does not have. PDLF's release sequence respects the platform. The Step 42A
integration/E2E addition reflects a direct finding that a smoke test alone verifies too little
before a Production promotion — cross-feature interactions need a real check at Staging first.

---

## Where

Steps 17–45 (all Anvil-IDE interactions and deployment). This policy is itself the
detailed reference — there is no separate mechanics file. An earlier reference to
`stepwise/step-6-24-anvil-integration.md` was removed 2026-07-18: investigated and
confirmed that file was never created, and its intended content already lives here.

**Source:** Anvil.works deployment documentation
(verified 2026-07-10), [[[pdlf:pdlf-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md) §2.7, §2.10, §2.11.

---

*Updated 2026-07-12: release sequence extended with Step 42A (Staging integration/E2E suite).*
