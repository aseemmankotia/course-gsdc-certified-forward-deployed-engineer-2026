## Chapter 4: Data Engineering and Storage Strategy for AI Systems — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | ETL vs ELT: where does transformation happen? | ETL = transform BEFORE loading, using an external processing engine. ELT = load raw data first, then transform AFTER, using the target warehouse/lake's own compute. Exam tip: ELT is favored with elastic cloud warehouses (e.g., Snowflake, BigQuery). |
| 2 | Batch vs streaming: key differentiator? | Batch = scheduled processing of accumulated data (minutes-to-hours latency). Streaming = continuous processing of events as they arrive (sub-second to seconds latency). Exam tip: 'real-time' or millisecond/second SLA in the scenario = streaming. |
| 3 | When does the exam want a vector database as the answer? | When the scenario mentions embeddings, semantic similarity search, or RAG retrieval. Vector DBs use ANN algorithms (e.g., HNSW), not B-tree indexes. |
| 4 | SQL vs NoSQL: which fits flexible, inconsistent schemas across records? | NoSQL document databases (e.g., MongoDB). SQL requires a fixed schema and is better suited for strong consistency plus complex joins/transactions. |
| 5 | When is an in-memory store (e.g., Redis) the correct storage choice? | When the scenario needs sub-millisecond latency for ephemeral, cache-like data (sessions, leaderboards, hot lookups) — not for durable system-of-record data. |
| 6 | Name the core data observability pillars. | Freshness, Volume, Schema, Distribution, Lineage. Exam tip: 'schema drift' = structure/type change; 'distribution anomaly' = values outside statistical range. |
| 7 | What does a 'schema drift' alert mean? | The incoming data's field names or types changed unexpectedly vs. the expected schema. Common trap: confusing this with a volume or freshness alert. |
| 8 | What problem does normalization (3NF) primarily solve? | Removes transitive dependencies, reducing data redundancy and update anomalies. Trade-off: more joins at read time — denormalize for read-heavy analytics workloads. |
| 9 | What is Change Data Capture (CDC) used for? | Capturing row-level inserts/updates/deletes from a source database in near-real-time to feed downstream systems (streaming pipelines, replicas). It's a source-capture pattern, not a storage type. |
| 10 | Parquet vs JSON for analytics storage: which is preferred and why? | Parquet — columnar and compressed, faster for large-scale analytical (column-scan) queries. JSON is row-based and human-readable, better for flexible/nested data exchange, not large-scale analytics. |
| 11 | ACID vs BASE: which applies to typical SQL vs typical NoSQL systems? | SQL = ACID (Atomicity, Consistency, Isolation, Durability) — strong consistency. NoSQL = BASE (Basically Available, Soft state, Eventual consistency) — prioritizes availability and scale over strict consistency. |
| 12 | What is stored alongside the vector in a vector database? | Metadata/payload (e.g., source document ID, text chunk) plus the embedding vector. Similarity search ranks results by a distance metric — cosine similarity, dot product, or Euclidean distance. |
