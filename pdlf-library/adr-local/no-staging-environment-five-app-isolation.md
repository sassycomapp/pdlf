---
title: "adr-no-staging-environment-five-app-isolation"
doc-id: "mb-5b1e8fd8"
updated: "2026-10-11"
---
# ADR — PDLF Does Not Need a Staging/Production Environment Split

**Status:** Accepted

**Date:** 2026-07-18

**Source:** [[[mb-3-cs-project-library:docs-local/platform-architecture-narrative|platform-architecture-narrative]]](C:/dev/dev-mb-3-cs/mb-3-cs-project-library/docs-local/platform-architecture-narrative.md) (mb-3-cs project library) § 11, The Five-App Structure.

---

## Context

Anvil natively supports "Deployment Environments" — a mechanism where a single app can
have multiple environments (e.g. Development, Staging, Production), each tracking a
different branch or commit, each with its own URL and its own Data Tables. PDLF's
original Phase F design (Steps 42–44) was modeled on this generic mechanism: publish to
a staging environment, run integration/smoke tests there, then promote to a production
environment via a gate.

The question this ADR resolves: does PDLF actually need this staging/production split?
Raised because the developer's working style is single-branch, single-environment —
work directly on `master`/`main`, one click to publish, whatever is pushed goes live
immediately. On its face this looked like it traded safety for simplicity. It does not.
The generic staging/production model does not describe how this platform (Mybizz,
built on the Five-App Structure) actually works.

## The Five-App Structure — the part that matters here

The platform is not one Anvil app with multiple environments. It is five separate Anvil
apps with a dependency chain between them:

| App | Role | Ever seen by real users? |
|---|---|---|
| App 1 — `mb-3-cs` (or equivalent, e.g. `mb4ecom`) | Development workspace. All feature development happens here. | **No.** Explicit key rule: "This is the authoring environment, not the publishing environment. It is never a dependency for any client instance." |
| App 2 — `master_template` | The sole source of server logic and UI for every client. Tracks the `stable` GitHub branch. | No — clients depend on it, but it is never given to a client directly. |
| App 3 — `blank_client_template` | Clone source for provisioning new clients. Updated only on schema change. | No. |
| App 4 — `[client-name]-cs` | One per paying client. Depends on App 2. This is the only app real users ever touch. | **Yes — this is production, for real.** |
| App 5 — `Mybizz_management` | Platform-operator tooling. Deferred, post-launch. | No (operator-only). |

PDLF operates entirely inside App 1. Every push PDLF makes during a build cycle lands on
the `develop` branch of App 1's code repo. App 1 is structurally excluded from ever being
a dependency for a client instance — this isn't a policy PDLF has to enforce, it's a
property of how the platform's apps are wired together.

## Why this settles the question

Real users are only ever exposed to App 4, and App 4 only ever changes when App 2 updates,
and App 2 only updates when a human deliberately merges `develop` → `stable` on GitHub.
That merge is a separate, operator-controlled action. It is not a step PDLF's pipeline
performs, and no step in PDLF's pipeline as currently modeled even reaches it.

This means the risk a staging environment exists to prevent — a broken push reaching a
live user before anyone reviews it — cannot happen through PDLF's own pipeline, at all,
regardless of whether the app already has paying clients (like `mb4ecom`) or is brand
new. This is not a timing argument ("there are no users yet, for now"). It is a
structural isolation the platform's own architecture enforces, permanently, for as long
as PDLF only ever pushes to App 1.

## The developer's mitigation strategy is correctly scoped as a result

Given the above, the residual risk PDLF's build process actually carries is not
"broken code reaches a user" — it's "something goes wrong locally and work is lost or
hard to recover." That risk is fully covered by:

1. Anvil's automatic backup of App 1 to GitHub (protects the code repo).
2. Manual full-app clone backups of App 1 taken between steps (protects the code repo).
3. Manual full local-disk backups of both the code repo and the docs repo, taken between
   steps (protects both repos).

These three, taken together, are correctly matched to the actual risk. A staging
environment would protect against a different risk — live-user exposure — that doesn't
exist in this architecture. Adding one would be complexity without a corresponding
safety gain, which fails the developer's own standing test: simple, secure, robust, fit
for purpose.

## Decision

PDLF does not model a staging/production environment split. PDLF operates entirely
within the development-workspace app (App 1) and never publishes directly to anything a
real user can reach. The `develop` → `stable` merge that actually exposes changes to
clients is an operator action outside PDLF's pipeline, not a PDLF step.

## Consequences

- **Steps 42, 42A, 43, and 44, as currently drafted, no longer match this platform's
  actual publishing mechanism.** They describe staging-environment mechanics (publish to
  staging, staging E2E, staging smoke test, promote-to-production gate) that don't apply
  here. These steps need to be rebuilt around what actually happens after a feature is
  signed off in App 1 — up to and possibly including the point where the operator
  decides to merge `develop` → `stable`. Not yet rebuilt as of this ADR; logged on the
  Active-PDLF ToDo list.
- The `production-released` gate (currently positioned at Step 44) will need to be
  re-anchored to whatever event actually corresponds to "real users can now see this" —
  almost certainly the `develop` → `stable` merge, not any action PDLF itself performs.
- This ADR is the reference to cite the next time the staging/environment question comes
  up, rather than re-deriving the argument from scratch.
- Applies specifically to platforms built on this Five-App dependency model. If PDLF is
  ever pointed at a project that is a single Anvil app with no dependency-based client
  isolation, this ADR's conclusion does not automatically carry over — the staging
  question would need to be re-asked for that project's actual architecture.
