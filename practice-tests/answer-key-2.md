# Answer Key — Practice Test 2

**Q1. Correct: B**

FDE methodology requires first decomposing an ambiguous business complaint into MECE root-cause categories with stakeholder alignment before any technical solution is scoped — this prevents solving the wrong problem.

---

**Q2. Correct: B**

The defining line is ownership and iteration mode: Solutions Architects typically design and hand off a reference architecture, while FDEs embed on-site, adapt the solution against live production realities, and remain accountable for the delivered outcome.

---

**Q3. Correct: D**

Constraint and feasibility analysis requires surfacing hard technical limitations immediately and renegotiating the definition of the business requirement with the client before any architecture decision is made.

---

**Q4. Correct: A**

A MECE-structured requirements matrix lets the FDE bucket contradictory stakeholder input into non-overlapping categories and rank by impact/frequency, which is the standard technique for separating true signal from noise in client requirements.

---

**Q5. Correct: A**

The input-processing-output model requires validating what data inputs actually exist and precisely defining the target output metric before any processing approach (model, rule, or dashboard) is chosen.

---

**Q6. Correct: D**

FastAPI automatically runs synchronous `def` route handlers in a separate thread pool executor, so a blocking call no longer stalls the single-threaded async event loop that all `async def` routes share within one worker.

---

**Q7. Correct: A**

`poetry install` reads `poetry.lock` and installs the exact pinned versions of every dependency, overwriting the manually upgraded package and restoring reproducibility.

---

**Q8. Correct: B**

JWTs are self-contained and cryptographically signed, so any service holding the verification key can validate the token and read embedded role claims locally, with expiration enforcing short lifetimes and no shared state required.

---

**Q9. Correct: A**

Pydantic's numeric constraint parameters are `ge` (greater than or equal) and `le` (less than or equal), which correctly allow the inclusive range 0 through 120.

---

**Q10. Correct: D**

WARNING indicates an unexpected but non-fatal condition worth noting for later investigation, without demanding immediate operator intervention, which matches an automatically-retried transient failure.

---

**Q11. Correct: C**

Publishing to a message queue decouples the two services: Service A completes quickly after enqueueing the event, and Service B processes it independently whenever ready, satisfying the non-blocking requirement.

---

**Q12. Correct: C**

Wrapping the yield in try/finally ensures FastAPI's dependency teardown code (the code after yield) always runs, including when the route handler raises an exception, because Python guarantees the finally block executes during exception propagation through the generator.

---

**Q13. Correct: B**

Publish/subscribe over a message broker decouples the producer from consumers entirely: Service A publishes once and has no knowledge of who consumes the event, a down subscriber (C) simply processes the backlog when it recovers instead of blocking A, and new consumers can subscribe to the same topic without any change to Service A.

---

**Q14. Correct: A**

A streaming pipeline processes events as they arrive and can score fraud within milliseconds, meeting the 200ms latency requirement with continuously updated features.

---

**Q15. Correct: C**

Vector databases index embeddings using ANN algorithms (e.g., HNSW), enabling fast semantic similarity search at millions-of-vectors scale, which is exactly what RAG retrieval requires.

---

**Q16. Correct: D**

Stratified k-fold ensures every fold maintains the same 2% positive-class ratio as the full dataset, preventing folds that contain zero or very few positive examples and producing more reliable evaluation metrics.

---

**Q17. Correct: A**

Self-attention computes weighted relationships between every pair of tokens simultaneously, enabling parallel computation (unlike RNNs' step-by-step processing) and directly modeling long-range dependencies without vanishing-gradient issues.

---

**Q18. Correct: D**

True reproducibility requires capturing the exact code version, dataset snapshot, hyperparameters, and environment/library versions — this is precisely what experiment tracking tools like MLflow or Weights & Biases are designed to log automatically.

---

**Q19. Correct: A**

When categories are few, fixed, and mapped by clear deterministic keyword rules that rarely change, a rule-based system is the simplest, cheapest, most maintainable, and fully explainable solution — exactly the scenario where the exam expects you to avoid over-engineering with ML/LLM.

---

**Q20. Correct: C**

Real-time fraud scoring requires a streaming architecture so features and predictions are computed with minimal latency, and an online feature store keeps training/serving features consistent. Automated drift and data-quality monitoring is the observability layer the exam expects for production pipelines that must catch distribution shift without human intervention.

---

**Q21. Correct: B**

With abundant structured numeric data and millions of labeled examples, a gradient-boosted tree ensemble captures complex nonlinear feature interactions far better than static rules, runs inference in well under 5ms, and SHAP provides per-prediction feature attribution that satisfies regulator interpretability requirements — the exact ML-vs-rule-based-vs-LLM tradeoff the exam tests.

---

**Q22. Correct: D**

Sparse or local (windowed) attention restricts each token's attention computation to a fixed-size neighborhood instead of the full sequence, reducing complexity from roughly O(n^2) to O(n*w), where w is the window size — this is the standard conceptual technique referenced for scaling transformers to long sequences.

---

**Q23. Correct: A**

Self-consistency exactly matches the pattern of sampling N reasoning paths and aggregating via majority vote, and 5 samples fits neatly within a 5x cost budget while directly reducing variance-driven errors.

---

**Q24. Correct: C**

This is the well-documented 'lost in the middle' effect: recall degrades for facts placed in the middle of long contexts regardless of their relevance ranking, exactly matching the symptom of a confirmed-relevant chunk at position 5-6 being missed.

---

**Q25. Correct: B**

Hybrid retrieval combines BM25's strength at exact token/citation matching with dense embeddings' strength at semantic similarity, fused via a method like reciprocal rank fusion — the standard fix for this exact class of problem.

---

**Q26. Correct: D**

The correct pattern is retrieve-broad-then-rerank-narrow: a bi-encoder/vector search maximizes recall over the full corpus, then a cross-encoder scores each query-chunk pair for precision, and only the top-N re-ranked chunks are forwarded to the LLM.

---

**Q27. Correct: C**

Length bias in LLM-as-judge setups is a known failure mode; the standard mitigation is rubric engineering that explicitly decouples the scored dimension (helpfulness) from length, reinforced with contrastive calibration examples.

---

**Q28. Correct: B**

ReAct follows a reason-act-observe loop where the model takes actions (typically tool/environment calls) and incorporates observations into further reasoning; Reflection is a self-critique loop where the model evaluates and revises its own prior output, generally without needing external tools.

---

**Q29. Correct: B**

Exact-match identifiers like SKUs and part codes are poorly captured by dense embeddings, which encode semantic meaning rather than lexical form. BM25 excels at exact keyword/token matching, so combining it with dense retrieval in a hybrid pipeline (followed by re-ranking) recovers the lexically-matched but semantically-diluted results dense search alone misses.

---

**Q30. Correct: D**

Boundary splitting occurs because a clause's beginning and end land in different chunks with zero shared content. Adding overlap ensures boundary text appears in both adjacent chunks, and attaching section-header metadata gives the retriever and generator structural context to reassemble split clauses correctly.

---

**Q31. Correct: A**

Self-consistency samples multiple independent reasoning traces (typically via higher-temperature decoding) for the same prompt and selects the final answer via majority vote, improving accuracy on reasoning tasks without any tool use or iterative self-critique.

---

**Q32. Correct: C**

The workflow is fully deterministic with no dynamic decision-making or tool selection required at runtime. A scripted pipeline with a single LLM extraction step is faster, cheaper, more reliable, and easier to debug than an autonomous agent loop — this is a core FDE judgment call: agents add value only when the path isn't known in advance.

---

**Q33. Correct: C**

Unbounded agent-to-agent loops are a known reliability failure mode in multi-agent systems. The standard guardrail is a hard iteration cap with a supervising controller that halts execution and escalates rather than letting the loop run indefinitely — this preserves the collaborative design while bounding cost and risk.

---

**Q34. Correct: C**

Recalling specific past interactions across sessions requires persistent, retrievable episodic memory — storing past interactions with metadata (customer ID, timestamp) in a vector store and retrieving them via semantic search is the standard pattern for this requirement.

---

**Q35. Correct: B**

Multi-stage builds are the standard pattern for keeping production images minimal: compilers and build tools stay in the discarded builder stage, and only the resulting artifacts (e.g., a populated virtualenv or wheel files) are copied into the slim runtime image, reducing both size and attack surface.

---

**Q36. Correct: B**

Semantic caching compares embedding similarity rather than exact strings, so paraphrased or reworded questions with the same intent still hit the cache — directly solving the near-duplicate problem described, while a similarity threshold protects against serving irrelevant cached answers.

---

**Q37. Correct: A**

Streamlit's native multipage app support (`pages/` directory) combined with sidebar navigation is purpose-built for distinct, navigable views, and `st.write_stream` handles token-by-token streaming cleanly — matching all three stated requirements in one framework.

---

**Q38. Correct: B**

This is a deterministic, single-step retrieve-then-generate task with no branching decisions, no tool selection ambiguity, and no cross-turn state. Agentic loops add latency, cost, and non-determinism without any corresponding benefit here—this is the textbook 'when NOT to use agents' case from the syllabus.

---

**Q39. Correct: D**

The root cause is redundant identical/near-identical LLM calls, not raw compute capacity or per-call cost. A normalized-key cache with TTL directly eliminates duplicate LLM invocations for the same questions, cutting both cost and latency while leaving distinct queries unaffected—this is the core performance-optimization pattern (caching) taught for exactly this scenario.

---

**Q40. Correct: C**

FDE demo craft under uncertainty requires a rehearsed failover plan: briefly acknowledge the glitch to maintain credibility, then pivot to a pre-validated backup asset so the narrative momentum and executive attention are preserved without dwelling on the failure.

---

**Q41. Correct: A**

The economic buyer holds final budget authority and must be identified and engaged early in stakeholder mapping; failing to surface this person — even when a champion is enthusiastic — is a classic discovery gap that stalls deals late in the cycle.

---

**Q42. Correct: D**

The PoC-to-MVP transition depends on a defensible business case; if results are presented as pure technical proof without tying outcomes back to the ROI metrics agreed during scoping, budget holders have no basis to approve continued investment.

---

**Q43. Correct: C**

Anchoring success metrics to a documented baseline cost/time and a projected dollar-value reduction gives the business sponsor a direct ROI calculation, which is the currency executives use to approve continued investment.

---

**Q44. Correct: A**

The Insight stage exists to surface a surprising, client-specific finding that reframes the stated problem as more urgent or differently-shaped than the client assumed, which is what makes the subsequent Solution feel earned and necessary rather than generic.

---

**Q45. Correct: D**

Crisis management protocol prioritizes rapid, transparent communication and visible mitigation ahead of full diagnosis — this preserves trust during a high-stakes incident (billing impact) and demonstrates the trusted-advisor posture the client expects from an FDE.

---

