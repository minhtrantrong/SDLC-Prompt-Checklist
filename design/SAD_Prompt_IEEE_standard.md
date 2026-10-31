# IEEE 1016-2009 Software Architecture Design Document (SADD) Prompt

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (software design descriptions); 4+1 view model
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Principal Software Architect and Systems Engineer
> **Companion checklist:** [design/SAD_IEEE_1016_Checklist.xlsx](./SAD_IEEE_1016_Checklist.xlsx)
> **Output:** `docs/04-design/SAD.md` and `docs/04-design/ADR-*.md`

## 1. Role and mission

You are a **Principal Software Architect and Systems Engineer**. You author a production-grade Software
Architecture Design Document for a new system, from the baselined requirements and the approved technology
constraints, following IEEE 1016-2009.

Be specific about patterns, data flows and protocols. "Use a modern database" is not a design statement;
"PostgreSQL 16, one schema per service, indexed on `(tenant_id, created_at)`" is.

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
CORE_BUSINESS_FUNCTION: "[What the system does, in one sentence]"
SAD_DOCUMENT_ID: "[e.g., PROJECT-XXX-SAD]"
SAD_VERSION: "[e.g., 0.1]"
SAD_OWNER: "[Name, role]"
SAD_APPROVERS: "[Name, role; Name, role]"
SAD_OUTPUT_PATH: "docs/04-design/SAD.md"
ADR_DIR: "docs/04-design"
DIAGRAM_DIR: "docs/04-design/diagrams"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
TARGET_SCALE: "[e.g., 10k concurrent users, 500 requests/sec, 1TB data growth/month]"
APPROVED_TECH_STACK: "[approved platforms, languages, data stores, hosting]"
CRITICAL_CONSTRAINTS: "[data residency, low-power edge, zero-downtime, legacy integration]"
RISK_TIER: "[Low | Medium | High]"
REGULATORY_CONTEXT: "[e.g., none, GDPR, PCI DSS, HIPAA]"
MINIMUM_ADRS: "3"
HOUSE_TEMPLATE: "[path, or 'none']"
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

1. Summarize the technical constraints and the architectural drivers before writing the document.
2. Produce the four parts specified in §7, in order: goals and principles, component decomposition, data
   architecture and integration flows, cross-cutting concerns and infrastructure.
3. Attach `FR-xxx`/`NFR-xxx` IDs to components, flows and cross-cutting decisions.
4. Record the decisions that are hard to reverse as ADRs in `ADR_DIR`, with alternatives and consequences.
5. State, for every quality attribute, where in the design it is realized and how it will be measured.
6. Run the §6 self-check and report the score with the document.

## 4. Rules and constraints

- Every component has one clear responsibility and a stated interface; no component without a requirement.
- Every integration flow names the protocol, the payload shape and the failure behaviour.
- Security, authorization, data protection and observability are design elements, not afterthoughts.
- Do not invent a technology that is neither in the approved stack nor justified by an ADR.
- Do not modify the input requirements; record conflicts as `OQ-xxx`.

## 5. Output contract

- Write the document to `SAD_OUTPUT_PATH` and the ADRs to `ADR_DIR`; a chat-only answer is not an artifact.
- Write in `OUTPUT_LANGUAGE`, keeping IDs, component names and standard terms in English.
- Begin with document control: ID, version, status, owner, approvers, date and the prompt version used
  (`design/SAD_Prompt_IEEE_standard.md` v2.0).
- Follow the four-part structure of §7 and its sub-headings.
- End with the requirement-to-component map, the ADR index and the `OQ-xxx` list with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against `design/SAD_IEEE_1016_Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] The architectural drivers and constraints are stated before the design.
- [ ] Every component traces to `FR-xxx`/`NFR-xxx` and has a defined interface.
- [ ] Every critical flow has a step-by-step narrative with failure behaviour.
- [ ] Security, data protection, reliability and observability are addressed explicitly.
- [ ] At least `MINIMUM_ADRS` hard-to-reverse decisions are recorded as ADRs.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

### INSTRUCTIONS FOR GENERATION
Please generate the Architecture Design Document using the following structured layout. Be highly specific regarding patterns, data flows, and protocols. Avoid hand-waving or vague assertions like "use a modern database"—specify the type, indexing strategy, or replication mechanism where appropriate.

#### 1. Architectural Goals & Design Principles
* **1.1 Key Drivers:** Identify the top 3 architectural drivers (e.g., Maintainability, Fault Tolerance, Low Latency) and how the design prioritizes them.
* **1.2 Architectural Patterns:** Define the macro-pattern chosen (e.g., Event-Driven Architecture, Microservices, Clean Architecture Monolith) and justify the choice.

#### 2. System Component Decomposition
Break down the system into its logical layers or services using a structured approach:
* **2.1 Frontend / Client Layer:** State management, delivery mechanics (CDN, SSR, SPA), and communication protocols (REST, GraphQL, gRPC).
* **2.2 Application / Business Logic Layer:** Service boundaries, processing modules, and asynchronous task workers.
* **2.3 Data Infrastructure Layer:** Primary databases, caching tiers, message brokers/queues, and data retention policies.
* **2.4 Backend / API layers:** REST, Query and service boundaries, procressing modules, input/output declaration.

#### 3. Data Architecture & Integration Flows
* **3.1 Core Data Model Strategy:** Describe how data is structured, synchronized, or isolated across components (e.g., Database-per-service vs. shared schema, relational vs. NoSQL strategy).
* **3.2 Sequence/Data Flow Narrative:** Step-by-step description of a critical system flow (e.g., "End-to-End Order Processing Flow") explaining how components interact over the network.

#### 4. Cross-Cutting Concerns & Infrastructure
* **4.1 Security & Compliance:** Authentication/Authorization patterns (e.g., OAuth2/OIDC, JWT validation at API Gateway), data encryption (At-Rest & In-Transit), and secret management.
* **4.2 Reliability & Fault Tolerance:** Strategies for high availability (e.g., multi-region deployment, circuit breakers, retry-with-exponential-backoff, rate-limiting).
* **4.3 Observability:** Metrics, logging aggregation, and distributed tracing strategies to monitor system health.

Begin your response by summarizing the technical constraints, then output the formal Architecture Design Document.

@[Add your_SRS_and_PRD_document at here for AI reference]
