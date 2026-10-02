# Chapter 1 Cheat Sheet — FDE Mindset & Problem Structuring (~10% of exam)

## Role Comparison (heavily tested)
| Role | Engagement Model | Core Deliverable |
|---|---|---|
| **FDE** | Embedded with client, hands-on, iterative | Working, shipped technical solution |
| **ML Engineer** | Defined technical scope | Trained/optimized model within that scope |
| **Solutions Architect** | Pre-sales/advisory, often less hands-on | System architecture & technical spec/design |
| **Consultant** | Advisory, analysis-driven | Strategic recommendations/frameworks, not implementation |

**Exam trap:** Options that swap 'builds/ships' with 'recommends' between FDE and Consultant, or confuse ML Engineer's narrow scope with FDE's end-to-end ownership.

## MECE Framework
- **M**utually **E**xclusive → no category overlaps another
- **C**ollectively **E**xhaustive → categories cover the full problem space, no gaps
- **Red flags a breakdown is NOT MECE:** catch-all buckets ('other,' 'general issues,' 'everything else'), categories that could both apply to the same instance

## Input-Processing-Output (IPO) Model
| Component | Definition | Vague-requirement fix |
|---|---|---|
| Input | Data/signals feeding the system | Ask: what data exists today? |
| Processing | Logic/decision applied to inputs | Ask: what rule/model transforms input → output? |
| Output | Concrete result produced | Ask: what decision does this output support? |

**Rule:** Vague asks ('automatically,' 'should just work') map to none of the three — always force explicit definition before scoping.

## Business-to-Technical Translation — 3 Questions
1. What decision/action does this output drive?
2. What inputs/data currently exist?
3. What does success look like, measurably?

## Constraints vs. Trade-offs
| Term | Meaning | Exam trap |
|---|---|---|
| Constraint | Hard limit, cannot be violated (e.g., no historical data) | Disguised as a trade-off in scenario questions |
| Trade-off | Choice between competing goods (speed vs. accuracy, cost vs. latency) | Confused with a fixed constraint |

## Signal vs. Noise
- **Noise:** sentiment/symptom language ('it's a mess,' 'we need AI')
- **Signal:** specific, measurable, tied to a decision ('reduce turnaround from 3 days to 1')
- Always convert noise → testable requirement before proposing a solution.

## Top 3 Exam Gotchas
1. Choosing a role-swap answer (e.g., calling ML Engineer responsibilities 'FDE work')
2. Solutioning before scoping — jumping to a build recommendation before discovery
3. Treating a real constraint (missing data/infra) as if it were just a trade-off to negotiate

## Passing Threshold
This domain requires solid conceptual accuracy on role boundaries and MECE/IPO application — these concepts recur as supporting logic in later, higher-weighted domains, so mastery here compounds.
