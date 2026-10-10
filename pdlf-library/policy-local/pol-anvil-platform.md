---
title: "pol-anvil-platform"
doc-id: "mb-f219a912"
updated: "2026-10-10"
---
# PDLF Policy — Anvil Platform

**Binding.** The agent must comply whenever it works on an Anvil application. These rules reflect how Anvil works and have no exceptions.

---

## What

### `anvil.yaml` is never written

The agent never creates, edits, reformats, regenerates, merges or patches `anvil.yaml`. Anvil manages it. A task that seems to need a change to it stops and asks David.

### Two repositories

Every application has two repositories:

- **the code repository**, which is the Anvil app (App 1, the development workspace): `anvil.yaml`, `client_code/`, `server_code/`, `theme/`;
- **the documentation repository**, which holds everything else: documents, decisions, PDLF records.

They are never mixed: no documents in the code repository, no code in the documentation repository.

### What travels to Anvil

Only `anvil.yaml`, `client_code`, `server_code` and `theme` travel to Anvil, and within `theme` only `theme/assets`. Everything else stays local and is kept out of what Anvil receives. Every review checks this boundary: everything the code needs is inside those items, and nothing that must not ship (credentials, development files) is. This list is to be confirmed against Anvil's documentation.

### The five-app structure

Every application follows [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md):

- All development happens in App 1.
- Release is the `develop` → `stable` merge that updates `master_template` (App 2). David performs it, as a gated step. There is no separate staging or production environment.
- Client instances (App 4) are cloned from `blank_client_template` (App 3) and run on `master_template`. The agent never adds a form or server module to a client instance: doing so silently and permanently cuts that instance off from future updates.

### No multi-tenancy

No application is ever multi-tenant. Every client has its own app instance and its own database. The agent never writes code that shares one database between clients and separates them by filtering on a client or instance field. This decision is sealed: [[[default:adr-global/adr-dependency-based-not-multi-tenant|ADR: Dependency-Based, Not Multi-Tenant]]](C:/dev/project-library-global/adr-global/adr-dependency-based-not-multi-tenant.md). It is given to the agent as context before any code is written.

### Pull to local

The code repository is pulled to local after every step where work was done in the Anvil editor, before local work continues:

| Pull | After |
|---|---|
| Step 18 | Data tables created in Anvil at Step 17. |
| Step 30 | UI forms built in Anvil at Step 29. |
| Step 33 | The scaffold built in Anvil at Step 32. |
| Each feature cycle | The feature's connected test, run against Anvil. |

---

## Why

These are Anvil's own mechanics. Anvil publishes from a Git branch, manages its own configuration file, and serves each client from its own app. Rules that ignore this produce code that works elsewhere but fails on Anvil, or client instances that silently stop receiving updates.

---

## Where

Every step that touches an Anvil application. Steps 42 to 44 still model a staging and production split that Anvil, under the five-app structure, does not have; they are rebuilt around the `develop` → `stable` release in steps work. The reasoning is in [[[pdlf:pdlf-library/adr-local/no-staging-environment-five-app-isolation|ADR: No Staging Environment Five App Isolation]]](C:/pdlf/pdlf-library/adr-local/no-staging-environment-five-app-isolation.md).
