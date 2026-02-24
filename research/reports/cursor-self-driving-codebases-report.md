# Cursor "Towards Self-Driving Codebases" - Analysis Report

Source: [cursor.com/blog/self-driving-codebases](https://cursor.com/blog/self-driving-codebases) (Feb 5, 2026)
Author: Wilson Lin, Cursor/Anysphere

Cursor built a multi-agent harness that orchestrated thousands of agents to build a web browser from scratch. Peaked at ~1,000 commits/hour across 10M tool calls, running continuously for one week with no human intervention. Research project, not a product - the browser had imperfections, but it ran.

---

## Key Learnings

**1. Self-coordination between equal agents fails.**
First attempt: agents share a state file, decide their own work, update the file. Failed fast. Agents mismanaged locks, created contention, and avoided complex tasks. 20 agents produced the throughput of 1-3. Flat structures don't work.

**2. Structure and roles solve coordination.**
What worked: Planner (decides what) -> Executor (ensures delivery) -> Workers (do the coding) -> Judge (validates completion). Separation of ownership and accountability made agents productive. Single responsibility per role.

**3. Static plans are too rigid.**
Upfront planning couldn't adjust as agents discovered new issues. System bottlenecked on the slowest worker. Solution: merge planner and executor into a continuous loop that can replan dynamically.

**4. Too many roles on one agent causes pathological behavior.**
When executor was responsible for planning, exploring, spawning, reviewing, merging, and judging simultaneously, it degraded: random sleeping, premature completion claims, refusal to delegate. Agents overwhelmed by multi-objective prompts.

**5. Final design: recursive planners + isolated workers.**
- Root planner owns entire scope, spawns subplanners for subdivisions (recursive)
- Workers pick up tasks in isolation, work on their own repo copy, return a handoff document (not just code - includes notes, concerns, deviations, feedback)
- Information propagates up the chain to owners with increasingly global views
- No global synchronization or cross-talk needed

**6. Accept a small error rate for throughput.**
Requiring 100% correctness before every commit caused the system to grind to a halt. Agents would pile on the same issue, go outside scope, trample each other. Better approach: accept a small stable error rate, use a "green branch" with periodic fixup passes.

**7. Instructions amplify at scale.**
Agents follow instructions exactly, good or bad. Vague specs ("implement spec") led to agents going deep into obscure features. Missing performance requirements meant no performance optimization. Unclear dependency policy meant agents pulled unnecessary libraries. The harness was correct - the instructions were wrong.

**8. Constraints > instructions.**
"No TODOs, no partial implementations" works better than "remember to finish implementations." Models do good things by default. Constraints define boundaries. Don't instruct what the model already knows - only what's specific to your domain.

**9. Concrete numbers beat vague language.**
"Generate many tasks" produces 3-5. "Generate 20-100 tasks" produces actual scale. Models default to conservative interpretation of ambiguous quantity.

**10. Architecture affects agent throughput directly.**
Monolith project with hundreds of agents compiling simultaneously saturated disk I/O. Restructuring into self-contained crates dramatically improved throughput. Project structure is an agent performance variable.

---

## System Evolution: Step by Step

| Phase | Design | Outcome |
|-------|--------|---------|
| **1. Single agent** | One agent, manual nudging | Too slow. Lost track, claimed premature success. Could write good code in small pieces. |
| **2. Manual dependency graph** | Human plans tasks, agents pick them up | Better throughput, but agents can't communicate or give feedback. Too static. |
| **3. Self-coordinating peers** | Equal agents, shared state file, self-organize | Failed. Lock contention, 20 agents -> throughput of 1-3. Agents avoid complex work. |
| **4. Structured roles** | Planner -> Executor -> Workers -> Judge | Coordination solved. But bottlenecked on slowest worker. Static plans can't adapt. |
| **5. Continuous executor** | Executor also plans, no separate planner. Scratchpad, self-reflection, freshness mechanisms. | Dynamic and flexible, but executor overwhelmed by too many simultaneous roles. |
| **6. Final: recursive planners** | Root planner -> subplanners (recursive) -> isolated workers. Handoff docs propagate info upward. | Stable. ~1,000 commits/hour. Ran one week unattended. Linear scaling. |

---

## Prompting Principles

- Don't instruct what the model already knows (engineering). Only instruct domain-specific knowledge (your codebase, your deploy pipeline).
- Treat the model like a brilliant new hire who knows engineering but not your processes.
- Constraints are more effective than instructions.
- Avoid checkbox mentality for complex tasks. Give intent, let the model use judgment.
- Give concrete numbers and ranges for scope.
- Architecture matters: initial spec determined whether the system converged on a viable design or a dead end.

---

## Reality Check

This is a research project, not production software. A browser built by agents over one week with no human code review. The browser had imperfections and wasn't intended for external use.

The transferable lessons are about **multi-agent coordination patterns and instruction design**, not raw throughput:
- Role separation with clear ownership beats flat self-coordination
- Recursive delegation with handoff documents enables scale
- Instructions are the bottleneck more often than model capability
- Architecture decisions directly affect agent productivity
- Accepting controlled imperfection enables throughput that perfect-or-block can't
