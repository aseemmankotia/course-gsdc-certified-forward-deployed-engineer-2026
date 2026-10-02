## Chapter 11 Cheat Sheet: PoC-to-Production, Demo Delivery, Trusted Advisor

### PoC → MVP → Production Gates
| Stage | Goal | Exit Criteria |
|---|---|---|
| PoC | Prove technical feasibility | Works in controlled conditions; disposable code OK |
| MVP | Prove business value | Real users, real data, measurable value signal |
| Production | Operate reliably at scale | SLAs defined, monitoring/observability live, security review passed, named business owner |

**Exam trap:** High accuracy alone never satisfies the Production gate — operational rigor does.

### Demo Narrative Arc
| Stage | Purpose |
|---|---|
| Problem | State pain in the client's own words |
| Insight | Explain why current approaches fail (root cause) |
| Solution | Map directly to the insight |
| Impact | Quantified outcome — closes the arc, right before Q&A |

### Live Demo Failure Protocol
1. Acknowledge briefly (no over-apologizing)
2. Pivot to pre-captured backup output
3. Keep narrating the same insight/impact story
4. Never troubleshoot live in front of stakeholders for more than a few seconds

### Trusted-Advisor Engagement Model
| Model | Cadence | Best For |
|---|---|---|
| Fixed-scope SOW | None after delivery | One-off technical deliverable |
| Trusted-advisor retainer | Recurring (e.g., quarterly business reviews) tied to KPIs | Ongoing strategic guidance, roadmap alignment |

### Renewal & Success Metrics
- Anchor renewal conversations to **original success criteria** set at kickoff, not new vanity metrics.
- Trigger an Executive Business Review proactively **~60-90 days before renewal**, or immediately if usage goes flat/declines — never wait for the renewal call.

### Crisis Management Protocol (order matters)
1. Acknowledge transparently
2. Contain the impact
3. Establish a communication cadence with the client
4. Run root cause analysis in parallel (not before step 1-3)

**Exam trap:** "Wait for full RCA before contacting client" is always the wrong answer.

### Change Management for Stalled Adoption
- Symptom: technically successful PoC, no production movement.
- Root cause: usually organizational, not technical.
- Fix: identify a **change champion**, run a **phased pilot** with defined success metrics before full cutover.

### Post-Demo Follow-Up Checklist
- [ ] Recap problem-insight-solution-impact
- [ ] Answer open questions from the session
- [ ] Next step with a **date and owner**

### Visualizing AI Outputs
- Present in the client's business context/dashboard, never raw model logs or JSON, to non-technical stakeholders.
