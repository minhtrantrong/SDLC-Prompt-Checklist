Create a comprehensive Vector Database Design for [SYSTEM NAME] including complete schema design, vector embedding strategies, **metadata management**, indexing methods, similarity search optimization, and best practices. The output should be a well-structured markdown file with complete vector database implementation details.

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
- Save the output as a .md file into [your document folder such as ./docs]