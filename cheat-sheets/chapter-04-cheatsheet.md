## Chapter 4 Cheat Sheet: Data Engineering & Storage Strategy

### ETL vs ELT
| Pattern | Transform Location | Best When |
|---|---|---|
| ETL | External engine, BEFORE load | Limited target compute, need to clean/mask before landing |
| ELT | Target warehouse/lake, AFTER load | Elastic cloud warehouse compute, analysts iterate in SQL |

### Batch vs Streaming
| Pattern | Latency | Use Case |
|---|---|---|
| Batch | Minutes–hours | Reporting, nightly aggregates, large historical loads |
| Streaming | Sub-second–seconds | Fraud detection, real-time dashboards, alerting |
| Micro-batch | Seconds–minutes | Middle ground (e.g., Spark Structured Streaming) |

### Storage Strategy Decision Table
| Need | Choose |
|---|---|
| Structured data, transactions, joins, strong consistency | SQL (RDBMS) |
| Flexible/evolving schema, high write scale | NoSQL (document/key-value/column) |
| Semantic similarity search, embeddings, RAG | Vector DB (ANN search: HNSW) |
| Sub-millisecond, ephemeral data | In-memory (Redis, Memcached) |
| Large-scale analytical columnar scans | File formats (Parquet, ORC) on object storage |
| Human-readable, nested, semi-structured exchange | JSON |

### Consistency Models
- **ACID** (SQL): Atomicity, Consistency, Isolation, Durability — strong guarantees.
- **BASE** (NoSQL): Basically Available, Soft state, Eventual consistency — favors availability/scale.

### Database Design Fundamentals
- **Normalization (1NF→3NF):** removes redundancy/anomalies; more joins at read time.
- **Denormalization:** duplicates data to speed reads; common in analytics/read-heavy systems.
- **Primary key / Foreign key:** enforce entity identity and referential integrity.
- **Indexing (B-tree):** speeds exact-match/range queries in SQL; not suited for high-dimensional similarity.

### Data Observability — 5 Pillars
| Pillar | Monitors |
|---|---|
| Freshness | Is data arriving on time? |
| Volume | Is the expected amount of data arriving? |
| Schema | Did field names/types change unexpectedly (drift)? |
| Distribution | Are values statistically within expected ranges? |
| Lineage | Where did the data originate and how was it transformed? |

### Exam Traps
- ETL vs ELT: exam distinguishes by WHERE transform compute runs, not WHERE data lands.
- 'Real-time'/'millisecond' keyword → streaming, not batch.
- Vector DB ≠ generic NoSQL — reserved for embedding/similarity use cases.
- Schema drift ≠ volume anomaly ≠ freshness anomaly — each is a distinct observability pillar.
- Normalization improves write integrity, NOT read speed (denormalize for reads).
