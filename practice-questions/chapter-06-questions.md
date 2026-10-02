## Chapter 6: Prompt Engineering and LLM Workflow Design — Practice Questions

**Q1.** A company builds a customer support bot needing multi-step arithmetic reasoning for billing dispute calculations. Which prompting technique should be applied to maximize accuracy?

A) Zero-shot prompting with a clear system role
B) Few-shot prompting with 20 examples of billing scenarios
C) Increasing temperature to 1.5 for creative reasoning
D) Chain-of-thought prompting instructing step-by-step reasoning

<details>
<summary>Answer</summary>

**Correct: D**

CoT improves multi-step arithmetic/logic reasoning accuracy by making the model externalize intermediate steps before the final answer.

**Why the others are wrong:**
- Zero-shot without explicit reasoning steps performs poorly on multi-step math tasks.
- Few-shot with many examples increases token cost without teaching the model how to reason through arithmetic steps.
- Higher temperature increases randomness, which hurts deterministic calculation accuracy.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team must produce highly reproducible outputs for automated regression testing of LLM-generated reports, calling the same prompt repeatedly. Which combination of API settings BEST minimizes output variance?

A) temperature=1.0, top_p=1.0, no seed
B) temperature=0, top_p=1.0, fixed seed parameter (if supported)
C) temperature=0.7, frequency_penalty=1.0
D) temperature=0, but vary the system prompt each run for diversity

<details>
<summary>Answer</summary>

**Correct: B**

temperature=0 minimizes sampling randomness, and a fixed seed (where supported) further reduces run-to-run variance, though full determinism is still not guaranteed.

**Why the others are wrong:**
- Default sampling settings (temp=1, no seed) maximize randomness — the worst option for reproducibility.
- Moderate temperature with a frequency penalty still introduces meaningful output variability.
- Intentionally varying the system prompt each run directly contradicts the goal of reproducibility.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A production RAG pipeline must route simple FAQ queries to a smaller, cheaper model while sending complex multi-turn technical queries to a larger model, with automatic retry to a secondary provider if the primary model times out. Which architecture pattern BEST describes this design?

A) A router/classifier stage combined with model tiering and a fallback mechanism
B) A single monolithic prompt with dynamic few-shot examples
C) Prompt chaining only, with no model switching
D) Self-consistency sampling with majority voting across all queries

<details>
<summary>Answer</summary>

**Correct: A**

This matches routing (classify query complexity), model tiering (send to appropriate model by cost/capability), and fallback (secondary provider on timeout) — a standard production LLM workflow pattern.

**Why the others are wrong:**
- A monolithic prompt doesn't address cost-based model selection or failure handling.
- Chaining alone describes sequential steps within one pipeline, not conditional model selection or failure recovery.
- Self-consistency addresses accuracy via multiple samples from the SAME model, not cost-based routing or provider fallback.

</details>

---

**Q4.** A developer needs an LLM response that MUST reliably parse into a predefined schema (specific fields, types) for downstream application code, with zero tolerance for malformed output being silently accepted. Which approach BEST meets this requirement?

A) Function/tool calling with a defined JSON schema, plus server-side schema validation of the response
B) Plain text prompting requesting "please respond in JSON format"
C) JSON mode / response_format alone with no further validation
D) Increasing temperature to encourage more creative formatting compliance

<details>
<summary>Answer</summary>

**Correct: A**

Function/tool calling constrains output to a defined schema at generation time, and adding server-side validation catches any edge-case schema violations — the most reliable combination.

**Why the others are wrong:**
- Plain text instructions have no structural guarantee; models frequently deviate from requested format.
- JSON mode guarantees syntactically valid JSON but not adherence to your specific field schema — a common exam trap.
- Higher temperature increases randomness, working against reliable, consistent structured output.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A team is evaluating thousands of LLM-generated summaries daily and needs a scalable, low-cost evaluation method to catch major quality regressions, accepting some risk of evaluator bias. Which evaluation approach BEST fits this requirement?

A) LLM-as-judge scoring against a rubric, with periodic human spot-checks
B) Full human review of every summary
C) No evaluation, rely on user complaints only
D) A/B testing in production with no scoring mechanism

<details>
<summary>Answer</summary>

**Correct: A**

LLM-as-judge scales to high volume at low cost, and periodic human spot-checks mitigate the judge-bias risk noted in the scenario.

**Why the others are wrong:**
- Full human review does not scale cost-effectively to thousands of items per day.
- Reactive-only monitoring via complaints misses regressions until users are already affected.
- A/B testing without any scoring mechanism provides no quality signal to detect regressions.

</details>

---

**Q6.** Which parameter setting is generally recommended when using an LLM to extract structured data fields from documents, where consistency and accuracy matter more than creative variation?

A) temperature=1.5, top_p=0.5
B) temperature=0 to 0.2, top_p near 1.0
C) temperature=2.0, frequency_penalty=0
D) temperature=0.9, presence_penalty=2.0

<details>
<summary>Answer</summary>

**Correct: B**

Low temperature (0–0.2) reduces sampling randomness and increases determinism/consistency, which is ideal for extraction tasks.

**Why the others are wrong:**
- High temperature combined with low top_p still introduces meaningful variability, hurting extraction consistency.
- Maximum temperature maximizes randomness — the worst setting for structured, consistent extraction.
- High temperature with a heavy presence penalty pushes toward novel phrasing, not deterministic field extraction.

</details>

---

**Q7.** When enabling JSON mode via an API's response_format parameter, which additional step is REQUIRED for the request to succeed on most providers?

A) Setting temperature to exactly 0
B) Disabling streaming entirely
C) Providing at least 5 few-shot examples
D) Including the word "JSON" somewhere in the prompt/system message

<details>
<summary>Answer</summary>

**Correct: D**

Most providers require the prompt to explicitly mention "JSON" or the request errors out, since JSON mode only enforces output syntax, not the user's intent.

**Why the others are wrong:**
- Temperature is unrelated to JSON mode's syntactic requirement and can be set to any value.
- Streaming can typically be used alongside JSON mode on most providers.
- Few-shot examples are optional and are not a technical requirement for JSON mode to function.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the KEY difference between the ReAct pattern and simple Chain-of-Thought (CoT) prompting?

A) ReAct requires fine-tuning while CoT does not
B) CoT is only usable with GPT models, while ReAct works with any model
C) ReAct interleaves reasoning steps with external tool/action calls and observations, while CoT only produces internal reasoning text
D) ReAct eliminates the need for prompting entirely

<details>
<summary>Answer</summary>

**Correct: C**

ReAct explicitly loops Thought → Action → Observation, invoking external tools/APIs between reasoning steps, whereas CoT is purely textual step-by-step reasoning with no tool interaction.

**Why the others are wrong:**
- Neither technique inherently requires fine-tuning; both are prompting strategies applied at inference time.
- Both CoT and ReAct are model-agnostic prompting patterns, not tied to a specific vendor.
- ReAct still requires carefully engineered prompts to structure the thought/action/observation loop.

</details>

---

