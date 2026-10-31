# IEEE 1016-2009 API Design Prompt

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (interface design); OpenAPI 3.x
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** API Designer and Integration Architect
> **Companion checklist:** [design/API_Design_IEEE-1016-2009Checklist.xlsx](./API_Design_IEEE-1016-2009Checklist.xlsx)
> **Output:** `docs/04-design/openapi.yaml` and `docs/04-design/api.md`

## 1. Role and mission

You are an **API Designer and Integration Architect**. You turn the architecture's interface view and the
baselined requirements into an implementable, testable interface contract with full traceability to
stakeholder concerns and requirements.

The contract is the source of truth for both the implementation and the tests. Changing it later is a design
change, not a code change.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/04-design/SAD.md` | Yes | Interface view, components, protocols and boundaries |
| IN-2 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Functional and non-functional requirements, including NFR targets for latency and availability |
| IN-3 | `docs/03-analysis/USER_STORIES.md` | Optional | User-visible flows the interface must support |
| IN-4 | `docs/04-design/ADR-*.md` | Optional | Decisions the contract must respect |
| IN-5 | Organization API style guide, security standard and data classification | Yes | Naming, versioning, auth, error format and rate-limit rules |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[INSERT SYSTEM NAME]"
API_DOCUMENT_ID: "[e.g., PROJECT-XXX-API]"
API_VERSION: "[e.g., v1]"
DOCUMENT_OWNER: "[Name, role]"
DOCUMENT_APPROVERS: "[Name, role; Name, role]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
OPENAPI_OUTPUT_PATH: "docs/04-design/openapi.yaml"
API_DOC_OUTPUT_PATH: "docs/04-design/api.md"
PROTOCOL: "[REST | GraphQL | gRPC | event/message]"
AUTH_MODEL: "[e.g., OAuth2/OIDC + JWT at the gateway, mTLS for internal calls]"
ERROR_FORMAT: "[e.g., RFC 9457 problem+json]"
PAGINATION_PAGINATION: "[e.g., cursor-based]"
RATE_LIMIT_POLICY: "[per-client limit and burst, or 'none']"
COMPATIBILITY_POLICY: "[backward compatible within a major version, deprecation window]"
DATA_CLASSIFICATION: "[public | internal | confidential | restricted]"
TESTABLE_ACCEPTANCE: "yes"
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

1. Complete the context, scope, stakeholders, concerns, quality-attribute scenarios and constraints tables in
   §7.1 and §7.2 from the SAD and the requirements.
2. Design the interface operations under §7.3: every operation has a purpose, an owner component, auth and
   authorization rules, request and response schemas, examples, error codes and a requirement mapping.
3. Define cross-cutting behaviour explicitly: versioning, pagination, filtering, idempotency for mutating
   calls, rate limits, timeouts, retries and error format.
4. Write the machine-readable contract to `OPENAPI_OUTPUT_PATH` and the narrative to `API_DOC_OUTPUT_PATH`.
5. Map every operation to `FR-xxx` and to the requirement it serves; flag any operation with no requirement.
6. Do not change a contract that the SAD already fixes; a necessary difference becomes a new ADR.
7. Run the §6 self-check and report the score with the contract.

## 4. Rules and constraints

- One operation, one purpose; no endpoint that exists only to serve a screen.
- Every request is validated, every error is typed and documented, and no error leaks internal detail.
- Authorization is specified per operation and per role, not assumed from authentication.
- Mutating operations state their idempotency behaviour; the contract must be safe to retry.
- No secrets, tokens or personal data in examples; use synthetic values.
- The contract must be valid OpenAPI 3.x and reference no undefined schema.

## 5. Output contract

- Write the contract to `OPENAPI_OUTPUT_PATH` and the narrative to `API_DOC_OUTPUT_PATH`; a chat-only answer is
  not an artifact.
- Write the narrative in `OUTPUT_LANGUAGE`, keeping operation IDs, schema names and standard terms in English.
- Begin with document control: document ID, API version, owner, approvers, date and the prompt version used
  (`design/apiDesign_prompt.md` v2.0).
- Follow the section order of §7 unchanged.
- End with the requirement-to-operation matrix, the compatibility and deprecation notes, and the `OQ-xxx` list
  with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against `design/API_Design_IEEE-1016-2009Checklist.xlsx` before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every operation traces to an `FR-xxx` and declares auth, authorization, schemas and error codes.
- [ ] All schemas are defined once and referenced; no undefined or duplicated schema.
- [ ] Versioning, pagination, idempotency, rate limits and error format are specified.
- [ ] The contract conforms to the SAD interface view; every difference has an ADR.
- [ ] The OpenAPI document validates against the 3.x specification.
- [ ] No secret, token or real personal data appears in examples.

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

[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

| Attribute | Value |
|-----------|-------|
| **System Name** | [INSERT SYSTEM NAME] |
| **SDD Version** | [e.g., v1.0] |
| **Document Date** | [YYYY-MM-DD] |
| **Document Owner** | [Lead Architect / UX Lead / API Lead / Team] |
| **Revision History** | [Version, Date, Author, Changes] |

#### 1.2 System Scope and External Boundaries

Define the **external boundaries** of the system—what is inside the architecture versus what exists outside.

| Boundary Type | Description |
|---------------|-------------|
| **System Purpose** | [Briefly describe what the system does and its primary business value] |
| **User Personas** | [List primary user types with roles, goals, and pain points—see Section 2.1] |
| **API Consumers** | [List all API consumers: internal services, external partners, third-party integrations, mobile apps] |
| **User Journey Context** | [Where does this system fit in the user's overall workflow?] |
| **External Systems** | [List all external systems, services, APIs, and third-party dependencies] |
| **External Interfaces** | [e.g., REST APIs, GraphQL, gRPC, Webhooks, Message Queues, File Transfers] |
| **UI Channels** | [e.g., Web Application, Mobile App, Desktop App, Voice Interface, Chatbot] |
| **API Channels** | [e.g., Public API, Partner API, Internal API, Webhook endpoints] |
| **Touchpoints** | [All user interaction points: login, dashboard, forms, notifications, reports] |
| **API Touchpoints** | [All API interaction points: authentication, data access, webhook callbacks] |
| **Trust Boundaries** | [Security boundaries—internal network, DMZ, public internet, third-party domains] |
| **Deployment Environment** | [e.g., AWS Cloud, On-premise, Hybrid, Edge Devices] |
| **Device Support** | [e.g., Desktop (1920x1080+), Tablet (768x1024), Mobile (375x667+)] |
| **Browser Support** | [e.g., Chrome 90+, Firefox 88+, Safari 14+, Edge 90+] |

#### 1.3 Assumptions and Constraints

| Type | Description |
|------|-------------|
| **Technical Constraints** | [e.g., Must use React 18, Must support OAuth2, Must follow WCAG 2.1 AA, Must use OpenAPI 3.0] |
| **Business Constraints** | [e.g., Budget cap, Timeline, Regulatory deadlines, Brand guidelines] |
| **UX/UI Assumptions** | [e.g., Users have basic computer literacy, Average session duration 5 minutes] |
| **API Assumptions** | [e.g., API consumers have technical expertise, Average API call volume 10k/min] |
| **Device Assumptions** | [e.g., 80% desktop users, 15% mobile, 5% tablet] |
| **Network Assumptions** | [e.g., 4G/LTE or better, Latency <300ms for mobile, <100ms for API] |
| **Data Assumptions** | [e.g., Maximum dataset size, Data growth rate, Data retention policy] |

---

### 7.2 Stakeholders & Concerns

#### 2.1 User Personas

Define the primary users of the system with their goals, needs, and pain points.

| Persona | Role | Demographics | Goals | Pain Points | Tech Proficiency | Usage Frequency |
|---------|------|--------------|-------|-------------|------------------|-----------------|
| **[e.g., Sarah]** | [e.g., Financial Analyst] | [e.g., 35-45, MBA] | [e.g., Generate reports quickly, Identify trends] | [e.g., Complex UI, Slow loading] | [Medium-High] | [Daily] |
| **[e.g., Mike]** | [e.g., IT Administrator] | [e.g., 25-40, Technical] | [e.g., Monitor system health, Manage users] | [e.g., Lack of dashboards, Poor alerts] | [High] | [Weekly] |
| **[e.g., Emily]** | [e.g., Customer Service Rep] | [e.g., 22-35, High School+] | [e.g., Resolve tickets fast, Access customer history] | [e.g., Cluttered interface, Hard to find info] | [Medium] | [Hourly] |

#### 2.2 API Consumer Personas

Define the primary API consumers of the system.

| API Consumer | Type | Technical Level | Goals | Pain Points | Expected Volume | SLAs |
|--------------|------|-----------------|-------|-------------|-----------------|------|
| **[e.g., Mobile App]** | [First-party] | [High] | [Fast data sync, Offline support] | [Network issues, Payload size] | [High: 100k/day] | [<200ms] |
| **[e.g., Partner Integration]** | [Third-party] | [Medium] | [Easy integration, Clear docs] | [Poor documentation, Rate limiting] | [Medium: 10k/day] | [<500ms] |
| **[e.g., Internal Service]** | [First-party] | [High] | [Low latency, High throughput] | [Versioning, Backward compatibility] | [Very High: 1M/day] | [<50ms] |
| **[e.g., Web App]** | [First-party] | [Medium] | [Rich data, Good UX] | [Over-fetching, Under-fetching] | [High: 50k/day] | [<300ms] |

#### 2.3 Stakeholder Identification

Identify all stakeholders who have a vested interest in the system's design and operation.

| Stakeholder | Role/Title | Primary Interest | UX/UI Specific Concern | API Specific Concern |
|-------------|------------|------------------|------------------------|----------------------|
| **End-Users** | [e.g., Customers] | [e.g., Usability, Performance] | [e.g., Intuitive navigation, Fast page loads] | [e.g., API powers the experience] |
| **UX Designers** | [e.g., Product Design] | [e.g., Design consistency, User research] | [e.g., Design system adherence] | [e.g., API data shapes] |
| **UI Developers** | [e.g., Frontend Team] | [e.g., Implementation feasibility] | [e.g., Component library, Responsive] | [e.g., API response formats] |
| **API Developers** | [e.g., Backend Team] | [e.g., API quality, Performance] | [e.g., API-driven UI] | [e.g., OpenAPI specs, Versioning] |
| **API Consumers** | [e.g., Partner Devs] | [e.g., Integration ease] | [e.g., Documentation clarity] | [e.g., Stability, Rate limits] |
| **Product Owners** | [e.g., Business] | [e.g., Feature adoption] | [e.g., Conversion rates] | [e.g., API usage metrics] |
| **Accessibility Officer** | [e.g., Compliance] | [e.g., WCAG compliance] | [e.g., Screen reader support] | [e.g., Accessible API responses] |
| **Security Officer** | [e.g., Compliance] | [e.g., Data protection] | [e.g., Secure forms, Session timeout] | [e.g., OAuth2, Rate limiting] |
| **DevOps/SRE** | [e.g., Platform Team] | [e.g., Scalability, Resilience] | [e.g., UI performance monitoring] | [e.g., API monitoring, SLAs] |
| **QA Engineers** | [e.g., Testing] | [e.g., Testability] | [e.g., Component testing] | [e.g., API contract testing] |

#### 2.4 Stakeholder Concerns (IEEE 1016-2009)

Map each stakeholder to their specific **concerns**—the non-functional requirements, quality attributes, and risks they care about.

| Stakeholder | Concern | Priority | UX/UI Acceptance Criteria | API Acceptance Criteria |
|-------------|---------|----------|---------------------------|-------------------------|
| End-User | Ease of Use | High | [Task completion in <3 clicks] | [API returns predictable data] |
| End-User | Task Completion | High | [95% success rate on forms] | [API availability >99.99%] |
| End-User | Visual Clarity | High | [Information hierarchy clear] | [API responses well-structured] |
| UX Designer | Design Consistency | High | [Follow design system] | [Consistent API patterns] |
| UI Developer | Component Reusability | High | [80% components reusable] | [API responses consistent] |
| API Developer | API Quality | High | [API drives UI effectively] | [OpenAPI 3.0 specs complete] |
| API Consumer | Developer Experience | High | [Clear error messages] | [Self-documenting API] |
| Product Owner | User Engagement | High | [DAU/MAU >40%] | [API usage growth >20% YoY] |
| Accessibility Officer | WCAG Compliance | High | [WCAG 2.1 AA level] | [Accessible API responses] |
| Security Officer | Secure Auth | High | [MFA flow] | [OAuth2, JWT, Rate limiting] |
| DevOps/SRE | Performance | High | [LCP <2.5s] | [API P95 <200ms] |
| QA Engineer | Testability | High | [Component testing] | [API contract testing] |

#### 2.5 API Design Quality Attribute Scenarios

Define concrete, measurable API quality scenarios.

| Quality Attribute | API Scenario |
|-------------------|--------------|
| **Performance** | [e.g., P95 latency <200ms, P99 <500ms at peak load] |
| **Scalability** | [e.g., Handle 10k RPS with linear scaling] |
| **Availability** | [e.g., 99.99% uptime, MTTR <5 minutes] |
| **Security** | [e.g., OAuth2, JWT validation <10ms, Rate limiting 1000/min] |
| **Reliability** | [e.g., 0% data loss, Idempotent operations] |
| **Versioning** | [e.g., Semantic versioning, 2-year deprecation policy] |
| **Documentation** | [e.g., OpenAPI 3.0, Interactive docs, Code examples] |
| **Developer Experience** | [e.g., 15-minute integration, SDKs available] |
| **Observing** | [e.g., Distributed tracing, Structured logs] |
| **Backward Compatibility** | [e.g., 100% for 2 major versions] |

#### 2.6 API Design Constraints Matrix

| API Constraint | Requirement | Tool/Standard | Verification Method |
|----------------|-------------|---------------|---------------------|
| **API Specification** | [OpenAPI 3.0+ or AsyncAPI] | [OpenAPI] | [Swagger validator] |
| **Authentication** | [OAuth2.0 / JWT] | [IETF RFC 6749] | [Security audit] |
| **Rate Limiting** | [1000 req/min per API key] | [IETF RFC 7234] | [Load testing] |
| **Pagination** | [Cursor-based or offset-limit] | [JSON:API] | [API review] |
| **Versioning** | [URI versioning: /api/v1/] | [Semantic Versioning] | [API review] |
| **Error Response** | [RFC 7807 Problem Details] | [IETF RFC 7807] | [API review] |
| **Idempotency** | [Idempotency-Key header] | [API best practice] | [API testing] |
| **CORS** | [Secure CORS configuration] | [IETF RFC 6454] | [Security audit] |
| **Content Negotiation** | [Accept/Content-Type headers] | [HTTP/1.1] | [API testing] |
| **Deprecation** | [Deprecation header, Sunset] | [RFC 8594] | [API review] |

---

### 7.3 Design Views (IEEE 1016-2009 Core)

The design is documented through **eight distinct views**, each addressing specific stakeholder concerns. **Every view now includes both UI/UX and API design elements.**

---

#### 3.1 Composition View

**Purpose:** Describes how the system is assembled from smaller units. Shows the hierarchical decomposition—**including UI layer and API layer composition**.

**Viewpoint:** Structural breakdown into UI, API, and backend layers.

**Stakeholder Concerns Addressed:** Maintainability, Modularity, Component Reusability, API Organization.

##### Full System Composition Diagram:

```
flowchart TD
    subgraph Presentation[Presentation Layer - UI]
        Pages[Pages / Routes]
        Layouts[Layout Templates]
        Components[UI Components]
        State[State Management]
    end

    subgraph API[API Layer]
        subgraph Gateway[API Gateway]
            Auth[Authentication]
            Routing[Route Routing]
            RateLimit[Rate Limiting]
            Cache[Response Cache]
        end

        subgraph Public[Public API]
            REST[REST Endpoints]
            GraphQL[GraphQL Schema]
            Webhooks[Webhook Publishers]
        end

        subgraph Internal[Internal API]
            gRPC[gRPC Services]
            Events[Event Publishers]
            Admin[Admin API]
        end
    end

    subgraph Backend[Backend Services]
        SVC1[Service 1]
        SVC2[Service 2]
        SVC3[Service 3]
    end

    subgraph Data[Data Layer]
        DB[(Database)]
        CacheDB[(Redis Cache)]
        Search[(Elasticsearch)]
        Queue[(Message Queue)]
    end

    Pages --> Components
    Pages --> State
    State --> REST
    State --> GraphQL

    API --> Gateway
    Gateway --> Public
    Gateway --> Internal
    Public --> SVC1
    Public --> SVC2
    Internal --> SVC3

    SVC1 --> DB
    SVC1 --> CacheDB
    SVC2 --> Search
    SVC2 --> Queue
    SVC3 --> DB
```
