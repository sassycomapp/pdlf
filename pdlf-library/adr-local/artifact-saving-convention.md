---
title: "pdlf-adr-artifact-saving-convention"
doc-id: "mb-353516c1"
updated: "2026-10-24"
---
# PDLF — Artifact-Saving Convention

Status: Accepted

---

## Context

GStack skills chain by file: each skill saves its output under a per-project folder (`~/.gstack/projects/<project-name>/…`), and a later skill finds the earlier skill's output by searching that folder for a matching filename. The chain therefore depends on every run agreeing on the project name. GStack derives that name from the repository's Git remote and caches it by working directory, and the cache is never reconciled with the remote, so a stale entry can silently diverge. When the name diverges, a later skill finds no prior artifact and carries on without it: the chain breaks with no error.

## Decision

1. **Skills save where they natively save.** No third-party skill is modified to change where it writes. GStack, Matt Pocock and Magdoub skills keep their own save behaviour; PDLF adapts around it.

2. **The orchestrator owns the handoff: paste, capture, verify, record.** The orchestrator pastes the full text of prior artifacts into each skill invocation, so a later skill never depends on finding an earlier skill's file by searching. It captures the output path the skill reports, verifies the artifact exists on disk, and records the location in the ledger (`artifact_path`). If an expected artifact is missing, the step stops with a deviation; it never proceeds silently.

3. **Every artifact is also copied to the step's output folder,** `{slug}-project-library\pdlf-outputs\{step}\`, so all of a step's outputs for a project are in one place. Skills that can be told where to save (Archify, the Magdoub wireframe skills, Sentinel) save there directly.

4. **Copy naming.** Every file in a step's output folder is named `{slug}-{step}-{run}-{name}`, where `{slug}` is the business slug recorded at Step 11 and `{run}` is `app{n}` for a whole application (`app1`, `app2`, `app3` or `app5`) or the feature's short name, so the step and the run that produced it are clear and a feature never overwrites the application's files.

5. **The naming invariant.** PDLF creates each project library's GitHub repository as `{slug}-project-library` and each code repository as `{slug}-app{n}`, in the `sassycomapp` account. GStack's project name is therefore predictable: `sassycomapp-{slug}-project-library` for a skill run in the project library, and `sassycomapp-{slug}-app{n}` in a code repository. When GStack's cached name differs from the name the remote gives, the remote's name is written into the cache, with the developer's permission.

The binding detail that every step follows is [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md).

## Rationale

The orchestrator mediates every handoff and verifies every output, so the chain never depends on skills finding each other's files, and an unstable project name cannot break it silently. The third-party tools stay untouched, because their behaviour is upstream and could not be maintained if patched. The output folder gives each project one place holding everything each step produced, and its naming makes every file self-describing.
