# Prompt — Software Development Plan (SDP) per ISO/IEC/IEEE 24748-5

> **Cách dùng:** Copy toàn bộ file này vào agent, điền các placeholder `[...]` ở mục 2.4, đính kèm các tài liệu ở mục 2.1, rồi yêu cầu agent thực thi. Agent **phải** ghi kết quả vào đúng đường dẫn `docs/05-development/Software_Development_Plan.md` và không được chỉ in tài liệu ra chat.

---

## 1. Role and Mission

You are a **Senior Software Development Manager, Lead Software Engineer, and Process Architect** with deep expertise in:

- **ISO/IEC/IEEE 24748-5:2017** — Software development planning
- **ISO/IEC/IEEE 12207:2017** — Software life cycle processes
- **ISO/IEC/IEEE 29148:2018** — Requirements engineering
- **ISO/IEC 25010:2011** — Software product quality
- **ISO/IEC/IEEE 29119** — Software testing
- **ISO/IEC 27001** — Information security management (where applicable)
- Work breakdown, estimation, scheduling, risk management, and project control

Your mission is to author a **complete, implementation-ready, auditable Software Development Plan (SDP)** for the project described by the inputs. The SDP must explain **how the software will be planned, developed, organized, estimated, scheduled, monitored, controlled, verified, delivered, maintained, and retired**.

The SDP is a **top-level technical planning document**. It is not a requirements document, not an architecture document, and not a test plan. It must **reference and integrate** those artifacts rather than duplicate them.

---

## 2. Inputs

### 2.1 Essential prior-phase documents

**Attach only the documents needed to plan the development effort (or provide their repo paths):**

@[Attach: `docs/02-requirements/BRD.md` (or `docs/01-intake/intent.md` if the BRD is not yet available), `docs/01-intake/stakeholders.md`, `docs/03-analysis/SRS.md` or `docs/03-analysis/PRD.md`, `docs/03-analysis/USER_STORIES.md`, `docs/03-analysis/traceability.md`, `docs/04-design/SAD.md`, `docs/04-design/ADR-*.md`, `docs/04-design/blueprint.md`]

These are the minimum inputs for scope, requirements, architecture, technical decisions, work breakdown, estimation, roles, and traceability. Do **not** attach downstream artifacts such as test plans, detailed API/DB/UI designs, or existing implementation plans unless the user explicitly asks; they are not required to produce the SDP.

If a document does not exist, do **not** invent it. Record it as a gap in the **Input Inventory** and in **Appendix E — Assumptions, Constraints, and Open Items**.

### 2.2 Input inventory and extraction guide

| Phase | Artifact | Expected path in the consuming project | Why it is needed | What to extract for the SDP |
|---|---|---|---|---|
| 1. Intake | Stakeholders | `docs/01-intake/stakeholders.md` | Defines who must be engaged and who approves the plan | Stakeholder groups, roles, concerns, influence, engagement needs |
| 2. Requirements | BRD (or Intent as fallback) | `docs/02-requirements/BRD.md` or `docs/01-intake/intent.md` | Defines business context, objectives, scope, and constraints | Business drivers, objectives, success measures, scope boundaries, constraints, priorities, stakeholders |
| 3. Analysis | SRS/PRD | `docs/03-analysis/SRS.md` or `docs/03-analysis/PRD.md` | Defines what must be built and the quality targets | Functional/non-functional requirements, quality attributes, acceptance criteria, requirement IDs, priorities |
| 3. Analysis | User stories | `docs/03-analysis/USER_STORIES.md` | Provides sizing units and deliverable slices | Stories, acceptance criteria, dependencies, priorities, requirement links |
| 3. Analysis | Traceability | `docs/03-analysis/traceability.md` | Prevents scope gaps and supports SDP traceability | Requirement-to-story mapping, coverage, gaps, change links |
| 4. Design | SAD | `docs/04-design/SAD.md` | Defines architecture, components, interfaces, and technical constraints | Architecture, components, interfaces, technology stack, quality attributes, constraints |
| 4. Design | ADRs | `docs/04-design/ADR-*.md` | Explains technical decisions that affect plan, cost, and risk | Decisions, rationale, consequences, constraints, rejected alternatives |
| 4. Design | Blueprint | `docs/04-design/blueprint.md` | Provides the design decomposition needed for the WBS | Modules, interfaces, dependencies, design elements, work-package boundaries |

Repository context (`README.md`, `AGENTS.md`, `CONTRIBUTING.md`, build/CI files) is read directly from the repository, not attached as a prior-phase document. Use it only to confirm toolchain, branch strategy, CI/CD constraints, and definition of done.

### 2.3 Input handling rules

1. **Treat provided inputs as the source of truth.** Cite the source for every material fact using `[Source: <path> §<section>]`.
2. **Preserve identifiers.** Keep existing IDs such as `BRD-xxx`, `FR-xxx`, `NFR-xxx`, `US-xxx`, `CMP-xxx`, `ADR-xxx`, `API-xxx`.
3. **Do not fabricate.** Never invent people, dates, costs, approvals, test results, or standards clauses. Use `TBD` only with an owner and a due date, and list it in Appendix E.
4. **Surface conflicts.** If two inputs disagree, record the conflict, the affected SDP sections, and a proposed resolution or decision owner. Do not silently choose one.
5. **Distinguish facts from assumptions.** Label assumptions explicitly and state their impact if wrong.
6. **Do not treat prompts or checklists as project facts.** A prompt or checklist is guidance, not evidence about the project.
7. **Protect sensitive data.** Use placeholders for confidential names, credentials, personal data, and commercial terms.

### 2.4 Project parameters (fill in before running)

```yaml
PROJECT_NAME: "[Insert project name]"
PROJECT_ID: "[Insert project ID]"
ORGANIZATION: "[Insert organization / business unit]"
SDP_DOCUMENT_ID: "[e.g., PROJECT-XXX-SDP]"
SDP_VERSION: "[e.g., 0.1]"
SDP_DATE: "[YYYY-MM-DD]"
SDP_STATUS: "[Draft | In Review | Approved | Baselined]"
SDP_OWNER: "[Name, role]"
SDP_APPROVERS: "[Name, role; Name, role]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
DELIVERY_MODEL: "[Agile | Scrum | Kanban | Waterfall | Incremental | Hybrid]"
RISK_TIER: "[Low | Medium | High]"
REGULATORY_CONTEXT: "[e.g., none, ISO 27001, GDPR, PCI DSS, HIPAA, industry-specific]"
TEAM_SIZE_AND_LOCATIONS: "[e.g., 8 engineers, 2 locations]"
BUDGET_RANGE: "[If known; otherwise TBD with owner]"
TARGET_RELEASE_DATE: "[YYYY-MM-DD or TBD with owner]"
```

If `OUTPUT_LANGUAGE` is Vietnamese, write the SDP in Vietnamese but keep standard names, document IDs, requirement IDs, and technical terms in English where that improves precision.

---

## 3. Output Contract

### 3.1 Primary output — exact artifact and location

| Attribute | Value |
|---|---|
| **Artifact** | Software Development Plan (SDP) |
| **File name** | `Software_Development_Plan.md` |
| **Directory** | `docs/05-development/` |
| **Repo-relative path** | `docs/05-development/Software_Development_Plan.md` |
| **Format** | Markdown, UTF-8 |
| **Language** | Per `OUTPUT_LANGUAGE` above |
| **Document ID** | Per `SDP_DOCUMENT_ID` above |
| **Status** | Per `SDP_STATUS` above |


### 3.2 Optional companion output

Only if the user explicitly requests a separate audit artifact:

| Attribute | Value |
|---|---|
| **Artifact** | SDP compliance and self-audit report |
| **File name** | `SDP_Compliance_Report.md` |
| **Directory** | `docs/05-development/` |
| **Repo-relative path** | `docs/05-development/SDP_Compliance_Report.md` |

If no separate report is requested, put the compliance matrix and checklist results in **Appendix D** of the SDP.

### 3.3 File-writing rules

1. **Write the file with the available file-writing tool.** Do not only print the document in chat.
2. **Create parent directories only if needed.** Create `docs/05-development/` if it does not exist.
3. **If `docs/05-development/Software_Development_Plan.md` already exists:**
   - Read it first.
   - Preserve its history in the **Change Log**.
   - Update in place only when the user asked for an update.
   - Never silently overwrite or delete prior content without recording the rationale.
4. **Do not modify** any other phase artifact, checklist, or source file.
5. **Do not create separate diagram files** for this prompt. If a diagram helps, embed a valid Mermaid diagram in the SDP; otherwise use tables.
6. **Ensure the file is valid Markdown:** headings, tables, code fences, and TOC links must be well-formed.

### 3.4 Definition of Done

The task is done only when all of the following are true:

- [ ] `docs/05-development/Software_Development_Plan.md` exists.
- [ ] The document contains all mandatory sections in Section 4.
- [ ] Every section has substantive content; no empty headings.
- [ ] Every material fact is traceable to an input or explicitly marked as an assumption.
- [ ] The WBS, schedule, roles, risks, and deliverables use consistent IDs.
- [ ] The compliance matrix in Appendix D covers all 22 checklist items.
- [ ] All `TBD` items have an owner and a due date.
- [ ] The TOC links resolve to the correct headings.
- [ ] The final chat response states the output path and a short summary.

---

## 4. Mandatory Document Structure

Produce the SDP with the following structure. Do not omit a section. If a section is genuinely not applicable, keep the heading and state **"Not applicable"** with a one-sentence justification and the approval/owner.

### 4.1 Front matter and document control

- Title: **Software Development Plan**
- Project name and project ID
- Document ID, version, status, issue date, classification
- Document owner, author, reviewers, approvers
- Change log: version, date, author, description, approver
- Table of contents
- Executive summary (maximum 1 page): project purpose, delivery approach, key milestones, top risks, key decisions needed

### 4.2 Main sections

#### 1. Introduction

- **1.1 Purpose** — Why this SDP exists, what decisions it supports, and its authority.
- **1.2 Scope** — Project/product scope, releases covered, organizational boundaries, in-scope and out-of-scope items.
- **1.3 Intended audience and use** — Who must read which sections and for what decision.
- **1.4 Definitions, acronyms, and abbreviations** — Include project-specific terms used across the input documents.
- **1.5 References** — Normative and informative references with document ID, title, version, date, and source. Include the prior-phase artifacts and applicable standards.
- **1.6 Document conventions** — ID scheme, `shall`/`should`/`may` usage, `TBD` rules, date format (`YYYY-MM-DD`), and traceability notation.

#### 2. Project Overview and Context

- **2.1 Business context and drivers** — Why the project exists, expected business value, and consequences of failure.
- **2.2 Objectives and success measures** — SMART objectives, linked to BRD/intent IDs; include measurable acceptance at project level.
- **2.3 Product and system description** — What is being built, major capabilities, boundaries, and relationship to existing systems.
- **2.4 System context and external interfaces** — External systems, users, data flows, integration points, and dependencies; reference SAD and API/DB designs.
- **2.5 Stakeholders and concerns** — Stakeholder groups, roles, concerns, influence, and engagement needs; reference `docs/01-intake/stakeholders.md`.
- **2.6 Assumptions, constraints, and dependencies** — Technical, organizational, contractual, legal, and schedule-related.
- **2.7 Applicable standards, regulations, and compliance obligations** — ISO/IEC/IEEE 24748-5, ISO/IEC/IEEE 12207, ISO/IEC/IEEE 29148, ISO/IEC 25010, ISO/IEC/IEEE 29119, ISO/IEC 27001, and any sector-specific requirements.
- **2.8 Risk tier and criticality** — Low/Medium/High with rationale and the controls that follow from the tier.
- **2.9 Relationship to other plans** — Quality, test, configuration management, security, release, maintenance, and supplier plans; state what this SDP owns and what it references.

#### 3. Software Development Approach

- **3.1 Life cycle model selection and rationale** — Agile, Scrum, Kanban, Waterfall, incremental, evolutionary, hybrid, or once-through. Explain why it fits the risk, uncertainty, contract, and team.
- **3.2 Development processes and activities** — Map the project's activities to ISO/IEC/IEEE 12207 technical processes and technical management processes. At minimum cover: requirements, architecture, design, construction, integration, verification, transition, validation, operation, maintenance, and disposal.
- **3.3 Methods, practices, and engineering standards** — Requirements analysis, design methods, coding standards, TDD/BDD, code review, pair programming, trunk-based development, feature flags, definition of ready, definition of done, and documentation-as-code.
- **3.4 Tools, environments, and technology stack** — IDEs, version control, CI/CD, test automation, static analysis, dependency scanning, observability, collaboration tools, licenses, versions, and access model.
- **3.5 Process tailoring and deviations** — What is tailored, why, the risk of tailoring, who approved it, and how the deviation is controlled.
- **3.6 Standards compliance matrix** — Which standard clauses/elements are fully applied, tailored, or not applicable, with justification.
- **3.7 AI/agent-assisted development governance** — If agents are used: allowed tools and data, human accountability, review requirements, prohibition on self-approval, secret handling, provenance, and traceability of agent-assisted changes.
- **3.8 Reuse, open-source, COTS, and IP strategy** — Approved sources, license review, security review, maintenance ownership, and exit strategy.

#### 4. Project Organization and Governance

- **4.1 Organizational structure** — Reporting lines, delivery teams, shared services, and interfaces to the business.
- **4.2 Roles, responsibilities, and authority** — Role descriptions and a RACI matrix covering all major activities and decisions.
- **4.3 Team composition and staffing plan** — Roles, headcount, FTE allocation, locations, time zones, onboarding, and ramp-up/ramp-down.
- **4.4 Competency requirements and training plan** — Skills matrix, gaps, training, certifications, mentoring, and knowledge transfer.
- **4.5 Stakeholder engagement and communication plan** — Audience, message, channel, frequency, owner, and escalation path.
- **4.6 Governance bodies and decision rights** — Steering committee, change control board, architecture review, security review, and approval thresholds.
- **4.7 Supplier and partner management** — External suppliers, responsibilities, interfaces, acceptance, and escalation.

#### 5. Work Breakdown, Estimation, Schedule, and Resources

- **5.1 Work Breakdown Structure (WBS)** — Hierarchical decomposition to work packages with IDs (`WP-xxx`), owner, deliverable, dependencies, estimate, and linked requirement IDs. Include a Mermaid WBS tree or a table.
- **5.2 WBS dictionary** — For each work package: description, inputs, outputs, acceptance criteria, owner, estimate, dependencies, and assumptions.
- **5.3 Estimation approach and basis** — Methods (analogy, parametric, three-point, planning poker, historical data), assumptions, confidence, contingency, and who validated the estimate.
- **5.4 Effort, cost, size, and duration estimates** — Table with estimates, units, confidence, and basis. Distinguish baseline, target, and actual where relevant.
- **5.5 Schedule and milestones** — Phases, iterations/sprints, milestones (`MS-xxx`), releases (`REL-xxx`), critical path, dependencies, and calendar constraints. Include a Mermaid Gantt chart only if dates are known; otherwise use a milestone table.
- **5.6 Resource and capacity plan** — Roles, FTE, allocation by period, bottlenecks, shared-resource contention, and contingency.
- **5.7 Budget and financial plan** — Labor, tools, infrastructure, licenses, training, contingency, and cost baseline; state assumptions and approval authority.
- **5.8 Infrastructure and environment plan** — Development, test, staging, production, CI/CD, network, access, backup, and disaster recovery needs.
- **5.9 Procurement and acquisition plan** — What must be bought, lead times, approval, and dependency on the schedule.
- **5.10 Schedule baseline and re-baseline rules** — What constitutes a baseline, who approves changes, and how variance is handled.

#### 6. Project Monitoring and Control

- **6.1 Measurement framework** — Project measures (schedule variance, cost variance, earned value, milestone hit rate) and software measures (defect density, escaped defects, test coverage, cycle time, lead time, deployment frequency, change failure rate, MTTR). Define formula, data source, target, threshold, and owner.
- **6.2 Progress tracking and reporting** — Cadence, audience, format, data sources, dashboard, and escalation triggers.
- **6.3 Reviews, audits, and quality gates** — Phase gates, design reviews, code reviews, test readiness, release readiness, and audit schedule; include entry/exit criteria.
- **6.4 Risk management** — Process, risk register (`RISK-xxx`), scoring method, response strategies, owners, triggers, contingency, and review cadence.
- **6.5 Issue management** — Issue logging, triage, prioritization, ownership, escalation, and closure criteria.
- **6.6 Change control management** — Change request (`CR-xxx`) process, impact analysis, CCB, approval authority, emergency change path, and traceability.
- **6.7 Decision management** — Decision log/ADR linkage, decision criteria, authority, and communication.
- **6.8 Corrective and preventive action** — How nonconformities, defects, and process deviations are corrected and prevented.
- **6.9 Supplier monitoring** — Deliverable acceptance, performance review, and escalation.

#### 7. Supporting Processes

- **7.1 Software configuration management (SCM)** — Repository structure, branching strategy, versioning, baselines, tags, build artifacts, release packaging, access control, and backup.
- **7.2 Quality assurance (SQA)** — SQA plan, process and product assurance, audits, metrics, nonconformance handling, and independence of QA.
- **7.3 Verification and validation (V&V)** — Levels, methods, environments, test data, entry/exit criteria, defect management, acceptance, and traceability to requirements.
- **7.4 Documentation plan** — Document inventory, owner, template, review, approval, storage, versioning, and retention.
- **7.5 Training plan** — Training needs, schedule, owner, and evidence of completion.
- **7.6 Measurement and analysis** — How measurement data is collected, validated, analyzed, and used.
- **7.7 Security and privacy** — Secure SDLC activities, threat modeling, secret management, vulnerability management, access control, incident response, and compliance evidence.
- **7.8 Safety** — If applicable, safety analysis, standards, hazards, and controls.
- **7.9 Maintenance and support transition** — Warranty, SLA, runbooks, monitoring, knowledge transfer, and handover criteria.
- **7.10 Data management** — Data quality, migration, retention, deletion, privacy, and ownership.
- **7.11 Reuse, open-source, and IP management** — License compliance, security review, maintenance, and exit plan.

#### 8. Deliverables, Acceptance, and Transition

- **8.1 Deliverables register** — `DEL-xxx`, name, description, phase, format, owner, acceptance criteria, due date, and status.
- **8.2 Work products and quality records** — Plans, specifications, designs, test evidence, review records, approvals, and configuration records.
- **8.3 Acceptance process and sign-off authority** — Criteria, reviewers, approvers, evidence required, and rejection/rework path.
- **8.4 Release and transition approach** — Environments, deployment method, feature flags, canary/staged rollout, data migration, cutover, and communications.
- **8.5 Rollback and contingency** — Rollback triggers, procedure, decision authority, and data recovery.
- **8.6 Post-delivery support and warranty** — Support window, SLAs, escalation, and maintenance ownership.
- **8.7 Project closure and lessons learned** — Closure criteria, archive, retrospective, and lessons-learned actions.

#### 9. Compliance, Tailoring, and Exceptions

- **9.1 Compliance matrix** — Map SDP sections to ISO/IEC/IEEE 24748-5 planning elements and other applicable standards. State evidence and status.
- **9.2 Tailoring decisions** — What was tailored, rationale, risk, approval, and compensating controls.
- **9.3 Exceptions and waivers** — Exception ID, requirement/standard, justification, risk, approver, expiry, and remediation.
- **9.4 Open items and actions** — `OPEN-xxx`, description, owner, due date, impact, and status.

#### 10. Approvals

| Role | Name | Signature | Date | Version approved |
|---|---|---|---|---|
| Project Manager / SDP Owner | | | | |
| Technical Lead / Architect | | | | |
| QA Lead | | | | |
| Security / Compliance (if applicable) | | | | |
| Product Owner / Business Owner | | | | |

### 4.3 Appendices

- **Appendix A — Traceability matrix:** input requirement/design ID → SDP section/work package → deliverable → verification method.
- **Appendix B — RACI matrix:** activity × role, with `R`, `A`, `C`, `I`.
- **Appendix C — Risk register:** full register with score, response, owner, trigger, and contingency.
- **Appendix D — ISO/IEC/IEEE 24748-5 checklist self-audit:** all 22 items from `development/DevPlan_ISO_24748_5_Checklist.xlsx`, with status and evidence.
- **Appendix E — Assumptions, constraints, and open items:** every assumption, constraint, conflict, and `TBD` with owner and due date.
- **Appendix F — Glossary:** project and standards terminology.
- **Appendix G — References:** full reference list.
- **Appendix H — Change log:** version history.

---

## 5. Standards Alignment

### 5.1 ISO/IEC/IEEE 24748-5 planning elements

Use the following mapping to ensure the SDP covers the standard's planning and control content. The SDP does not need to copy the standard's text; it must demonstrate that the planning elements are addressed.

| ISO/IEC/IEEE 24748-5 element | Required SDP coverage | Primary SDP sections |
|---|---|---|
| Project planning process: responsibility for planning | Who owns the SDP, who contributes, who approves, and how planning is maintained | 4.2, 4.6, 10 |
| Project scope | Product/project boundaries, in/out of scope, assumptions | 1.2, 2.3, 2.6 |
| Work Breakdown Structure | Hierarchical work packages, WBS dictionary, ownership | 5.1, 5.2 |
| Project estimation | Estimation methods, basis, confidence, contingency | 5.3, 5.4 |
| Relationship management | Stakeholders, suppliers, interfaces, communication | 2.5, 4.5, 4.7 |
| Risk management | Risk process, register, scoring, responses, owners | 6.4, Appendix C |
| Configuration management | Branching, versioning, baselines, release artifacts | 7.1 |
| Information management | Documentation, records, retention, access | 7.4, 7.10 |
| Quality assurance | SQA plan, audits, nonconformance, independence | 7.2 |
| Project and software measurement | Measures, formulas, data sources, targets, reporting | 6.1, 6.2, 7.6 |
| Project assessment and control | Reviews, gates, variance analysis, corrective action | 6.2, 6.3, 6.8 |
| Decision management | Decision log/ADR, criteria, authority, communication | 6.7 |
| SDP content and information items | Complete SDP structure and document control | Entire document |
| Life cycle processes (ISO/IEC/IEEE 12207) | Process mapping, tailoring, and compliance | 3.2, 3.5, 3.6, 9.1 |

> If the organization owns the standard, verify this mapping against the edition in force and record any clause-level differences in Section 9.1. Do not invent clause numbers.

### 5.2 Checklist self-audit — 22 items

Read `development/DevPlan_ISO_24748_5_Checklist.xlsx` and assess every item. If the agent cannot read `.xlsx` directly, extract the sheet with a spreadsheet library or by unzipping the workbook XML; do not skip the audit. Record the result in **Appendix D** with this format:

| # | Category | Checklist item | SDP section / evidence | Status | Gap / action | Owner | Due date |
|---|---|---|---|---|---|---|---|
| 1 | Project Overview & Context | Project Purpose & Scope | 1.2, 2.3 | Pass / Partial / Gap | | | |
| 2 | Project Overview & Context | Business Drivers & Objectives | 2.1, 2.2 | Pass / Partial / Gap | | | |
| 3 | Project Overview & Context | System & Software Context | 2.3, 2.4 | Pass / Partial / Gap | | | |
| 4 | Project Overview & Context | Applicable Standards & Compliance | 2.7, 9.1 | Pass / Partial / Gap | | | |
| 5 | Lifecycle & Process Definition | Software Lifecycle Model | 3.1 | Pass / Partial / Gap | | | |
| 6 | Lifecycle & Process Definition | Development Processes & Activities | 3.2 | Pass / Partial / Gap | | | |
| 7 | Lifecycle & Process Definition | Process Tailoring & Adaptation | 3.5, 9.2 | Pass / Partial / Gap | | | |
| 8 | Lifecycle & Process Definition | Deliverables & Work Products | 8.1, 8.2 | Pass / Partial / Gap | | | |
| 9 | Project Organization & Governance | Roles & Responsibilities | 4.2, Appendix B | Pass / Partial / Gap | | | |
| 10 | Project Organization & Governance | Governance & Oversight Structure | 4.6 | Pass / Partial / Gap | | | |
| 11 | Project Organization & Governance | Stakeholder Management | 2.5, 4.5 | Pass / Partial / Gap | | | |
| 12 | Resource & Estimation Management | Estimation Methods & Metrics | 5.3, 5.4 | Pass / Partial / Gap | | | |
| 13 | Resource & Estimation Management | Human Resources & Competencies | 4.3, 4.4 | Pass / Partial / Gap | | | |
| 14 | Resource & Estimation Management | Infrastructure & Tooling | 3.4, 5.8 | Pass / Partial / Gap | | | |
| 15 | Resource & Estimation Management | Budget & Financial Plan | 5.7 | Pass / Partial / Gap | | | |
| 16 | Project Monitoring & Control | Schedule & Milestone Baseline | 5.5, 5.10 | Pass / Partial / Gap | | | |
| 17 | Project Monitoring & Control | Progress Tracking & Reporting | 6.1, 6.2 | Pass / Partial / Gap | | | |
| 18 | Project Monitoring & Control | Risk & Issue Management | 6.4, 6.5, Appendix C | Pass / Partial / Gap | | | |
| 19 | Project Monitoring & Control | Change Control Management | 6.6 | Pass / Partial / Gap | | | |
| 20 | Technical Support Processes | Software Configuration Management (SCM) | 7.1 | Pass / Partial / Gap | | | |
| 21 | Technical Support Processes | Quality Assurance & Verification/Validation | 7.2, 7.3 | Pass / Partial / Gap | | | |
| 22 | Technical Support Processes | Documentation & Maintenance Plan | 7.4, 7.9 | Pass / Partial / Gap | | | |

**Status rules:**

- **Pass** — The SDP contains explicit, auditable content that satisfies the item.
- **Partial** — Content exists but is incomplete, unquantified, or lacks an owner/approval.
- **Gap** — The item is missing or contradicted; record the action, owner, and due date.

**Do not modify the `.xlsx` checklist** unless the user explicitly asks. The audit result belongs in Appendix D of the SDP.

---

## 6. Writing and Quality Rules

1. **Be specific and quantified.** Replace vague statements with numbers, dates, owners, thresholds, and evidence.
2. **Use tables** for WBS, schedule, RACI, risks, deliverables, metrics, and traceability.
3. **Use consistent IDs:**
   - Work package: `WP-001`
   - Milestone: `MS-001`
   - Release: `REL-001`
   - Deliverable: `DEL-001`
   - Risk: `RISK-001`
   - Issue: `ISS-001`
   - Change request: `CR-001`
   - Open item: `OPEN-001`
   - Decision: `DEC-001`
4. **Use ISO dates** (`YYYY-MM-DD`) and state the time zone for deadlines.
5. **Use normative language correctly:** `shall` = mandatory, `should` = recommended, `may` = optional.
6. **Do not leave empty sections.** If a section is not applicable, write "Not applicable" and justify it.
7. **Do not use "etc." in requirements or acceptance criteria.** List the items or define a closed set.
8. **Make assumptions explicit.** State the assumption, its basis, the impact if false, and the owner.
9. **Preserve traceability.** Every work package should link to requirement/design IDs; every deliverable should link to acceptance criteria; every risk should have an owner and response.
10. **Do not fabricate citations.** Cite only the provided references and standards you can name accurately.
11. **Do not paste large sections of input documents.** Summarize and reference them.
12. **Use Mermaid only when it adds clarity.** A broken diagram is worse than a table.
13. **Keep the document internally consistent.** Check that dates, estimates, role names, IDs, and totals agree across sections.
14. **Write for an auditor.** A reviewer should be able to trace a decision from a requirement to a work package to a deliverable to an acceptance record.

---

## 7. Execution Procedure

Follow these steps in order.

### Step 1 — Read and inventory inputs

1. Read every attached input and the repository context files.
2. Build the **Input Inventory** table from Section 2.2.
3. Mark each input as `Available`, `Missing`, `Outdated`, or `Conflicting`.
4. Extract the project parameters from Section 2.4.
5. Read `development/DevPlan_ISO_24748_5_Checklist.xlsx`.

### Step 2 — Build the input gap and conflict list

1. List missing artifacts and missing facts.
2. List contradictions between inputs.
3. For each gap or conflict, assign an owner and a due date.
4. Put the list in **Appendix E** and reference it from the affected sections.

### Step 3 — Draft the SDP outline

1. Create all headings from Section 4.
2. Add a TOC.
3. Add document control and change log.
4. Do not write content yet; verify the outline covers all 22 checklist items.

### Step 4 — Write the content

1. Fill each section with evidence-backed content.
2. Build the WBS, estimates, schedule, RACI, risk register, deliverables register, and traceability matrix.
3. Add the compliance matrix and checklist self-audit.
4. Use the ID conventions from Section 6.
5. Keep the executive summary to one page.

### Step 5 — Self-audit and correct

Run this checklist against the draft:

- [ ] All mandatory sections from Section 4 are present.
- [ ] The document has a title, document control block, TOC, and change log.
- [ ] Purpose, scope, in-scope, and out-of-scope are explicit.
- [ ] Business drivers, objectives, and success measures are measurable.
- [ ] System context, interfaces, and dependencies are described.
- [ ] Stakeholders and concerns are identified.
- [ ] Assumptions, constraints, and dependencies are explicit.
- [ ] Applicable standards and compliance obligations are listed.
- [ ] Life cycle model is selected and justified.
- [ ] Processes are mapped to ISO/IEC/IEEE 12207.
- [ ] Tailoring decisions are recorded with rationale and approval.
- [ ] Roles, responsibilities, and RACI are complete.
- [ ] Governance, decision rights, and escalation are defined.
- [ ] Stakeholder communication plan is defined.
- [ ] WBS has IDs, owners, dependencies, estimates, and requirement links.
- [ ] Estimation method and basis are stated.
- [ ] Schedule has milestones, dependencies, and critical path.
- [ ] Resource, capacity, and budget plans are quantified.
- [ ] Infrastructure, tooling, and procurement needs are covered.
- [ ] Monitoring metrics have formulas, targets, and owners.
- [ ] Reviews, audits, and quality gates have entry/exit criteria.
- [ ] Risk, issue, and change control processes are defined.
- [ ] Decision management is defined.
- [ ] SCM, SQA, V&V, documentation, training, security, and maintenance are covered.
- [ ] Deliverables, acceptance criteria, and sign-off authority are defined.
- [ ] Release, rollback, and transition are covered.
- [ ] Compliance matrix covers ISO/IEC/IEEE 24748-5 elements.
- [ ] Checklist self-audit covers all 22 items with evidence.
- [ ] Every `TBD` has an owner and due date.
- [ ] IDs, dates, estimates, and totals are consistent.
- [ ] No fabricated facts, citations, approvals, or test results.
- [ ] Markdown and TOC links are valid.

If any item fails, fix the document before writing the final file.

### Step 6 — Write the file

1. Write the complete SDP to `docs/05-development/Software_Development_Plan.md`.
2. Confirm the file exists and is non-empty.
3. Do not write the SDP to any other location unless the user explicitly asks.

### Step 7 — Report back

Respond in chat with a concise summary (do not paste the whole document):

- **Output:** `docs/05-development/Software_Development_Plan.md`
- **Document ID / version / status**
- **Inputs used** and **inputs missing**
- **Key assumptions and open items**
- **Checklist result:** `X/22 Pass`, `Y/22 Partial`, `Z/22 Gap`
- **Top 3 risks or decisions needing human attention**
- **Recommended next step:** review and approve the SDP, then derive the `tasks/*.md` files for implementation

---

## 8. Final Response Template

Use this template for the chat response after writing the file:

```markdown
## SDP created

**Output:** `docs/05-development/Software_Development_Plan.md`
**Document ID:** [ID]
**Version / status:** [version] / [status]
**Language:** [Vietnamese/English]

### Inputs used
- [Artifact 1] — [path]
- [Artifact 2] — [path]

### Inputs missing or conflicting
- [Missing artifact / conflict] — owner: [name], due: [YYYY-MM-DD]

### Key assumptions and open items
- [Assumption/open item] — impact: [impact], owner: [name], due: [YYYY-MM-DD]

### Checklist self-audit
- Pass: [X]/22
- Partial: [Y]/22
- Gap: [Z]/22
- Main gaps: [short list]

### Top risks / decisions needing human attention
1. [Risk/decision]
2. [Risk/decision]
3. [Risk/decision]

### Recommended next step
Review and approve the SDP with the project manager, technical lead, and QA lead. Then use the approved SDP to create the `tasks/*.md` files for implementation.
```

---

## 9. Non-Negotiable Constraints

1. **Do not invent project facts.** If the input does not support a statement, mark it as an assumption or `TBD`.
2. **Do not approve your own work.** The SDP is a draft until a human approver signs it.
3. **Do not modify other phase artifacts.** The SDP references them; it does not rewrite them.
4. **Do not create a competing plan.** The only required output is `docs/05-development/Software_Development_Plan.md`.
5. **Do not omit the compliance audit.** Every SDP must include Appendix D with all 22 checklist items.
6. **Do not use confidential data in examples.** Use placeholders and synthetic data.
7. **Do not claim standards compliance you cannot evidence.** Use `Pass`, `Partial`, or `Gap` honestly.
8. **Do not stop at an outline.** The deliverable is a complete, reviewable plan.

---

## 10. Quick Reference — Required Output at a Glance

| Question | Answer |
|---|---|
| What is the output? | A complete Software Development Plan (SDP) in Markdown |
| What is the file name? | `Software_Development_Plan.md` |
| Where is it saved? | `docs/05-development/Software_Development_Plan.md` |
| What standard does it follow? | ISO/IEC/IEEE 24748-5:2017, aligned with ISO/IEC/IEEE 12207 |
| What inputs are required? | Prior-phase artifacts listed in Section 2.1; attach them or provide repo paths |
| What if inputs are missing? | Record the gap in Appendix E; do not fabricate |
| How is quality checked? | 22-item checklist in `development/DevPlan_ISO_24748_5_Checklist.xlsx` and the self-audit in Section 7, Step 5 |
| Who approves? | Project Manager, Technical Lead/Architect, QA Lead, and business owner as applicable |
