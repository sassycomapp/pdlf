---
document: "PDLF — Artifact and Handover Specification"
doc-id: pdlf-spec-artifact-handover
state: Live
date-created: 2026-09-11
---

# PDLF — Artifact and Handover Specification

Canonical binding technical truth for how artifacts are produced, captured,
handed over between steps, copied to the safety net, and archived at ship
time. Implements `pdlf-adr-artifact-saving-convention`. For the naming rules:
`pdlf-spec-nomenclature.md`. For the narrative account:
`pdlf-expl-artifact-lifecycle.md`.

Facts marked "verified 2026-09-11" were checked directly against the live
environment on that date. Unverified expectations are marked as such and must
be verified before a module relies on them.

---

## 1. Native save locations — where skills actually save

### 1.1 GStack skills

All GStack skills save under a per-project folder:

    ~/.gstack/projects/<gstack-slug>/…

The `<gstack-slug>` is resolved at the start of every skill run by
`gstack-slug` (see `pdlf-spec-nomenclature.md` for the derivation chain).
Current preambles invoke it as:

    eval "$($GSTACK_BIN/gstack-slug 2>/dev/null)" 2>/dev/null || true

Verified per skill 2026-09-11 (all PDLF-relevant skills clean of any
`~/.claude` path — the June defect is gone from the current install):

| Skill | Native save (from its SKILL.md) |
|---|---|
| `/office-hours` | `~/.gstack/projects/<slug>/{user}-{branch}-design-{datetime}.md` |
| `/plan-ceo-review` | `~/.gstack/projects/<slug>/ceo-plans/{date}-{feature-slug}.md` — **SCOPE EXPANSION and SELECTIVE EXPANSION only**; in HOLD SCOPE / SCOPE REDUCTION the skill persists nothing to disk |
| `/plan-eng-review` | Test Plan Artifact `~/.gstack/projects/<slug>/{user}-{branch}-eng-review-test-plan-{datetime}.md`; everything else lands inside the plan file it was handed (append-in-place of `## GSTACK REVIEW REPORT`) |
| `/design-consultation` | `~/.gstack/projects/<slug>/designs/` |
| `/qa` | `~/.gstack/projects/<slug>/{user}-{branch}-test-outcome-{datetime}.md` |
| `/review` | Findings persisted to a named path prescribed by the invoking step |

### 1.2 How later skills look for earlier artifacts (mechanism of record
inside the skills, and why PDLF does not rely on it)

Verified 2026-09-11 in the current SKILL.md files:

- `/plan-ceo-review` and `/plan-eng-review` glob
  `~/.gstack/projects/$SLUG/*-design-*.md` in their pre-review audit.
- `/qa` searches `ls -t ~/.gstack/projects/$SLUG/*-test-plan-*.md`.
- `/autoplan` and `/plan-eng-review` glob `~/.gstack/projects/$SLUG/*-design-*.md`.
- `/ship` searches several fallback locations in turn
  (`~/.gstack/projects/<slug>`, `~/.claude/plans`, `~/.codex/plans`,
  `.gstack/plans`).

PDLF does not rely on any of these searches for correctness — the handoff
contract (§2) makes them redundant. Where a skill's own search could
contradict a decision already made (see §2.3), the invocation preempts it.

### 1.3 Matt Pocock skills and OpenCode-native outputs

- `domain-modeling` (via `/grill-with-docs`) → `CONTEXT.md` + ADR folder;
  PDLF overrides both destinations at invocation (built Step 16:
  `CONTEXT.md` at the docs-repo root, ADRs to `adr-local\`).
- `to-tickets`, `triage` → `.scratch/` by default; PDLF overrides as each
  step prescribes.
- OpenCode-native outputs save to the path each step file prescribes
  (receipts: `pdlf\step-NN-receipt.md`).

## 2. The handoff contract

2.1 **Paste-in-full.** The orchestrator assembles the full text of every
incoming artifact directly into the skill's invocation prompt. A later step
never depends on a skill locating a prior skill's file on disk.

2.2 **State what exists, explicitly.** Where a skill runs its own
file-existence check regardless of what is pasted (the plan reviews glob
`~/.gstack/projects/$SLUG/*-design-*.md`), the invocation states explicitly
that the design doc already exists and is provided in the prompt. This
prevents the skill's own "prerequisite offer" from re-opening a decision an
earlier step already settled (built Steps 12 and 14 both apply this).

2.3 **Capture the real path.** The orchestrator captures the output location
from the skill's own reported output — not an assumed path.

2.4 **Never modify the native file.** GStack-native artifacts stay where the
skill wrote them. Copies (§5) are separate files; the native file is never
renamed, moved, or edited by PDLF.

## 3. Capture–verify–record procedure (every step, in order)

1. Invoke the skill with the pasted context (§2).
2. Capture the artifact path the skill reports (or capture the conversational
   output itself when the mode persists nothing — §6).
3. Verify the artifact exists on disk at the captured path.
4. Write the ledger `steps` row with `artifact_path` = the captured path.
5. Generate and save the Step Receipt at
   `dev-{slug}\{slug}-project-library\pdlf\step-NN-receipt.md`.
6. Make the stable copy (§4) and the safety-net copy (§5).
7. Verify both copies exist.
8. If any expected artifact is missing: STOP and raise a deviation request
   per the execution discipline. Never proceed silently.

## 4. Stable copies

Stable copies are the PDLF-controlled, deterministically named copies a later
step reads when the native path is unavailable or mode-dependent.

- Naming: `{slug}-step-NN-filename.md` (decision 5 of the convention ADR) —
  for example `makepdlf-step-14-ceo-plan.md`.
- The built steps 14–15 predate this convention: they write
  `gstack-outputs\step-14-ceo-plan.md`, `step-15-eng-plan.md`,
  `step-15-test-plan.md` (legacy folder name, no slug prefix). Both aspects
  are corrected in those files as part of convention adoption (tracked:
  master task list, item 18).
- A stable copy is a snapshot of that step's state; a later step that appends
  to the native file updates the stable copy after its append (built Step 15
  does this for Step 14's plan file).

## 5. Safety-net routing and ship-time archival

5.1 **Routing — per environment:**

| Environment / phase | Producer | Destination |
|---|---|---|
| PDLF environment (system phase) | GStack skills | `C:\pdlf\output\pdlf-output-gstack\` |
| PDLF environment (system phase) | Matt Pocock skills | `C:\pdlf\output\pdlf-output-pocock\` |
| PDLF environment (system phase) | OpenCode-native | `C:\pdlf\output\pdlf-output-opencode\` (when created) |
| makePDLF environment (exception phase) | GStack skills | `output-gstack\` in the makepdlf docs repo |
| makePDLF environment (exception phase) | OpenCode direct | `output-opencode\` |
| makePDLF environment (exception phase) | Matt Pocock skills | `output-matt-skills\` |

The makePDLF environment also holds an `output-staging\` folder whose routing
is not yet defined — flagged, not assigned (dev project decision).

5.2 **Copy procedure:** after the stable copy exists, copy it into the
safety-net folder named `{slug}-filename` (§4 naming, same filename rule),
confirm the copy landed, and state both locations in the step's output.

5.3 **Ship-time archival (binding procedure):**

1. Copy every safety-net copy for the shipping project into that project's
   own folders (the project's output folders / archive location).
2. Verify each copy arrived — list and compare counts and sizes.
3. Only after verification: clear `C:\pdlf\output\` (or the exception-phase
   equivalent) for the next project.
4. Never clear before verification. Nothing is ever silently lost.

## 6. Mode-dependent persistence

Some skills persist nothing in some modes. Confirmed: `/plan-ceo-review`
writes a ceo-plans file only in SCOPE EXPANSION / SELECTIVE EXPANSION; in
HOLD SCOPE / SCOPE REDUCTION the review exists only as conversational output.
In those modes the orchestrator saves the transcript capture itself and treats
that capture as the artifact. A missing disk file is a failure only when the
mode predicted one; it is never treated as failure when the mode predicts
none — but the capture, the stable copy, and the safety-net copy are still
required in every mode.

## 7. Verification-or-deviation

An expected artifact that does not exist at verification time is a STOP: a
formal deviation request per the execution discipline, never a silent
proceed, never an assumption that the skill "probably wrote it."

## 8. Ledger and receipt integration

- The `steps` ledger row records `artifact_path` = the captured native path
  (or the orchestrator-saved capture path, per §6).
- The Step Receipt carries the artifact locations; downstream steps receive
  INPUT NOTICEs through the receipt chain per the conditional-state policy.
- Only the orchestrator, operating through a real PDLF step, writes to the
  ledger. A raw write bypassing a step is a policy violation by definition.

## 9. Watched items and pending corrections

| # | Item | Status |
|---|---|---|
| 1 | Built steps 14–15: legacy `gstack-outputs\` folder name; missing `{slug}-` copy prefix; stale quote of an older skill generation's `~/.claude` path in Step 14's description (current skill source verified clean 2026-09-11) | Correction tracked — master task list, item 18 |
| 2 | End-to-end live verification of the chain (one governed skill run: slug stability, native save, safety-net copy) never performed on the current install | Open — master task list, item 17 |
| 3 | GStack pinned at 1.58.1.0; upstream at 1.81.0.0 (23 minor versions behind). Upstream fixes may change save behavior | Watched — version upgrade is a separate decision |
| 4 | Slug cache never reconciles against the git remote; stale entries possible (observed on a placeholder project; heal tracked) | Watched — heal rule in `pdlf-spec-nomenclature.md` |
| 5 | makePDLF's `output-staging\` folder has no routing rule | Open — dev-side decision |

---

*End of pdlf-spec-artifact-handover*