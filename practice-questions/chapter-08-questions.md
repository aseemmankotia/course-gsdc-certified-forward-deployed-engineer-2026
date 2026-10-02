## Chapter 8: Agentic Systems and Tool Use — Practice Questions

**Q1.** A support team needs a system that takes a customer question, retrieves the answer from a static FAQ knowledge base, and returns it verbatim — the flow never varies. Which approach BEST meets this requirement?

A) A ReAct agent with access to 5 tools for search, summarization, and escalation
B) A simple retrieval chain: embed query → fetch top-k FAQ chunks → single LLM call to answer
C) A multi-agent system with a planner agent and a retriever agent
D) An agent with unlimited max_iterations to ensure it always finds an answer

<details>
<summary>Answer</summary>

**Correct: B**

The task is a fixed, deterministic sequence with no branching decisions — a simple chain is cheaper, faster, and more reliable than an agent.

**Why the others are wrong:**
- An agent adds unnecessary tool-selection risk and latency for a task with no conditional logic.
- Multi-agent coordination overhead is unjustified for a single deterministic lookup task.
- Unlimited iterations increases cost and infinite-loop risk with zero benefit for a fixed workflow.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An agent must check a user's order status via one API, and if the order is delayed, call a second API to issue a discount code, then draft an apology email — the next action depends on each previous API's result. Which architecture is BEST?

A) A single prompt that generates all three outputs in one LLM call
B) A hardcoded sequential chain that calls all three APIs unconditionally
C) An agent with a tool-calling loop that conditionally decides which tool to call based on intermediate observations
D) Three independent agents running in parallel with no shared state

<details>
<summary>Answer</summary>

**Correct: C**

Conditional branching based on the result of a prior tool call is exactly the scenario the plan-act-observe agent loop is designed for.

**Why the others are wrong:**
- An LLM cannot reliably execute live API calls and branch logic correctly in a single generation without a tool loop.
- A hardcoded chain would call the discount and email APIs even when the order isn't delayed — incorrect behavior.
- Parallel independent agents with no shared state cannot respect the required dependency between steps.

</details>

---

**Q3.** A personal assistant app must remember a user's dietary restrictions and stated preferences across sessions spanning several months, even after the app is fully closed and reopened. Where should this information be stored?

A) In the LLM's context window for the current session only
B) In a long-term memory store (e.g., vector DB or persistent key-value store) keyed to the user
C) In episodic memory logs of only the most recent conversation
D) Discarded after each session to avoid context window overflow

<details>
<summary>Answer</summary>

**Correct: B**

Persistence across sessions and months requires storage outside the ephemeral context window — this is precisely what long-term memory stores provide.

**Why the others are wrong:**
- Context windows are cleared/reset between sessions and cannot persist information for months.
- Episodic memory of only the most recent conversation would lose preferences stated in earlier sessions.
- Discarding the data directly contradicts the stated requirement to remember it long-term.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team is building a production RAG system that must ingest documents from 40 different data connectors (Notion, Slack, Google Drive, SQL databases) with minimal custom integration code. Which framework is the BEST starting point?

A) LangChain, using only its basic LLMChain abstraction
B) LlamaIndex, using its built-in data connectors and index abstractions
C) Custom orchestration built entirely from scratch with raw API calls
D) A single-agent ReAct loop with no retrieval framework

<details>
<summary>Answer</summary>

**Correct: B**

LlamaIndex specializes in data ingestion and indexing across a wide range of connector types, directly matching the stated requirement.

**Why the others are wrong:**
- LangChain can perform RAG but is not the connector-specialized tool and would require more custom integration for 40 sources.
- Reinventing 40 connectors from scratch wastes engineering effort when a purpose-built framework already solves this.
- An agent loop alone does not address the underlying data ingestion/indexing problem.

</details>

---

**Q5.** A startup needs an extremely low-latency tool-calling loop with only 2 tools, full control over retry logic, and no willingness to add heavy third-party dependencies to a small production service. What is the BEST approach?

A) Custom orchestration: call the model API directly with a tool schema and handle the loop manually
B) LangChain's full AgentExecutor with default configuration
C) LlamaIndex's query engine wrapped in an agent
D) A multi-agent framework with a supervisor agent coordinating sub-agents

<details>
<summary>Answer</summary>

**Correct: A**

For a 2-tool loop under tight latency and dependency constraints, hand-rolled orchestration avoids framework overhead and gives full control over retries.

**Why the others are wrong:**
- A full agent framework adds dependency weight and abstraction overhead unnecessary for a 2-tool loop.
- LlamaIndex is retrieval/indexing-focused and not the best fit for a generic low-latency tool loop.
- A multi-agent supervisor architecture adds unnecessary coordination complexity for a simple 2-tool task.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** When defining a function/tool schema for an LLM tool-calling API, which field has the GREATEST impact on whether the model selects the correct tool at the correct time?

A) The function's return type annotation
B) The function's description field
C) The length of the function's name
D) The order in which tools are listed in the request

<details>
<summary>Answer</summary>

**Correct: B**

The description is the primary natural-language signal the model uses to decide when and why to invoke a tool; vague descriptions cause wrong or missed calls.

**Why the others are wrong:**
- Return type only affects how output is parsed after the call, not tool selection.
- Name length has negligible effect on selection compared to description quality.
- Tool order can have minor influence in some implementations but is not the primary or reliable lever.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** An agent occasionally enters a loop where it keeps calling the same tool without making progress, consuming excessive cost and time. Which configuration change directly addresses this?

A) Increase the temperature to encourage more varied tool choices
B) Set a max_iterations (step limit) on the agent executor so it halts and returns after N steps
C) Remove all tools so the agent cannot call anything
D) Switch to a model with a larger context window

<details>
<summary>Answer</summary>

**Correct: B**

A hard step/iteration limit is the standard, direct guardrail against runaway tool-calling loops.

**Why the others are wrong:**
- Higher temperature increases randomness but does not guarantee loop termination and can worsen unpredictability.
- Removing all tools eliminates the agent's core functionality entirely, not just the faulty loop.
- Context window size is unrelated to whether an agent decides to stop calling a tool.

</details>

---

**Q8.** Which statement BEST distinguishes episodic memory from long-term semantic memory in an agentic system?

A) Episodic memory stores general facts about the world; semantic memory stores specific past conversation traces
B) Episodic memory stores specific past experiences/interactions the agent can recall and learn from; semantic/long-term memory stores generalized, durable facts (e.g., user preferences) independent of when they were learned
C) They are functionally identical and the terms are interchangeable in every framework
D) Episodic memory only exists within a single context window and can never be persisted

<details>
<summary>Answer</summary>

**Correct: B**

This is the standard distinction: episodic memory captures specific event/interaction traces, while semantic/long-term memory holds generalized, durable knowledge.

**Why the others are wrong:**
- This reverses the actual definitions of the two memory types.
- The two types serve different purposes and are treated distinctly even when backed by similar storage.
- Episodic memory can be persisted (e.g., logged interaction history) well beyond a single context window.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

