---
title: "adr-no-staging-environment-five-app-isolation"
doc-id: "mb-5b1e8fd8"
updated: "2026-10-23"
---
# ADR — PDLF Has No Staging/Production Environment Split

**Status:** Accepted

---

## Context

Anvil supports Deployment Environments: one app with several environments (for example Development, Staging and Production), each tracking a different branch or commit, each with its own URL and Data Tables. Every client starts on Anvil's Hobby plan, which gives each app one environment and one database. Mybizz is not built as one app with several environments; it is five separate Anvil apps with a dependency chain between them.

## The Five-App Structure — the part that matters here

| App | Role | Seen by real users? |
|---|---|---|
| App 1 — `{slug}-app1` | Development workspace. All feature development happens here. It is never a dependency of any client instance. | **No.** |
| App 2 — `master_template` | The sole source of server logic and UI for every client. Receives App 1's tagged releases, pushed into its repository by the developer at Step 42. | No: clients depend on it, but it is never given to a client. |
| App 3 — `blank_client_template` | The clone source for provisioning new clients. | No. |
| App 4 — `[client-name]-{vertical}` | One per paying client, on the client's own Anvil account. Depends on App 2. The only app real users touch. | **Yes: this is production.** |
| App 5 — `{Product}_management` | Platform-operator tooling. | No (operator only). |

Every build step works inside App 1, and every push a build step makes lands in App 1's repository. App 1 is structurally never a dependency of a client instance; this is how the apps are wired, not a policy PDLF must enforce.

## Why there is no staging environment

Real users see only App 4. App 4 changes only when App 2 changes, and App 2 changes only when the developer pushes App 1's approved, tagged release into App 2's repository at Step 42. No agent performs that action.

So the risk a staging environment exists to prevent — a broken push reaching a live user before anyone reviews it — cannot arise through PDLF's pipeline, whether or not the application already has paying clients. This is structural isolation, permanent for as long as only the developer releases into App 2.

The risk PDLF's build process does carry is that something goes wrong locally and work is lost or hard to recover. That is covered by:

1. Anvil's synchronisation of App 1 with GitHub, and every commit pushed.
2. Backups of App 1 around every test run against hosted App 1 (the testing policy).
3. Backups of every client instance before a release (test RL-02).

A staging environment would add complexity against a risk this architecture does not have, which fails the credo: simple, secure, robust, fit for purpose.

## Decision

PDLF has no staging/production environment split. Build steps work only in App 1 and never publish to anything a real user can reach. The release that exposes changes to clients is Step 42: the developer pushes App 1's tagged release into App 2. Testing before release runs on the Anvil App Server on the developer's computer and on the test client instance.

## Consequences

- Steps 42, 42A, 43 and 44 are built around the release into App 2: Step 42 releases, Step 42A tests every feature on App 2 as released, Step 43 checks the test client instance on the new release, and at Step 44 the developer confirms the release on the results of Steps 41 to 43 (the `production-released` gate).
