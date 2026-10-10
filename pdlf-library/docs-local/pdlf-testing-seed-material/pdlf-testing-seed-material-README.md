---
title: "pdlf-testing-seed-material-README"
doc-id: "mb-cd88fa17"
updated: "2026-10-10"
---
# PDLF Testing System — Seed Material

## What this folder actually is

This is real, hand-built testing work from an earlier iteration of MB-3-CS
— built before PDLF existed, before OpenCode was the harness, through
several different tooling setups. It represents genuine hours of real
work: a working, hand-built CI-equivalent (checks run and enforced
without needing a formal pull-request pipeline), covering a real Anvil
authentication system end to end.

It is **not** a working system today. The orchestration layer it once ran
inside — Continue.dev, pointed at a folder path (`C:\_Data\_Mybizz\
mybizz-core`) that no longer exists — is gone, and that part was
deliberately not kept. What's in this folder is what survived a real
review: content judged genuinely reusable, not the dead scaffolding
around it.

**PDLF does not yet have its own testing system.** This folder is seed
material for building that system, not a working substitute for it —
the standing task for that build is item 9 on the PDLF to-do list in the
developer's operating documents.

---

## What's actually in this folder, and what each piece is for

### `feature-test-example.py`
A real, working `pytest` file testing Anvil server and client validation
logic directly — no Anvil runtime required. The genuinely reusable part
is the `_load_module()` technique at the top: it loads a `.py` file from
disk via `importlib`, bypassing Anvil's own import machinery entirely.
This is the real, non-obvious trick that makes fast, local, Anvil-aware
testing possible at all — worth understanding and reusing, not just the
individual test cases underneath it.

The individual tests are also worth reading as *examples of thoroughness*
— several test genuinely adversarial input (a null byte inside an email
address, a newline injected into a field) rather than just the happy
path.

### `1.2-test-local-run.yaml`
Kept for its **categorization taxonomy**, not its data. Every test in
this file is tagged one of: `happy_path`, `edge_case`, `boundary`, or
`adversarial`. That's a real, useful, systematic way to check whether a
function's test coverage is actually complete — a checklist to run
against any new function, not just this one. The specific PASS/FAIL
values recorded here are from one specific run in March and have no
ongoing meaning; ignore them.

Also confirms the real, working invocation:
```
pytest -v --import-mode=importlib tests/test_1.2_auth.py
```
The `--import-mode=importlib` flag matters — it's what makes the
`_load_module()` technique above actually work correctly.

### The eleven check-criteria files
([[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/security|Security Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/security.md), [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/m3-compliance|M3 Compliance Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/m3-compliance.md), [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/data-integrity|Data Integrity Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/data-integrity.md),
[[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/error-handling|Error Handling Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/error-handling.md), [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/response-envelope|Response Envelope Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/response-envelope.md), [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/data-binding|Data Binding Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/data-binding.md),
[[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/naming-conventions|Naming Conventions Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/naming-conventions.md), `navigation.md`, [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/compliance|Compliance Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/compliance.md),
[[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/code-quality|Code Quality Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/code-quality.md), [[[pdlf:pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/test-coverage|Test Coverage Check]]](C:/pdlf/pdlf-library/docs-local/pdlf-testing-seed-material/ci-based-checks-format/checks/test-coverage.md))

Real, specific, hand-written pass/fail criteria for an Anvil + M3
application, written from direct experience — not generic advice.
Several of these independently arrived at security and design patterns
that later turned out to be correct and important on their own merits —
most notably: **derive user identity from `anvil.users.get_user()`
server-side, never trust a client-supplied identifier** — the exact same
principle that PDLF's own Sentinel system uses today as a named threat
model ([[[default:security-global/threat-models/sec-broken-access-control-within-instance|Broken Access Control Within a Client Instance]]](C:/dev/project-library-global/security-global/threat-models/sec-broken-access-control-within-instance.md)). That's real
convergent evidence this isn't boilerplate.

These are written for MB-3-CS's specific file structure and are **not**
directly portable to PDLF as-is — PDLF's structure is different. Read
them as source material for extracting real *criteria* and *patterns*,
not as a checklist to copy-paste wholesale.

---

## How to actually use this, when the time comes

1. **Don't start from a blank page.** When building PDLF's testing
   system, read this folder first — the taxonomy, the import technique,
   and the specific Anvil/M3 pass/fail criteria are a real head start,
   not just historical curiosity.
2. **Extract patterns, not files.** The eleven criteria files are
   MB-3-CS-shaped. Pull out the *underlying rule* (e.g. "identity is
   always server-derived, never client-supplied") and re-express it in
   whatever form PDLF's real testing system ends up taking — don't just
   drop these files in unchanged.
3. **Reuse the taxonomy directly.** `happy_path` / `edge_case` /
   `boundary` / `adversarial` is a genuinely good, minimal coverage
   checklist — apply it to PDLF's own test design from day one, rather
   than reinventing a categorization scheme.
4. **Reuse the `_load_module()` technique directly**, if PDLF's own
   testing approach also needs to test Anvil-context code without a full
   Anvil runtime — it's already proven to work.

---

*The standing task this folder exists to support is item 9 on the PDLF
to-do list, tracked in the developer's operating documents.*
