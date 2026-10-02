## Chapter 8 Cheat Sheet: Agentic Systems and Tool Use

### Agent vs Chain — The #1 Exam Judgment Call
| Signal in the question | Use |
|---|---|
| Fixed, known sequence of steps | Simple chain |
| Next step depends on unpredictable prior output | Agent (loop) |
| Single deterministic lookup/transform | Simple chain |
| Need to choose among multiple tools dynamically | Agent |
| "Always do X then Y then Z" | Chain |
| "Decide what to do based on the result" | Agent |
Rule: agents cost more (tokens, latency, failure surface). Never pick an agent when a chain fully satisfies the requirement — this is the most commonly missed wrong answer type.

### Tool/Function Calling Pattern
1. Define schema: `name`, `description`, `parameters` (JSON Schema).
2. Model returns a tool call request (not the tool's output).
3. Your code executes the tool and returns the result as an observation.
4. Model incorporates the observation into the next step or final answer.
`description` quality drives correct tool selection more than any other field.
`tool_choice`: `auto` | `none` | `required` | forced specific tool.

### Multi-Step Planning Loop (ReAct)
Thought → Action (tool call) → Observation → repeat → Final Answer.
Guardrail: set a hard `max_iterations` / step limit (LangChain default = 15) to prevent runaway loops and runaway cost.

### Framework Landscape
| Framework | Best for | Weak point |
|---|---|---|
| LangChain | General agent orchestration, multi-tool workflows | Heavier abstraction for simple tasks |
| LlamaIndex | Data ingestion/indexing across many connectors, RAG | Less agent-orchestration-focused |
| Custom orchestration | Low latency, few tools, full control, minimal deps | More code to write/maintain |

### Memory Types
| Type | Scope | Example |
|---|---|---|
| Short-term | Current context window, ephemeral | Chat turn history in this session |
| Long-term / semantic | Persistent, durable, cross-session | User preferences in a vector DB |
| Episodic | Specific past interaction traces | "Last time X failed because Y" |

### Reliability, Guardrails, and Safety Checklist
- Step/iteration limit (prevent infinite loops)
- Tool allow-list (restrict which tools an agent can invoke)
- Output schema validation before acting on results
- Human-in-the-loop approval for high-risk/irreversible actions
- Sandbox tool execution (no unrestricted shell/API access)
- Log every tool call + observation for auditability

### Multi-Agent Collaboration
Justified only when subtasks need distinct roles/expertise (planner, coder, reviewer) and coordination value exceeds added latency/cost/failure points. Exam trap: multi-agent chosen for a task one agent could do — always the wrong answer if a simpler option exists.

### When NOT to Use Agents (memorize)
- Fixed workflow with no branching
- Single deterministic API call or lookup
- Latency-critical path where loop overhead is unacceptable
- Task fully solvable by one prompt + one retrieval step
