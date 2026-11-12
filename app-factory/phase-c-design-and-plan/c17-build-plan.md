---
title: "c17-build-plan"
doc-id: "mb-2b6de0f2"
updated: "2026-11-12"
---
# Step 17 — Create Anvil Data Tables: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 17: Create Anvil data tables

**Must achieve:** App 1's data tables in Anvil match the authoritative schema, which agrees with the data design locked at Step 16.

**Starts from:** the items Step 16 handed over (the glossary, the ADRs, the reviewed plan with its data design, the access matrix, the threat model, the domain map and Step 16's receipt); the project library's `docs-standard-local\authoritative-schema.md` and `docs-local\schema-migration-log.md`; App 1's `anvil.yaml`.

**Produces:** `authoritative-schema.md`, written from the data design when it is empty and approved by David; the schema difference list; App 1's `anvil.yaml` with the whole schema in `db_schema`; the schema applied to App 1's live tables by David; the rows of this run in `schema-migration-log.md`; in `pdlf-outputs\c17\`: the copies, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with Anvil's `data-models` and `anvil-yaml`, Magnus919's `secure-software-engineering`, Matt Pocock's `wizard` and `mb-sentinel-review`. David approves the authoritative schema, renames columns by hand, commits App 1 and applies the schema with Resolve in Anvil's Data Tables view.

**Must be built so that:**
- the authoritative schema is the one source the tables are built from: when `authoritative-schema.md` is empty, the agent writes it from the data design, in the structure the project template gives the file, with `data-models`, and David approves it before anything else is done; when it is filled, the agent checks it against the data design and stops with a deviation on any disagreement;
- the agent lists every difference between the authoritative schema and the tables in App 1's `anvil.yaml`, sorted into three kinds: additions, renames and removals; a rename is taken from `schema-migration-log.md`, or confirmed by David when a column disappears and another appears in the same table;
- renames are done first, by David, by hand in the Data Tables view, following numbered instructions written with `wizard`, and David then pulls App 1, because a rename done by hand keeps the column's data, while the same change made through Resolve deletes it;
- the agent then writes the whole schema into `db_schema` in `anvil.yaml`, only through Anvil's `anvil-yaml` skill, and checks the file with `anvil --json validate anvil.yaml`;
- every table refuses client access (`client: none`), every table has `created_at`, and every core table carries the metadata column (Simple Object), as the common aspects policy sets out;
- `secure-software-engineering` checks every table's access against Step 15's threat model and trust boundaries;
- David commits and pushes App 1 with `git pull` followed by `gcp`, clicks Resolve in the Data Tables view, and applies each difference, following numbered instructions written with `wizard`; each removal on the difference list is checked by name before it is applied, because a removal deletes that column's data;
- every change of the run is recorded in `schema-migration-log.md`, with its migration plan, so that Step 41 can check that a migration plan exists;
- before David commits, the agent compares `db_schema` in `anvil.yaml` with the authoritative schema, table by table and column by column, and stops with a deviation on any difference; after Resolve, David confirms that the Data Tables view no longer reports a schema mismatch, which proves the live tables match `anvil.yaml`;
- Anvil's agent is not used in this step; the agent never applies a schema change and never changes `dependencies` in `anvil.yaml`;
- for a feature, only the feature's additions are applied; a rename or removal in a feature run is a breaking change and is approved by David by name before it is applied;
- its ledger row is `step_type = 'skill'`, `skill_family = 'anvil'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 16.

**BFT level:** Light.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md), [[[default:anvil-docs/ai-agent/anvil-ai-agent|The Anvil AI Agent]]](C:/dev/project-library-global/anvil-docs/ai-agent/anvil-ai-agent.md) (how a schema change reaches the tables).

**Skills.** Every skill's output is used by the step named after the arrow.
- `data-models` (Anvil): table ownership, client access and the shape of each table → the authoritative schema, then Steps 31 and 35.
- `anvil-yaml` (Anvil): writes and checks `db_schema` → David's Resolve, then Step 18.
- `secure-software-engineering` (Magnus919): each table's access checked against Step 15's threat model → the schema.
- `wizard` (Matt Pocock): David's instructions for the renames, the commit and Resolve → Step 18.
- `mb-sentinel-review`, High → `triage_findings`.

**Layers with no skill:** display, documentation (the authoritative schema is its own record).

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c17-test-spec|Step 17 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c17-test-spec.md): `anvil.yaml` validates, the schema obeys the data rules and matches the authoritative schema, and the live tables match it.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) section 10 (access rules); [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md); [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md), aspect 4 (the metadata column).

## Why it is built this way

- **One source for the tables.** The authoritative schema names every table and column; building from it, and checking it against the data design first, means the tables carry the vocabulary and decisions locked at Step 16.
- **Renames by hand first.** Anvil applies a rename made in `anvil.yaml` as a removal and an addition, which deletes the column's data. A rename made by hand in the Data Tables view keeps it.
- **OpenCode writes, David applies.** The agent can write the schema but cannot change the live tables; Anvil applies a schema change only when David clicks Resolve and accepts each difference. Every removal is therefore seen by David before any data is deleted.
- **Checked twice.** The comparison before the commit proves `anvil.yaml` is what was designed; the absence of a schema mismatch after Resolve proves the live tables match `anvil.yaml`. Together they prove the tables are what was designed, before any code is written against them.
