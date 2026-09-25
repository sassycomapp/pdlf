---
title: "pdlf-expl-artifact-lifecycle"
doc-id: "pdlf-expl-artifact-lifecycle"
---
# PDLF — The Life of an Artifact

*The plain narrative of how a work product moves through the PDLF system —
where it is born, where it lands, how the next step receives it, and where it
finally rests. The narrative companion to
[[pdlf-spec-artifact-handover]] (the binding rules) and
[[pdlf-adr-artifact-saving-convention]] (the decisions).*

---

## Born inside a skill

An artifact begins when a step invokes a skill — a plan review, a design
consultation, a QA run. The step's orchestrator has already pasted the full
text of everything the skill needs directly into the invocation prompt, so
the skill starts fully informed and never has to go looking for its
predecessor's work.

When the skill finishes, it saves its output where all GStack skills save:
a per-project folder in the user's home directory,
`~/.gstack/projects/<project-name>/…`. The project name in that path is not
chosen — it is derived, mechanically, from the git repository the skill ran
in. Because PDLF always creates each project's repositories under fixed
names, that derived name is predictable for every project, every run. (The
full derivation story lives in [[pdlf-spec-nomenclature]].)

## Seen, verified, recorded

The orchestrator then does three things, always in the same order. It
**captures** the output path exactly as the skill reported it. It
**verifies** that the file genuinely exists on disk — if it does not, the
step stops and raises a formal deviation request; nothing ever proceeds on
the assumption that a file "probably" exists. It **records** the location in
the ledger — the database that remembers, across sessions and weeks, exactly
where every artifact of every step lives.

From this point on, the artifact's location is a matter of record, not of
memory.

## Copied — twice, for two different reasons

The orchestrator then makes two copies, each serving a different purpose.

The **stable copy** is the deterministic, PDLF-named version —
`{slug}-step-14-ceo-plan.md` style — that later steps read when the native
location is inconvenient or mode-dependent. It is the working-handoff copy.

The **safety-net copy** goes to the producer-routed output folder (GStack
work to `pdlf-output-gstack`, Matt Pocock work to `pdlf-output-pocock`, and
so on), named with the project slug so an archived set is always
self-describing. The safety net exists for one reason: so that nothing is
ever lost merely because it lived in a hidden per-project folder. It is a
convenience and an insurance policy — the chain itself never depends on it.

## Handed on

The next step receives the artifact the same way this one was born: the
orchestrator pastes its full text into the next skill's invocation. The next
skill starts knowing everything. If a later skill would run its own search
for a file and that search could contradict a decision already made, the
orchestrator states plainly in the invocation that the artifact exists and is
provided — so the skill never re-opens a settled question.

And so the artifact chain runs, step to step: born, seen, verified, recorded,
copied, handed on. Some artifacts live long lives — the design doc is read
by nearly every step that follows. Some are consumed once. All of them are
recorded.

## At rest

When the project finally ships, every safety-net copy is moved into the
project's own folders, the move is verified, and only then is the output
area cleared for the next project. The project's artifacts rest where the
project rests — archived together, self-describing, nothing left behind.

## Why it works this way

In June 2026, before this discipline existed, the chain ran on luck: skills
saved to folders whose names could differ between runs, so a later skill
would search under one name for a file saved under another, find nothing,
and continue as if the prior work had never happened — silently. One skill
asked whether to save and, told no, saved nothing anywhere. A fallback
folder literally named `unknown` appeared. That investigation is why the
orchestrator now owns every handoff, why verification precedes every
advance, why the ledger remembers every location, and why nothing in this
system is ever allowed to disappear quietly.

---

*End of pdlf-expl-artifact-lifecycle*