# Answer Key — Practice Test 1

**Q1. Correct: D**

The FDE mindset requires structuring an ambiguous problem before reaching for technology. When three teams describe the same problem differently, the correct first move is problem decomposition and reconciling conflicting inputs (a MECE-style breakdown) to find the real, well-defined problem before any modeling or tooling decision is made.

---

**Q2. Correct: D**

The CFDE framing positions the FDE as a hybrid engineer-consultant embedded with the client, doing both business-to-technical translation and hands-on implementation/iteration, unlike a Solutions Architect who typically focuses on high-level architecture and design and hands off build work to other teams.

---

**Q3. Correct: A**

First-principles thinking means breaking a problem down to its fundamental, client-specific components rather than relying on analogy, precedent, or industry generalization. Identifying the actual drivers of churn for this specific client before choosing a technical approach is the correct application of the technique.

---

**Q4. Correct: D**

Signal, in the FDE context, refers to information that is directly actionable for defining and solving the problem: measurable goals, real constraints (data, budget, timeline, compliance), and success criteria. These are what feed into problem structuring and feasibility analysis.

---

**Q5. Correct: A**

The input-processing-output model requires that once inputs and outputs are fixed, the FDE must explicitly define the processing (transformation) step — what logic converts inputs to outputs — before any tool or vendor selection. This keeps the problem structured independent of implementation choice.

---

**Q6. Correct: B**

A generator-based dependency with `yield`, injected via `Depends()`, gives FastAPI clean setup/teardown semantics — code before `yield` runs on request start, code after runs after the response — and FastAPI's dependency_overrides mechanism lets tests substitute a fake session without touching route code.

---

**Q7. Correct: A**

A circuit breaker with an enforced timeout fails fast when Service B is unhealthy, prevents Service A's threads from blocking indefinitely, and lets the system degrade gracefully with a fallback response instead of cascading into total unavailability.

---

**Q8. Correct: C**

Poetry performs full dependency resolution, writes a `poetry.lock` file that pins exact versions of every transitive dependency for reproducibility, and ships `poetry build`/`poetry publish` for packaging — matching all stated requirements in one tool.

---

**Q9. Correct: B**

FastAPI's default exception handler for `RequestValidationError` (raised when Pydantic validation fails on a request body, query params, or path params) returns HTTP 422 Unprocessable Entity along with a JSON body detailing which fields failed and why.

---

**Q10. Correct: D**

By REST convention, PUT replaces the full resource representation and is idempotent (repeating the same PUT produces the same end state), while PATCH sends only the fields to change and is not required to be idempotent.

---

**Q11. Correct: D**

An API key passed in a header (e.g., `X-API-Key`) and checked against a stored allowlist is the simplest fit for stateless, non-interactive service-to-service calls with manually rotated static credentials — no user identity, sessions, or token refresh logic needed.

---

**Q12. Correct: B**

201 Created is the correct REST status code when a POST request successfully creates a new resource, and the response body typically includes the newly created resource's representation.

---

**Q13. Correct: B**

Poetry's caret (^) operator allows updates that do not modify the leftmost non-zero digit of the version. For 2.31.0, that means any 2.x.x release >=2.31.0 is allowed, but 3.0.0 (a breaking major version bump under semantic versioning) is excluded.

---

**Q14. Correct: A**

Modern cloud warehouses with elastic, cheap compute favor ELT: load raw data first, then transform in-place with SQL. This preserves the raw source for reprocessing and offloads transformation to scalable warehouse compute — the exact scenario described.

---

**Q15. Correct: C**

A sub-second latency requirement (200ms) can only be met by a true streaming architecture with an event broker and real-time stream processors that act on each event as it arrives.

---

**Q16. Correct: A**

Vector databases are purpose-built for high-dimensional similarity search using ANN indexing (e.g., HNSW), enabling fast top-k semantic retrieval at tens of millions of vectors — exactly what RAG retrieval requires.

---

**Q17. Correct: C**

Minimizing undetected defects means minimizing false negatives, which is directly measured by recall on the positive (defective) class. Prioritizing recall is the correct optimization target here, even at the cost of more false positives.

---

**Q18. Correct: C**

Stratified k-fold preserves the original class ratio in every fold, which is critical when data is imbalanced. k=5 or k=10 is standard practice, balancing bias and variance in the performance estimate while keeping computation reasonable.

---

**Q19. Correct: B**

Self-attention computes a weighted combination of all tokens in a sequence for each token's representation, letting the model capture context and long-range dependencies regardless of token distance — this is the core innovation of transformers.

---

**Q20. Correct: B**

Semantic similarity search requires comparing vector embeddings of meaning, not exact text or keys. Vector databases with ANN indexes (e.g., HNSW) are purpose-built for this at scale and are the standard RAG retrieval pattern covered in the syllabus.

---

**Q21. Correct: C**

On highly imbalanced classification problems, accuracy is misleading because predicting the majority class alone yields high accuracy. Recall measures the proportion of actual fraud cases correctly identified, directly exposing the model's failure to catch fraud.

---

**Q22. Correct: C**

Self-attention computes weighted relationships between all token pairs in a sequence, letting each token's representation incorporate context from every other token — this is the core innovation that replaced recurrence in transformers and enables long-range dependency modeling.

---

**Q23. Correct: B**

Fixed-size chunking with no overlap frequently splits a clause across two chunks or mixes unrelated clauses together, destroying the semantic unit an embedding needs to represent accurately. Structure-aware chunking (splitting on clause/section boundaries) plus overlap keeps each clause coherent, so its embedding is a faithful representation and retrieval precision improves.

---

**Q24. Correct: C**

Pinecone is a fully managed, cloud-hosted vector database offering automatic horizontal scaling, native metadata filtering, and multi-region replication without the team managing servers -- exactly matching the stated production requirements.

---

**Q25. Correct: C**

JSON mode guarantees syntactically valid JSON but does not guarantee the object matches your specific schema (correct keys, types, required fields) or that it will never fail under edge cases like truncation. Production pipelines must still validate the parsed object and have a retry/fallback path.

---

**Q26. Correct: D**

Few-shot prompting supplies several demonstration examples of input-output pairs so the model infers the task pattern. Chain-of-thought prompting instructs (or demonstrates) that the model should reason step by step before producing a final answer -- the two techniques are orthogonal and are often combined (few-shot CoT).

---

**Q27. Correct: A**

This is a classic 'hallucination despite retrieval' failure caused by the LLM defaulting to parametric knowledge rather than admitting the context is insufficient. Explicitly instructing abstention behavior and adding a groundedness check before generation are the standard mitigations that directly target this behavior.

---

**Q28. Correct: A**

ReAct explicitly interleaves reasoning traces ('thoughts') with tool-invoking actions and observes results before deciding the next step, exactly matching the described loop of reason-act-observe-repeat until enough information is gathered.

---

**Q29. Correct: A**

Naive fixed-size token chunking ignores document structure, so code blocks and logical units get split arbitrarily. Structure-aware (semantic/structural) chunking respects natural boundaries like code fences, function definitions, and headers, and a small overlap prevents context loss at edges — directly fixing the broken-fragment problem.

---

**Q30. Correct: C**

Dense embeddings capture semantic similarity but often fail on exact-match tokens like IDs, SKUs, or codes, since these carry little semantic meaning. Sparse keyword methods like BM25 excel at exact term matching. Hybrid retrieval merges both signals, catching cases pure dense search misses.

---

**Q31. Correct: C**

A key documented risk of LLM-as-judge is correlated bias: if the judge model has similar training data, reasoning patterns, or weaknesses as the generator model, it may fail to catch the same errors a human would flag, inflating perceived quality. This is why human-in-the-loop spot-checks are still recommended alongside LLM-as-judge.

---

**Q32. Correct: A**

When steps are fixed, well-defined, and require low-latency deterministic behavior, a straightforward pipeline of function calls is faster, cheaper, and more predictable than an agent loop — this is the core 'when NOT to use agents' judgment call the exam tests.

---

**Q33. Correct: D**

Unbounded agent-to-agent loops are a classic multi-agent reliability failure; the standard guardrail is a hard iteration/turn cap plus a supervisor or convergence check that forces termination.

---

**Q34. Correct: D**

Streamlit is designed for multi-page apps with session state and custom layouts, making it the better fit for a full dashboard, while Gradio specializes in fast, simple input/output demos for ML models — its standard use case.

---

**Q35. Correct: B**

Copying requirements.txt and installing dependencies before copying application code lets Docker cache the dependency layer, so it's skipped on rebuilds unless requirements.txt changes — code changes alone don't trigger a full reinstall.

---

**Q36. Correct: A**

Once a secret is exposed in a public repo it must be treated as compromised immediately: revoke/rotate it, migrate to environment variables or a dedicated secrets manager, and remove it from git history since it remains in prior commits even after later edits.

---

**Q37. Correct: C**

Short-term memory holds context within the current conversation or task session (e.g., the active message history) and is cleared once the session ends, distinguishing it from persistent storage types.

---

**Q38. Correct: A**

Injecting secrets at runtime from a dedicated secrets manager keeps credentials out of the image layers and out of version control entirely, satisfying the 'never in image or Git history' requirement and aligning with standard MLOps secrets-management practice.

---

**Q39. Correct: D**

When the workflow is fixed, deterministic, and doesn't require dynamic multi-step planning or tool selection, a single structured extraction call plus a deterministic pipeline is simpler, cheaper, faster, and more reliable than an agentic loop — this is the classic 'when NOT to use agents' judgment call.

---

**Q40. Correct: D**

Transparency paired with a concrete mitigation plan preserves trust while still respecting the executive's time investment — this is the core of crisis management protocol for FDEs.

---

**Q41. Correct: B**

Post-demo follow-up protocol requires honest acknowledgment of unknowns plus a committed, tracked action item — this builds credibility rather than eroding it.

---

**Q42. Correct: B**

A power-interest grid is purpose-built for stakeholder mapping, classifying people by influence and interest to prioritize engagement effort — exactly what's needed to plan workshop invitees.

---

**Q43. Correct: B**

The arc establishes the pain point first, builds a data-backed insight that reframes it, then reveals the solution as the natural answer, closing with quantified impact — this order maximizes narrative tension and executive buy-in.

---

**Q44. Correct: A**

Trusted-advisor status is earned through consistently prioritizing the client's business outcomes over vendor self-interest, including recommending against your own solution when appropriate.

---

**Q45. Correct: D**

CFOs evaluate risk-adjusted financial rigor — payback period, sensitivity analysis, and phased de-risked investment directly address financial governance concerns and build credible approval justification.

---

