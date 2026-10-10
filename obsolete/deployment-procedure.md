---
title: "deployment-procedure"
doc-id: "mb-6f7ff3fe"
updated: "2026-10-10"
---
# PDLF Skill — Deployment Procedure

How the PDLF stepwise package is developed, deployed, and loaded by OpenCode.

---

## Deployment Chain

```
source files            deployed files        symlink                     loaded by
─────────────────────────────────────────────────────────────────────────────────
C:\dev\dev-makepdlf\        C:\pdlf\stepwise\     ~/.config/opencode/         OpenCode
stepwise\               (canonical steps +    skills/pdlf/                /pdlf command
                        lettered sub-steps +
                        5 shared refs)
        │                        │                    │                         │
        │    cp -r ───────────────┤                    │                         │
        │                        │    symlink ────────┤                         │
        │                        │                    │   reads ────────────────┤
```

1. **Source**: `C:\dev\dev-makepdlf\stepwise\` — the canonical step skills, lettered sub-steps, and 5 shared reference files we edit during development
2. **Deploy**: Copy the entire `stepwise/` folder to `C:\pdlf\stepwise\` — the deployed package that OpenCode loads
3. **Symlink**: `~/.config/opencode/skills/pdlf/` → `C:\pdlf\stepwise/`
4. **Runtime**: OpenCode discovers `/pdlf` via the symlink and loads stepwise skills

The symlink was created once during initial PDLF setup. It does not change on deployment.

---

## When to Deploy

Deploy the stepwise package after any structural change to the files in `stepwise/`:
- New stepwise files added
- Shared reference documents changed (pdlf-spec-execution-discipline, pdlf-spec-bft, pdlf-spec-gate-procedure)
- INDEX.md or run-plan.md updated
- Step file content changed (task order, procedures, references)
- Step numbering changes
- Gate position changes (e.g., the `build-verified` gate moving from one step to another)

Do NOT deploy after cosmetic changes (typo fixes, wording improvements) unless they affect
runtime behavior.

---

## Deployment Commands

From WSL:
```bash
rm -rf /mnt/c/pdlf/stepwise/
cp -r /mnt/c/dev/dev-makepdlf/stepwise/ /mnt/c/pdlf/stepwise/
```

From Windows (PowerShell):
```powershell
Remove-Item -Recurse -Force "C:\pdlf\stepwise\"
Copy-Item -Recurse "C:\dev\dev-makepdlf\stepwise\" "C:\pdlf\stepwise\"
```

### Selective deployment (single file)
```bash
cp /mnt/c/dev/dev-makepdlf/stepwise/step-11-init.md /mnt/c/pdlf/stepwise/step-11-init.md
```

---

## Verification

After deployment, verify the deployed files are identical to source:
```bash
diff -r /mnt/c/pdlf/stepwise/ /mnt/c/dev/dev-makepdlf/stepwise/
```
No output = identical = deployment succeeded.

Verify OpenCode is loading the correct version:
```
/pdlf  (should trigger the new skill behavior)
```

---

## What C:\pdlf\ Contains

```
C:\pdlf\
├── stepwise/                            ← canonical step skills + lettered sub-steps + 5 shared references
│   ├── step-01-orchestrator.md          ← The PDLF orchestrator
│   ├── step-11-init.md
│   ├── ...
│   ├── step-35A-testing.md
│   ├── step-38A-dependency-scan-confirm.md
│   ├── step-40B-remediation.md
│   ├── step-42A-staging-integration-e2e.md
│   ├── step-46-LEARN-junction.md
│   ├── INDEX.md
│   └── run-plan.md
├── registry/
│   └── projects.json                    ← Project slug → path resolution
└── .gitignore
```

`C:\pdlf\` is the minimal system home — only what the running orchestrator needs. All
development, documentation, templates, and reference files live in `C:\dev\dev-makepdlf\`.

---

## Relationship to dev-makepdlf

- `dev-makepdlf\` is where PDLF is developed — source stepwise files, docs, templates, policies, ADRs
- `C:\pdlf\` is where PDLF runs from — the scaffolded home (pdlf-library, app-factory machinery, output area)
- Never edit the deployed tree under `C:\pdlf\` directly — always edit the source in dev-makepdlf, then deploy

---

*Deployment procedure version 2.2. Updated 2026-07-18: fixed step-38A filename
(dependency-scan-confirm, not ci-confirm); removed step-02, step-03, and
the retired `sop-existing-project-resume-audit.md` from the deployed tree — all three retired with the
disposition-audit model. Last revised: 2026-07-18.*
