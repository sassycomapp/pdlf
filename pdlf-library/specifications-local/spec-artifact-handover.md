---
title: "pdlf-spec-artifact-handover"
doc-id: "mb-f1745959"
updated: "2026-10-24"
---
# PDLF — Artifact and Handover Specification

The binding detail of how artifacts are produced, captured, handed over between steps and copied to each step's output folder. It implements [[[pdlf:pdlf-library/adr-local/artifact-saving-convention|Artifact-Saving Convention]]](C:/pdlf/pdlf-library/adr-local/artifact-saving-convention.md). Naming rules: [[[default:specifications-global/spec-nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md).

The save locations below are those of the pinned skill versions (GStack `c580561`, Matt Pocock `5beb35b`). A change of version is checked against this document first.

---

## 1. Native save locations — where skills actually save

### 1.1 GStack skills

All GStack skills save under a per-project folder in GStack's state root (`~/.gstack` by default):

    ~/.gstack/projects/<gstack-slug>/…

The `<gstack-slug>` is resolved at the start of every skill run by
`gstack-slug` (see [[[default:specifications-global/spec-nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) for the derivation chain).
Current preambles invoke it as:

    eval "$($GSTACK_BIN/gstack-slug 2>/dev/null)" 2>/dev/null || true

| Skill | Native save (from its SKILL.md) |
|---|---|
| `/office-hours` | `~/.gstack/projects/<slug>/{user}-{branch}-design-{datetime}.md`; inside a git repository also `docs/designs/{topic-slug}.md`, which Step 12 moves into its step folder |
| `/plan-ceo-review` | The working plan it is given (PDLF names the run's `design-doc.md`), amended in place with `## GSTACK REVIEW REPORT` last, in every mode; in SCOPE EXPANSION and SELECTIVE EXPANSION also the CEO summary `~/.gstack/projects/<slug>/ceo-plans/{YYYY-MM-DD}-{feature-slug}.md` |
| `/plan-eng-review` | The plan and report file it is given (PDLF names the run's `design-doc.md`), amended in place with `## GSTACK REVIEW REPORT` last; its test plan `~/.gstack/projects/<slug>/{user}-{branch}-eng-review-test-plan-{datetime}.md` |
| `/design-consultation` | `~/.gstack/projects/<slug>/designs/` |
| `/qa` | `~/.gstack/projects/<slug>/{user}-{branch}-test-outcome-{datetime}.md` |
| `/review` | Findings persisted to a named path prescribed by the invoking step |

### 1.2 How later skills look for earlier artifacts (mechanism of record
inside the skills, and why PDLF does not rely on it)

In the skills' own SKILL.md files:

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
  `CONTEXT.md` in the project library's `docs-local\`, ADRs to `adr-local\`).
- `to-tickets`, `triage` → `.scratch/` by default; PDLF overrides as each
  step prescribes.
- OpenCode-native outputs save to the path each step file prescribes
  (receipts: `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-{run}-receipt.md`).

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
skill wrote them. Copies (§4) are separate files; the native file is never
renamed, moved, or edited by PDLF.

2.5 **GStack skills start from the project library.** Every GStack skill PDLF
invokes in Phase B is started from the project library,
`C:\dev\dev-{slug}\{slug}-project-library`. Its GStack slug is therefore always
`sassycomapp-{slug}-project-library`, and every GStack skill finds the others'
files in the same place. The code of an existing application reaches the skill
by being pasted in, never through the skill's own audit of a code repository.
Why: Phase B produces documents, not code, and the project library is where
those documents belong.

2.6 **The context pack.** Every skill invocation also receives, after the step's
own handoff material, the full text of the files listed in
[[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md).

## 3. Capture–verify–record procedure (every step, in order)

1. Invoke the skill with the pasted context (§2).
2. Capture the artifact path the skill reports, or the working file the step
   named for it (§6).
3. Verify the artifact exists on disk at the captured path.
4. Write the ledger `steps` row with `artifact_path` = the captured path.
5. Generate and save the Step Receipt at
   `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-{run}-receipt.md`.
6. Make the step-folder copy (§4) of every artifact saved outside the step folder.
7. Verify every copy exists.
8. If any expected artifact is missing: STOP and raise a deviation request
   per the execution discipline. Never proceed silently.

## 4. The step output folder

Every project library holds `pdlf-outputs\`, with one folder per step (`a01\` to `f46\`, named as in the app factory). Everything a step produces for that project is kept in its step folder:

- the Step Receipt, `{slug}-{step}-{run}-receipt.md`;
- a copy of every artifact a skill saved elsewhere (for example in GStack's own save location), named `{slug}-{step}-{run}-{name}`;
- the artifacts of skills that are told where to save (such as Archify, the Magdoub wireframe skills and Sentinel), which save into the step folder directly.

**The run.** `{run}` is `app{n}` when the work is a whole application (`app1`, `app2`, `app3` or `app5`), or the feature's short name (the feature slug from the entry record) when the work is a feature or an update. For example `mb-3-cs-b14-app1-ceo-plan.md`, `mb-3-cs-b14-app5-ceo-plan.md` and `mb-3-cs-b14-reminders-ceo-plan.md`. Why: App 1 and App 5 each run Steps 11 to 16 as a whole application, and the feature path runs Steps 12 to 16 again for every feature, so a name without the run would be overwritten, and each run's outputs stay beside the others.

The step-folder copy is the copy a later step reads when a skill's own save location is unavailable or depends on the skill's mode. It is a snapshot of that step's state; a later step that appends to a skill's own file updates the copy after its append.

## 5. No outputs in PDLF

Nothing an application produces is kept in `C:\pdlf`. There is no separate output area to copy into or clear: the step folders in the project library are the one place where each step's outputs are collected, and they are kept with the project.

## 6. Mode-dependent persistence

Some skills write a file only in some modes. Every such skill PDLF uses is also given a named working file that it writes in every mode, so a step's main artifact never depends on the mode. Confirmed: `/plan-ceo-review` always amends the working plan it is given, the run's `design-doc.md`, and writes its CEO summary to `ceo-plans/` only in SCOPE EXPANSION and SELECTIVE EXPANSION. A mode-dependent file is expected, and its absence is a failure, only in the modes that write it.

## 7. Verification-or-deviation

An expected artifact that does not exist at verification time is a STOP: a
formal deviation request per the execution discipline, never a silent
proceed, never an assumption that the skill "probably wrote it."

## 8. Ledger and receipt integration

- The `steps` ledger row records `artifact_path` = the step's main artifact:
  the captured native path, or the working file the step named (§6).
- The Step Receipt carries the artifact locations; downstream steps receive
  INPUT NOTICEs through the receipt chain per the conditional-state policy.
- Only the orchestrator, operating through a real PDLF step, writes to the
  ledger. A raw write bypassing a step is a policy violation by definition.

## 9. Watched item

GStack caches each project's name by working directory and never reconciles it with the Git remote, so a stale entry is possible. The rule for correcting it is in [[[default:specifications-global/spec-nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md).
