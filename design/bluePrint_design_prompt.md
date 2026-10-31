# IEEE 1016-2009 Software Design Description (Blueprint) Prompt

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (software design descriptions)
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Software Designer and Architect
> **Companion checklist:** [design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx](./BluePrint_Design_IEEE_1016_2009_Checklist.xlsx)
> **Output:** `docs/04-design/blueprint.md` (or `.sql` where the design is expressed as DDL)

## 1. Role and mission

You are a **Software Designer** producing a complete, standards-compliant Software Design Description (the
blueprint) with full traceability from stakeholder concern to design element, following IEEE 1016-2009.

The blueprint is the design-level bridge between the architecture description and the implementation. It
describes **how** the system is structured; it does not repeat the SAD's architecture rationale and does not
carry UI, interface-contract or database-detail specifications, which have their own prompts in this folder.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | Architecture description; the blueprint elaborates it |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Requirements and quality attributes |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible outcomes the design must support |
| IN-4 | `docs/04-design/ADR-*.md` | Optional | Decisions the design must respect |
| IN-5 | Approved coding and design conventions | Yes | Naming, layering and structural rules the design must follow |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[INSERT SYSTEM NAME]"
SDD_VERSION: "[e.g., v1.0]"
DOCUMENT_DATE: "[YYYY-MM-DD]"
DOCUMENT_OWNER: "[Lead Architect / Team]"
DOCUMENT_APPROVERS: "[Name, role; Name, role]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
BLUEPRINT_OUTPUT_PATH: "docs/04-design/blueprint.md"
DIAGRAM_FORMAT: "[Mermaid embedded in the .md | .drawio in docs/04-design/diagrams]"
DESIGN_CONVENTIONS: "[layering, package naming, module boundaries from the organization standard]"
```

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

1. Complete the context, scope, assumptions and constraints tables in §7.1 using the SAD and the requirements.
2. Identify stakeholders and their concerns, and map each concern to a quality-attribute scenario in §7.2.
3. Describe the design through the eight views in §7.3, in the order given; keep every view traceable to the
   concerns in §7.2.
4. Link every design element to the `FR-xxx`/`NFR-xxx` IDs and `CMP-xxx` components it realizes.
5. Where the SAD leaves a decision open, record it as `OQ-xxx`; do not invent an architectural decision here.
6. Run the §6 self-check and report the score with the document.

## 4. Rules and constraints

- Every stakeholder concern maps to at least one view element, and every design element maps back to a concern
  or a requirement. A design element with no upstream concern is either unnecessary or belongs in another view.
- Describe design at the level of modules, classes, interfaces and interactions — not deployment topology,
  which belongs to the SAD and the deployment diagram.
- Fill every `[placeholder]` in the template; an unfilled placeholder is an incomplete design, not a style
  choice.
- Do not introduce a component that the SAD does not have; if one is missing from the SAD, raise `OQ-xxx`.

## 5. Output contract

- Write to `BLUEPRINT_OUTPUT_PATH`; a chat-only answer is not an artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, element names and standard terms in English.
- Begin with document control: system name, version, date, owner, approvers and the prompt version used
  (`design/bluePrint_design_prompt.md` v2.0).
- Follow the section order of §7 unchanged, including the view order.
- End with a concern-to-element traceability table and the `OQ-xxx` list with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against `design/BluePrint_Design_IEEE_1016_2009_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every stakeholder concern is addressed by at least one design view.
- [ ] All eight IEEE 1016 views in §7.3 are present and consistent with each other.
- [ ] Every design element traces to a requirement or a concern; no orphan element.
- [ ] Quality-attribute scenarios carry a measurable response.
- [ ] No placeholder remains, and no element contradicts the SAD.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### 7.1 Context & Subject

#### 1.1 System Identification

| Attribute | Value |
|-----------|-------|
| **System Name** | [INSERT SYSTEM NAME] |
| **SDD Version** | [e.g., v1.0] |
| **Document Date** | [YYYY-MM-DD] |
| **Document Owner** | [Lead Architect / Team] |
| **Revision History** | [Version, Date, Author, Changes] |
[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

#### 1.2 System Scope and External Boundaries

Define the **external boundaries** of the system—what is inside the architecture versus what exists outside.

| Boundary Type | Description |
|---------------|-------------|
| **System Purpose** | [Briefly describe what the system does and its primary business value] |
| **External Systems** | [List all external systems, services, APIs, and third-party dependencies that the system interacts with] |
| **User Types** | [Identify all human actors interacting with the system] |
| **External Interfaces** | [e.g., REST APIs, Message Queues, File Transfers, Webhooks, Databases] |
| **Trust Boundaries** | [Identify security boundaries—internal network, DMZ, public internet, third-party domains] |
| **Deployment Environment** | [e.g., AWS Cloud, On-premise, Hybrid, Edge Devices] |

#### 1.3 Assumptions and Constraints

| Type | Description |
|------|-------------|
| **Technical Constraints** | [e.g., Must use PostgreSQL, Must support IPv6, Must run on Kubernetes] |
| **Business Constraints** | [e.g., Budget cap, Timeline, Regulatory deadlines] |
| **Environmental Assumptions** | [e.g., Network latency <100ms, 99.9% uptime from cloud provider] |
| **Data Assumptions** | [e.g., Maximum dataset size, Data growth rate, Data retention policy] |

---

### 7.2 Stakeholders & Concerns

#### 2.1 Stakeholder Identification

Identify all stakeholders who have a vested interest in the system's design and operation.

| Stakeholder | Role/Title | Primary Interest |
|-------------|------------|------------------|
| [e.g., End-User] | [e.g., Customer] | [e.g., Usability, Performance, Reliability] |
| [e.g., System Administrator] | [e.g., Ops Team] | [e.g., Deployability, Monitorability, Logging] |
| [e.g., Developer] | [e.g., Engineering Team] | [e.g., Maintainability, Testability, Understandability] |
| [e.g., DevOps/SRE] | [e.g., Platform Team] | [e.g., Scalability, Resilience, Auto-scaling] |
| [e.g., Product Owner] | [e.g., Business] | [e.g., Time-to-market, Feature agility, Cost] |
| [e.g., Security Officer] | [e.g., Compliance] | [e.g., Data protection, Authentication, Audit trails] |
| [e.g., Data Scientist] | [e.g., AI/ML Team] | [e.g., Model accuracy, Data pipeline, Feature store] |

#### 2.2 Stakeholder Concerns (IEEE 1016-2009)

Map each stakeholder to their specific **concerns**—the non-functional requirements, quality attributes, and risks they care about.

| Stakeholder | Concern | Priority (High/Med/Low) | Acceptance Criteria |
|-------------|---------|-------------------------|---------------------|
| [Stakeholder] | [Concern description] | [Priority] | [Measurable criterion] |

#### 2.3 Quality Attribute Scenarios

For critical quality attributes, define concrete, measurable scenarios using the **six-part scenario format** (Source, Stimulus, Artifact, Environment, Response, Response Measure).

| Quality Attribute | Scenario |
|-------------------|----------|
| **Performance** | [e.g., Under peak load of 10k concurrent users, 95% of API requests complete within 200ms] |
| **Scalability** | [e.g., System can horizontally scale from 3 to 30 nodes with linear throughput increase] |
| **Availability** | [e.g., System achieves 99.99% uptime with recovery time < 30 seconds for any single-node failure] |
| **Security** | [e.g., All sensitive data encrypted at rest (AES-256) and in transit (TLS 1.3)] |
| **Maintainability** | [e.g., A code change affecting one module impacts <3 other modules] |
| **Testability** | [e.g., Unit test coverage >80%, Integration tests run in <5 minutes] |
| **Deployability** | [e.g., Canary deployments with automated rollback on error rate >1%] |
| **Observability** | [e.g., Distributed tracing, structured logging, and metrics exposed in Prometheus format] |

#### 2.4 UX/UI Quality Attribute Scenarios

Define concrete, measurable UX/UI quality scenarios.

| Quality Attribute | UX/UI Scenario |
|-------------------|----------------|
| **Usability** | [e.g., A first-time user can complete the onboarding flow (5 steps) within 90 seconds with zero errors] |
| **Accessibility** | [e.g., All interactive elements are keyboard-navigable and screen-reader compatible (WCAG 2.1 AA)] |
| **Performance** | [e.g., First Contentful Paint < 1.5s, Largest Contentful Paint < 2.5s on a 4G connection] |
| **Responsiveness** | [e.g., UI gracefully adapts from 320px to 2560px width with no horizontal scroll] |
| **Visual Consistency** | [e.g., 100% adherence to design system for color, typography, spacing, and components] |
| **Error Recovery** | [e.g., Form validation errors are displayed inline with clear messaging; user recovers without page reload] |
| **Feedback & Affordance** | [e.g., All clickable elements have hover/active states; loading states for async operations within 300ms] |
| **Information Architecture** | [e.g., User can find key functionality within 2 clicks from any page] |
| **Internationalization** | [e.g., UI supports RTL languages, text expansion (+30%), and date/time localization] |
| **Mobile Experience** | [e.g., Touch targets minimum 44px, gestures (swipe, pinch) optimized] |

#### 2.5 UX/UI Constraints Matrix

| UX/UI Constraint | Requirement | Tool/Standard | Verification Method |
|------------------|-------------|---------------|---------------------|
| **Color Contrast** | [e.g., Minimum 4.5:1 for normal text] | [WCAG 2.1 AA] | [Automated + manual testing] |
| **Typography** | [e.g., Body text 16px min, scalable] | [Design System] | [Design audit] |
| **Touch Targets** | [e.g., 44x44px min for touch devices] | [Apple HIG / Material Design] | [UI testing] |
| **Loading States** | [e.g., Show skeleton or spinner within 300ms] | [UX best practice] | [Performance monitoring] |
| **Error Messaging** | [e.g., Clear, actionable, not technical] | [UX writing guidelines] | [Content review] |
| **Empty States** | [e.g., Every empty state guides next action] | [UX best practice] | [UI inventory] |
| **Notifications** | [e.g., Non-intrusive, time-sensitive] | [UX best practice] | [User testing] |
| **Help & Onboarding** | [e.g., Contextual help available] | [UX best practice] | [Task completion metrics] |
---

### 7.3 Design Views (IEEE 1016-2009 Core)

The design is documented through **eight distinct views**, each addressing specific stakeholder concerns. Every view must be explicitly linked back to the concerns identified in Section 2.

---

#### 3.1 Composition View

**Purpose:** Describes how the system is assembled from smaller units. Shows the hierarchical decomposition of the software into modules, subsystems, and packages.

**Viewpoint:** Structural breakdown of the system into its constituent parts.

**Stakeholder Concerns Addressed:** Maintainability, Understandability, Modularity.

| Element | Type | Parent | Responsibility | Dependencies |
|---------|------|--------|----------------|--------------|
| [Subsystem] | [e.g., Module/Package] | [e.g., System Root] | [Description] | [e.g., Depends on Utils] |

**Diagram:**

```
flowchart TD
    Root[System Root] --> SubsystemA[Core Domain]
    Root --> SubsystemB[Infrastructure]
    Root --> SubsystemC[API Layer]
    Root --> SubsystemD[Data Access]

    SubsystemA --> ModuleA1[Domain Entities]
    SubsystemA --> ModuleA2[Business Logic]

    SubsystemB --> ModuleB1[Logging]
    SubsystemB --> ModuleB2[Configuration]
    SubsystemB --> ModuleB3[Security]

    SubsystemC --> ModuleC1[REST Controllers]
    SubsystemC --> ModuleC2[GraphQL Resolvers]

    SubsystemD --> ModuleD1[Repository Layer]
    SubsystemD --> ModuleD2[Cache Manager]
```
