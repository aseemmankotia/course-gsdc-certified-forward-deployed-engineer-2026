## Chapter 7: RAG Systems End to End — Practice Questions

**Q1.** A company's internal HR chatbot must answer employee questions using policy documents that change every week (new PTO rules, updated benefits). Which approach BEST meets this requirement?

A) Fine-tune a base LLM on the current policy documents monthly
B) Prompt engineering alone with the full policy document pasted into every system prompt
C) Use RAG: store policy documents in a vector database and retrieve relevant chunks at query time
D) Fine-tune the LLM once and re-fine-tune only when major policy overhauls occur

<details>
<summary>Answer</summary>

**Correct: C**

RAG allows instant updates by re-indexing the vector store without retraining, matching weekly-changing content perfectly.

**Why the others are wrong:**
- Fine-tuning monthly is costly, slow, and doesn't reflect changes made mid-cycle, risking stale answers.
- Pasting full docs into every prompt wastes context window and cost and doesn't scale as documents grow.
- Same staleness problem — fine-tuning doesn't fit fast-changing factual content.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A RAG system retrieves the correct answer chunk among 10 retrieved chunks, but the LLM's final answer ignores it because the chunk is placed in the middle of a long context window. Which mitigation directly addresses this failure mode?

A) Reduce the embedding dimensionality
B) Switch to a larger context window model with no other changes
C) Increase the chunk size to reduce the total number of chunks retrieved
D) Re-rank retrieved chunks so the most relevant ones are placed near the start or end of the prompt

<details>
<summary>Answer</summary>

**Correct: D**

This is the 'lost-in-the-middle' problem — LLMs attend better to information at the start/end of context, so re-ranking to position top chunks accordingly mitigates it.

**Why the others are wrong:**
- Embedding dimensionality affects retrieval quality, not positional attention bias.
- A bigger context window doesn't fix attention bias and may worsen it by adding more middle positions.
- Larger chunks add noise and don't solve positional attention bias.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Users ask short, ambiguous queries like 'refund policy' and the retriever returns irrelevant or overly broad chunks. Which technique BEST improves retrieval relevance in this scenario?

A) Increase the top-k retrieval count to 50
B) Query rewriting: use an LLM to expand/clarify the query before retrieval (add context, synonyms, intent)
C) Switch to a smaller embedding model
D) Disable metadata filtering entirely

<details>
<summary>Answer</summary>

**Correct: B**

Query rewriting/expansion clarifies intent and adds relevant terms, directly improving retrieval precision for vague queries.

**Why the others are wrong:**
- More retrieved chunks increases noise without fixing the underlying ambiguity.
- A smaller embedding model generally reduces retrieval quality, not improves it.
- Disabling metadata filtering removes a useful precision tool and worsens relevance.

</details>

---

**Q4.** A startup needs a fully managed, serverless vector database that auto-scales with usage and requires no infrastructure management. Which is the BEST fit?

A) Pinecone
B) FAISS
C) Chroma running locally
D) A self-hosted PostgreSQL with pgvector on an unmanaged VM

<details>
<summary>Answer</summary>

**Correct: A**

Pinecone is a fully managed, serverless vector database service — no infrastructure to provision or scale manually.

**Why the others are wrong:**
- FAISS is a library, not a managed service — requires you to host and scale it yourself.
- Chroma is lightweight and typically self-hosted/embedded, not a managed serverless offering.
- Self-hosted pgvector on an unmanaged VM requires manual scaling and ops, the opposite of the requirement.

</details>

---

**Q5.** A research team needs maximum control over indexing algorithms, wants to run entirely in-memory on their own GPUs, and does not need built-in metadata filtering or a hosted API. Which tool BEST fits?

A) Pinecone
B) A managed cloud vector search API with built-in dashboards
C) FAISS
D) Chroma with a REST server

<details>
<summary>Answer</summary>

**Correct: C**

FAISS is an open-source library for efficient similarity search that runs in-memory/on GPU and gives full control over index type, with no managed layer or built-in metadata filtering.

**Why the others are wrong:**
- Pinecone is managed and abstracts away index control, the opposite of maximum control.
- A managed API also abstracts index internals, not suited for teams wanting low-level control.
- Chroma emphasizes ease of use and metadata filtering, not raw low-level index control.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A developer wants to prototype a RAG chatbot locally in Python with minimal setup, embedding the vector store directly in their application without running a separate server. Which is the BEST choice?

A) Pinecone
B) Chroma (in-process/embedded mode)
C) A distributed Elasticsearch cluster
D) FAISS with a custom REST wrapper built from scratch

<details>
<summary>Answer</summary>

**Correct: B**

Chroma is designed for lightweight, embedded local use in Python with minimal setup, ideal for prototyping.

**Why the others are wrong:**
- Pinecone requires an account, API keys, and network calls, more setup than needed for local prototyping.
- An Elasticsearch cluster is heavy infrastructure, overkill for a quick local prototype.
- Building a custom REST wrapper around FAISS adds unnecessary engineering overhead for prototyping.

</details>

---

**Q7.** You are designing a chunking strategy for a knowledge base of long technical manuals with clear section headers. Which chunking configuration is the BEST practice?

A) One chunk per entire document, regardless of length
B) Fixed 50-token chunks with no overlap, ignoring document structure
C) Random chunk sizes generated per query at retrieval time
D) Chunks of roughly 300-512 tokens, split along semantic/section boundaries, with ~10-15% overlap between chunks

<details>
<summary>Answer</summary>

**Correct: D**

Moderate chunk sizes aligned to semantic boundaries preserve context and avoid splitting related information; overlap prevents losing context at chunk edges — standard RAG best practice.

**Why the others are wrong:**
- Whole-document chunks are too large, exceeding useful retrieval granularity and diluting relevance scores.
- Very small chunks with no overlap fragment sentences/ideas and lose surrounding context, hurting answer quality.
- Chunking must happen at indexing time, not randomly at query time — retrieval requires pre-built consistent chunks.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What does 'hybrid retrieval' mean in the context of RAG systems?

A) Combining sparse keyword-based search (e.g., BM25) with dense vector similarity search to improve retrieval accuracy
B) Retrieving from two different LLM providers simultaneously
C) Using two separate vector databases for redundancy
D) Fine-tuning the embedding model on both public and private data

<details>
<summary>Answer</summary>

**Correct: A**

Hybrid retrieval blends keyword-based (sparse) and embedding-based (dense) search, capturing exact term matches and semantic similarity together.

**Why the others are wrong:**
- This isn't about LLM providers at all; it's about retrieval methods.
- Using two vector databases for redundancy is a reliability pattern, not hybrid retrieval.
- Fine-tuning embeddings is a separate technique, unrelated to combining sparse and dense retrieval.

</details>

---

