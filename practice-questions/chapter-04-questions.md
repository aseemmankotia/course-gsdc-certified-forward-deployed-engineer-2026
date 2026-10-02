## Chapter 4: Data Engineering and Storage Strategy for AI Systems — Practice Questions

**Q1.** A company needs real-time fraud detection that scores each payment transaction within 200ms of occurrence, with data arriving continuously from thousands of terminals. Which architecture BEST meets these requirements?

A) Batch ETL job running every hour to score accumulated transactions
B) ELT into a data warehouse followed by a nightly batch scoring job
C) Streaming pipeline with real-time feature computation and low-latency scoring
D) Manual CSV export processed weekly by an analyst

<details>
<summary>Answer</summary>

**Correct: C**

Streaming architectures process events continuously with sub-second latency, meeting the 200ms SLA.

**Why the others are wrong:**
- Hourly batch introduces up to 60 minutes of delay — far exceeds the 200ms requirement
- Nightly scoring means fraud is detected a day late, defeating the purpose
- Weekly manual processing is neither real-time nor scalable

</details>

---

**Q2.** A team is building a RAG (retrieval-augmented generation) application that must find semantically similar documents given a user query embedding. Which storage should be the primary retrieval layer?

A) Vector database using approximate nearest neighbor (ANN) search
B) Relational SQL database with B-tree indexes
C) Document-oriented NoSQL database with key-based lookups
D) In-memory key-value cache

<details>
<summary>Answer</summary>

**Correct: A**

Vector databases are purpose-built for high-dimensional similarity search using ANN algorithms like HNSW.

**Why the others are wrong:**
- B-tree indexes are optimized for exact-match/range queries, not high-dimensional similarity
- NoSQL document stores retrieve by key or filter, not by semantic distance
- In-memory caches provide fast exact-key lookup, not similarity ranking

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Raw data lands in cloud object storage in multiple formats. It is loaded as-is into a cloud data warehouse, and transformations are then written and executed in SQL using the warehouse's own compute engine, letting analysts iterate on transform logic without a separate ETL tool. Which pattern is this?

A) ETL
B) Change Data Capture
C) Streaming ingestion
D) ELT

<details>
<summary>Answer</summary>

**Correct: D**

Loading raw data first and transforming afterward using the target system's compute is the defining trait of ELT.

**Why the others are wrong:**
- ETL transforms data in an external engine BEFORE it is loaded into the target
- CDC captures row-level changes from a source; it doesn't describe where transformation compute runs
- Streaming ingestion describes how data arrives, not where transformation logic executes

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which storage type is BEST for user session data that must be retrieved with sub-millisecond latency and does not need durability beyond the session lifetime?

A) SQL relational database
B) Vector database
C) File-based storage (e.g., Parquet on object storage)
D) In-memory data store (e.g., Redis)

<details>
<summary>Answer</summary>

**Correct: D**

In-memory stores serve reads in microseconds with no disk I/O, ideal for ephemeral session state.

**Why the others are wrong:**
- SQL adds disk I/O and transactional overhead, increasing latency beyond sub-millisecond targets
- Vector databases are built for similarity search, not simple key-based session retrieval
- Object storage/Parquet is optimized for batch analytical scans, with latency far higher than in-memory access

</details>

---

**Q5.** An application stores a product catalog where attributes vary widely by category (electronics have different fields than clothing) and the schema changes frequently. Which storage is BEST?

A) NoSQL document database with flexible schema
B) Normalized SQL relational database with a fixed schema
C) Vector database
D) In-memory cache only

<details>
<summary>Answer</summary>

**Correct: A**

Document-oriented NoSQL stores allow each document to have a different set of fields without schema migrations.

**Why the others are wrong:**
- SQL requires a fixed schema, forcing sparse null columns or complex EAV modeling for variable attributes
- Vector databases store embeddings for similarity search, not structured product attributes
- A cache is not a durable system of record for catalog data

</details>

---

**Q6.** In relational database design, applying third normal form (3NF) to a schema primarily achieves what?

A) Elimination of transitive dependencies to reduce data redundancy and update anomalies
B) Faster read query performance through denormalization
C) Automatic sharding of tables across multiple nodes
D) Conversion of relational rows into vector embeddings

<details>
<summary>Answer</summary>

**Correct: A**

3NF removes transitive dependencies between non-key attributes, reducing redundancy and preventing update anomalies.

**Why the others are wrong:**
- Normalization typically trades some read speed (more joins) for write integrity — this is the opposite goal of denormalization
- Normalization is a logical schema design concept unrelated to physical sharding
- Normalization has nothing to do with embeddings or vector representations

</details>

---

**Q7.** A data observability system flags a 'schema drift' alert on an ingestion pipeline. What does this MOST likely indicate?

A) The pipeline's compute cluster ran out of memory
B) The incoming data's structure (field names or types) changed unexpectedly from the expected schema
C) The data volume dropped below the historical baseline
D) A downstream dashboard query timed out

<details>
<summary>Answer</summary>

**Correct: B**

Schema drift specifically refers to unexpected changes in the structure/types of incoming data.

**Why the others are wrong:**
- Memory exhaustion is an infrastructure/resource alert, unrelated to schema
- A volume drop is a separate observability pillar (Volume), not Schema
- A dashboard timeout is a downstream consumption issue, not a pipeline observability signal

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which pair correctly matches a data observability pillar to what it monitors?

A) Distribution — whether the statistical values of data fall within expected ranges
B) Freshness — whether data types match the expected schema
C) Volume — whether data arrived within the expected time window
D) Lineage — whether data uses proper indexing for query speed

<details>
<summary>Answer</summary>

**Correct: A**

Distribution tracks whether data values are statistically within expected ranges, catching anomalies like sudden spikes or nulls.

**Why the others are wrong:**
- Freshness measures timeliness of data arrival, not type matching (that's Schema)
- Volume measures the amount/count of records received, not the time window (that's Freshness)
- Lineage tracks a data element's origin and transformation history, not query indexing

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

