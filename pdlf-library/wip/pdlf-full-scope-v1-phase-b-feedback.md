---
title: "pdlf-full-scope-v1-phase-b-feedback"
doc-id: "mb-aa7bd177"
updated: "2026-10-13"
---
**B.1 What Phase B receives from Phase A**

1\.  The health check needs to be designed

2\.  changed aspect under "Where it joins Phase B"
- 07, 08, 10

3\. "Proposal for the entry record"
- 4. "for a feature or an update, a short statement of it in David's words, and a short name for it (the feature slug)" - The orchestrator must ask David for this

4\. "\*\*Proposal: the health check is one shared procedure."
- The health check and the self-audit must be standard procedures and saved at: "C:\\pdlf\\pdlf-library\\operating-procedures"


**B.2 Rules that apply to every Phase B step**

1. All rules are saved as separate files at this path and are referenced in the phase and step where applicable: "C:\\pdlf\\pdlf-library\\app-factory-rules"
2. app-factory-rules and adr-local can quite easily become conflated therefore there should be a clear distinction between the two or they should be merged under adr-local and the decision clearly defined in PDF full scope V2 onwards



**B.2.1 The step pattern**

1. Finding: every Phase B step still carries housekeeping that has been retired
- Clean up as indicated in this paragraph
- The decision must be recorded in either of these folders as appropriate:
"C:\\pdlf\\pdlf-library\\app-factory-rules"
"C:\\pdlf\\pdlf-library\\operating-procedures"
"C:\\pdlf\\pdlf-library\\policy-local"
"C:\\pdlf\\pdlf-library\\adr-local"



1. 2\. Finding: the shared specifications are behind the build plan
- Clean up as indicated in this paragraph
- The decision must be recorded in either of these folders as appropriate:
"C:\\pdlf\\pdlf-library\\app-factory-rules"
"C:\\pdlf\\pdlf-library\\operating-procedures"
"C:\\pdlf\\pdlf-library\\policy-local"
"C:\\pdlf\\pdlf-library\\adr-local"
- Proposal is approved



**B.2.2 Searching GBrain with the real source names**

1. PDLF-Library must be a federated source as every application being developed in App Factory will require to use this library
2. Project-Library-Global must be a federated source as every application being developed in App Factory will require to use this library
3. A {slug}-project-library For any project, must be an unset source and must by default, be read by the project owning that project library. Other projects should only read a {slug}-project-library across projects when specifically named as one project's {slug}-project-library does not necessarily apply to another.
4. A {slug}-code repo For any project, must be an unset source and must by default, be read by the project owning that project code repo. Other projects should only read a {slug}-code repo across projects when specifically named as one project's {slug}-code repo does not necessarily apply to another. We have since established that GBrain can read code files. This must be confirmed, and necessary changes across Mybizz-OS should be implemented as required. The to-do list (item D1) my need to be corrected 
5. Graphify has been employed to create a graph for each code repo and should be used to search code repos as specified by the skill



































































































