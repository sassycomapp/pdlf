---
title: "pol-anvil-platform"
doc-id: "mb-f219a912"
updated: "2026-11-08"
---
# PDLF Policy — Anvil Platform

**Binding.** The agent must comply whenever it works on an Anvil application. These rules reflect how Anvil works and have no exceptions.

---

## What

### `anvil.yaml` is changed only through Anvil's skill

The agent changes `anvil.yaml` only through Anvil's `anvil-yaml` skill, which Anvil issues for that purpose, and validates every change with `anvil --json validate anvil.yaml`. It never changes `dependencies`; David changes them in the Anvil editor. A schema change reaches the live app only when David applies it in Anvil's Data Tables view.

### Code and documents are kept apart

Every business has one code repository per app it develops (`{slug}-app1`, `{slug}-app2`, `{slug}-app3`, `{slug}-app5`), each an Anvil app holding `anvil.yaml`, `client_code/`, `server_code/` and `theme/`; one GitHub repository, `{slug}-app4`, holding the release image definition; and one project library, `{slug}-project-library`, which holds everything else: documents, decisions and PDLF records.

They are never mixed: no project documents in a code repository, no code in the project library. Client-facing material that the application itself serves to its users, such as help documents, is part of the application, not project documentation; it lives in `theme/assets` under the rules below.

### What goes to Anvil

An Anvil application is its Git repository. Everything committed to the code repository is pushed to Anvil and stored there; nothing stays behind except what `.gitignore` excludes. `.gitignore` therefore keeps out everything local-only: `.env`, credentials, `__pycache__`, test output and development files.

Anvil uses only `anvil.yaml`, `client_code/`, `server_code/` and `theme/` (within `theme/`: `assets/`, `parameters.yaml` and `templates.yaml`). Other committed files, such as tests or a README, are stored by Anvil but not used. Only the Python and YAML files in `client_code/` and `server_code/` run.

Two parts are public:

- **`theme/assets/`.** Every file in it is served at `<app-url>/_/theme/<path>`, and anyone with the link can open it, without logging in.
- **`client_code/`.** It runs in the user's browser, where it can be read.

Nothing secret, internal or for paying clients only ever goes in either. Material that must be restricted to logged-in users is served from the server side; how is decided in steps work. Every review checks these boundaries.

### Client documents and videos

**Documents.** Client-facing documents, such as user guides, may be placed in `theme/assets/docs/`. Anvil does not block this: each document is served by link and can be opened from the application. They are public, as above.

**Videos.** Help and explainer videos are stored once per language in a Mybizz-owned Cloudflare R2 bucket published at `media.mybizz.live`, and played in the video component as direct video addresses; they set no cookies ([[[default:policy-global/pol-legal-documents-and-consent|Legal Documents and Consent]]](C:/dev/project-library-global/policy-global/pol-legal-documents-and-consent.md)). They are not placed in `theme/assets/`: every asset is stored in the Git repository, so large video files would be carried by every clone and push and would make the five apps of a business heavy over time. A client's own videos (F-09) are embedded from outside video services and load only after cookie consent.

### The five-app structure

Every application follows [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md):

- All development happens in App 1.
- Release is App 1's approved, tagged release, pushed into App 2's repository (`master_template`) by David at Step 42, built with App 3 into the release image, and moved to every client instance by App 5's Release action at Step 44. There is no separate staging or production environment.
- Client instances (App 4) run the release image: App 3 (`blank_client_template`) on `master_template`, on the Anvil App Server ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)). The agent never adds a form or server module to App 3: one added there overrides `master_template` for every client, and the image build stops on it.

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

These are Anvil's own mechanics. Anvil publishes from a Git branch, manages its own configuration file, and the App Server serves each client from its own instance. Rules that ignore this produce code that works elsewhere but fails on Anvil, or client instances that silently stop receiving updates.

---

## Where

Every step that touches an Anvil application.
