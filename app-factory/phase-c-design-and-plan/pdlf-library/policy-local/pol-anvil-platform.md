---
title: "pol-anvil-platform"
doc-id: "mb-58673d41"
updated: "2026-10-20"
---
# PDLF Policy — Anvil Platform

**Binding.** The agent must comply whenever it works on an Anvil application. These rules reflect how Anvil works and have no exceptions.

---

## What

### `anvil.yaml` is changed only through Anvil's skill

The agent changes `anvil.yaml` only through Anvil's `anvil-yaml` skill, which Anvil issues for that purpose, and validates every change with `anvil --json validate anvil.yaml`. It never changes `dependencies`; David changes them in the Anvil editor. A schema change reaches the live app only when David applies it in Anvil's Data Tables view.

### Two repositories

Every application has two repositories:

- **the code repository**, which is the Anvil app (App 1, the development workspace): `anvil.yaml`, `client_code/`, `server_code/`, `theme/`;
- **the documentation repository**, which holds everything else: documents, decisions, PDLF records.

They are never mixed: no project documents in the code repository, no code in the documentation repository. Client-facing material that the application itself serves to its users, such as help documents, is part of the application, not project documentation; it lives in `theme/assets` under the rules below.

### What goes to Anvil

An Anvil application is its Git repository. Everything committed to the code repository is pushed to Anvil and stored there; nothing stays behind except what `.gitignore` excludes. `.gitignore` therefore keeps out everything local-only: `.env`, credentials, `__pycache__`, test output and development files.

Anvil uses only `anvil.yaml`, `client_code/`, `server_code/` and `theme/` (within `theme/`: `assets/`, `parameters.yaml` and `templates.yaml`). Other committed files, such as tests or a README, are stored by Anvil but not used. Only the Python and YAML files in `client_code/` and `server_code/` run.

Two parts are public:

- **`theme/assets/`.** Every file in it is served at `<app-url>/_/theme/<path>`, and anyone with the link can open it, without logging in.
- **`client_code/`.** It runs in the user's browser, where it can be read.

Nothing secret, internal or for paying clients only ever goes in either. Material that must be restricted to logged-in users is served from the server side; how is decided in steps work. Every review checks these boundaries.

### Client documents and videos

**Documents.** Client-facing documents, such as user guides, may be placed in `theme/assets/docs/`. Anvil does not block this: each document is served by link and can be opened from the application. They are public, as above.

**Videos.** Explainer videos are hosted on YouTube and linked or embedded in the application. They are not placed in `theme/assets/`. Anvil would serve them, but every asset is stored in the Git repository, so large video files would be carried by every clone and push and would make the five apps of a business heavy over time. Anvil's documentation states no size limit for assets, and large videos there are untested.

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
| Each step that works in the Anvil editor | The pull named in that step's own build plan. |
| Each feature cycle | The feature's connected test, run against Anvil. |

---

## Why

These are Anvil's own mechanics. Anvil publishes from a Git branch, manages its own configuration file, and serves each client from its own app. Rules that ignore this produce code that works elsewhere but fails on Anvil, or client instances that silently stop receiving updates.

---

## Where

Every step that touches an Anvil application.
