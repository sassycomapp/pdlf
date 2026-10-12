---
title: "pol-testing-and-quality"
doc-id: "mb-6296454f"
updated: "2026-10-12"
---
# PDLF Policy — Testing and Quality

**Binding.** The agent must comply during Step 35 (build loop) through Step 39 (triage) and the
`build-verified` gate. No exceptions without a deviation request.

---

## What

### Three-level testing methodology

Every feature built in Step 35 passes through three testing levels in strict sequence:

| Level | Scope | Precondition |
|---|---|---|
| 1 — Pure logic | Local Python, no Anvil imports, fully deterministic | None — written first, run constantly |
| 2 — Uplink integration | Local Python + live Anvil via Uplink, server-side only | Level 1 passes + pre-integration backup created |
| 3 — Manual verification | Browser-based, complete feature | Levels 1 and 2 pass |

Level 2 tests use the **Development Environment's** Uplink key (not Staging). The Development
Environment auto-tracks the latest code and has its own Uplink keys — no manual publish is
needed per feature cycle. The formal Staging publish is a single event at Step 42.

### Two backups per feature

- **Pre-integration backup:** before any integration code touches the live app (before Level 2). Protects against the integration attempt itself going wrong.
- **Post-success backup:** after Level 2 passes and before Level 3. The known-good checkpoint.

Never skip either backup. "One backup after testing passes" is insufficient — the first backup
is the safety net for the integration attempt that produces the second.

### Feature signoff

A feature is not complete until the entire loop below is passed and the developer signs off.
After signoff:

- The feature is a **known-good baseline**. Later breakage is attributable to something done
  after this point, not to this feature.
- The Step Receipt records the signoff.
- Proceed to the next feature only after signoff.

### Pure logic modules

A Pure Logic Module has zero `import anvil` statements, no Data Tables access, no server calls,
no side effects, and is fully deterministic. Server Modules are thin wrappers around Pure Logic
Modules — they handle auth and persistence; the pure module handles the business rule. This is
not a style preference. It is what makes Level 1 testing possible.

### Uplink rules

- Always use a Server Uplink key (not Client) for server-side integration testing.
- Never hardcode the Uplink key — read from environment variable.
- Always disconnect after the operation.
- Restart the Anvil server runtime after Designer changes, before the next Uplink test.
- Mark test data with `source='Test'` and verify cleanup.

### Full per-feature loop (corrected 2026-07-12)

Step 35's three-level testing is the start of a larger per-feature loop, not the whole of it.
The full sequence, in order:

```
35  — Build feature. Three-level testing (above), two backups.
35A — Testing: CI checks + broader test coverage.
40  — Architecture scan (optional, read-only report).
40B — Apply developer-approved remediation from Step 40, if any.
36  — /design-review — retest, post-remediation.
37  — /review — structural code review.
38  — /qa — functional + regression testing.
38A — CI/pipeline results consolidated.
39  — triage — processes findings from 36–38. build-verified gate evaluated here.
```

Remediation (40B) is retested by 36–38, not shipped straight through — this is why the
`build-verified` gate sits at 39, after the retest, and not at 40, before it.

### Artifact persistence requirement (new, 2026-07-12)

`/review` (Step 37) and [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md) (Step 38) are **required** to write their findings to a
specified artifact path as part of invocation — this is not assumed to happen as a side
effect of running the skill. OpenCode verifies the artifact exists before marking either
step complete; its absence is a step failure requiring developer attention, not a silent
pass. This requirement exists because GStack's own repository states that its skills'
claimed persistence behavior is unverified even by the maintainer — it cannot be relied on
without an explicit check.

---

## Why

Built on mb-3-cs's already-validated testing methodology — not invented for PDLF. The developer
was emphatic: "code all in one" is "a really fast way to land in trouble... deep trouble that
you cannot dig your way out of." Two backups per feature is stricter than it looks and
deliberate: the pre-integration backup protects against the integration attempt itself.

The loop reorder and artifact-persistence requirement (2026-07-12) both close a real gap: the
original sequence let unverified remediation ship, and let review/QA findings go unrecorded
by assumption rather than by confirmed behavior.

---

## Where

Steps 35 through 39, and the `build-verified` gate. This policy is itself the detailed
reference — there is no separate mechanics file. An earlier reference to
`stepwise/step-16-testing-policy.md` was removed 2026-07-18: Step 16 is domain modeling,
not testing — this pointer predated a renumbering and was never corrected. Investigated
and confirmed no such file was ever created; its intended content already lives here.

**Runnable checklists (added 2026-07-18):**
- [[[pdlf:pdlf-library/templates-local/chk-pdlf-self-test|PDLF Self-Test Checklist]]](C:/pdlf/pdlf-library/templates-local/chk-pdlf-self-test.md) — tests PDLF's own orchestration (execution
  discipline, gate integrity, ledger schema, skill invocation correctness, documentation
  consistency, deviation mechanism). Not about testing an Anvil app — about testing PDLF
  itself.
- The earlier `chk-anvil-app-testing.md` (MB-3-CS era) — operationalized this policy's content (and
  [[[default:specifications-global/spec-testing-methodology-standards|Testing Methodology]]](C:/dev/project-library-global/specifications-global/spec-testing-methodology-standards.md)) into runnable pass/fail
  items for testing an Anvil app PDLF builds. Retired; no longer on disk anywhere
  (verified 2026-09-18). Sections 1–3 restated what this policy already
  covers as checklist items; Sections 4–5 (Test Plan Shape, RBAC Verification) are content
  this policy doesn't yet have locally — the description above is now the only surviving
  record of that shape. Related preserved source material: `docs-local/pdlf-testing-seed-material/`.

**Deferred, not yet done:** integrating the retired chk-anvil-app-testing.md's checks (file
gone; its Sections 4–5 shape survives only in the description above) directly into
Steps 35A, 36, 37, 38, and 39 themselves, so running those steps actually exercises the
checklist rather than the checklist sitting separately from the pipeline. Addressed when
Phase E is reached.

**Source:** [[[pdlf:pdlf-library/specifications-local/spec-skill-design|Spec: Skill Design]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-design.md) §2.8, §2.6.
