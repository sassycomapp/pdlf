---
title: "d34-config"
doc-id: "mb-192abeee"
updated: "2026-11-12"
---
# Step 34 — Architecture Audit: Configuration

The fixed values of Step 34. Agent-facing. What the agent does, in order: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-reference|Step 34 Reference]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-reference.md). What the step is and why: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-explainer|Step 34 Explainer]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-explainer.md). What it must prove: [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-test-spec|Step 34 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-test-spec.md).

## Identity

| Item | Value |
|---|---|
| Step | 34, Architecture audit |
| Phase | D, Scaffold and Assemble; the last step of the phase |
| Carried out by | OpenCode, with the skills below; David decides findings and answers the gate |
| Runs for | Every run that reached Step 33 |
| Previous step | 33 |
| Next step | 35, the first step of Phase E |
| Gate | `architecture-verified` ([[[pdlf:pdlf-library/specifications-local/spec-gate-procedure\|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)) |
| BFT level | Full (gate) |
| Sentinel scrutiny | Very High |
| Conditional | No; the rework list only for an existing app |

## Inputs

| Input | Where |
|---|---|
| The app, as pulled | `C:\dev\dev-{slug}\{slug}-app{n}` |
| Scaffold specification | `{slug}-project-library\docs-standard-local\scaffold-spec.md` |
| Disposition list and stub list | `{slug}-project-library\pdlf-outputs\d31\`; `pdlf-outputs\d32\` |
| Authoritative schema | `{slug}-project-library\docs-standard-local\authoritative-schema.md` |
| Reviewed plan and architecture diagram | `{slug}-project-library\docs-local\design\{run}\design-doc.md`; `pdlf-outputs\b15\{slug}-b15-{run}-architecture.*` |
| Access matrix and threat model | `{slug}-project-library\docs-local\design\app{n}\` |
| Approved screen requirements and index | `{slug}-project-library\ui\`; `pdlf-outputs\c22\{slug}-c22-{run}-requirement-index.md` |
| Receipts of Steps 31 to 33 | `{slug}-project-library\pdlf-outputs\d31\` to `d33\` |

## Checks

| Check | By | Pass when |
|---|---|---|
| Validate | `anvil --json validate .` | No error |
| Static checks | `ts_scan.py`; bandit, pip-audit, `/cso` | ST-02 to ST-13 pass, or each failure in existing code is on the rework list |
| Tables | `data-models` | Tables, model classes and client access equal the authoritative schema and the data design |
| Structure | `graphify` | Every module and function traces to `scaffold-spec.md` and the architecture diagram; nothing unplanned |
| Screens | OpenCode | Every server function a screen requirement names exists, with its access rule |
| Trust boundaries | `secure-software-engineering` | Every boundary's control exists in the skeleton (DC-06) |
| Security assessment | `security-audit-methodology` | The architecture part of Step 15's plan passes |
| Common aspects | OpenCode | Each common aspect is met or has its ADR; App 3 needs no code (DC-08) |
| Receipts | `ts_report.py --check` | The receipts of Steps 31 to 33 match their evidence (PR-05) |

## Fault handling

| Fault in | Handling |
|---|---|
| What PDLF built: tables, `scaffold-spec.md`, a stub | Corrected at its step; that step's checks run again |
| Existing code or an existing form of an existing app | On the rework list with its ticket, and marked rework or remove in the disposition list; otherwise it blocks the gate |

## Outputs

| Output | Where |
|---|---|
| Audit report | `pdlf-outputs\d34\{slug}-d34-{run}-architecture-audit.md`: each check, its evidence, each finding and its handling, the verdict |
| Rework list, existing app | `pdlf-outputs\d34\{slug}-d34-{run}-rework.md`: each accepted fault, its file and its ticket |
| Test results | `pdlf-outputs\d34\{slug}-d34-{run}-checks.xml`; the scanner report `{slug}-d34-{run}-ts-scan.xml` |
| Step Receipt | `pdlf-outputs\d34\{slug}-d34-{run}-receipt.md` |
| Ledger | the Step 34 `steps` row; the `gates` row of `architecture-verified`; its BFT record; its `triage_findings` row |

All paths without a repository name are inside `{slug}-project-library\`.

## Gate summary block

```
██████████████████████████████████████████████
█  GATE — architecture-verified
█
█  Step: 34   Run: {run}   BFT: Full — all six passed
█  Audit: every check passed; {n} faults on the rework list
█  Sentinel: Very High, no open finding
█  Locks: the tables, the structure, access and trust boundaries
█
█  Proceed to the build loop? (yes/no)
██████████████████████████████████████████████
```

## Hand-over to Phase E

| Item | Where |
|---|---|
| The verified app | `{slug}-app{n}` |
| Scaffold specification | `docs-standard-local\scaffold-spec.md` |
| Rework list | `pdlf-outputs\d34\{slug}-d34-{run}-rework.md` |
| Approved screen requirements | `ui\` |
| Tickets | `pdlf-tickets\{run}\` |
| Step Receipt | `pdlf-outputs\d34\{slug}-d34-{run}-receipt.md` |

## Ledger values

| Column | Value |
|---|---|
| `step_number` | `34` |
| `step_type` | `gate` |
| `skill_family` | `opencode` |
| `run` | From the entry record |
| `app_number` | From the entry record |
| `status` | `complete` after the gate passes; `blocked` when David says no |
| `synthesized` | `false` |
| `artifact_path` | `pdlf-outputs\d34\{slug}-d34-{run}-architecture-audit.md` |
| `inputs_used` | Steps 31 to 33 |
| `gates` row | Written by David with `bash /mnt/c/mybizz/scripts/pdlf-gate.sh {slug} architecture-verified {run}`; the agent only reads it |
