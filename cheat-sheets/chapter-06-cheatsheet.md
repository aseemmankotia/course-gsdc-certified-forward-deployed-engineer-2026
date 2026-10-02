# Chapter 6 Cheat Sheet: Prompt Engineering & LLM Workflow Design

## Prompting Pattern Selection
| Pattern | Best For | Avoid When | Cost/Latency Impact |
|---|---|---|---|
| Zero-shot | Simple, well-known tasks | Novel/ambiguous formats | Lowest |
| Few-shot | Enforcing specific output format/style | Task already well-understood by model | Moderate (extra tokens) |
| Chain-of-Thought (CoT) | Multi-step math/logic/reasoning | Simple lookup/classification | Higher (more output tokens) |
| Self-consistency | High-stakes reasoning accuracy | Cost-sensitive, high-volume tasks | Highest (N× calls) |
| ReAct | Agentic tasks needing tool calls | Pure text generation, no tools needed | Higher (multi-turn loop) |
| Reflection | Self-correction / quality improvement | Latency-critical single-pass tasks | Extra call per revision |

## Managing Non-Determinism
- `temperature=0` → near-deterministic, NOT guaranteed 100% reproducible.
- Fixed `seed` param (if supported) → improves run-to-run reproducibility, still not absolute.
- `top_p` (nucleus sampling) 0–1: lower = more focused, higher = more diverse.
- Extraction/structured tasks → temperature 0–0.2, top_p near 1.0.
- Creative tasks → higher temperature (0.7–1.2).

## Structured Output
- **JSON mode / response_format**: guarantees valid JSON syntax ONLY — not schema conformance. Most providers require the word "JSON" in the prompt or the call errors.
- **Function/tool calling**: enforces a defined schema at generation time — pair with server-side validation for zero-tolerance pipelines.
- Always validate structured output downstream; never trust format compliance blindly.

## Workflow Integration Patterns
| Pattern | Purpose |
|---|---|
| Chaining | Sequential steps; output of step N feeds step N+1 |
| Routing | Classifier decides which model/chain handles a request (cost optimization) |
| Fallback | Secondary model/provider triggered on timeout, error, or invalid output |
| Retry + backoff | Combine with fallback for resilience against transient failures |

## Evaluation Methods
| Method | Scale | Cost | Reliability | Use Case |
|---|---|---|---|---|
| Rubric-based scoring | Medium | Low | Consistent but rigid | Well-defined tasks |
| LLM-as-judge | High | Low | Biased (position/verbosity/self-preference) | High-volume screening |
| Human-in-the-loop | Low | High | Highest | High-stakes decisions |

**Bias mitigation for LLM-as-judge**: randomize answer order, use multiple judge models, cross-check with periodic human spot-checks.

## Cost & Latency Optimization
- **Prompt caching**: place static content (system prompt, few-shot examples) FIRST to maximize cache hits, reducing repeated-token cost/latency.
- **Routing to smaller models**: send simple/FAQ queries to cheaper models, reserve large models for complex queries.
- **Reduce output tokens**: shorter CoT / concise instructions cut generation cost — but don't strip CoT from tasks that need it.
- **Self-consistency & multi-agent patterns**: multiply cost linearly with sample count — use selectively, not by default.

## Exam Traps
- Confusing JSON mode with guaranteed schema compliance.
- Assuming temperature=0 means fully deterministic output.
- Applying CoT to tasks where it adds no accuracy (simple extraction/classification).
- Treating LLM-as-judge as unbiased ground truth without mitigation.
