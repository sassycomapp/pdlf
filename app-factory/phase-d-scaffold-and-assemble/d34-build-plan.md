---
title: "d34-build-plan"
doc-id: "mb-08fb22cb"
updated: "2026-11-12"
---
# Step 34 — Architecture Audit: Build Plan

## Step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (this step).

#### Step 34: Architecture audit

**Must achieve:** the physical app checked against every locked decision before any code is written: its tables against the authoritative schema and the data design, its structure against `scaffold-spec.md` and the architecture, its access and trust boundaries against the access matrix and the threat model, and the approved screen requirements against the planned functions; every fault corrected at its step or, in existing code, tied to the ticket that removes it; and the result locked by David at the gate `architecture-verified`, so that the build loop builds on a verified skeleton; Phase D closed.

**Starts from:** the app as pulled at Step 33; `scaffold-spec.md`, the disposition list and the stub list; the authoritative schema; the reviewed plan with its architecture, data design and Step 15's architecture diagram; the access matrix and the threat model with its plan of security assessments; the approved screen requirements and the requirement index; the Step Receipts of Steps 31 to 33.

**Produces:** the architecture audit report; the rework list of an existing app, each fault with its ticket; the `gates` row of `architecture-verified`; in `pdlf-outputs\d34\`: the report, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with `graphify`, Anvil's `data-models`, Magnus919's `secure-software-engineering` and `security-audit-methodology`, GStack's `/cso` and `mb-sentinel-review`. David decides each finding he is asked about and passes or blocks the gate.

**Must be built so that:**
- `anvil --json validate .` passes over the whole app, and `ts_scan.py` runs every static check, ST-02 to ST-12, with bandit, pip-audit and `/cso` for ST-13;
- `data-models` checks the tables, model classes and client access against the authoritative schema and the data design;
- `graphify` builds the app's code graph, which is compared with `scaffold-spec.md` and Step 15's architecture diagram: every module and function traces to the plan, and nothing exists that the plan does not name;
- every server function a screen requirement names exists as a stub with the access rule the access matrix gives it;
- `secure-software-engineering` verifies the skeleton against every trust boundary of the threat model (test DC-06), and `security-audit-methodology` runs the architecture part of Step 15's plan of security assessments;
- the skeleton is checked against [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md) (test DC-08), and App 3 is confirmed to need no code of its own;
- a fault in what PDLF built (the tables, `scaffold-spec.md`, a stub) is corrected at its step, and that step's checks run again;
- for an existing app, a fault in existing code or in an existing form is accepted only when it is on the rework list with the ticket whose build removes it, and that ticket's module or form is marked rework or remove in the disposition list; any other fault blocks the gate;
- `mb-sentinel-review` runs at Very High scrutiny on the audit; a Flag or Escalate stops the step and goes to David; no finding may be open at the gate;
- before the gate, the receipts of Steps 31 to 33 of the run match their evidence (test PR-05);
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, and the agent reads the row; the agent never writes it;
- after the gate, the structure changes only through a deviation David authorises;
- it hands to Phase E the verified app, `scaffold-spec.md`, the rework list, the approved screen requirements and the tickets;
- its ledger row is `step_type = 'gate'`, `skill_family = 'opencode'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 31 to 33.

**BFT level:** Full (gate).

**Gate:** `architecture-verified`: the app's tables, structure and access are verified against the locked decisions; coding may begin.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `graphify`: the app's code graph → the comparison with `scaffold-spec.md` and the architecture diagram, then Steps 35 and 40.
- `data-models` (Anvil): tables, model classes and client access checked → the audit report.
- `secure-software-engineering` (Magnus919): the skeleton against the trust boundaries → the audit report.
- `security-audit-methodology` (Magnus919): the architecture part of the security assessment plan → the audit report.
- `/cso` (GStack): the security scan of the skeleton → test ST-13, the audit report.
- `mb-sentinel-review`, Very High → `triage_findings`; an open finding blocks the gate.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d34-test-spec|Step 34 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d34-test-spec.md): the skeleton passes every static check, traces to the locked decisions and implements the threat model's controls, and the gate has David's approval.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md); [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md); [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md).

## Why it is built this way

- **Verify before code.** A wrong table, a missing access rule or an unplanned module costs little to fix now and a great deal once code is built on it.
- **Every decision checked.** Tables, structure, access, trust boundaries and screens are each checked against the document that locked them, so no drift passes the gate.
- **Existing apps without a free pass.** Old code may fail today's rules only where a named ticket will replace it; nothing else gets through.
- **David passes the gate.** Coding starts only on his yes.
