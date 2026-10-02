# RAG Systems End to End — Cheat Sheet

## RAG vs Fine-Tuning
| Use RAG when... | Use Fine-Tuning when... |
|---|---|
| Knowledge changes frequently | Need to change tone/style/format |
| Need source citations | Fixed, stable domain |
| Data too large for weights | Teaching a new output structure |
| Need to add facts fast | Reducing prompt length for a fixed task |

## The Core Flow
**Chunk → Embed → Retrieve → Generate**
1. Split docs into chunks
2. Convert chunks to vectors (embedding model)
3. At query time, embed the query and retrieve top-k similar chunks
4. Pass retrieved chunks + query to LLM as context

## Vector Database Comparison
| Tool | Type | Best For | Metadata Filtering |
|---|---|---|---|
| FAISS | Open-source library | Max control, self-hosted, in-memory/GPU | Manual/limited |
| Chroma | Lightweight, embedded | Local prototyping, small-medium apps | Built-in |
| Pinecone | Fully managed, serverless | Production, auto-scaling, no ops | Built-in |

## Chunking Best Practices
- Chunk size: **~300-512 tokens**
- Overlap: **~10-15%** between adjacent chunks
- Split along semantic/section boundaries, not arbitrary character counts
- Metadata to include: `doc_id`, `source`, `section/title`, `timestamp`, `page`

## RAG Failure Modes & Mitigations
| Failure Mode | Symptom | Mitigation |
|---|---|---|
| Lost-in-the-middle | Correct chunk retrieved but ignored | Re-rank so top chunks sit near start/end of prompt |
| Low recall | Vague query → irrelevant results | Query rewriting/expansion |
| Noisy top-k | Many marginally relevant chunks | Re-ranking with a cross-encoder |
| Missing exact terms | Embeddings miss codes/IDs | Hybrid retrieval (BM25 + dense vectors) |
| Hallucination despite good context | Generation ignores retrieved facts | Strengthen prompt instructions to ground answer strictly in context |

## Hybrid Retrieval & Re-ranking
- **Hybrid retrieval** = sparse (BM25/keyword) + dense (embedding) search combined
- **Re-ranking** = second-stage model re-scores initial top-k for relevance before generation
- **Query rewriting** = LLM expands/clarifies query before retrieval

## Evaluating RAG Systems (RAGAS-style metrics)
| Metric | Measures |
|---|---|
| Faithfulness | Is the answer grounded in retrieved context (no hallucination)? |
| Answer Relevancy | Does the answer address the actual question? |
| Context Precision | Are retrieved chunks relevant (low noise)? |
| Context Recall | Did retrieval capture all needed information? |

## Exam Traps
- Fine-tuning does NOT reliably teach new facts — don't pick it for fast-changing knowledge questions
- Bigger context window ≠ fixes lost-in-the-middle — position matters, not just size
- FAISS is a library, not a hosted service — don't confuse with Pinecone
- Metadata filtering improves precision, not just organization — disabling it hurts retrieval quality
