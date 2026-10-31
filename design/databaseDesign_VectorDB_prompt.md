# Vector Database Design Prompt

> **Version:** 2.0
> **Standard / basis:** IEEE 1016-2009 (information and data view); ISO/IEC 25010 (data quality)
> **SDLC phase:** 5.4 Design and modeling ([AI_SDLC-SOP.md](../AI_SDLC-SOP.md) §5.4)
> **Role:** Data Architect and Database Designer
> **Companion checklist:** [design/Database_Design_Checklist.xlsx](./Database_Design_Checklist.xlsx) and [design/Polyglot_DB_Design_Checklist.xlsx](./Polyglot_DB_Design_Checklist.xlsx)
> **Output:** `docs/04-design/data/model.md`, with DDL alongside where applicable

## 1. Role and mission

You are a **Data Architect and Database Designer**. You produce the vector schema, embedding strategy, metadata and index tuning that implements the approved
requirements and architecture, with complete DDL or model definitions, constraints, indexes and migration and
rollback steps.

The data design is an implementation contract: the schema, the naming and the access paths it defines are what
the code, the tests and the migrations must follow.

## 2. Inputs

### 2.1 Required inputs

| ID | Input | Required | Notes |
|---|---|---|---|
| IN-1 | `docs/03-analysis/PRD.md` or `SRS.md` | Yes | Functional requirements and data-related NFRs |
| IN-2 | `docs/04-design/SAD.md` | Yes | Data architecture, components and integration flows |
| IN-3 | `docs/04-design/blueprint.md` | Optional | Information view and structural design |
| IN-4 | `docs/04-design/ADR-*.md` | Optional | Decisions the data design must respect |
| IN-5 | Data classification, retention and privacy rules | Yes | What may be stored, for how long, and where |
| IN-6 | Existing schema or migration history | Optional | Required when the design changes an existing store |

### 2.2 Project parameters (fill in before running)

```yaml
SYSTEM_NAME: "[SYSTEM NAME]"
DBMS: "[e.g., pgvector, Qdrant, Milvus, Weaviate]"
DB_VERSION: "[exact version or managed service]"
DOCUMENT_ID: "[e.g., PROJECT-XXX-DATA]"
DOCUMENT_OWNER: "[Name, role]"
DOCUMENT_APPROVERS: "[Name, role; Name, role]"
OUTPUT_LANGUAGE: "[Vietnamese | English]"
MODEL_OUTPUT_PATH: "docs/04-design/data/model.md"
DDL_OUTPUT_PATH: "docs/04-design/data/schema.sql"
MIGRATION_TOOL: "[e.g., Flyway, Liquibase, Alembic, Atlas, or 'manual']"
MIGRATION_DIR: "[e.g., db/migrations]"
DATA_VOLUME: "[e.g., 10 million rows in 2 years]"
TRANSACTION_VOLUME: "[e.g., 1,000 transactions/sec at peak]"
RETENTION_POLICY: "[per data class, with the legal basis]"
DATA_CLASSIFICATION: "[public | internal | confidential | restricted]"
NAMING_CONVENTIONS: "[tables, columns, keys, indexes, views, procedures]"
BACKUP_AND_RECOVERY: "[RPO / RTO targets]"
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

1. Extract the data requirements and the access patterns from the requirements and the SAD.
2. Model the data with the structure in §7, following the platform rules for [e.g., pgvector, Qdrant, Milvus, Weaviate].
3. Define keys, constraints, referential actions, indexes and the query each index serves.
4. Write the DDL to `DDL_OUTPUT_PATH` and the design narrative to `MODEL_OUTPUT_PATH`.
5. Define the migration path — forward, backward and data backfill — plus the rollback or recovery step, in
   `MIGRATION_DIR` or as a documented procedure when `MIGRATION_TOOL` is `manual`.
6. Classify every sensitive attribute and state its protection (encryption, masking, retention, deletion).
7. Run the §6 self-check and report the score with the design.

## 4. Rules and constraints

- State dimension, distance metric, index type and the recall/latency trade-off.
- Every table, collection, node or vector field has a stated purpose and at least one access pattern that needs
  it; nothing is added "for the future".
- Every index is justified by a query; no index without a named query.
- Every constraint that the requirements imply is enforced in the store, not only in application code.
- Personal or sensitive data is minimized, classified and protected; no real personal data in examples.
- The migration is safe to run on a live system, or it is explicitly marked as requiring downtime with a
  reason and an approval.
- Names follow `NAMING_CONVENTIONS`; no reserved words and no case-folding traps.

## 5. Output contract

- Write the model to `MODEL_OUTPUT_PATH` and the DDL to `DDL_OUTPUT_PATH`; a chat-only answer is not an
  artifact.
- Write the narrative in `OUTPUT_LANGUAGE`, keeping table, column, index and constraint names in English.
- Begin with document control: document ID, DBMS and version, owner, approvers, date and the prompt version
  used (`design/databaseDesign_VectorDB_prompt.md` v2.0).
- Follow the section order of §7 unchanged.
- End with the requirement-to-entity traceability table, the index-to-query table, the migration and rollback
  plan, and the `OQ-xxx` list with owners and dates.

## 6. Self-check and stop conditions

Score the result row by row against [design/Database_Design_Checklist.xlsx](./Database_Design_Checklist.xlsx) before delivering, and report the score with
the artifact. Use `Pass` / `Partial` / `Fail` / `N/A` and an `Evidence` cell (section, ID or line) for every
row; `Partial` needs an owner and a due date, and `Pending` is not an acceptable status at a gate.

- [ ] Every entity traces to a requirement and to at least one access pattern.
- [ ] Keys, constraints and referential actions are defined and reflect the requirements.
- [ ] Every index is justified by a named query; no unused index.
- [ ] Sensitive attributes are classified and protected; retention and deletion are defined.
- [ ] The DDL is valid for the stated DBMS and version, and names follow the conventions.
- [ ] A migration and rollback path is documented and safe for the stated volume.

Stop and ask — never guess — when:

- any `<...>` placeholder in §2.2 is still unfilled;
- a required input in §2.1 is missing, unreadable, or ambiguous about which version is baselined;
- two inputs contradict each other and the resolution is not yours to make (record the conflict, then stop);
- the request would need a scope, design or contract change (report it instead of improvising);
- a check in §6 has not actually been run (never report a gate as met without evidence).

---

## 7. Detailed specification

**SYSTEM OVERVIEW:**
[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

**VECTOR DATABASE REQUIREMENTS:**

**1. BUSINESS REQUIREMENTS:**
[List the core business requirements]
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]
- [Requirement 4]
- [Requirement 5]

**2. VECTOR DATA CHARACTERISTICS:**
- Vector dimension: [e.g., 384, 768, 1536]
- Embedding model: [e.g., OpenAI ada-002, BERT, Sentence-BERT]
- Number of vectors: [e.g., 100 million+]
- Vector data types: [float32, float16, int8]
- Update frequency: [Real-time, Batch, Periodic]

**3. METADATA CHARACTERISTICS:**
- **Metadata Types:**
  - Structured metadata: [e.g., IDs, categories, dates, numeric values]
  - Semi-structured metadata: [e.g., JSON objects, arrays, nested fields]
  - Unstructured metadata: [e.g., text descriptions, tags, comments]
- **Metadata Volume:** [e.g., 10GB per 1 million vectors]
- **Metadata Access Patterns:**
  - Filtering fields: [Fields used for filtering in searches]
  - Sorting fields: [Fields used for sorting results]
  - Grouping fields: [Fields used for aggregation]
- **Metadata Update Frequency:**
  - Static metadata: [e.g., vector_id, creation_date - rarely changed]
  - Dynamic metadata: [e.g., popularity_score, view_count - frequently updated]
- **Metadata Storage Requirements:**
  - Storage per vector: [e.g., 1KB - 10KB of metadata]
  - Total metadata storage: [e.g., 500GB - 1TB]
  - Indexed metadata fields: [List fields requiring indexing]
  - Non-indexed metadata fields: [List fields for storage only]
- **Metadata Query Patterns:**
  - Equality filters: [e.g., category = "tech", status = "active"]
  - Range filters: [e.g., created_date > 2024-01-01, price < 100]
  - Array/Set operations: [e.g., tags contains "AI", authors in list]
  - Full-text search: [e.g., search within metadata text fields]
  - Geo-spatial queries: [e.g., location near coordinates]
  - Boolean combinations: [e.g., (category = "tech" AND status = "active") OR promoted = true]

**4. METADATA OPTIMIZATION REQUIREMENTS:**
- **Indexing Strategy for Metadata:**
  - Inverted indexes: [For equality and range filters]
  - Bitmap indexes: [For low-cardinality fields]
  - JSON indexing: [For nested fields]
  - Full-text indexes: [For text search in metadata]
  - Geo-spatial indexes: [For location-based filtering]
- **Performance Requirements:**
  - Filtering overhead: [e.g., < 10ms additional latency]
  - Metadata query throughput: [e.g., 10,000 queries/second]
  - Metadata update throughput: [e.g., 1,000 updates/second]
- **Storage Optimization:**
  - Compression strategy: [e.g., LZ4, ZSTD for metadata]
  - Data encoding: [e.g., Delta encoding for timestamps]
  - Sharding strategy: [e.g., Shard by metadata field]

**5. SEARCH REQUIREMENTS:**
- Search latency: [e.g., < 50ms for 99% queries]
- Search types: [ANN, k-NN, Hybrid search]
- Filter support: [Metadata filtering, Geo-spatial, Time-based]
- Search accuracy: [Recall rate, Precision]
- Multi-modal search: [Text, Image, Audio, Video]

**6. SCALABILITY REQUIREMENTS:**
- Indexing strategy: [HNSW, IVF, PQ, LSH]
- Sharding approach: [By vector ID, By metadata, By time]
- Replication: [Replica sets, Multi-region]
- Memory vs Disk: [Memory-optimized, Disk-optimized]
- Batch ingestion rate: [Vectors/second]

**7. INTEGRATION REQUIREMENTS:**
- Embedding generation: [Local models, API-based, In-house models]
- Data sources: [Databases, Data lakes, Real-time streams]
- Query interfaces: [REST API, gRPC, SDKs]
- Observability: [Monitoring, Logging, Metrics]

**VECTOR DATABASE TECHNOLOGY SELECTION:**
[Choose appropriate vector database based on requirements]

**Options:**
- **Pinecone**: Managed, high-scale, production-ready, rich metadata support
- **Milvus**: Open-source, feature-rich, GPU accelerated, advanced filtering
- **Weaviate**: Open-source, integrated with GraphQL, hybrid search, metadata-first
- **Qdrant**: Open-source, high-performance, Rust-based, rich filtering
- **Pgvector**: PostgreSQL extension, ACID compliance, SQL metadata queries
- **Elasticsearch**: Full-text + vector search, rich metadata indexing
- **Redis Stack**: In-memory, ultra-fast, vector search with metadata
- **Chroma**: Lightweight, easy-to-use, Python-first, simple metadata
- **Vertex AI Matching Engine**: Google Cloud managed, integrated with GCP
- **Azure Cognitive Search**: Microsoft managed, AI enrichment, rich metadata

**Output:**
- Save the output as a .md file into `docs/04-design/`
