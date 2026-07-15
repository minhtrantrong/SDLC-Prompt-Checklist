Create a comprehensive SQL Database Design for [SYSTEM NAME] including complete schema design, SQL DDL statements, relationships, constraints, indexes, and best practices. The output should be a well-structured markdown file with complete SQL code.

**SYSTEM OVERVIEW:**
[Provide detail description of your system - or attach your SRS/PRD or/and SAD documents at here]

**DATABASE REQUIREMENTS:**

**1. BUSINESS REQUIREMENTS:**
[List the core business requirements]
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]
- [Requirement 4]
- [Requirement 5]

**2. DATA STORAGE REQUIREMENTS:**
- Estimated data volume: [e.g., 10 million rows in 2 years]
- Transaction volume: [e.g., 1000 transactions/second]
- Data retention period: [e.g., 7 years]
- Growth rate: [e.g., 20% annually]
- Availability requirements: [e.g., 99.99% uptime]
- Backup frequency: [e.g., Daily full, hourly incremental]

**3. PERFORMANCE REQUIREMENTS:**
- Query response time: [e.g., < 100ms for 90% queries]
- Concurrent users: [e.g., 10,000 concurrent users]
- Reporting queries: [e.g., Complex reporting on historical data]
- Batch processing: [e.g., Nightly ETL jobs]

**4. SECURITY REQUIREMENTS:**
- Data encryption: [e.g., AES-256 at rest]
- Access control: [e.g., Row-level security]
- Audit logging: [e.g., Track all changes]
- Compliance standards: [e.g., GDPR, HIPAA, PCI-DSS]

**OUTPUT FORMAT:**

**1. ENTITY-RELATIONSHIP DIAGRAM (Text-based)**
- List all entities and their relationships
- Include cardinality and participation constraints

**2. TABLE DEFINITIONS**
- Complete DDL statements for each table
- All columns with proper data types
- Primary keys and foreign keys
- CHECK constraints
- DEFAULT values
- NOT NULL constraints
- Unique constraints

**3. RELATIONSHIP MAPPING**
- Foreign key definitions
- Referential actions (CASCADE, SET NULL, RESTRICT)
- Junction tables for many-to-many relationships

**4. INDEXES AND PERFORMANCE**
- Clustered/Non-clustered indexes
- Composite indexes
- Full-text indexes
- Index usage strategy

**5. VIEWS**
- Business views
- Reporting views
- Materialized views

**6. STORED PROCEDURES AND FUNCTIONS**
- Business logic implementation
- Data validation procedures
- Batch processing procedures

**7. TRIGGERS**
- Audit triggers
- Validation triggers
- Computed column triggers

**8. DATA TYPES AND CONSTRAINTS**
- Detailed explanation of data type choices
- Constraint definitions
- Validation rules

**9. MIGRATION AND SEEDING SCRIPTS**
- Initial data population
- Sample data for testing
- Migration scripts for versioning

**10. DATABASE ADMINISTRATION**
- Backup strategies
- Maintenance plans
- Monitoring queries
- Performance tuning recommendations

**TECHNICAL SPECIFICATIONS:**

**Database Platform:** [PostgreSQL/MySQL/SQL Server/Oracle]
**Version:** [Version number]
**Character Set:** UTF-8
**Collation:** [Appropriate collation]
**Storage Engine:** [InnoDB/MyISAM/PostgreSQL default]

**NAMING CONVENTIONS:**
- Tables: [e.g., snake_case, plural]
- Columns: [e.g., snake_case, singular]
- Primary Keys: [e.g., id, {table}_id]
- Foreign Keys: [e.g., {referenced_table}_id]
- Indexes: [e.g., idx_{table}_{column}]
- Views: [e.g., vw_{purpose}]
- Stored Procedures: [e.g., sp_{action}_{object}]
- Triggers: [e.g., trg_{table}_{action}_{timing}]

**Output:**
- Save the output as a .md or [.sql] file into [your document folder such as ./docs]