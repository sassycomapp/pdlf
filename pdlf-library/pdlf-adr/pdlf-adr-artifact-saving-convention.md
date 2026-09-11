---
document: "PDLF — Artifact-Saving Convention"
doc-id: pdlf-adr-artifact-saving-convention
state: Live
date-created: 2026-09-11
---

# PDLF — Artifact-Saving Convention

Date: 2026-09-11
Status: Accepted
Origin: developer-directed design session 2026-09-11, building on the
artifact-saving investigation of 2026-06-25/26
(`C:\_data-mybizz-mgt\_desktop\artifact-saving-issue\`, 10 documents).

---

## Context

GStack skills chain by file: each skill saves its output under a per-project
folder (`~/.gstack/projects/<project-name>/…`), and a later skill finds the
earlier skill's output by searching that folder for a matching filename. The
entire skill-to-skill handover therefore depends on every run agreeing on the
project name.

The June 2026 investigation established that this agreement could not be
relied on: the same project resolved to at least three different names
depending on how a skill run started, one skill saved to an undocumented
location, one skill asked for confirmation and then saved nothing, and the
`unknown`-name fallback folder appeared. The suspected root cause — a
hardcoded Claude-Code-only path (`~/.claude/skills/gstack/bin/gstack-slug`)
inside the skill preambles — was confirmed as a real defect of that era's
skill files.

Re-verified 2026-09-11 against the current pinned install (GStack 1.58.1.0):

- The root cause is fully fixed. Every PDLF-relevant skill and the root skill
  file now resolve the project name through `$GSTACK_BIN/gstack-slug` or the
  explicit OpenCode install path. No `~/.claude` path remains anywhere
  (verified across all seven PDLF-relevant skills). The `unknown` fallback
  folder no longer exists under `~/.gstack/projects/`.
- The failure mode remains latent in the mechanism itself: the project-name
  cache is keyed by the exact working directory and never reconciles against
  the git remote, so a stale entry can silently diverge (observed on a
  placeholder project; tracked for heal on the master task list). No
  end-to-end verification with a real skill run has been performed on the
  current install; that verification remains open (master task list item 17).
- PDLF's own built steps (11–16) already mediate handoffs by a different and
  stronger mechanism: paste-in-full, ledger-recorded artifact paths,
  verify-or-stop, and stable copies.

Separately, the PDLF system's own home (`C:\pdlf`) now exists with its
library (`pdlf-library`), its machinery scaffold (`app-factory`), and a
producer-routed safety-net output area (`C:\pdlf\output\`). The decisions
below consolidate how artifacts are saved, handed over, copied, and archived
across both environments.

## Decision

1. **Skills save where they natively save.** No third-party skill is modified
   to change where it writes. GStack, Matt Pocock, and Magdoub skills keep
   their own native save behavior; PDLF adapts around it.

2. **The orchestrator owns the handoff — paste, capture, verify, record.**
   PDLF's orchestrator is the skill-to-skill chain. It pastes the full text of
   prior artifacts directly into each skill invocation (a later skill never
   depends on finding an earlier skill's file by searching). It captures the
   output path the skill reports. It verifies the artifact genuinely exists on
   disk. It records the location in the ledger (`artifact_path`). If an
   expected artifact is missing, the step stops with a formal deviation
   request — it never proceeds silently.

3. **The output folders are a safety net, not the chain.** Copies of skill
   outputs go to producer-routed output folders for human reference and loss
   recovery. The native artifact and the ledger record remain the primary
   truth. The safety net may be lost without losing the chain.

4. **The exception — makePDLF.** While the PDLF system is still being built,
   makePDLF's runs cannot be routed by the PDLF system (which does not yet
   exist). makePDLF's outputs therefore save in the makePDLF environment's own
   output folders (per that project's own artifact governance). This exception
   ends when makePDLF completes: its output folders are copied across to the
   makePDLF project before that project is archived.

5. **Copy naming — `{slug}-filename`.** Every safety-net copy carries the
   project's canonical short slug as a filename prefix, so an archived set is
   self-describing without reference to any folder.

6. **Ship-time rule — copy first, then clear.** When a project ships, its
   safety-net copies are copied into that project's own folders, their arrival
   is verified, and only then is the output area cleared for the next project.
   Nothing is ever silently lost.

7. **One project in the pipeline at a time — standing rule.** The output area
   serves exactly the one project PDLF is currently building. If two projects
   ever overlap, this convention must be revisited before they do.

8. **The naming invariant.** PDLF creates each project's GitHub documentation
   repository under a fixed name pattern (`{slug}-project-library`, in the
   sassycomapp organization). Because GStack derives its project name from the
   git remote, the GStack name for any skill run in a project's docs repo is
   therefore predictable: `sassycomapp-{slug}-project-library`. Skills running
   in the code repo derive `sassycomapp-{slug}`. Both forms are deterministic
   per repository; neither is left to chance.

9. **Canonical folder names — settled.** The routing rule, not a single
   universal folder name, is the invariant: producer-routed copies, named
   `{slug}-filename`, per environment. Concrete names:
   - **PDLF environment (system phase):** `C:\pdlf\output\pdlf-output-gstack`,
     `C:\pdlf\output\pdlf-output-pocock` (Matt Pocock skills), and
     `pdlf-output-opencode` for OpenCode-native outputs when created.
   - **makePDLF environment (exception phase):** the project's own governance
     names — `output-gstack\`, `output-opencode\`, `output-matt-skills\`.
   - The `gstack-outputs\` references in built step files 14 and 15 are a
     legacy of the pre-convention naming and are corrected to
     `output-gstack\` in those files (tracked: master task list, item 18).
     The stable-copy filenames in those steps likewise predate decision 5 and
     gain the `{slug}-` prefix at the same correction.

10. **The `{slug}` value — settled.** In decision 5's `{slug}-filename`, the
    slug is the project's canonical short slug — the developer-supplied
    project slug from Step 11, which the ledger, the folder structure, and
    every project document already use (for the PDLF system's own builder
    runs: `makepdlf`). The longer GStack-derived name remains a derived fact
    recorded in the nomenclature specification, not the basis for filenames.

## Rationale

The June investigation demonstrated that the skill-to-skill chain breaks
silently when the project name is unstable — no error, just "no prior artifact
found." PDLF's own built steps (11–16) already contain the stronger mechanism:
the orchestrator mediates every handoff and verifies every output, so the
chain no longer depends on skills finding each other's files. This convention
makes that mechanism the rule, keeps the third-party tools untouched (their
behavior is upstream and could not be maintained if patched), provides the
safety net as copies rather than as the chain, and pins the naming facts that
make every project name deterministic. The copy-first-then-clear rule and the
one-project rule both follow from the system's standing principle that nothing
disappears quietly.

## Consequences

- The app-factory modules implement this convention step by step as makePDLF
  completes each step; the specification
  (`pdlf-spec-artifact-handover.md`) is the binding detail modules follow.
- Built step files 14 and 15 require the correction described in decision 9
  (tracked: master task list, item 18). Their stale quote of an older skill
  generation's `~/.claude` path is corrected in the same pass — the current
  skill source was verified clean of it on 2026-09-11.
- An end-to-end live verification of the chain (one governed skill run:
  slug stability, native save, safety-net copy) remains open work, tracked on
  the master task list (item 17).
- The June investigation folder remains the historical record of why this
  convention exists; it is not a living document.

---

*End of `pdlf-adr-artifact-saving-convention` ADR*