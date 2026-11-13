---
title: "e37-build-plan"
doc-id: "mb-78301dea"
updated: "2026-11-13"
---
# Step 37 — Code Review: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 37: Code review

**Must achieve:** the feature's changes reviewed for bugs that would break in use and for every standard they must meet: its code against the Anvil skills' rules, `project-library-global` and its ticket; its forms and spec sheets against their approved screen requirements; its security by a separate review; with every finding recorded and a clean-pass statement when there is none.

**Starts from:** the feature's changes since the previous ticket's gate; the ticket; `scaffold-spec.md`; the approved screen requirements; the test plan.

**Produces:** the code findings; in `pdlf-outputs\e37\`: the findings, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with Matt Pocock's `code-review`, GStack's `/cso --diff` and `mb-sentinel-review`, each in its own session.

**Must be built so that:**
- `code-review` reviews the changes on its two axes: standards (the rules of Anvil's `server-code`, `client-modules`, `client-forms`, `data-models` and `anvil-yaml` skills, [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md), [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md) and [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md)) and the ticket (does the change do what the ticket asks);
- each form and spec sheet is checked against its approved screen requirement, and Anvil's agent is confirmed to have changed only handler bodies;
- `ts_scan.py` passes on the changed code (ST-02 to ST-12);
- `/cso --diff` reviews only the feature's changes for security;
- `mb-sentinel-review` runs at Very High scrutiny on the changes, against the same documents as at Step 35;
- every finding goes to the findings file with its file, line and severity; with none, the file states a clean pass; nothing is fixed in this step;
- its ledger row carries the ticket, with `step_type = 'skill'`, `skill_family = 'matt-skills'`, `synthesized = false`, and `inputs_used` naming Step 36.

**BFT level:** Full.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md); [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `code-review` (Matt Pocock), with the Anvil skills' rules as its standards → the findings, then Step 39.
- `/cso --diff` (GStack): the security of the feature's changes → the findings, then Step 39.
- `mb-sentinel-review`, Very High → `triage_findings`.

**Not used:** GStack's `/review`, because it applies fixes itself; fixes are decided at Step 39 and made at Step 35.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e37-test-spec|Step 37 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e37-test-spec.md).

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md); [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects for Mybizz Anvil Applications]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md); [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md).

## Why it is built this way

- **Anvil's own rules as the standard.** Anvil's skills say how Anvil code, forms and data must be written; reviewing against them catches what Anvil would reject or mishandle.
- **Separate eyes.** Each review runs in its own session, so no reviewer sees another's conclusions.
- **Review, not repair.** Findings go to triage, where each is decided.
