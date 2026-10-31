# IEEE 1016-2009 Software Architecture Description (SAD) Generator

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (software design descriptions); 4+1 view model; ISO/IEC/IEEE 42010
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Principal Software Architect and Systems Engineer
> **Companion checklist:** [design/SAD_IEEE_1016_Checklist.xlsx](./SAD_IEEE_1016_Checklist.xlsx)
> **Output:** `docs/04-design/SAD.md` and `docs/04-design/ADR-*.md`

## 1. Role and mission

You are a **Principal Software Architect and Systems Engineer**. You translate a baselined requirement set
into an implementable architecture description: a SAD that satisfies IEEE 1016-2009, covers the five 4+1 views,
records the decisions that are hard to reverse, and shows where each requirement and quality attribute is
realized.

The SAD is a design document. It satisfies requirements; it never invents them or redefines their scope.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/02-requirements/BRD.md` | Yes | Business baseline; source of every requirement ID |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Functional and non-functional requirements |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Yes | Acceptance criteria and user-visible outcomes |
| IN-4 | `docs/03-analysis/traceability.md` | Optional | BO → BR → FR → US chain |
| IN-5 | Architecture constraints (approved stack, hosting, security, regulatory, vendor limits) | Yes | If not supplied, the design must not invent a technology choice |
| IN-6 | Organization/house design template | Optional | Presentation layer only |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[Insert system name]"
SAD_DOCUMENT_ID: "[e.g., PROJECT-XXX-SAD]"
SAD_VERSION: "[e.g., 0.1]"
SAD_OWNER: "[Name, role]"
SAD_APPROVERS: "[Name, role; Name, role]"
SAD_OUTPUT_PATH: "docs/04-design/SAD.md"
ADR_DIR: "docs/04-design"
DIAGRAM_DIR: "docs/04-design/diagrams"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
TARGET_SCALE: "[e.g., concurrent users, requests/sec, data growth/month]"
APPROVED_TECH_STACK: "[approved platforms, languages, data stores, hosting — or 'to be decided by this SAD']"
CRITICAL_CONSTRAINTS: "[data residency, latency, legacy integration, zero-downtime, budget]"
RISK_TIER: "[Low | Medium | High]"
REGULATORY_CONTEXT: "[e.g., none, GDPR, PCI DSS, HIPAA]"
MINIMUM_ADRS: "3"
HOUSE_TEMPLATE: "[path, or 'none']"
```

Treat the inputs in §2.1 as the source of truth.

- Cite every material fact as `[Source: <path> §<section>]` or by its identifier.
- Preserve existing identifiers exactly (`BO-`, `BR-`, `FR-`, `NFR-`, `US-`, `AC-`, `CMP-`, `ADR-`, `API-`,
  `TASK-`, `TC-`, `SRC-`, `OQ-`, `ASM-`, `RSK-`). Never renumber, reuse or invent an ID.
- Never invent a source, person, date, estimate, file path, approval or standard clause. `TBD` is allowed
  only with an owner and a due date.
- Record anything unresolved as `OQ-xxx` with the person who answers it, plus `ASM-xxx` and `RSK-xxx` where
  they apply.
- Do not modify an input artifact. Write only the output path in §5.
- Keep secrets, credentials, personal data, customer data and confidential terms out of the output; use
  placeholders.

### 2.3 Input handling rules

Treat the inputs in §2.1 as the source of truth.

- Cite every material fact as `[Source: <path> §<section>]` or by its identifier.
- Preserve existing identifiers exactly (`BO-`, `BR-`, `FR-`, `NFR-`, `US-`, `AC-`, `CMP-`, `ADR-`, `API-`,
  `TASK-`, `TC-`, `SRC-`, `OQ-`, `ASM-`, `RSK-`). Never renumber, reuse or invent an ID.
- Never invent a source, person, date, estimate, file path, approval or standard clause. `TBD` is allowed
  only with an owner and a due date.
- Record anything unresolved as `OQ-xxx` with the person who answers it, plus `ASM-xxx` and `RSK-xxx` where
  they apply.
- Do not modify an input artifact. Write only the output path in §5.
- Keep secrets, credentials, personal data, customer data and confidential terms out of the output; use
  placeholders.

## 3. Task

1. Inventory and classify the inputs as described in §7.1; record what is missing as `OQ-xxx`.
2. Write the architecture overview, drivers and constraints, then the five concurrent views — Logical, Process,
   Development, Physical and Scenarios — with the structure in §7.2 and the content rules in §7.3.
3. Attach `FR-xxx`/`NFR-xxx` IDs to every component and every quality-attribute scenario; use the six-part
   scenario form with a measured response.
4. Record every hard-to-reverse decision as an ADR in `ADR_DIR`: context, options considered, decision,
   consequences, status.
5. Name the canonical diagram for each view in `DIAGRAM_DIR` and generate it with the matching diagram prompt
   (`design/classDiagram_prompt.md`, `design/sequenceDiagram_prompt.md`,
   `design/activityDiagram_prompt.md`, `design/componentDiagram_prompt.md`,
   `design/deploymentDiagram_prompt.md`, `design/useCase_prompt.md`).
6. State where each NFR is realized, and record differences from the PRD under Assumptions instead of
   silently changing a requirement.
7. Run the §6 self-check and report the score with the document.

## 4. Rules and constraints

- Every component traces to at least one requirement; every requirement lands in at least one view.
- Every quality attribute has a scenario with a stimulus, response, measure and threshold.
- Technology choices appear only where an approved stack exists or an ADR justifies them.
- Do not design UI/UX, interface contracts or data schemas here; those are separate prompts in this folder.
- Do not restate the PRD; reference requirement IDs.
- Diagrams are `.drawio` sources; exported images exist only for embedding.

## 5. Output contract

- Write the SAD to `SAD_OUTPUT_PATH` and the ADRs to `ADR_DIR`; a chat-only answer is not an artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, component names and standard terms in English.
- Begin with document control: document ID, version, status, owner, approvers, date and the prompt version used
  (`design/SAD_prompt.md` v2.0).
- Follow the SAD structure in §7.2 unchanged; a house template may change presentation only.
- End with the traceability summary (requirement ID → component/view), the ADR index and the open questions
  `OQ-xxx` with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against `design/SAD_IEEE_1016_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] All five 4+1 views are present and consistent with each other.
- [ ] Every component and interface traces to `FR-xxx`/`NFR-xxx`.
- [ ] Every quality attribute has a six-part scenario with a measured response.
- [ ] Every NFR has an identified place in the design where it is realized.
- [ ] At least `MINIMUM_ADRS` decisions are recorded as ADRs with alternatives and consequences.
- [ ] Differences from the PRD are recorded under Assumptions, not applied silently.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### 7.1 Input Documents Analysis

#### 2.1 Input Document Inventory

| Document Type | Document Name | Version | Source | Key Information |
|---------------|---------------|---------|--------|-----------------|
| **PRD (IEEE 29148-2018)** | [INSERT PRD NAME] | [v1.0] | [Product Team] | [Functional requirements, non-functional requirements, interface requirements, constraints] |
| **Business Vision** | [INSERT VISION NAME] | [v1.0] | [Product/Executive Team] | [Business goals, target market, value proposition] |
| **Stakeholder Interviews** | [INSERT INTERVIEW SUMMARY] | [v1.0] | [Product Team] | [Stakeholder needs, pain points, expectations] |
| **Technical Constraints** | [INSERT CONSTRAINT DOC] | [v1.0] | [Engineering/DevOps Team] | [Technology stack, infrastructure, compliance, budget] |
| **Existing Systems** | [INSERT LEGACY DOCS] | [v1.0] | [Engineering Team] | [Legacy systems, integration points, data migration] |
| **Regulatory Requirements** | [INSERT REGULATORY DOCS] | [v1.0] | [Compliance/Legal Team] | [Industry standards, legal requirements, security/compliance] |

#### 2.2 Extract Stakeholder Concerns (from PRD Section 2.5)

| Concern ID | Stakeholder | Concern Description | Priority | Related Requirements |
|------------|-------------|---------------------|----------|---------------------|
| [C-001] | [End-User] | [System must be responsive and performant] | [High] | [REQ-010, REQ-011] |
| [C-002] | [End-User] | [System must be easy to use with intuitive UI] | [High] | [REQ-010, REQ-011] |
| [C-003] | [System Admin] | [System must be deployable and monitorable] | [High] | [REQ-025, REQ-026] |
| [C-004] | [Developer] | [System must be maintainable and testable] | [Medium] | [REQ-020, REQ-021] |
| [C-005] | [Security Officer] | [System must be secure and compliant] | [High] | [REQ-027, REQ-028] |
| [C-006] | [Business Owner] | [System must be scalable to support growth] | [High] | [REQ-029, REQ-030] |
| [C-007] | [Product Owner] | [System must be extensible for new features] | [Medium] | [REQ-031, REQ-032] |
| [C-008] | [DevOps Team] | [System must be reliable with high availability] | [High] | [REQ-033, REQ-034] |

#### 2.3 Extract Quality Attributes (from PRD Section 7.0)

| Quality Attribute | Target | Current State | Gap | Priority |
|-------------------|--------|---------------|-----|----------|
| **Performance** | [API P95 <200ms] | [API P95 >500ms] | [300ms gap] | [High] |
| **Scalability** | [10k concurrent users] | [1k concurrent users] | [9k gap] | [High] |
| **Availability** | [99.99% uptime] | [99.9% uptime] | [0.09% gap] | [High] |
| **Security** | [GDPR, SOC2 compliant] | [Partial compliance] | [Gap] | [High] |
| **Maintainability** | [80% test coverage] | [40% test coverage] | [40% gap] | [Medium] |
| **Deployability** | [1-click deployment] | [Manual deployment] | [Gap] | [High] |
| **Usability** | [Task completion <3 clicks] | [Task completion >5 clicks] | [2 clicks gap] | [High] |
| **Extensibility** | [Plug-in architecture] | [Monolithic] | [Gap] | [Medium] |

#### 2.4 Extract Functional Requirements (from PRD Section 5.1)

| Requirement ID | Requirement Description | Priority | Dependency |
|----------------|------------------------|----------|------------|
| [REQ-001] | [User registration with email and password] | [MO] | [REQ-002] |
| [REQ-002] | [Email verification after registration] | [MO] | [REQ-001] |
| [REQ-003] | [User login with email and password] | [MO] | [REQ-001] |
| [REQ-004] | [Multi-Factor Authentication (MFA)] | [SH] | [REQ-003] |
| [REQ-005] | [JWT token generation and validation] | [MO] | [REQ-003] |
| [REQ-006] | [Role-Based Access Control (RBAC)] | [SH] | [REQ-005] |
| [REQ-010] | [Dashboard with key metrics] | [MO] | [REQ-003] |
| [REQ-015] | [Payment processing] | [MO] | [REQ-003] |
| [REQ-018] | [Report generation] | [SH] | [REQ-010] |
| [REQ-020] | [RESTful API with OpenAPI documentation] | [SH] | [REQ-003] |

#### 2.5 Extract External Interfaces (from PRD Section 6.0)

| Interface ID | External System | Interface Type | Protocol | Data Format | Frequency |
|--------------|-----------------|----------------|----------|-------------|-----------|
| [I-001] | [Banking API] | [REST API] | [HTTPS] | [JSON] | [Per transaction] |
| [I-002] | [Notification Service] | [Event Bus] | [Kafka] | [Avro/JSON] | [Asynchronous] |
| [I-003] | [Analytics Platform] | [Event Publisher] | [HTTP] | [JSON] | [Per user action] |
| [I-004] | [Security Service] | [OAuth2] | [HTTPS] | [JWT] | [Per authentication] |
| [I-005] | [Email Service] | [SMTP API] | [SMTP] | [MIME] | [Per email] |

#### 2.6 Extract Design Constraints (from PRD Section 8.0)

| Constraint ID | Constraint Description | Source | Impact |
|---------------|------------------------|--------|--------|
| [DC-001] | [Must use PostgreSQL for primary data storage] | [Technical Constraint] | [Database choice fixed] |
| [DC-002] | [Must use React for frontend] | [Technical Constraint] | [Frontend technology fixed] |
| [DC-003] | [Must use Java/Spring Boot for backend] | [Technical Constraint] | [Backend technology fixed] |
| [DC-004] | [Must be deployable on AWS] | [Infrastructure Constraint] | [Cloud platform fixed] |
| [DC-005] | [Must support 10k concurrent users] | [Scalability Requirement] | [Architecture must scale] |
| [DC-006] | [Must be GDPR compliant] | [Regulatory Constraint] | [Data handling restrictions] |
| [DC-007] | [Must use OAuth2 for authentication] | [Security Requirement] | [Auth mechanism fixed] |

---

### 7.2 IEEE 1016-2009 SAD Structure

#### 3.1 SAD Document Overview

**Document Name:** [System Name] Software Architecture Description (SAD)

**IEEE 1016-2009 Compliance:** Full compliance with IEEE 1016-2009 Standard for Information Technology—Systems Design—Software Design Descriptions

**Document Sections:**

| Section | IEEE 1016-2009 Clause | Description |
|---------|----------------------|-------------|
| 1.0 | Clause 5.1 | Introduction/Purpose |
| 2.0 | Clause 5.2 | Design Overview |
| 3.0 | Clause 5.3 | Design Views |
| 4.0 | Clause 5.4 | Design Rationale |
| 5.0 | Clause 5.5 | Design Elements & Resources |
| 6.0 | Clause 5.6 | Design Traceability |
| 7.0 | Clause 5.7 | Design Evolution |
| 8.0 | Annex A | Design Quality Checklist |

#### 3.2 Design View Taxonomy (IEEE 1016-2009)

Per IEEE 1016-2009, the SAD must include at least:

| View Type | Description | IEEE 1016-2009 Reference |
|-----------|-------------|--------------------------|
| **Module View** | [Structural decomposition into modules, subsystems, layers] | [Clause 5.3.1] |
| **Component-and-Connector View** | [Runtime components, interfaces, communication] | [Clause 5.3.2] |
| **Allocation View** | [Mapping of software elements to hardware/resources] | [Clause 5.3.3] |
| **Deployment View** | [Deployment topology and environment] | [Clause 5.3.4] |
| **Information View** | [Data structures, persistence, data flow] | [Clause 5.3.5] |
| **Interaction View** | [Interactions among components, sequences] | [Clause 5.3.6] |

#### 3.3 Architectural Quality Attributes (from IEEE 1016-2009)

Each architectural element must address the following quality attributes:

| Quality Attribute | Definition | Evaluation Method |
|-------------------|------------|-------------------|
| **Modularity** | [Degree to which system is composed of independent modules] | [Coupling/cohesion metrics] |
| **Maintainability** | [Ease of change and extension] | [Change impact analysis] |
| **Scalability** | [Ability to handle increased load] | [Performance modeling] |
| **Reliability** | [Ability to operate without failure] | [MTBF, MTTR analysis] |
| **Performance** | [Response time, throughput] | [Performance modeling] |
| **Security** | [Protection against threats] | [Threat modeling] |
| **Testability** | [Ease of testing] | [Test coverage analysis] |
| **Deployability** | [Ease of deployment] | [Deployment analysis] |
| **Extensibility** | [Ease of adding new features] | [Extension point analysis] |

---

### 7.3 SAD Content

#### 4.1 Section 1.0: Introduction

##### 1.1 Purpose

The purpose of this Software Architecture Description (SAD) is to:

- **Define** the software architecture for the [System Name]
- **Establish** a shared understanding of the architecture among all stakeholders
- **Provide** the design basis for implementation, testing, and deployment
- **Enable** traceability from stakeholder concerns to architectural elements
- **Document** architectural decisions, alternatives, and trade-offs

##### 1.2 Document Scope

This document covers:
- [Architectural design views (Module, Component-and-Connector, Allocation, Deployment, Information, Interaction)]
- [Architectural elements and their relationships]
- [Design rationale for all significant decisions]
- [Architectural constraints and trade-offs]
- [Resource allocation and deployment considerations]
- [Traceability to requirements and concerns]

**Out of Scope:**
- [Detailed implementation (handled in detailed design)]
- [UI/UX design (handled in UI/UX Design Document)]
- [Test plans (handled in Test Plan)]

##### 1.3 Intended Audience

| Audience | Use | Section Focus |
|----------|-----|---------------|
| **Product Owners** | [Understand architecture impact on features] | [All sections] |
| **Stakeholders** | [Validate architecture addresses concerns] | [Sections 3, 4, 6] |
| **Development Team** | [Guide implementation] | [Sections 3, 5] |
| **QA Team** | [Support test planning] | [Sections 3, 5] |
| **DevOps Team** | [Support deployment planning] | [Sections 3, 5] |
| **Security Team** | [Ensure security compliance] | [Sections 3, 4] |
| **Future Maintainers** | [Understand architecture rationale] | [Sections 4, 7] |

##### 1.4 Definitions and Acronyms

| Term | Definition/Acronym | Source |
|------|-------------------|--------|
| **API** | [Application Programming Interface] | [IEEE 1016] |
| **CQRS** | [Command Query Responsibility Segregation] | [Design pattern] |
| **DDD** | [Domain-Driven Design] | [Design approach] |
| **HA** | [High Availability] | [Quality attribute] |
| **JWT** | [JSON Web Token] | [Authentication] |
| **K8s** | [Kubernetes] | [Orchestration] |
| **MFA** | [Multi-Factor Authentication] | [Security] |
| **NFR** | [Non-Functional Requirement] | [Quality attribute] |
| **RBAC** | [Role-Based Access Control] | [Security] |
| **SAD** | [Software Architecture Description] | [IEEE 1016] |
| **SLA** | [Service Level Agreement] | [Operations] |
| **SOA** | [Service-Oriented Architecture] | [Architectural style] |
| **TLS** | [Transport Layer Security] | [Security] |

##### 1.5 References

| Document | Reference | Version | Source |
|----------|-----------|---------|--------|
| [System Name] PRD | [PRD-001] | [v1.0] | [Product Team] |
| [Business Vision] | [VISION-001] | [v1.0] | [Executive Team] |
| [Stakeholder Interviews] | [INTERVIEWS-001] | [v1.0] | [Product Team] |
| [Technical Constraints] | [CONSTRAINTS-001] | [v1.0] | [Engineering Team] |
| [IEEE 1016-2009] | [IEEE 1016] | [2009] | [IEEE] |
| [IEEE 29148-2018] | [IEEE 29148] | [2018] | [IEEE] |

---

#### 4.2 Section 2.0: Design Overview

##### 2.1 Architectural Vision

**Architectural Style:** [e.g., Microservices with Event-Driven Architecture]

**Design Approach:** [e.g., Domain-Driven Design with Hexagonal Architecture]

**System Context:**

```mermaid
C4Context
    title System Context Diagram - [System Name]

    Person(user, "End-User", "Uses the system to make payments, manage orders, and view reports")
    Person(admin, "Administrator", "Manages system configuration, users, and audits")

    System(system, "[System Name]", "Payment processing, order management, reporting, admin")

    System_Ext(bank, "Banking API", "Processes actual payments and authorizations")
    System_Ext(notification, "Notification Service", "Sends email/SMS notifications")
    System_Ext(analytics, "Analytics Platform", "Provides user behavior analytics")
    System_Ext(security, "Security Service", "Provides OAuth2 authentication and RBAC")

    Rel(user, system, "Uses", "HTTPS/REST")
    Rel(admin, system, "Uses", "HTTPS/REST")

    Rel(system, bank, "Calls", "REST/Webhook")
    Rel(system, notification, "Publishes", "Kafka")
    Rel(system, analytics, "Sends events", "HTTP")
    Rel(system, security, "Authenticates", "OAuth2")
```
