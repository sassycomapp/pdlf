---
title: "c23-build-plan"
doc-id: "mb-780ca546"
updated: "2026-11-12"
---
# Step 23 — Design Review: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 23: Design review

**Must achieve:** every screen requirement and `DESIGN.md` reviewed for usability and for full use of `m3-custom-theme`, with every finding recorded and its severity, so that Step 26 corrects them before David approves the screens.

**Starts from:** the screen requirements and the requirement index from Step 22; `DESIGN.md`; the tickets and flows; the theme's whole component documentation.

**Produces:** the design review, with every finding; in `pdlf-outputs\c23\`: the review, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with GStack's `/plan-design-review`. David decides the severity of any finding the agent cannot rate.

**Must be built so that:**
- `/plan-design-review` rates the screen requirements and `DESIGN.md` on each design dimension it covers, and every gap it finds becomes a finding;
- the theme-usage check runs on every screen requirement: each element is compared with the theme's whole component inventory, and every element for which a better-fitting theme component exists is a finding, naming the better component and why;
- the accessibility rules of [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 13 and the always-available controls of section 12 are checked on every screen requirement, and each gap is a finding;
- every finding names its screen requirement, its element, the correction proposed and its severity: high, medium or low; every theme-usage finding is high;
- no screen requirement is changed in this step; Step 26 corrects them;
- its ledger row is `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 22.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/plan-design-review` (GStack): the usability findings → Step 26.

**Layers with no skill:** the theme-usage check; no installed skill knows `m3-custom-theme`, so OpenCode runs it against the theme's inventory.

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c23-test-spec|Step 23 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c23-test-spec.md): every screen requirement was reviewed, and every finding is recorded with its severity.

**Standards:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) sections 3, 12 and 13.

## Why it is built this way

- **Review before approval.** Findings recorded here are corrected at Step 26, before David approves, so he approves screens that have already been challenged.
- **Full use of the theme is checked, not assumed.** Comparing each element with the whole inventory catches every place where a plainer component was chosen over a better one; each such finding is high, because the rule admits no exception.
- **Review and correction apart.** Keeping this step read-only means every finding is recorded, never silently fixed.
