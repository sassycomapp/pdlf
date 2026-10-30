---

title: "pdlf-skills-scoping-strategy"
doc-id: "mb-bf8e49f0"
updated: "2026-10-30"

---

# PDLF Skills Scoping Strategy

## 1. What this document is

This document is the strategy by which PDLF's skills are scoped. It states what PDLF is for, the order in which PDLF's purpose is reasoned down to its skills, the layers every step is scoped across, the skill commitments already made, the method by which each skill is chosen, how conflicts are settled, which sources are used, the stages in which the work is done, and where every result is recorded.

It is the cornerstone of PDLF's skill selection. Every stage of the skills work is carried out to it.

It does not map skills to steps. That mapping is the output of the stages (section 10), and it is recorded in the step build plans and the skills catalog (section 11), never here.

Where this document and the system build plan, `C:\pdlf\app-factory\pdlf-build-plan.md`, disagree about what PDLF is, the build plan is right and this document is corrected. Where they disagree about how skills are scoped, this document is right and the build plan is corrected.

## 2. What PDLF is, and why its skills matter

MyBizz builds many applications. Every one of them is an Anvil.works web application, and every one is its own Mybizz business, with its own five-app set.

PDLF is the system that builds them. It consists of two things:

- **the orchestrator**, which runs the steps in order and stops at every gate for David's approval;
- **the skill set**, which the steps use to do their work.

Building Anvil.works applications in this way is the whole function of PDLF and nothing else.

PDLF is built and run by three members:

| Member                  | Role                                                                                                            |
| ----------------------- | --------------------------------------------------------------------------------------------------------------- |
| David                   | Project manager and developer. Decides intent and approves every change. He reads code but is not a programmer. |
| Claude (web interface)  | Architect and engineer. Designs PDLF, resolves its technical questions, and makes the engineering decisions.    |
| OpenCode and its models | The worker. Carries out the steps, inside the WSL terminal.                                                     |

Because David does not judge code himself, PDLF carries the responsibility for correct code. The steps do the work, and the skills are what make a step's work good. A step that uses the wrong skill, or misses a skill that does its job better, builds a worse application with no one placed to notice. That is why skill scoping is foundational, and why it is done deliberately, step by step, against the whole catalog.

PDLF's credo applies to the skill set as to everything else: **simple, secure, robust, fit for purpose.** PDLF consists only of the skills that best serve its objectives: nothing superfluous and nothing lacking.

## 3. The order of reasoning

Skills are scoped from the outcome down, never from the skills up. Each level serves the level above it:

1. **Outcome.** Working, secure Anvil.works web applications, built well, for each Mybizz business.
2. **Objectives.** What PDLF must achieve to deliver that outcome.
3. **Intent.** The declared statement of what PDLF is and does. It must serve the objectives. It is held in the system build plan.
4. **Build plan and steps.** The intent turned into a sequence of steps. Each step has documented obligations: what that step must do.
5. **Skill mapping.** Each step is given the skills it needs to meet its obligations.
6. **Skills catalog.** The catalog's PDLF Steps column records the mapping. It mirrors the steps and never leads them.

Each level is checked against the level above it. A fault high in the chain makes everything below it wrong, so checking starts at the top.

### The four checks

The skills work makes four checks, in this order:

1. **Is the intent accurate?** Does it truly serve the outcome of building Anvil.works applications?
2. **Do the documented obligations fulfil the intent?** Is any needed step missing, and does any step serve nothing?
3. **Does each step actually fulfil its obligations?**
4. **Does each step use the right skills?** No needed skill missing, no wrong skill, and nothing superfluous.

A finding at any level is resolved at that level, at its source, before the levels below it are relied on.

## 4. The state PDLF is in

PDLF is in its design stage. Its documents are a work in progress, and the skills work continues that work; it does not audit a finished system.

- **Steps are not fixed.** The app factory currently holds steps 01 to 46 across Phases A to F, with inserted steps such as 35a, 38a, 40b and 42a. More steps may be inserted, and Phase G, the remaining apps, is still to be designed. Step numbers are never changed; an inserted step takes a letter after its number. Steps are referred to by their app-factory codes, never by a count.
- **Phase A holds the entry points.** Steps 02 to 10 are the points at which work joins the pipeline: a new application with or without context, a new feature, an update, and work on Apps 2, 3 and 5.
- **Design depth varies.** Some steps are designed in depth, as Phase B is. Many are entries and placeholders that indicate a step's function and nothing more.
- **A step's current skill names its function, not its skill set.** Where a step entry names one skill, that skill indicates what the step is for. It is not the step's skill selection. Each step's skills are selected when the step is developed, and a step almost never uses only one skill.

## 5. The layers every step is scoped across

Every step is scoped across every layer below. For each layer, the step either names the skills that serve it, with the reason, or states that the layer does not apply to that step and why.

| Layer                   | What it covers                                                                                                                                                                     | Principal sources                                                                                                                                             |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Development             | Building the Anvil application itself: schema, data flow, forms, client modules, server modules, the manifest.                                                                     | Anvil's `anvil-agent-references` skills: `data-models`, `anvil-yaml`, `client-forms`, `client-modules`, `server-code`.                                        |
| Foundation and workflow | The structured stages of product work: interrogating the idea, plan reviews from several angles, design, QA, shipping, monitoring, and any GStack pipeline that fits.              | GStack.                                                                                                                                                       |
| Engineering support     | Engineering discipline: domain modelling, tickets, triage, test-first building, debugging, architecture health, walkthroughs for steps only David can perform, writing for agents. | Matt Pocock's skills.                                                                                                                                         |
| Security                | Prevention in design and build, step-triggered review, and assessment.                                                                                                             | `mb-sentinel-review`; Magnus919's `secure-software-engineering` and `security-audit-methodology`; GStack's `/cso`.                                            |
| Testing | What the step must prove, in its test specification (`{step}-test-spec.md`). | The test suite in `C:\dev\project-library-global\test-suite\` and PDLF's process tests. |
| Documentation           | Documents the step produces for the application, for its developers and, later, for its users.                                                                                     | GStack's documentation skills, MiniMax's document skills, `mb-project-docs`. User help documentation is designed as one job with video documentation (to-do E5).                                   |
| Display and diagrams    | Wireframes, UI screens, decision trees, workflows, user flows and feature flows.                                                                                                   | Magdoub `wireframe`; `mb-archify-scope` and Archify. Video documentation is designed with user help documentation (to-do E5). ["[[[data-mybizz-mgt:creative/video-creation-suite/video-creation-suite]]](C:/data-mybizz-mgt/creative/video-creation-suite/video-creation-suite.md)"] |
| Memory and learning     | What the step looks up before it acts, and what it teaches the next build.                                                                                                         | GBrain, `mb-submit-memory` with the memory governor, Graphify, GStack's `learn`.                                                                              |

The layers exist so that no kind of skill is forgotten. A step is scoped only when every layer has been considered.

## 6. Commitments already made

These are settled. Every pass works within them.

1. **Anvil compliance is central.** Anvil's own skill set, `anvil-agent-references`, at `C:\mybizz\anvil-agent-references\skills\` (`server-code`, `anvil-yaml`, `client-forms`, `client-modules`, `data-models`), is central to the PDLF process. It is issued by Anvil itself and is how agents apply Anvil correctly. Every step that touches the application's code, schema, forms or manifest uses the matching Anvil skill. Together with Anvil's documentation compiled in `C:\dev\project-library-global\anvil-docs`, it is the principal source of Anvil knowledge. Every Mybizz application is built strictly to Anvil's Material 3 theme.
2. **Security is paramount.** David is absolutely paranoid about security. Security uses `mb-sentinel-review` and Magnus919's skills, `secure-software-engineering` and `security-audit-methodology`. GStack's `/cso` is also available. Where both `/cso` and `security-audit-methodology` serve a step, both may run. Security is never traded away for simplicity.
3. **Engineering support comes from Matt Pocock's skills.** Matt's `diagnosing-bugs` is built in wherever it fits its purpose, once its own file has been read.
4. **GStack is the foundation suite.** Its skills, and possibly some of its pipelines and principal development skills, are used wherever they serve a step.
5. **All wireframes and UI screens use the Magdoub wireframe skill.**
6. **Diagrams move to Archify.** Decision trees are written in HTML while the design is still being worked out. Once it is known what the trees must show, PDLF switches over: every decision tree, workflow, user flow and feature flow is then scoped with `mb-archify-scope` and drawn with Archify. Which steps need these diagrams is established as each step is scoped; it may be most of them. This is very important to David.
7. **Testing is a layer in every step.** Each step's test specification states what it must prove and which tests it runs.

## 7. How a skill is chosen

1. **The catalog is considered as a whole.** For each step, every skill in `C:\mybizz\mybizz-os-docs\os-reference-docs\skills-catalog.md` is considered against every layer. The catalog lists every skill, system and agent on the computer, and every skill in it is available to PDLF.
2. **A skill is read before it is chosen.** A skill's name does not reliably say what it does. Before a skill is chosen, its own installed `SKILL.md` and its canonical documentation are read, and what it really does is recorded in the step's build plan.
3. **A skill earns its place.** A skill is preferred over Opencode. Once chosen for a task, it is always used for that task, and the agent never improvises a task a skill covers.
4. **Overlapping skills are compared, not assumed duplicates.** GStack and Matt Pocock may both offer a QA skill or a review skill; GStack's `learn` and `mb-submit-memory` both concern lessons. Studied closely, such skills are rarely identical and often serve different purposes. Each is used where it best serves the function required: one in one situation, the other in another, or both where both add value. The aim is the best use of the resources available, never a contest between them.
5. **The reason is stated.** Every skill named in a step carries the reason it is there, and every layer a step leaves without a skill carries the reason it needs none.
6. **A skill used by no step stays in the catalog.** Its PDLF Steps cell is blank.

## 8. Conflicts and rules

1. **Conflicts are resolved to the known source of truth.** Where two documents, two skills or a skill and a rule disagree, the disagreement is resolved by going to the source that actually governs the matter, never by letting one silently win. Where two Anvil sources conflict, the conflict is raised to David, who resolves it.
2. **`anvil.yaml`.** An agent changes `anvil.yaml` only through Anvil's `anvil-yaml` skill, and validates every change with `anvil --json validate` ([[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md)).
3. **Rules are editable.** PDLF's structures and David's rules can be changed. When a rule no longer serves PDLF, Claude brings it to David with a proposal, and David decides. The aim is that PDLF works in the end.

## 9. Sources and memory

Full use of the memory system is essential throughout the skills work. Without it, ADRs, specifications, learnings and stored facts are missed.

The skills work draws on these sources:

| Source                                                                                    | Where                                                                                                                         | How Claude reaches it                                                                                                 |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| The system build plan and step build plans                                                | `C:\pdlf\app-factory\`                                                                                                        | The public GitHub repository `pdlf`.                                                                                  |
| PDLF's library: policies, specifications, ADRs, explainers                                | `C:\pdlf\pdlf-library\`                                                                                                       | The public GitHub repository `pdlf`.                                                                                  |
| Standards, specifications, security library and Anvil documentation for every application | `C:\dev\project-library-global\`                                                                                              | Its public GitHub repository.                                                                                         |
| The skills catalog and system-wide explainers                                             | `C:\mybizz\mybizz-os-docs\`                                                                                                   | The public GitHub repository `mybizz-os-docs`.                                                                        |
| Each MyBizz-configured skill's or system's document suite                                 | `C:\mybizz\mybizz-config-docs\{system}\`                                                                                      | The public GitHub repository `mybizz-config-docs`.                                                                    |
| Third-party skills' canonical sources and documentation                                   | Under `C:\mybizz\` (for example `anvil-agent-references`, `gstack`, `matt-pocock-skills-source`, `archify`, `minimax-skills`) | The issuer's public repository, or David passes the file.                                                             |
| The installed skills                                                                      | `~/.config/opencode/skills/`, `~/.agents/skills/`, `~/.claude/skills/` (WSL)                                                  | Claude has no direct access. David passes the file, or Claude gives him a command or OpenCode prompt that fetches it. |
| GBrain: the documentation mirror and stored facts                                         | WSL                                                                                                                           | Through OpenCode in the WSL terminal, using prompts or commands Claude gives David.                                   |

Every repository the skills work needs is public. A repository that appears private to Claude means Claude has made a mistake, not that access is missing.

A GBrain search result is a pointer. The file it points to is read before anything is applied from it.

## 10. The stages

The skills work runs inside the stages every phase of PDLF passes through, built, proven and finished, in the order set out in the [[[pdlf:pdlf-library/docs-local/app-factory-docs-update-method|App Factory Docs Update Method]]](C:/pdlf/pdlf-library/docs-local/app-factory-docs-update-method.md).

### When a phase is built

**Purpose:** from the documents and the operational context, establish what each step does and scope the skills it requires.

**Operational context:** everything in the step folders; the document suites in `mybizz-config-docs`; the third-party skills' canonical documentation under `C:\mybizz\`; the installed skills at their pinned versions; and GBrain.

**Work:**

1. Make the four checks (section 3), from the outcome down.
2. For each step, read the skills that could serve it and scope the step across every layer (section 5), choosing skills by the method in section 7.
3. Settle every conflict found (section 8).
4. Find the gaps: needed steps that are missing, steps that serve nothing, obligations a step does not meet, and skills no step uses that one should.

**Produces:** the skills of every step, recorded in its build plan with their reasons; any system-wide rule recorded in the system build plan; and the catalog's PDLF Steps column filled in from the steps.

### When a phase is proven

**Purpose:** run `mb-3-cs` (Mybizz consulting and services) through the phase, so that what building a real application demands corrects the skill mapping. `mb-4-ecom` (Mybizz e-commerce) follows.

**Produces:** corrections to the intent, the steps and the skill mapping, recorded in the same places as when the phase is built.

### Services designed on their own

User help documentation and video documentation are designed as one job, before Phase E is built (to-do E5). Testing is designed: the test suite and each step's test specification.

## 11. Where the results are recorded

Every result has one home, and a fact lives in only one of them.

| Result                                           | Recorded in                                                                              |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| A skill decision that applies to PDLF as a whole | `C:\pdlf\app-factory\pdlf-build-plan.md`                                                 |
| A skill decision for one step                    | That step's build plan, for example `C:\pdlf\app-factory\phase-a-init\a01-build-plan.md` |
| Which steps use each skill                       | The PDLF Steps column of `skills-catalog.md`                                             |
| How the skills are scoped                        | This document                                                                            |

**The PDLF Steps column** lists, for each skill, the app-factory codes of the steps that use it, separated by commas, for example `b11, c17, e35a`. The column only mirrors the step build plans. Where the two differ, the step build plan is right and the column is corrected. A skill used by no step has an empty cell.

When a step is built, its build plan becomes the step's config, reference and explainer, as the system build plan sets out, and the step's skills move with it into its config.

## 12. How the work is carried out

- **Claude is the engineer.** Claude reads the sources, makes the technical decisions, chooses the skills with their reasons, and tells David plainly where anything is wrong, including in Claude's own work. David is asked only about intent.
- **David approves every change.** No step build plan, rule or catalog entry is changed without his approval.
- **The work is done, not discussed.** This strategy closes the scoping conversation. From here the stages are carried out against the documents, with questions raised only where a decision is David's to make.
- **One consistent rule everywhere.** Every step is scoped in the same way, across the same layers, recorded in the same form, so that no agent ever has to choose between methods.

## 13. Why it works this way

- **From the outcome down.** Skills chosen from the skills up serve themselves, not the applications. Reasoning from the outcome makes every skill answer to what PDLF is for.
- **Every layer, every step.** A step scoped for its main function alone misses its security, testing, documentation and memory needs. Naming each layer turns an omission into a checked decision.
- **Read before choosing.** A skill's name is not what it does. Choosing from names puts the wrong tool in a step that no one will question.
- **Compare, do not discard.** Skills that look alike often serve different purposes. Keeping both, each where it serves best, uses the resources PDLF already has.
- **Passes, not one sweep.** The documents alone cannot show what a real application demands. Each pass adds what the previous one could not see.
- **One home for each result.** A skill mapping kept in two places drifts. The step build plan is the authority, and the catalog only mirrors it.
- **Rules serve PDLF.** A rule that stops PDLF from working is changed through a proposal, never worked around.
