# Standard Operating Procedure: Software Development with Coding Agents

**Document owner:** Engineering  
**Applies to:** All team members and contractors who use AI coding agents in the software development lifecycle (SDLC)  
**Status:** TBD  
**Review cadence:** At least every six months, and after a significant agent-related incident or material change to the team's tools

## 1. Purpose

This SOP defines how the team uses coding agents safely and consistently from idea intake through production operation and retirement. It is intended to improve delivery speed without delegating engineering accountability to an agent.

## 2. Scope and terminology

This SOP applies to coding agents that can generate, edit, explain, test, review, or operate on software, whether they run in an IDE, terminal, hosted service, or internal platform. It covers production code, infrastructure as code, scripts, tests, documentation, and configuration.

- **Coding agent:** An AI-powered tool that can assist with software engineering tasks.
- **Agent output:** Code, configuration, tests, analysis, documentation, commands, or recommendations produced or materially transformed by an agent.
- **Human owner:** The engineer responsible for the task and its outcome.
- **Reviewer:** A qualified person other than the author who reviews a change before it is merged, subject to the team's normal review policy.
- **Sensitive data:** Credentials, tokens, private keys, personal data, customer data, regulated data, or confidential information not approved for use with the selected agent.

## 3. Mandatory operating principles

1. **Humans remain accountable.** A human owner must understand, validate, and approve every agent-assisted change. Agent output is a proposal, not evidence that a change is correct, safe, or compliant.
2. **Use approved tools and data only.** Use only organization-approved agents and integrations. Do not submit secrets, personal data, customer data, or confidential information unless the tool and use case are explicitly approved for that data classification.
3. **Apply least privilege.** Grant agents only the repository, files, tools, and permissions required for the task. Prefer read-only access until edits are needed. Require human confirmation for consequential commands or external actions.
4. **Keep changes reviewable.** Work in a branch or equivalent isolated change set. Keep each change focused, inspect the full diff, and do not merge agent-generated changes without normal review and required checks.
5. **Verify behavior independently.** Run the project's relevant tests, static analysis, security checks, and build. Do not rely solely on an agent's report that checks passed; inspect actual command results.
6. **Protect production.** Agents must not independently approve, merge, deploy, alter production data, rotate credentials, or perform other privileged production actions. A human authorized by the team's release process must approve and perform or supervise them.
7. **Respect policy and provenance.** Follow the organization's security, privacy, licensing, accessibility, records-retention, and secure-development policies. Escalate uncertain provenance, license, or policy concerns rather than assuming generated material is unrestricted.
8. **Be transparent.** Record material agent assistance and any required approvals in the work item or pull request, following the team's applicable disclosure and audit requirements.

## 4. Roles and responsibilities

| Role | Responsibilities |
|---|---|
| BA / product owner | Defines the problem, users, priorities, acceptance criteria, and business approvals. |
| Human owner / engineer | Selects an appropriate agent and scope; protects data; directs and supervises work; validates output; maintains traceability; and remains responsible for the change. |
| Reviewer | Reviews the change as software, not as “AI-generated code”; checks requirements, design, security, tests, maintainability, and evidence. |
| Tech lead / architect | Resolves significant design and risk questions and approves required architecture or exception decisions. |
| Security / privacy / compliance owner | Advises on sensitive data, threat models, regulated use, security findings, and policy exceptions. |
| Release owner / on-call engineer | Controls release authorization, deployment, monitoring, and rollback under the existing release and incident processes. |

One person may hold multiple roles where team size requires it, but the author must not waive mandatory independent review or approval controls.

## 5. SDLC phases

**Document organization:** every document produced by a phase is kept in the project's `docs/` folder, inside the sub-folder numbered for that phase, so the artifacts of a phase are always found in the same place. Do not create a competing top-level location for phase documents, and do not leave them loose in `docs/` or in the repository root.

| Phase | Sub-folder | Documents |
|---|---|---|
| 5.2 Requirements and discovery | docs/02-requirements/ | BRD.md |
| 5.3 Analysis | docs/03-analysis/ | SRS.md or PRD.md, USER_STORIES.md |
| 5.4 Design, modeling | docs/04-design/ | SAD.md, the blueprint design (.md or .sql), diagrams/*.drawio, UI_UX_design/ |
| 5.5 Planning | docs/05-planning/ | PLAN.md, tasks/*.md |

A phase that keeps a document rather than a work item, pull request or system record files it in its own numbered sub-folder as well — docs/07-verification/, docs/09-release/, docs/10-operations/, docs/11-decommissioning/. Records that live in the tracker, the review system or the incident system stay there and are linked from the work item instead of being duplicated under `docs/`.

### 5.1 General 

1. Goal: turn an intake request into a bounded work item with a named owner, acceptance criteria and a risk tier, so that every later phase has a clear starting point.
2. Agentic in intake: the requester or human owner may use an agent to draft the problem statement, scope or acceptance criteria, and the AI agent should be active in investigating the request, prior art and constraints and put all questions or requests that it need to make clear. The human owner remains accountable for the intake record.

**Risk tiers and minimum controls**

| Tier | Examples | Minimum controls |
|---|---|---|
| Low | Documentation, isolated tests, small non-sensitive UI or utility change | Human owner; focused diff; relevant checks; normal review. |
| Medium | Business logic, APIs, dependencies, data handling, authentication-adjacent changes | Human owner; documented acceptance criteria; focused tests; security-aware review; all required CI checks. |
| High | Authentication/authorization, cryptography, payments, sensitive data, safety-critical behavior, production infrastructure, migrations with material impact | Named technical owner; threat/risk assessment as applicable; qualified independent review; explicit domain/security approval where required; staged release and rollback plan. |

Use the highest applicable tier. Existing organizational or regulatory controls take precedence when stricter.

3. Release: the tracked work item, containing the owner, acceptance criteria, risk tier, and the required approvals or reviews identified.
4. Review and approval: the requester confirms that the problem and the desired outcome are represented accurately before the work item is handed to requirements and discovery.

**Exit criteria:** The work item has an owner, acceptance criteria, risk tier, and any required approvals or reviews identified.

**How to finish this phase**

- Put the problem statement, intended users, scope, priority, owner, acceptance criteria, and risk tier in the tracked work item.
- Record the required reviewers, specialist approvals, and any constraints on agent/tool or data use.
- Confirm the requester agrees that the problem and desired outcome are represented accurately. Hand the work item to the person responsible for requirements and discovery.
- Do not begin implementation while ownership, the expected outcome, or a material risk/approval requirement is unclear.

### 5.2 Requirements and discovery

1. Goal: create the BRD (Business Requirements Document)
2. Agentic in BA: The BA should create an agent for this role, the AI agent should be active in investigating and put all questions or requests that it need to make clear.
3. Release: a BRD.md in docs/02-requirements/ of the current project.
4. Review and approval: Request PM/PO for reviewing.

### 5.3 Analysis

1. Goal: analyze the approved BRD and baseline the requirements as an SRS (Software Requirements Specification) for engineering-led or regulated work, or a PRD (Product Requirements Document) for product-led work, together with the user stories that implement it. Use the repository prompts (`PRD_prompt.md`, `PRD_Prompt_IEEE_standard.md`) and check the result against `PRD_IEEE_29148_Checklist.xlsx`.
2. Agentic in BA/Dev: The BA or Developer should create an agent for this role, the AI agent should be active in analyzing the BRD and the source evidence, deriving and challenging requirements, and put all questions, ambiguities or requests that it need to make clear.
3. Analysis: make every requirement specific, measurable, testable and traceable to the BRD requirement ID it comes from. Resolve conflicting, duplicate or assumed requirements with the requester before baselining, and record anything still unresolved as an open question or risk instead of an accepted requirement.
4. User stories: write one story per user-visible outcome in "As a <role>, I want <capability>, so that <benefit>" form, with explicit acceptance criteria and the requirement IDs it covers. Keep each story small enough to size, sequence and verify on its own.
5. Release: a SRS.md or PRD.md, and a USER_STORIES.md, in docs/03-analysis/ of the current project.
6. Review and approval: Request PM/PO for reviewing, and the tech lead / architect as well when requirements affect architecture, data or non-functional targets.

### 5.4 Design, modeling

1. Goal: create the SAD (Software Architecture Document) that translates the approved BRD into an implementable design using the 4+1 architectural view model, together with the IEEE 1016-2009 blueprint and the UI/UX design that implement it.
2. Agentic in SA/Designer: The SA or Designer should create an agent for this role, the AI agent should be active in investigating the BRD, the existing codebase and the technical constraints, and put all questions, assumptions or requests that it need to make clear.
3. Modeling: document the architecture in the five concurrent views below, one canonical diagram per view, and record the BRD requirement IDs that each view satisfies.

| View | What it describes | Diagram | Prompt / checklist |
|---|---|---|---|
| Logical | Functional requirements: key abstractions, domain entities and their relationships | Class diagram | `classDiagram_prompt.md`, `Class_Diagram_UML2.0_Checklist.xlsx` |
| Process | Concurrency, performance, throughput and runtime behavior | Activity and sequence diagrams | `activityDiagram_prompt.md`, `sequenceDiagram_prompt.md`, `Activity_Diagram_UML2.0_Checklist.xlsx`, `Sequence_Diagram_UML2.0_Checklist.xlsx` |
| Development | Static organization in the development environment: layers, packages, modules and build units | Component diagram | `componentDiagram_prompt.md`, `Component_Diagram_UML2.0_Checklist.xlsx` |
| Physical | Mapping of software components onto infrastructure nodes | Deployment diagram | `deploymentDiagram_prompt.md`, `Deployment_Diagram_UML2.0_Checklist.xlsx` |
| Scenarios | The few key use cases that validate the other four views | Use case diagram | `useCase_prompt.md`, `UseCase_Document_UML2.0_Checklist.xlsx` |

4. Diagram format: every diagram must be saved as an editable `.drawio` file (draw.io / diagrams.net). Export PNG or SVG only for embedding in the SAD; the `.drawio` file is the source of truth. Do not commit a diagram that exists only as an image, and do not hand-edit exported files.
5. Blueprint design: produce the IEEE 1016-2009 Software Design Description with `bluePrint_design_prompt.md` and check it against `BluePrint_Design_IEEE_1016_2009_Checklist.xlsx`, keeping full traceability from stakeholder concerns to design elements. Save the blueprint as a .md (or .sql) file in docs/04-design/.
6. UI/UX design: translate the approved blueprint into the user interface using `UI-UX-Design_prompt.md`, deriving personas, interaction flows and design-system tokens from it, and check the result against `UI_UX_Design_IEEE-1016-2009_Checklist.xlsx`. Every screen must serve a persona goal and meet WCAG 2.1 AA; save the Figma frames and/or HTML pages in ./docs/04-design/UI_UX_design.
7. Screen traceability: add every designed screen to the appropriate section of USER_STORIES.md, naming the story or epic it serves and the requirement IDs it covers. A screen that maps to no story is either a missing story or out of scope; resolve it before the design is baselined.
8. Release: a SAD.md in docs/04-design/ of the current project, the blueprint design, the diagram sources in docs/04-design/diagrams/ — `logical-view.drawio`, `process-view.drawio`, `development-view.drawio`, `physical-view.drawio`, `scenarios-view.drawio` — and the UI/UX designs in docs/04-design/UI_UX_design/.
9. Review and approval: Request the tech lead / architect for reviewing, the security owner as well when the design touches sensitive data, authentication or external interfaces, and the PM/PO when the design changes user-visible behavior.

### 5.5 Planning

1. Goal: turn the approved SAD and the baselined requirements into an executable plan the team can commit to before implementation starts.
2. Agentic in planning: the PM or tech lead should create an agent for this role, the AI agent should be active in deriving the work breakdown, dependencies, sequencing and estimates from the SAD and the USER_STORIES.md, and put all assumptions, questions or requests that it need to make clear.
3. Plan: break the design into deliverable slices, each sized to a reviewable change, with sequencing, dependencies, estimates, owners and the requirement IDs it satisfies.
4. Decisions and risks: record significant architecture and scope decisions with their rationale, and keep open risks, unknowns and gaps visible with an owner until resolved.
5. Release: a PLAN.md and all task files as docs/05-planning/tasks/task_name-or-id.md, or the equivalent backlog or roadmap entries linked from the work item. Each task must be simple and clear, ready for coding (like a module, a class, a method or a function) and could be finished with a few iterations by agents with a small LLM model. 
6. Review and approval: Request PM/PO for reviewing the scope and sequencing, and the tech lead / architect for the technical feasibility and dependencies.

### 5.6 Implementation

1. Goal: implement the approved design and plan as a bounded, reviewable change that its human owner can explain, validate and defend.
2. Agentic in engineering: the human owner should create an agent for this role, the AI agent should be active in investigating the repository instructions, the SAD and the existing tests, and put all questions or requests that it need to make clear. The human owner remains accountable for every agent-assisted edit.
3. Work on the approved branch or isolated workspace. Confirm the correct repository, branch, and working-tree state before edits.
4. Provide the agent a bounded task, constraints, acceptance criteria, and relevant repository instructions. Ask it to avoid unrelated refactors and generated or vendored files unless specifically in scope.
5. Grant only the permissions necessary. Review proposed edits and commands before allowing destructive, networked, privileged, or broad-scope operations.
6. Do not place credentials or sensitive data in prompts, source code, logs, or test fixtures. Use approved secret-management and test-data mechanisms.
7. Keep changes incremental. Inspect the diff after each meaningful step; stop and correct scope drift before continuing.
8. The human owner must be able to explain the changed behavior and important implementation choices. Rewrite or remove code that cannot be understood or validated.
9. Do not allow an agent to fabricate test results, issue status, approvals, citations, or tool outcomes. Verify claims using repository state and command output.
10. Record significant agent use in the work item or pull request. Include the tool or agent identifier when required by internal policy; never record sensitive prompt content.
11. Release: the change committed to the approved branch and pushed for review, linked to the work item with a summary of what changed and any deviation from the approved design.
12. Review and approval: the human owner confirms the complete diff is intentional and understood before requesting review in 5.8; an agent must not approve, merge or deploy its own change.

**Exit criteria:** The change is bounded, understandable to its owner, consistent with the approved approach, and ready for verification.

**How to finish this phase**

- Inspect the complete working diff and confirm it implements the agreed scope without unrelated edits, temporary files, debug code, or unintended generated changes.
- Ensure the change is saved in the team's normal version-control workflow and linked to the work item. Summarize what changed and disclose deviations from the approved plan.
- Record known gaps, follow-up work, or behavior that needs special verification. Hand the change and context to verification; do not present an agent's completion message as proof the work is finished.
- Do not mark implementation ready while the owner cannot explain or validate the changed behavior.

### 5.7 Verification and testing

1. Goal: produce evidence, appropriate to the risk tier, that the change meets its acceptance criteria and does not regress existing behavior.
2. Agentic in QA: the verification owner should create an agent for this role, the AI agent should be active in selecting, drafting and running checks and in triaging failures, and put all questions or requests that it need to make clear. An agent's report that a check passed is not evidence; inspect the actual command output and results.
3. Scope: the human owner selects and runs verification appropriate to the change. At minimum:
   - Review the complete diff, including generated files, dependency changes, configuration, and deleted files.
   - Run relevant unit and integration tests, linting, formatting, type checks, and build checks defined by the project. Use `testPlan_prompt.md` and `Test_Plan_IEEE_829_Checklist.xlsx` where a test plan is required.
   - Add or update tests for changed behavior, important edge cases, and regressions. Tests must assert meaningful outcomes; do not add tests that simply mirror implementation or weaken existing assertions to make them pass.
   - For API, schema, or data changes, check compatibility, migration behavior, error handling, and rollback or recovery requirements.
   - For security-sensitive changes, perform the required threat-model review and security scans or specialist review. Inspect agent-suggested dependencies and code for known vulnerabilities, unsafe defaults, injection, authorization gaps, insecure cryptography, and unintended data exposure.
   - For user-facing changes, verify accessibility, localization, and supported browser/device behavior where applicable.
   - Review failures rather than asking an agent to suppress them. A failing or skipped required check must be resolved or explicitly handled through the team's documented exception process.
   - Report which checks ran and their actual results in the pull request or work item. Clearly identify checks not run and why.
4. Release: the recorded test evidence — the commands or checks run, their results, and the commit or change set tested — attached to the work item or pull request.
5. Review and approval: the reviewer confirms the evidence covers the acceptance criteria and that limitations and skipped checks are disclosed before approval.

**Exit criteria:** Required checks pass; failures and limitations are disclosed; evidence supports the acceptance criteria.

**How to finish this phase**

- Map acceptance criteria to tests or other concrete evidence and record the actual commands/checks run, results, and the commit or change set tested.
- Fix failures and rerun affected checks. Explicitly document checks not run, environmental limitations, and residual risks; obtain an approved exception where required.
- Confirm test coverage exercises changed behavior and important edge cases, not only the implementation's happy path. Hand the evidence and any disclosed limitations to the reviewer.
- Do not advance with failing required checks or unexplained results.

### 5.8 Code review and approval

1. Goal: obtain independent, qualified review of the change as software, and the approvals its risk tier requires, before merge.
2. Agentic in review: a reviewer may use an agent to summarize or analyze a diff, but the agent is never the reviewer or approver and cannot satisfy a required independent review. The human reviewer remains accountable for the approval decision.
3. Open a pull request or equivalent review request linked to the work item. Summarize the problem, behavior change, risk tier, test evidence, rollout considerations, and material agent assistance.
4. A qualified reviewer independently checks:
   - correctness against requirements and acceptance criteria;
   - scope, design, maintainability, and consistency with repository conventions;
   - tests and evidence, including meaningful edge cases;
   - security, privacy, authorization, and data-handling implications;
   - dependency, licensing, accessibility, operational, and compatibility implications as applicable;
   - whether generated artifacts and the full diff are intended.
5. Review the code itself, not just the agent's explanation, summary, or claimed test results.
6. Resolve all blocking comments. Re-run affected checks after changes. Obtain required domain, security, or architecture approvals for the risk tier.
7. Do not merge with failing required checks, missing mandatory approvals, unresolved blocking findings, or an unapproved exception.
8. Release: the approval record applied to the exact commit intended for merge, linked from the work item, with any accepted non-blocking follow-up recorded with an owner.
9. Review and approval: a qualified reviewer other than the author, plus the domain, security or architecture approvers the risk tier requires.

**Exit criteria:** Required independent reviews and checks are complete, and the change is approved under the normal branch protection policy.

**How to finish this phase**

- Resolve each blocking review comment and reply with the change or rationale. Re-run checks affected by review updates.
- Confirm approvals and required checks apply to the exact commit intended for merge. Record any accepted non-blocking follow-up with an owner.
- Hand the approved change, release notes or summary, and deployment considerations to the release owner. Do not self-waive a required independent approval.
- Do not merge until branch-protection and policy requirements are satisfied.

### 5.9 Release and deployment

1. Goal: deploy the reviewed artifact to production under the existing release process, with the ability to detect and reverse an unhealthy release.
2. Agentic in release: the release owner may use an agent to prepare release notes, analyze deployment options or summarize health signals, but the agent must not authorize, merge or execute privileged production changes.
3. Follow the existing release process and change-management requirements. Agent-assisted changes receive no reduced review or release control.
4. Before release, confirm the artifact corresponds to the reviewed commit and that required checks and approvals remain valid.
5. Confirm release notes, feature flags, migration sequence, monitoring, support readiness, and rollback or recovery steps as applicable.
6. A human release owner authorizes and performs or supervises deployment. The agent may help prepare or analyze release materials but must not autonomously authorize or execute privileged production changes.
7. Deploy using staged rollout, canary, or other risk-appropriate controls where available. Observe health indicators and stop or roll back when thresholds or release criteria are not met.
8. Release: the deployed artifact and its release record — version or commit, environment, deployment time, authorizing release owner, and rollout result.
9. Review and approval: a human release owner authorizes the release and confirms required checks and approvals remain valid for the exact artifact released.

**Exit criteria:** A human authorized the release, deployment evidence is recorded, and the service is stable or the rollback/incident process is active.

**How to finish this phase**

- Record the released version or commit, environment, deployment time, authorizing release owner, and rollout result in the normal release record.
- Verify post-deployment health against pre-agreed indicators and observation windows. Record any deviations, incidents, rollback, or mitigation and link the incident record if one was opened.
- Hand the service to its operational owner with current runbooks, dashboards, alerts, support contacts, and any active watch items.
- Do not declare the release complete while required health checks are outstanding or a release-impacting issue has no owner and response plan.

### 5.10 Operations, incidents, and maintenance

1. Goal: keep the running service healthy and the operational record current, and handle defects and incidents that follow a release.
2. Agentic in operations: the service or on-call owner may create an agent for this role, the AI agent should be active in investigating telemetry, logs and incident evidence and put all questions or requests that it need to make clear, subject to the data-handling rules below.
3. Monitor service health and user impact after deployment according to the service's operational requirements.
4. Agents may assist with log analysis, incident summaries, or remediation proposals only when the tool is approved for the data involved. Redact sensitive information and validate conclusions against authoritative telemetry.
5. During an incident, the incident commander and authorized operators retain decision-making and execution authority. Never let an agent independently change production or communicate unverified conclusions as facts.
6. Treat an agent-introduced defect as a normal defect or incident. Preserve relevant evidence, follow incident reporting requirements, and include agent use in the post-incident review where useful.
7. Feed verified lessons into tests, documentation, prompts, repository instructions, and this SOP without embedding secrets or sensitive incident data.
8. Release: the updated operational record — runbooks, dashboards, alerts, support contacts and active watch items — handed to the service owner.
9. Review and approval: the service owner accepts outstanding operational risks, and the incident commander owns incident decisions and their follow-up actions.

**Exit criteria:** Operational ownership, monitoring, alerting, and support information are current; incidents and follow-up actions are tracked.

**How to finish this phase or operational work item**

- For a change's post-release watch, compare observed behavior to the release success criteria and observation window; record the result and close or extend the watch explicitly.
- For an incident, use the incident process to record impact, timeline, verified cause (if known), recovery, and follow-up actions with owners and due dates. Do not state an unverified agent analysis as fact.
- For routine maintenance, link the completed work to its issue, verification evidence, and any updated operational documentation. Confirm the service owner has accepted outstanding operational risks.
- Keep the service's operational ownership active until a separately approved decommissioning process completes; closing a deployment task does not mean the service itself is retired.

### 5.11 Decommissioning

1. Goal: retire a feature, service or repository without leaving data, access, dependencies or customer commitments unresolved.
2. Agentic in decommissioning: the accountable owner may create an agent for this role, the AI agent should be active in inventorying dependents, data and access to be removed and put all questions or requests that it need to make clear. An agent's confirmation is never accepted as evidence of deletion or compliance.
3. For feature, service, or repository retirement, follow the normal decommissioning process. Verify data retention/deletion, access revocation, dependency cleanup, customer communication, and monitoring for residual use. Do not rely on an agent to certify deletion or compliance; obtain evidence from the authoritative systems and owners.
4. Release: the decommissioning record — retirement date, accountable owner, evidence from the authoritative systems, approvals, exceptions and any residual risks.
5. Review and approval: Request the service, data, security and business owners for reviewing and accepting the retirement evidence before the work item is closed.

**Exit criteria:** Required owners accept the retirement evidence; approved data disposition and access revocation are verified; residual risks and follow-up actions have owners.

**How to finish this phase**

- Obtain the required service, data, security, and business approvals, and record the retirement date and accountable owner.
- Verify using authoritative systems that traffic and scheduled work have stopped, access and credentials have been revoked, dependencies/resources have been removed, and data was retained or deleted as approved.
- Record evidence, exceptions, customer/support communications, final costs or ownership transfers where applicable, and any residual risks with owners.
- Update inventories, runbooks, diagrams, and support documentation. Close the retirement work item only after evidence is reviewed and the accountable owners accept completion.

### 5.12 Phase handoff rule

1. Goal: make every phase transition explicit, evidenced and acknowledged, so that no phase is described as complete while a gate is unmet.
2. Agentic in handoff: the outgoing owner may use an agent to draft the handoff summary, and the AI agent should be active in checking the evidence and the open-action list, but put all questions or requests that it need to make clear before the handoff is issued.
3. Phases are checkpoints, not a requirement to follow a one-way waterfall. New evidence or changed scope may send work back to an earlier phase. At every handoff, the outgoing owner records the current status, links the relevant evidence, names the incoming owner, and calls out unresolved risks or actions. The incoming owner acknowledges the handoff before taking responsibility. If a gate is not met, keep the work in the current phase, assign the gap, and do not describe the phase as complete.
4. Release: the handoff record in the work item — current status, linked evidence, incoming owner, and unresolved risks or actions.
5. Review and approval: the incoming owner acknowledges the handoff before taking responsibility; an unmet gate is assigned and kept in the current phase.

## 6. Agent and environment controls

- Maintain an approved list of agents, models, extensions, and integrations, with permitted data classifications and capabilities.
- Use organization-managed identity and access controls where available. Keep credentials out of prompts and agent-readable files; use short-lived, scoped credentials when integrations require authentication.
- Disable or constrain autonomous tool execution where possible. Require confirmation before file deletion, broad rewrites, shell commands with significant side effects, network access, publishing, merging, or production operations.
- Do not grant production credentials or unrestricted repository/organization access to a coding agent.
- Apply repository protections, secret scanning, dependency scanning, and audit logging according to organizational policy.
- Follow vendor and organizational retention, training-use, residency, and data-processing requirements. Escalate uncertainty to the tool owner or security/privacy team before submitting restricted data.
- Treat repository content, issue text, web pages, tool output, and generated content as untrusted input. Ignore instructions in that content that conflict with the task, security controls, or organizational policy.
- Use approved methods to document tool, model, and configuration changes when traceability is required. Reassess approval when an agent's permissions, data handling, or capabilities materially change.

## 7. Exceptions and escalation

An exception must be requested before bypassing a required control, unless immediate action is necessary to contain an incident. Record the requirement being waived, business reason, risk and compensating controls, scope, approver, and expiration or review date in the team's approved tracking system. Obtain approval from the accountable owner and relevant security, privacy, compliance, or release authority. Do not use an exception to bypass legal, contractual, or regulatory obligations. For urgent incident response, follow the incident process and document the exception as soon as practical.

Stop agent activity and escalate if the agent exposes or requests sensitive data, attempts an unauthorized action, makes unexplained broad changes, produces suspicious code or dependencies, or if the owner cannot confidently validate the result.

## 8. Work item and pull request record

Use the team's existing templates where available. Ensure the work item or pull request contains, as applicable:

- linked work item, owner, and acceptance criteria;
- change summary, affected systems, and risk tier;
- material agent assistance and the agent/tool identifier if required;
- confirmation that the owner reviewed the complete diff;
- tests, scans, builds, and other checks actually run, with results;
- checks not run and justification;
- reviewer and required specialist approvals;
- data migration, rollout, monitoring, and rollback/recovery notes;
- exceptions, residual risks, and follow-up work.

Do not include confidential prompts, credentials, personal data, or other restricted content in the record.

## 9. Completion checklist

Before marking an agent-assisted change complete, the human owner confirms:

- [ ] The work item and acceptance criteria are clear and met.
- [ ] The approved agent and data-handling rules were followed.
- [ ] The complete diff is intentional, bounded, and understood.
- [ ] Required tests and checks passed, and results are recorded.
- [ ] Required reviewers and specialist approvers approved the change.
- [ ] Security, privacy, compatibility, accessibility, and operational impacts were addressed as applicable.
- [ ] Release, monitoring, and rollback/recovery needs are ready.
- [ ] Documentation and follow-up items are updated.

## 10. Process health

Engineering leadership should periodically evaluate whether this SOP is effective using a balanced set of signals: escaped defects, security/privacy incidents, change failure and rollback rates, review and test quality, delivery time, and engineer feedback. Do not optimize solely for code volume, agent usage, or raw speed. Use results to improve the workflow, tools, training, and controls.
