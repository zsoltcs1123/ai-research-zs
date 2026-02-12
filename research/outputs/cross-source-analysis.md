# Cross-Source Analysis

Patterns and convergences across sources. Updated as new reports are added.

---

## OpenAI Harness Engineering x Cursor Self-Driving Codebases

### Key divergence: coordination model

Both use isolated workspaces per agent, but coordinate fundamentally differently.

**OpenAI:** Each agent works one task independently in its own git worktree. Parallelism = many independent agents on separate tasks. Coordination happens through the repo itself (PRs, CI, merge). Agents don't talk to each other; they communicate through code and review comments. Humans orchestrate what gets worked on.

**Cursor:** Agents collaborate through a hierarchy. Planner agents delegate to subplanners (recursively), which spawn isolated workers. Workers return handoff documents (code + notes + concerns + feedback) that propagate up to planners with increasingly global views. The system self-coordinates without human intervention.

| | OpenAI | Cursor |
|---|---|---|
| Parallelism unit | Independent task per agent | Coordinated subtasks under a planner |
| Communication | Via repo (PRs, code, docs) | Via handoff documents in the harness |
| Coordination | Human-driven or CI-enforced | Agent-driven (recursive planners) |
| Conflict resolution | Merge gates, linters, CI | Accept turbulence, let system converge |
| Scale target | ~10-20 concurrent tasks | Hundreds of agents, ~1,000 commits/hour |

OpenAI's model is closer to how a small team would adopt agentic development today. Cursor's model is research into what massive-compute agent swarms need to self-organize.

### Convergences

Both teams independently arrived at overlapping conclusions despite the different approaches:

| Finding | OpenAI | Cursor |
|---------|--------|--------|
| Environment > code | "Primary job became enabling agents to do useful work" | "Architecture and instructions matter more than the harness" |
| Constraints > instructions | Enforce invariants, not implementations | "No TODOs" works better than "remember to finish" |
| Accept imperfection | Minimal merge gates, corrections are cheap | Accept small error rate, green branch for fixup |
| Continuous cleanup | Golden principles + garbage collection agents | Periodic fixup passes on release branch |
| Progressive task breakdown | Depth-first building blocks | Recursive planners with subplanners |
| Observability | Full observability stack for agents | Logged all messages, actions, outputs with timestamps |
| Architecture = throughput | Layered domain model enables speed | Monolith -> crates dramatically improved throughput |
