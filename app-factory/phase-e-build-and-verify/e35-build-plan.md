---
title: "e35-build-plan"
doc-id: "mb-7c6d6f2b"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 35: Build

**Must achieve:** Builds one feature, tested at three levels: its logic alone, connected to the live Anvil app (with a backup before and after), and by hand in the browser. The developer signs the feature off.

**Carried out by:** OpenCode.

**Runs:** once per feature.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to this feature
2. Write the pure-logic function
3. Write Level 1 tests and run them locally
4. Decision point: Level 1 pass? Continue. Fail? Fix and retry
5. Create pre-integration backup
6. Write server-module (integration) wrapper
7. Write Level 2 tests
8. Push to Anvil — `git push` to branch, no auto-publish
9. Run Level 2 tests via Uplink against Development Environment
10. Decision point: Level 2 pass? Create post-success backup and continue. Fail? Restore from pre-integration backup, fix, retry
11. Pull repo back to local
12. Level 3: Manual/browser verification of complete feature
13. Decision point: Developer signoff on this feature
14. Generate Step Receipt for 35.N — `<project-library>/pdlf/outputs/step-35-{N}-receipt.md`
15. This feature is complete; the next feature starts again at Step 35 (the run plan governs the loop)
16. Follow execution sequence — Per cycle
17. Apply BFT — Full (per feature)

## From `spec-skill-design.md`: section 2.8

### 2.8 Feature-by-feature build loop for Step 35

**Decision:** Step 35 is not a single pass. It is a loop over each issue from Step 19 — one
build, test, and signoff cycle per feature. Each cycle gets its own `steps` row (35.1, 35.2...).

**Why:**
- Built on mb-3-cs's already-validated three-level testing methodology (pure logic → Uplink
  integration → manual verification), not invented for PDLF.
- The developer was emphatic: "code all in one" is "a really fast way to land in trouble...
  deep trouble that you cannot dig your way out of."
- Each signed-off feature is a known-good baseline. Later breakage is attributable to
  something done after signoff, not to the feature itself.
- Two backups per feature (pre-integration and post-success) — stricter than it looks, and
  deliberate.

**Rejected:** Building all features in one pass. The testing policy document is the detailed
specification.

**Addendum (2026-07-12):** The loop this section describes was found to have two structural
defects on review, both corrected: (1) the [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) skill and any
resulting remediation were being applied *after* the code-review/QA retest steps, meaning
shipped code could include unverified post-remediation changes — the `build-verified` gate
was moved from Step 40 to Step 39 and the loop reordered (35 → 35A → 40 → 40B → 36 → 37 →
38 → 38A → 39 → gate) so remediation is always retested before the gate. (2) Steps 37/38
(`/review`, [[[pdlf:app-factory/phase-e-build-and-verify/e38-reference|/qa]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-reference.md)) were assumed to persist their findings for Step 39 ([[[pdlf:app-factory/phase-e-build-and-verify/e39-reference|triage]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-reference.md)) to act on,
but GStack's own repository states this behavior is unverified even by the maintainer — both
steps now explicitly require writing to a specified artifact path, verified by OpenCode
before the step is marked complete, rather than relying on unconfirmed skill behavior.

## From `orchestrator-run-plan.md`: Step 35 feature loop

## Step 35 Feature Loop

Steps 35 through 39, including all lettered sub-steps, form a single loop that repeats
once per feature/package. A feature is not considered complete until it has passed
through the entire sequence below and reached `build-verified`.

```
Feature Cycle Entry (one per issue/ticket from Step 19)
  │
  ├── Step 35  — Build feature. Internal 3-level testing (pure logic →
  │              Uplink integration → manual verification), with a backup
  │              before and after the integration level.
  │
  ├── Step 35A — Testing: local-scope pip-audit (dev/test tooling only)
  │              + broader test coverage for this feature.
  │
  ├── Step 40  — Architecture scan (optional, read-only report) for this
  │              feature's code. Optional — RUN/SKIP decision per feature cycle.
  │
  ├── Step 40B — If Step 40 ran and produced findings: developer reviews
  │              and approves specific fixes. OpenCode applies only the
  │              approved fixes. Skipped entirely if Step 40 was skipped
  │              or produced no findings requiring action.
  │
  ├── Step 36  — Design review. Runs after remediation, not before —
  │              this retests the feature as it will actually ship.
  │
  ├── Step 37  — Code review. Must persist findings to
  │              step-37-findings.md, including a clean-pass statement.
  │
  ├── Step 38  — QA, cross-feature + regression. Must persist findings to
  │              step-38-findings.md, including a clean-pass statement.
  │
  ├── Step 38A — Capture Anvil's native pip-audit result for this cycle,
  │              if a server-environment rebuild occurred.
  │
  ├── Step 39  — Triage. Processes step-37/38-findings.md for this
  │              feature. build-verified gate evaluated here.
  │
  └── Gate: build-verified (evaluated for this feature only)
        ├── PASS → This feature is signed off. Record ledger row and
        │          Step Receipt for this cycle (e.g., 39.1, 39.2 ...).
        │          Return to Feature Cycle Entry for the next feature,
        │          OR — if this was the last feature — exit the loop.
        └── FAIL → Stop this feature's cycle, record blocker, do not
                   mark this feature signed off. Developer resolves,
                   re-enters the cycle at the failed step.
```

Each feature cycle produces its own ledger rows and Step Receipts for every step it
passes through, not one combined receipt for the whole loop. Do not proceed to the next
feature until the current one has reached a passed `build-verified` gate. A signed-off
feature is a known-good baseline. Step 41 is not reachable until every feature from
Step 19's ticket list has individually reached `build-verified`.

---
