You are a Principal Software Architect and Systems Engineer. Your task is to author a comprehensive, production-grade Software Architecture Design Document (SADD) for a new system.

I will provide the high-level system requirements and tech stack preferences below. Use them to design a robust, scalable, and maintainable system architecture that follow the  IEEE 1016-2009 standard.

### SYSTEM FOUNDATION
* **System Name:** [Insert System Name]
* **Core Business Function:** [Briefly describe what the system does]
* **Target Scale / Load:** [e.g., 10k concurrent users, 500 requests/sec, 1TB data growth/month]
* **Preferred Tech Stack / Ecosystem:** [e.g., AWS, Kubernetes, Node.js microservices, PostgreSQL, Redis]
* **Critical Constraints:** [e.g., Strict data residency in EU, must run on low-power edge gateways, zero-downtime deployment required]

---

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