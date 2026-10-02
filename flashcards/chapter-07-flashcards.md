## Chapter 7: RAG Systems End to End — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | RAG vs fine-tuning: when should you choose RAG? | When knowledge changes frequently, needs source attribution, or is too large to bake into weights. Exam tip: fast-changing/factual data → RAG; style/format/behavior changes → fine-tuning. |
| 2 | What is the 'lost-in-the-middle' problem? | LLMs pay less attention to information placed in the middle of a long context vs the start/end. Exam tip: re-rank so top chunks sit near the start of the prompt. |
| 3 | FAISS vs Pinecone vs Chroma — core distinction? | FAISS = open-source library, self-hosted, max control, no built-in metadata filtering. Pinecone = fully managed, serverless, auto-scaling. Chroma = lightweight, embedded, best for local prototyping. |
| 4 | Standard chunk size range for RAG text chunking? | ~300-512 tokens is a common sweet spot, with ~10-15% overlap between chunks. Exam tip: too small fragments context, too large dilutes relevance. |
| 5 | What metadata fields should a RAG chunk typically include? | source/doc_id, section/title, timestamp, page number. Exam tip: metadata enables filtering (e.g., only search docs updated in last 30 days) and improves precision. |
| 6 | What is query rewriting in RAG? | Using an LLM to expand/clarify a vague user query before retrieval (adding synonyms, context, intent). Exam tip: fixes low-recall retrieval from short/ambiguous queries. |
| 7 | What is re-ranking in a RAG pipeline? | A second-stage model (often a cross-encoder) re-scores initially retrieved chunks for relevance before sending to the LLM. Exam tip: improves precision when initial vector search returns noisy top-k results. |
| 8 | What is hybrid retrieval? | Combining sparse keyword search (BM25) with dense vector similarity search. Exam tip: captures exact-term matches (e.g., product codes) that pure embeddings can miss. |
| 9 | Name the four core RAGAS evaluation metrics. | Faithfulness, Answer Relevancy, Context Precision, Context Recall. Exam tip: faithfulness = no hallucination vs retrieved context; context recall = did retrieval find all needed info. |
| 10 | Common RAG failure mode: retrieval returns correct docs but answer still wrong. Root cause? | Often 'lost-in-the-middle' attention bias or poor prompt instructions telling the LLM to use context. Exam tip: distinguish retrieval failure vs generation failure before choosing a fix. |
| 11 | The chunk-embed-retrieve-generate flow — order of steps? | 1) Chunk documents, 2) Embed chunks into vectors, 3) Retrieve top-k similar chunks for a query, 4) Generate answer using retrieved chunks as context. Exam tip: failures can occur at any stage — diagnose which stage before fixing. |
| 12 | When does fine-tuning beat RAG? | When you need to change model behavior/style/format/tone, teach a new task format, or reduce prompt length for a fixed, stable domain. Exam tip: fine-tuning doesn't reliably add new factual knowledge — RAG does that better. |
