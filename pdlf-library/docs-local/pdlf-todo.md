---
title: "pdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-10-22"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

---

## A. Building the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`.

---

## B. Rules for building every step

### B1. Global-content query-fetch-apply sequence

The rule and its enforcement are set by [[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md) and [[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md). Every documentation repository is a federated GBrain source, so one search covers everything, and cross-repository links use the standard form `[[[source-id:slug]]](C:/full/path.md)`, written by agents as `[[name]]` and converted by the `mb-doc-check` commit hook. The five-step sequence and its citation requirement are built into each relevant step file (17, 20, 22, 26, 27, 35, 35A, 37, 38, 41–45 at minimum) as that step is rebuilt under A1, after the sequence is checked against that setup.

### B4. End-to-end proof of the governed memory pipeline

The governed memory pipeline is proven end to end, once, on the first real step run on `mb-5-pdlf`, the test project for PDLF.

---

## C. Testing

### C2. Prove the test suite on `mb-5-pdlf`

`mb-5-pdlf` holds no application until the Daily Intentions Tracker is built through PDLF. When it is, Step 11 runs PR-09 to prove the local runtime, both Uplink connections, the `TEST_` users with second factors and the mail catcher; each later step then runs its test specification. Correct any test, template or tool that does not work as written before another application relies on it.

---

## E. Skills and documentation

### E1. Verify Pass 1 against the installed copies

Phases B and C were scoped from the issuers' published sources (GStack `c580561`, Matt Pocock `5beb35b`, Anvil `14b1967`, Magdoub wireframe at its GitHub head). Run the verification command from the Phase B session, compare the installed copies, the two Magnus919 skill files, the Anvil CLI and the GBrain results with Steps 01–46, and correct any step that does not match. Step 17 depends on the Anvil CLI (`anvil --json validate`) being installed.

### E2. Anvil's `$app-testing` skill

Anvil's `data-models` and `server-code` skills call `$app-testing`, and `anvil-yaml` calls `anvil db apply-schema --force`, to test against the agent's temporary database. `$app-testing` is not yet published in `anvil-agent-references`. When Anvil publishes it, it is assessed as a complement to the local runtime of the test suite, and examined whenever `anvil-agent-references` is updated.

### E5. Pass 3: help and video documentation

Design the user help documentation and the video documentation, as one design job, before `mb-5-pdlf` reaches Phase E.

### E8. Cloudflare R2

Each client has one or two R2 buckets of its own, in a Cloudflare account dedicated to it, and leaves with them on exit (`adr-client-r2-storage-and-exit-handover`). Cloudflare is registered Deferred in the skills catalog; document it with `mb-sysdoc-creator` before the first step that uses it, and confirm which S3-compatible library runs on Anvil's server Python.

---

## F. Applications

### F1. Align both project libraries with the project template

`mb-3-cs-project-library` and `mb-4-ecom-project-library` were made before the project template. Bring each to the template's structure (`docs-local`, `adr-local`, `pdlf-outputs` with one folder per step, `pdlf-tickets`, `pre-project`, the Matt Pocock configuration in `docs\agents`) without changing any existing content. `mb-4-ecom` has `adr` and `docs` where the template has `adr-local` and `docs-local`. Done by Step 11, route B, when each application first enters PDLF; until then, nothing is moved.
