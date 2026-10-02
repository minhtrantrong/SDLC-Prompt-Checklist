You are a professional software developer, please generate a complete, standards-compliant Software API Design with full traceability from stakeholder concerns to design elements that following the **Standard:** IEEE 1016-2009.
**Output:**
- Save the output as a .md or [.sql] file into [your document folder such as ./docs]
---

## 1. Context & Subject

### 1.1 System Identification

[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

| Attribute | Value |
|-----------|-------|
| **System Name** | [INSERT SYSTEM NAME] |
| **SDD Version** | [e.g., v1.0] |
| **Document Date** | [YYYY-MM-DD] |
| **Document Owner** | [Lead Architect / UX Lead / API Lead / Team] |
| **Revision History** | [Version, Date, Author, Changes] |

### 1.2 System Scope and External Boundaries

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

### 1.3 Assumptions and Constraints

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

## 2. Stakeholders & Concerns

### 2.1 User Personas

Define the primary users of the system with their goals, needs, and pain points.

| Persona | Role | Demographics | Goals | Pain Points | Tech Proficiency | Usage Frequency |
|---------|------|--------------|-------|-------------|------------------|-----------------|
| **[e.g., Sarah]** | [e.g., Financial Analyst] | [e.g., 35-45, MBA] | [e.g., Generate reports quickly, Identify trends] | [e.g., Complex UI, Slow loading] | [Medium-High] | [Daily] |
| **[e.g., Mike]** | [e.g., IT Administrator] | [e.g., 25-40, Technical] | [e.g., Monitor system health, Manage users] | [e.g., Lack of dashboards, Poor alerts] | [High] | [Weekly] |
| **[e.g., Emily]** | [e.g., Customer Service Rep] | [e.g., 22-35, High School+] | [e.g., Resolve tickets fast, Access customer history] | [e.g., Cluttered interface, Hard to find info] | [Medium] | [Hourly] |

### 2.2 API Consumer Personas

Define the primary API consumers of the system.

| API Consumer | Type | Technical Level | Goals | Pain Points | Expected Volume | SLAs |
|--------------|------|-----------------|-------|-------------|-----------------|------|
| **[e.g., Mobile App]** | [First-party] | [High] | [Fast data sync, Offline support] | [Network issues, Payload size] | [High: 100k/day] | [<200ms] |
| **[e.g., Partner Integration]** | [Third-party] | [Medium] | [Easy integration, Clear docs] | [Poor documentation, Rate limiting] | [Medium: 10k/day] | [<500ms] |
| **[e.g., Internal Service]** | [First-party] | [High] | [Low latency, High throughput] | [Versioning, Backward compatibility] | [Very High: 1M/day] | [<50ms] |
| **[e.g., Web App]** | [First-party] | [Medium] | [Rich data, Good UX] | [Over-fetching, Under-fetching] | [High: 50k/day] | [<300ms] |

### 2.3 Stakeholder Identification

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

### 2.4 Stakeholder Concerns (IEEE 1016-2009)

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

### 2.5 API Design Quality Attribute Scenarios

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

### 2.6 API Design Constraints Matrix

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

## 3. Design Views (IEEE 1016-2009 Core)

The design is documented through **eight distinct views**, each addressing specific stakeholder concerns. **Every view now includes both UI/UX and API design elements.**

---

### 3.1 Composition View

**Purpose:** Describes how the system is assembled from smaller units. Shows the hierarchical decomposition—**including UI layer and API layer composition**.

**Viewpoint:** Structural breakdown into UI, API, and backend layers.

**Stakeholder Concerns Addressed:** Maintainability, Modularity, Component Reusability, API Organization.

#### Full System Composition Diagram:

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