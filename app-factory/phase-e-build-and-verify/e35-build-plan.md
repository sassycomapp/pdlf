---
title: "e35-build-plan"
doc-id: "mb-7c6d6f2b"
updated: "2026-11-13"
---
# Step 35 — Build: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`. Each ticket ends with the gate `build-verified` (Step 39).

#### Step 35: Build

**Must achieve:** one feature built and proven: its server code built test-first into the planned stubs, its forms built from their approved screen requirements and wired to that code, its rework items cleared and its old forms removed, and the whole feature proven at Levels 0 to 3 and signed off by David.

**Starts from:** the ticket; `scaffold-spec.md`; the approved screen requirements of the ticket's forms; the authoritative schema; the access matrix and the threat model; the test plan; the rework list and the disposition list; the app as verified at Step 34 or as left by the previous ticket.

**Produces:** the feature's server code, client modules and forms in the app; the forms' spec sheets in `theme\assets\docs\app{n}\`; the feature's tests in the app's `tests\`; the feature's entries in `access-matrix.yaml` and its phrase keys in `en.py`; the rework items of the ticket cleared; in `pdlf-outputs\e35\`: the review notes, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, in the order [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) section 4 sets, with the skills below; Anvil's agent wires the forms in the Anvil editor; Claude reviews the server code, the forms and the wiring through David; David commits, checks each form in Anvil and signs the feature off.

**Must be built so that:**
- the ticket, its approved screen requirements, the authoritative schema and the SRS are checked first and must still agree; a change to an approved screen requirement needs David's approval;
- every behaviour the ticket names is built test-first with `tdd` into the stub `scaffold-spec.md` planned for it, using `server-code`, `client-modules` and `data-models`; Level 1 tests the pure logic alone;
- the code stays inside the modules and seams `scaffold-spec.md` sets, as `codebase-design` holds it;
- the ticket's security acceptance criteria are built and tested with `secure-software-engineering`;
- every webhook stores its raw payload in the client's storage and an index row in the Data Tables, and is idempotent by transaction id; every outbound call retries with backoff when rate-limited; every state transition of a lifecycle has its test;
- any app setting the feature needs in `anvil.yaml` is changed only through `anvil-yaml`; a table the feature needs that does not exist returns the feature to Step 17;
- once the server code passes Levels 1 and 2 and Claude's review, `mb-form-builder` builds the ticket's forms from their approved screen requirements, following `client-forms`, and removes the old forms the ticket replaces;
- Anvil's agent fills only the empty event handlers, as each form's spec sheet states, and checks its own commit with `/review-commit`; Claude confirms only handler bodies changed;
- the rework items of the ticket on the rework list are cleared, and the modules the disposition list marks remove are removed;
- `anvil --json validate` and `ts_scan.py` pass after every change; Level 2 runs on the local runtime; Level 3 runs in the browser on hosted App {n} with `TEST_` data only, which is removed afterwards;
- a failing test at any level is diagnosed to its root cause with `diagnosing-bugs` before any fix, and the level runs again;
- `wizard` writes David's instructions for each commit, each check of a form in Anvil, and the Level 3 check;
- the agent never commits; David commits the documentation repositories with `commit-all` and the app with `git pull` followed by `gcp`;
- David signs the feature off against its ticket and its screen requirements (test BR-09);
- its ledger row carries the ticket, with `step_type = 'skill'`, `skill_family = 'opencode'`, `synthesized = false`, and `inputs_used` naming Step 34 or the previous ticket's Step 39.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md); [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md); [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md); [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `tdd` (Matt Pocock): every behaviour test-first → Levels 1 and 2, then Step 35A.
- `server-code`, `client-modules` and `data-models` (Anvil): the server code, client modules and data flow → Levels 1 and 2, then Step 37.
- `client-forms` (Anvil), through `mb-form-builder` (MyBizz): the forms from their approved screen requirements → Anvil's agent, then Step 36.
- `anvil-yaml` (Anvil): any app setting the feature needs → Level 2.
- `codebase-design` (Matt Pocock): the code inside its planned modules → Steps 37 and 40.
- `secure-software-engineering` (Magnus919): the ticket's security criteria built and tested → Step 37.
- `diagnosing-bugs` (Matt Pocock): the root cause of every failing test → the fix, then the level again.
- `wizard` (Matt Pocock): David's instructions for commits, form checks and Level 3 → the sign-off.
- `mb-sentinel-review`, High → `triage_findings`.

**Not used:** Matt Pocock's `implement`, because it commits its own work; agents never commit.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e35-test-spec|Step 35 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35-test-spec.md): the feature is built test-first, its forms match their approved screen requirements, it is proven at Levels 0 to 3, and David signs it off.

**Standards:** [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md); [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md); [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2, 3, 6 and 9; [[[default:specifications-global/spec-testing-methodology-standards|Testing Methodology Standards]]](C:/dev/project-library-global/specifications-global/spec-testing-methodology-standards.md).

## Why it is built this way

- **Server first, then forms.** Forms call server functions; building and proving those first means each form is wired to code that already works.
- **The approved design is built exactly.** `mb-form-builder` builds each form from its approved screen requirement, so the form David sees is the one he approved.
- **Each agent does what it does best.** OpenCode builds, Anvil's agent wires inside the editor it knows, and Claude reviews; no agent judges its own work.
- **Levels in order.** Each level tests only what the one before has proven, so a failure points to one place.
