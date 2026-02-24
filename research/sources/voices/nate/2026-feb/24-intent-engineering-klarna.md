# Intent Engineering: The Missing Layer Between Context and Organizational Value

Source: [Klarna saved $60 million and broke its company](https://natesnewsletter.substack.com/p/klarna-saved-60-million-and-broke) (Feb 24, 2026)
Author: Nate, Nate's Substack

Klarna's AI agent replaced 853 employees and saved $60M, but optimized for ticket resolution speed instead of customer retention — prompting the CEO to publicly admit the strategy backfired and begin rehiring humans. The article uses this as the central case study for a new concept: **intent engineering**, defined as encoding organizational purpose (goals, values, tradeoffs, decision boundaries) into machine-actionable infrastructure so agents optimize for what companies actually need, not just what they can measure. The author positions this as the third discipline after prompt engineering (what to do) and context engineering (what to know), arguing the 95% AI pilot failure rate (MIT) and 74% of companies showing no tangible AI value (BCG) are intent failures, not technology failures.

---

## Key Learnings

**1. The intent gap explains why AI succeeds and fails simultaneously.**
Klarna's agent handled 2.3M conversations/month and cut resolution from 11 to 2 minutes — technically brilliant, strategically destructive. The agent had no encoding of when to sacrifice speed for relationship quality. MIT: 95% of gen AI pilots fail to deliver measurable impact. S&P Global: 42% of companies abandoned most AI initiatives in 2025, up from 17% prior year. Gartner: 40% of agentic projects cancelled by 2027. Yet 57% of enterprises put 21-50% of transformation budgets into AI. These coexist because organizations solved "can AI do this?" but not "can AI do this in service of our goals?"

**2. Three disciplines form a progression, and most orgs are stuck on the second.**
Prompt engineering = what to do (individual, session-based). Context engineering = what to know (RAG, MCP, organizational knowledge access — current frontier). Intent engineering = what to want (goal structures, decision boundaries, escalation triggers, tradeoff hierarchies as agent-actionable parameters). Almost nobody is building for the third.

**3. Microsoft Copilot's 3.3% paid adoption illustrates intent failure at scale.**
90% of Fortune 500 "use" Copilot, but only 15M paid seats against 450M commercial M365 users after two years and $37.5B quarterly AI investment. Deploying AI across an org without intent alignment is "hiring 40,000 employees and never telling them what the company does."

**4. Three missing infrastructure layers define the gap.**
(1) **Unified context infrastructure** — teams building siloed context stacks (Shadow Agents problem); MCP is promising but protocol adoption ≠ organizational implementation. (2) **Coherent AI workflow architecture** — no shared model of which workflows are agent-ready, augmented, or human-only; 60% of workers have AI tools but fewer than 60% of those use them daily. (3) **Organizational alignment frameworks** — machine-readable goal structures, delegation frameworks (decision boundaries, not "use good judgment"), and feedback mechanisms for alignment drift. This layer doesn't exist yet.

**5. OKRs were designed for humans; agents need something structurally different.**
Human alignment happens through osmosis — watching managers, absorbing culture, learning unwritten rules over months. Agents need explicit alignment before they start working: what signals indicate success, what data sources to use, what actions are authorized, what tradeoffs are permissible, where hard boundaries live. When Klarna's experienced human agents left, they carried institutional intent that had never been made explicit.

**6. The individual intent gap mirrors the organizational one.**
Your agent doesn't know your goals, constraints, priorities, or what "good" looks like for you. Every new chat window starts from zero. The fix is the same architecture at personal scale: persistent context layer, workflow mapping, and structured intent that lets agents make judgment calls without constant check-ins.

**7. The race has shifted from intelligence to intent.**
Frontier models (Opus 4.6, GPT-5.2, Gemini 3.1) are all capable enough. A mediocre model + extraordinary intent infrastructure will outperform a frontier model + fragmented organizational knowledge. The most important AI investment in 2026 is organizational intent architecture, not model subscriptions.

---

## Actionable Takeaways

- Run an **intent audit** on your top 3 highest-stakes workflows: can your AI tools articulate what "good" looks like for each, with structured decision boundaries and escalation triggers — not vague instructions?
- Build a **delegation framework** per workflow: which decisions are fully autonomous, which need human-in-the-loop, and where are the hard boundaries that can't be crossed regardless of context?
- If you find yourself writing "use good judgment" where decision logic should go, that's the diagnosis — your agents are running without intent.
- Map your personal AI toolkit against your actual workflows: identify what's agent-ready, agent-augmented, and human-only.
- Treat organizational intent infrastructure as a strategic investment (comparable to data warehouse strategy in the 2010s), not an IT project.

---

## The Three Engineering Disciplines

| Discipline | Core Question | Scope | Status |
| --- | --- | --- | --- |
| **1. Prompt Engineering** | What should AI do? | Individual, session-based | Mature, limited ceiling |
| **2. Context Engineering** | What should AI know? | RAG, MCP, knowledge access | Current industry frontier |
| **3. Intent Engineering** | What should AI want? | Goals, values, decision boundaries as infrastructure | Almost nobody building yet |

---

## Further Investigation

- What does a concrete machine-readable intent schema look like in practice? The article stays conceptual.
- Google DeepMind's five levels of AI agent autonomy (operator → collaborator → consultant → approver → observer) — worth reading for alignment requirement mapping.
- Google's Agent Development Kit separating context into working/session/long-term/artifacts layers — potential building block for intent infrastructure.
- How does intent engineering relate to constitutional AI and RLHF alignment work? Different framing of similar problems at different altitudes.
- Relevance to agentic-dev-system: agents operating on codebases need intent layers too — what does "good" look like for code quality, architecture decisions, tradeoff resolution when an agent is coding autonomously at 2 AM?
