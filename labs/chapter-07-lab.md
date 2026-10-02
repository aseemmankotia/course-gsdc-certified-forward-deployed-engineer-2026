# Chapter 7 Lab: RAG Systems End to End

**Estimated time:** 30 minutes

## Exercise

Build a minimal RAG pipeline with FAISS or Chroma: chunk a document set, embed it, retrieve the top-k chunks, and generate an answer — then diagnose a hallucination failure and apply re-ranking as a mitigation

## Key takeaway

Most RAG problems in production are retrieval problems, not generation problems — diagnose chunking and retrieval before touching the model.
