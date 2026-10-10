---
title: "workflow"
doc-id: "mb-64817b10"
updated: "2026-10-10"
---
# Workflow (Steps, 11–46)

Steps 1 to 10 Or out of scope reserved for a different purpose 
This workflow starts with step 11 as the first step 
Task execution sequence for every step in the PDLF pipeline. Expanded from stepwise files.

---

### Step 11 — Init

1. Verify Postgres ledger reachable — Confirm `pdlf` database and all six tables exist
2. Register GBrain doc source — `gbrain sources add <slug> --path <project-library>` + sync
3. Register GBrain code source — `gbrain sources add <slug>-code --path <code-repo>` + sync
4. Embed GBrain — `gbrain embed --stale` on both sources
5. Check git remote on project-library repo — Ask developer if missing
6. Check git remote on code repo — Ask developer if missing
7. Check AGENTS.md in project-library — Create from template if missing
8. Create full folder structure — Fetch template from `C:\dev\project-template\dev-(SLUG)\project-library\`, apply slug substitutions
9. Initialize project-library repo — `git init`, add all files, commit
10. Initialize code repo — Confirm git remote connected, commit scaffold files
11. Push both repos to GitHub
12. Insert `projects` row in Postgres ledger
13. Add entry to registry — `/mnt/c/pdlf/registry/projects.json`
14. Write Step 11 ledger row — `completed_at`
15. Generate Step Receipt — `<project-library>/pdlf/outputs/step-11-receipt.md`
16. Run GStack `/sync-gbrain` — Index both repos in GBrain
17. Follow execution sequence — per `specifications-local/spec-execution-discipline.md`
18. Apply BFT — Full level

### Step 12 — /office-hours (GStack, conditional)

1. Query GBrain — Context relevant to product ideation
2. Read pre-project docs — `01-project-brief.md`, `02-scoping-ideas.md`, `03-constraints-and-notes.md`
3. Present yes/no decision — "Run `/office-hours`?"
   - Branch A (no): OpenCode synthesizes design doc from pre-project docs; save to `<project-library>/docs-local/design-doc.md`; record `synthesized = true`
   - Branch B (yes): Pre-load pre-project docs into prompt; invoke GStack `/office-hours`; capture output path; copy to `<project-library>/docs-local/design-doc.md`; record `synthesized = false`
4. Verify output exists — `<project-library>/docs-local/design-doc.md` must be present; STOP if missing
5. Write Step 12 ledger row — `completed_at`, `synthesized` flag, `artifact_path`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-12-receipt.md`
7. Apply BFT — Full level
8. Follow execution sequence — Housekeeping questions, stop, wait for continue

### Step 13 — to-spec (Matt Pocock)
**Removed 2026-08-11.** Original content archived to `obsolete/workflow-steps-13-and-25-removed.md`. Reason: `to-spec` was removed from the live PDLF pipeline per `spec-bft.md`'s 2026-07-18 correction — no confirmed downstream consumer.
### Step 14 — /plan-ceo-review (GStack)

1. Query GBrain — Context relevant to scope and strategy review
2. Check Step 12 `synthesized` flag — Note for INPUT NOTICE if `true`
3. Read Step 13 spec into context — `<project-library>/matt-skills-output/step-13-spec.md`
4. Determine branch from Step 12 state
   - Branch A (`synthesized = true`): No GStack design doc exists; `/plan-ceo-review` will print "No design doc found"; skip `/office-hours` offer; proceed with review
   - Branch B (`synthesized = false`): GStack finds design doc automatically at canonical path
5. Invoke GStack `/plan-ceo-review` — Runs pre-review audit, Step 0 (premise challenge, mode selection), 11-section deep review
6. Capture plan file path — Written to `~/.gstack/projects/{slug}/ceo-plans/{date}-{feature-slug}.md`
7. Copy to `gstack-outputs/` — `step-14-ceo-plan.md`
8. Verify outputs — Plan file at GStack canonical path, copy at `gstack-outputs/`; STOP if missing
9. Write Step 14 ledger row — `completed_at`, `artifact_path` = GStack plan file path
10. Generate Step Receipt — `<project-library>/pdlf/outputs/step-14-receipt.md`
11. Apply BFT — Full level
12. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 15 — /plan-eng-review (GStack)

1. Query GBrain — Context relevant to engineering review
2. Check Step 12 `synthesized` flag — Note for INPUT NOTICE if `true`
3. Read plan file — GStack finds CEO plan automatically at canonical path
4. Ensure design doc and spec are in context
5. Invoke GStack `/plan-eng-review` — Locks architecture, data flow, edge cases, test coverage
6. Capture TDD document cluster — `architecture.md`, `integration-architecture.md`, `security-architecture-canonical.md`, `globals-contract.md`, `authoritative-schema.md`
7. Capture test specification — Happy-path E2E specs, edge cases, error paths, RBAC matrix
8. Capture GSTACK REVIEW REPORT — Appended to plan file
9. Copy updated plan file to `gstack-outputs/` — `step-14-ceo-plan.md` (updated)
10. Verify outputs — TDD cluster documents, review report appended, test specification present; STOP if missing
11. Write Step 15 ledger row — `completed_at`
12. Generate Step Receipt — `<project-library>/pdlf/outputs/step-15-receipt.md`
13. Apply BFT — Full level
14. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 16 — domain-modeling (Matt Pocock)

1. Query GBrain — Context relevant to domain modeling
2. Invoke Matt `domain-modeling` — Captures glossary terms in CONTEXT.md, writes numbered ADRs
3. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
4. Gate: `domain-locked` — Full BFT, gate summary, developer approval required to proceed beyond Phase A
5. Write Step 16 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-16-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 17 — Create Anvil Data Tables (Manual)

1. Query GBrain — Context relevant to schema construction
2. Developer: Build data tables/schema in Anvil IDE — Per ADRs and authoritative schema from Steps 15–16
3. Verify tables exist — STOP if missing
4. Write Step 17 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-17-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 18 — Pull to Local (Manual)

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Updated schema from Step 17
3. Verify local repo updated — STOP if schema not present
4. Write Step 18 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-18-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 19 — to-tickets (Matt Pocock)

1. Query GBrain — Context relevant to issue decomposition
2. Read Step 13 spec — `<project-library>/matt-skills-output/step-13-spec.md` and GitHub issue
3. Read Step 14 CEO plan — `<project-library>/gstack-outputs/step-14-ceo-plan.md` (refined by Step 15)
4. Read CONTEXT.md + ADRs from Step 16
5. Confirm issue tracker config — From `/setup-matt-pocock-skills`
6. Invoke Matt `to-tickets` — Breaks spec into tracer-bullet issues in dependency order
7. Verify outputs — Issues published to project issue tracker; STOP if missing
8. Write Step 19 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-19-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 20 — /design-consultation (GStack)

1. Query GBrain — Context relevant to design system
2. Check test-mode flag — Present abbreviation offer (full/abbreviate/skip) if in test mode
3. Invoke GStack `/design-consultation` — Researches landscape, builds DESIGN.md + preview page
4. Verify outputs — DESIGN.md written, font/color preview page, design tokens; STOP if missing
5. Write Step 20 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-20-receipt.md`
7. Apply BFT — Full level
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 21 — Concept Sanity Audit (OpenCode)

1. Query GBrain — Context relevant to cross-artifact consistency
2. Read all Phase A+B outputs — spec (Step 13), CEO review (Step 14), Eng review (Step 15), CONTEXT.md + ADRs (Step 16), DESIGN.md (Step 20)
3. Cross-reference each document pair for contradictions
4. Produce audit report — What was checked, findings, discrepancies, verdict
5. Save audit report — `<project-library>/pdlf/step-21-concept-audit.md`
6. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
7. Gate: `concept-locked` — Full BFT, gate summary, developer approval required; no new feature without formal gate reopening
8. Write Step 21 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-21-receipt.md`
10. Apply BFT — Full (gate override)
11. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 22 — Wireframe Phase 1 (Claude Wireframe Skill)

1. Query GBrain — Context relevant to wireframe generation
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 1: 5 B&W UX wireframe approaches
3. Verify outputs — `wireframe/brain/design-context.md`, `design-taste.md`, `wireframe/DDMM-{feature}/index.html` + `styles.css`; STOP if missing
4. Write Step 22 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-22-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 23 — /plan-design-review (GStack)

1. Query GBrain — Context relevant to design review
2. Invoke GStack `/plan-design-review` — Rates UX dimensions 0–10, identifies gaps
3. Verify outputs — GSTACK REVIEW REPORT appended to plan file; STOP if missing
4. Write Step 23 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-23-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 24 — /plan-devex-review (GStack)

1. Query GBrain — Context relevant to developer experience review
2. Invoke GStack `/plan-devex-review` — Reviews API/CLI/SDK friction points and onboarding time
3. Verify outputs — DX scorecard appended to plan file; STOP if missing
4. Write Step 24 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-24-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 25 — prototype (Matt Pocock, optional)
**Removed 2026-08-11.** Original content archived to `obsolete/workflow-steps-13-and-25-removed.md`. Reason: `prototype` was removed from the live PDLF pipeline per `spec-bft.md`'s 2026-07-18 correction.
### Step 26 — Wireframe Phase 2 (Claude Wireframe Skill)

1. Query GBrain — Context relevant to wireframe refinement
2. Invoke Claude Wireframe Skill (Magdoub) — Phase 2: Clean + Polished color variants
3. Verify outputs — `styles-opt1.css` through `styles-opt5.css`; STOP if missing
4. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
5. Gate: `wireframes-approved` — Full BFT, gate summary, developer approval required to proceed beyond Phase B
6. Write Step 26 ledger row — `completed_at`
7. Generate Step Receipt — `<project-library>/pdlf/outputs/step-26-receipt.md`
8. Apply BFT — Full (gate override)
9. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 27 — Screen Production (OpenCode, deferred)

1. Query GBrain — Context relevant to screen production
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Produce screen HTML from approved wireframe (Step 26)
4. Apply wireframe fidelity checklist
5. Apply screen standard compliance checklist
6. Verify outputs — Screen HTML, both checklists; STOP if missing
7. Write Step 27 ledger row — `completed_at` (or `deferred`)
8. Generate Step Receipt — `<project-library>/pdlf/outputs/step-27-receipt.md`
9. Apply BFT — Full level (if active)
10. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 28 — Screen to PNG (External tool, deferred)

1. Query GBrain — Context relevant to screen conversion
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Convert screen HTML from Step 27 to PNG via external rendering tool
4. Verify output — Screen PNG in same folder as Step 27; STOP if missing
5. Write Step 28 ledger row — `completed_at` (or `deferred`)
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-28-receipt.md`
7. Apply BFT — None
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 29 — Build UI Forms (Manual, Anvil IDE)

1. Query GBrain — Context relevant to UI form construction
2. Developer + Anvil AI: Build UI forms in Anvil IDE — From approved wireframes and screens
3. Verify forms exist in Anvil IDE — STOP if missing
4. Write Step 29 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-29-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 30 — Pull to Local (Manual)

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Component tree with Anvil AI's wiring
3. Verify local repo updated — STOP if UI forms not present
4. Write Step 30 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-30-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 31 — Scaffold Planning (OpenCode)

1. Query GBrain — Context relevant to module/function structure planning
2. Review Step 15/16 architecture and domain model — TDD cluster, CONTEXT.md, ADRs
3. Review Step 30 pulled UI form structure
4. Review Step 21 concept audit report
5. Plan module/function structure — Determine what stubs to create
6. Write `scaffold-plan.md` — Saved to `<project-library>/`
7. Verify output — `scaffold-plan.md` exists; STOP if missing
8. Write Step 31 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-31-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 32 — Physical Scaffold Build (Manual, Anvil IDE)

1. Query GBrain — Context relevant to scaffold construction
2. Developer: Create empty client-code modules and server modules/functions in Anvil IDE — Per `scaffold-plan.md`
3. Verify stubs exist in Anvil IDE — STOP if missing
4. Write Step 32 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-32-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 33 — Pull to Local (Manual)

1. Query GBrain — Context relevant to codebase state
2. Pull Anvil-connected code repo to local — Scaffold structure
3. Verify local repo updated — STOP if stubs not present
4. Write Step 33 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-33-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 34 — Architectural Sanity Audit (OpenCode)

1. Query GBrain — Context relevant to architecture verification
2. Compare actual Anvil data tables against ADRs and domain model — Every table/column traces to a locked decision
3. Compare actual UI forms against approved screens and DESIGN.md
4. Compare actual scaffolding against `scaffold-plan.md` — Every planned module/function exists, nothing improvised
5. Check for drift — If found, correct Anvil-side artifact or formally update plan/ADR per deviation mechanism
6. Produce audit report — What was checked, findings, discrepancies, verdict
7. Save audit report — `<project-library>/pdlf/step-34-architecture-audit.md`
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `architecture-verified` — Full BFT, gate summary, developer approval required before any code-writing begins
10. Write Step 34 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-34-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 35 — Build Loop (OpenCode, per-feature)

For each issue from Step 19, in dependency order:

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
15. Decision point: More issues remain? Continue loop. All signed off? Exit loop
16. Follow execution sequence — Per cycle
17. Apply BFT — Full (per feature)

### Step 36 — /design-review (GStack)

1. Query GBrain — Context relevant to visual audit
2. Invoke GStack `/design-review` — 80-item live-site visual audit; before/after screenshots, atomic fix commits
3. Verify outputs — Design audit report, screenshots, fix commits; STOP if missing
4. Write Step 36 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-36-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 37 — /review (GStack)

1. Query GBrain — Context relevant to pre-landing code review
2. Invoke GStack `/review` — Finds bugs that pass CI but would break in production; auto-fixes obvious ones
3. Verify outputs — Review report, AUTO-FIXED commits; STOP if missing
4. Write Step 37 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-37-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 38 — /qa (GStack)

1. Query GBrain — Context relevant to QA testing
2. Invoke GStack `/qa` — Systematic QA testing; bug fixing; generates regression tests
3. Verify outputs — QA report with before/after screenshots, fix commits, regression test files; STOP if missing
4. Write Step 38 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-38-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 39 — triage (Matt Pocock)

1. Query GBrain — Context relevant to issue triage
2. Invoke Matt `triage` — Updates issue tracker: comments, labels, state changes, agent briefs
3. Verify outputs — Labels applied, comments added, briefs written; STOP if missing
4. Write Step 39 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-39-receipt.md`
6. Apply BFT — Light level

7. Follow execution sequence — Housekeeping, stop, wait for continue

> **Note:** `spec-gate-procedure.md` ties the `build-verified` gate to Step 39, not Step 40 as currently written below.

### Step 40 — improve-codebase-architecture (Matt Pocock, optional)

1. Query GBrain — Context relevant to architecture health scan
2. Present RUN/SKIP recommendation with justification
   - Branch RUN: Invoke Matt `improve-codebase-architecture` — Interactive HTML architecture report
   - Branch SKIP: Skip the scan
3. Execute gate procedure — Fires regardless of RUN/SKIP
4. Gate: `build-verified` — Full BFT, gate summary, developer approval required to proceed beyond Phase D
5. Write Step 40 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-40-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 41 — /ship (GStack, scope narrowed)

1. Query GBrain — Context relevant to ship readiness
2. Invoke GStack `/ship` — Tests, VERSION bump, CHANGELOG, commit, push; stops at push
3. Verify outputs — Merged base branch, tests pass, VERSION bumped, CHANGELOG updated, branch pushed; STOP if missing
4. Write Step 41 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-41-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 42 — Publish to Staging (Manual)

1. Query GBrain — Context relevant to staging deployment
2. Developer: Publish the pushed commit to Staging environment in Anvil IDE — Production untouched
3. Verify output — App running at Staging URL; STOP if not reachable
4. Write Step 42 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-42-receipt.md`
6. Apply BFT — None
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 43 — Staging Smoke Test (GStack)

1. Query GBrain — Context relevant to staging verification
2. Invoke GStack `/qa` or `/canary` — Retargeted at Staging URL from Step 42
3. Verify output — Smoke test report: pass/fail at Staging; STOP if failing
4. Write Step 43 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-43-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 44 — Promote to Production (Manual)

1. Query GBrain — Context relevant to production deployment
2. Developer: Promote the same reviewed commit from Staging to Production in Anvil IDE — Rollback is re-pointing, not `git revert`
3. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
4. Gate: `production-released` — Full BFT, gate summary, developer approval required; app is now live
5. Write Step 44 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-44-receipt.md`
7. Apply BFT — Full (gate override)
8. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 45 — /canary at Production (GStack)

1. Query GBrain — Context relevant to post-deploy monitoring
2. Invoke GStack `/canary` — Targeted at Production URL from Step 44; watches for console errors, performance regressions
3. Verify output — Canary report with initial health check; STOP if critical failures
4. Write Step 45 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-45-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue

### Step 46 — LEARN Junction (OpenCode)

1. Query GBrain — Context relevant to retrospective and learning
2. Invoke GStack `/retro` — Retrospective report
3. Invoke GStack `/learn` — Capture learnings
4. Invoke GStack `/context-save` — Persist working state
5. Update ISA — Fill Verification section, update Changelog
6. Update registry — `current_step: 46`, `last_gate: "released"`, `active: false`
7. Sync and embed GBrain — Learnings now searchable for next project
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `released` (jointly with Step 45) — Full BFT, gate summary, developer approval required to close the project cycle
10. Write Step 46 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-46-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop

---

### Skill Summary

| Step | Skill / Handler | Producer |
|---|---|---|
| 11 | Init | OpenCode |
| 12 | /office-hours (conditional) | GStack |
| 13 | to-spec | Matt Pocock |
| 14 | /plan-ceo-review | GStack |
| 15 | /plan-eng-review | GStack |
| 16 | domain-modeling | Matt Pocock |
| 17 | Create Anvil data tables | Manual |
| 18 | Pull to local | Manual |
| 19 | to-tickets | Matt Pocock |
| 20 | /design-consultation | GStack |
| 21 | Concept sanity audit | OpenCode |
| 22 | Wireframe Phase 1 | Claude Wireframe |
| 23 | /plan-design-review | GStack |
| 24 | /plan-devex-review | GStack |
| 25 | prototype (optional) | Matt Pocock |
| 26 | Wireframe Phase 2 | Claude Wireframe |
| 27 | Screen production (deferred) | OpenCode |
| 28 | Screen to PNG (deferred) | External tool |
| 29 | Build UI forms | Manual |
| 30 | Pull to local | Manual |
| 31 | Scaffold planning | OpenCode |
| 32 | Physical scaffold build | Manual |
| 33 | Pull to local | Manual |
| 34 | Architectural sanity audit | OpenCode |
| 35 | Build loop (per-feature) | OpenCode |
| 36 | /design-review | GStack |
| 37 | /review | GStack |
| 38 | /qa | GStack |
| 39 | triage | Matt Pocock |
| 40 | improve-codebase-architecture (optional) | Matt Pocock |
| 41 | /ship (scope narrowed) | GStack |
| 42 | Publish to Staging | Manual |
| 43 | Staging smoke test | GStack |
| 44 | Promote to Production | Manual |
| 45 | /canary at Production | GStack |
| 46 | LEARN junction | OpenCode |

---

*Skill Workflow Table v5 — Rewritten from stepwise files. Task-level expansion of the v4 step table. 2026-07-12.*
