---
title: "35-build-loop"
doc-id: "mb-60eeebb6"
updated: "2026-10-11"
---
## Task Execution Order

For each issue from Step 19, in dependency order:

1. Write the pure-logic function
2. Write Level 1 tests and run them locally
3. → Decision point: Level 1 pass? continue. fail? fix and retry.
4. Create pre-integration backup
5. Write server-module (integration) wrapper
6. Write Level 2 tests
7. Push to Anvil (git push to branch — no auto-publish)
8. Run Level 2 tests via Uplink against Development Environment
9. → Decision point: Level 2 pass? create post-success backup and continue. fail? restore from pre-integration backup, fix, retry.
10. Pull the repo back to local
11. Level 3: manual/browser verification of complete feature
12. → Decision point: Developer signoff on this feature
13. Generate Step Receipt for 35.N
14. → Decision point: More issues remain? continue loop. All signed off? exit loop.
15. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) (per cycle)
16. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full per feature)

---

## Description

Iterates over each issue from Step 19. One build, test, and signoff cycle per
feature. Each cycle gets its own `steps` row (35.1, 35.2...). Built on mb-3-cs's
validated three-level testing methodology.

## Inputs Required (Per Feature Cycle)

- The individual issue from Step 19
- Plan file (Steps 14–15, 23–24 review reports)
- Step 20 DESIGN.md
- Step 26 approved wireframes/screens
- Step 16 CONTEXT.md + ADRs
- Step 17 Anvil data tables
- Step 29 Anvil UI forms
- Step 31/32 scaffolding

## Outputs (Per Feature Cycle)

- Production code written into the Anvil app/repo
- Level 1 tests (pure logic) — run and pass
- Pre-integration backup
- Level 2 tests (Uplink integration) — run and pass
- Post-success backup
- Level 3 verification (manual/browser)
- Signoff — this feature is a known-good baseline
- Step Receipt for 35.N

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 35 | Agent loop | | OpenCode `/build`, feature-by-feature |

## Feature-by-Feature Build Loop

Step 35 is not a single ledger row — it is a loop over the issues produced at Step
19, one build-test-signoff cycle per feature. Full mechanics: [[[pdlf:pdlf-library/policy-local/pol-testing-and-quality|Policy: Testing and Quality]]](C:/pdlf/pdlf-library/policy-local/pol-testing-and-quality.md).

Each cycle gets its own `steps` row, numbered `35.1`, `35.2`, etc. Each cycle produces
its own Step Receipt, asks the two housekeeping questions, and stops for "continue."
The loop does not collapse the per-step stop discipline.

Do not proceed to the next feature until the current one is signed off. A signed-off
feature is a known-good baseline — later breakage is attributable to something done
after signoff, not to the feature itself.

## Test Plan Production

Steps 14–15 jointly produce the test plan consumed by Steps 35 and 38.

## Reference Files

| `policy-local/pol-testing-and-quality.md` | Step 35 (the build loop) |
| [[[pdlf:pdlf-library/templates-local/isa-template-v2\|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md) | Steps 26, 35, 38, 46 |
| Standards Library | Step 35 (testing methodology) |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.

- Feature loop cycle skipped or collapsed: one row per feature cycle, no exceptions.
