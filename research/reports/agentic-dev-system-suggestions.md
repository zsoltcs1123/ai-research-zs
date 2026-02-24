# Agentic Dev System - Suggestions

Synthesized recommendations for the `agentic-dev-system`, applied to Solution Center (.NET 10 / Angular 21 / ThingsBoard / Keycloak / Docker Compose / Nx monorepo). Updated as new sources are analyzed.

Context: team of 3-4, starting manual, building agent capabilities incrementally alongside the product. Greenfield rewrite of legacy Java MES.

---

## Sources

| Source                                                                                     | Key Takeaway                                                                                                |
| ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| [OpenAI Harness Engineering](https://openai.com/index/harness-engineering/) (Feb 2026)     | Environment design > code generation. Progressive disclosure, mechanical enforcement, continuous cleanup.   |
| [Cursor Self-Driving Codebases](https://cursor.com/blog/self-driving-codebases) (Feb 2026) | Constraints > instructions. Role separation with ownership. Architecture directly affects agent throughput. |

---

## Phase 0 (repo setup)

**AGENTS.md as map, not manual.**
Keep under ~100 lines. Point to `docs/` for architecture, conventions, and plans. OpenAI's monolithic AGENTS.md failed: crowded out task context, rotted fast, impossible to verify mechanically.

**Write constraints, not instructions.**
Both OpenAI and Cursor converge here. Models know how to engineer. Don't tell them how to write code - tell them what's off-limits and what's domain-specific. Frame golden principles as constraints:

- No service locator pattern. Constructor injection only.
- No direct TB API calls. All access through `IThingsBoardClient`.
- No `AsTracking()` on read queries. `AsNoTracking()` always.
- No manual RxJS subscriptions for state. Signals-first.
- No `dynamic` or `object` return types on API boundaries. Typed DTOs only.
- No TODOs or partial implementations in merged code.

Start as a doc agents reference. Promote to linter rules over time.

**~~Execution plans as repo artifacts.~~** Already implemented. The `plan` skill + `dev-cycle` state machine (`state.json`, `{task-id}-plan.md`) covers this. One gap: OpenAI also logs decision rationale inside the plan during execution (why choices were made, alternatives considered). Consider adding a "Decisions" section to the plan template that gets updated during implementation.

**Domain-specific instructions only.**
Cursor found: don't instruct what the model knows (engineering), only what it doesn't (your codebase, your deploy pipeline, your TB integration patterns). Treat it like a brilliant new hire who knows .NET/Angular but not Solution Center. Write instructions about how to run docker compose, how auth flows through Keycloak -> TB -> backend, how to run tests - not about how to write C# or Angular.

---

## Phase 1-2 (infrastructure + auth spike)

**`docker compose up` as agent validation gate.**
Stack already targets Docker Compose. Make it the primary agent feedback loop: every change must pass `docker compose up` + health checks. Agent runs compose, hits `/health` and `/ready`, checks logs for errors. This is the equivalent of OpenAI's "bootable per worktree."

**Nx module boundary enforcement.**
`@nx/enforce-module-boundaries` provides dependency direction linting out of the box. Define tags for layers (platform, energy-app, idx, shared-libs) and enforce import rules in CI. This is exactly what OpenAI built custom linters for, and Nx has it built in with agent-readable error messages.

**Custom .NET Roslyn analyzers.**
Start with 2-3 rules:

- No direct `HttpClient` usage (must go through typed clients)
- No `IThingsBoardClient` usage outside the platform layer
- Structured logging enforcement (`ILogger` with message templates, no string interpolation)

Write diagnostic messages for agents: include what's wrong and how to fix it.

---

## Phase 3-5 (app development)

**Agent self-validation: API + UI.**
Once backend services exist, give agents the ability to boot the Docker Compose stack, hit API endpoints and assert responses, and run Playwright scripts for Angular UI verification. Removes human QA bottleneck.

**Observability as agent feedback.**
Prometheus + Loki + Grafana already planned. Expose query endpoints so agents can check metrics after changes. Enables prompts like "verify no new error logs after EnergyApp migration."

**Doc-gardening process.**
Recurring agent task: scan `docs/` for stale content, check ARCHITECTURE.md reflects actual code, verify cross-links. Open fix-up PRs. Prevents knowledge base rot.

---

## Later (as throughput increases)

**Agent-to-agent review.**
Start with human review. As trust builds, agents do first-pass review using encoded criteria (boundary checks, test coverage, naming). Human reviews the agent's review. Gradually reduce involvement.

**Quality scoring per domain.**
Track grades across domains (Platform, EnergyApp, IDX, Asset Manager) and architectural layers. Gives agents concrete improvement targets and makes debt visible.

---

## What to skip (for now)

- **Zero-human-code policy.** Team is learning the stack and building agent capabilities simultaneously. Human + agent is the right model.
- **Minimal merge gates.** Keep PR review until validation tooling is strong. At 3-4 devs, review is not a bottleneck. (Though note: both OpenAI and Cursor found that accepting small error rates with follow-up fixes outperforms blocking on perfection. Keep this in mind as throughput grows.)
- **Multi-agent orchestration harnesses.** Cursor's recursive planner/worker design is for hundreds of concurrent agents. At your scale, a single agent per task with human orchestration is the right starting point. The patterns (role separation, handoff documents, isolated work copies) are worth understanding for later.
- **6-hour unattended runs.** Build the feedback loops first. Unattended runs are a consequence of trust, not a starting point.

---

## Principles (cross-source consensus)

These show up independently in both OpenAI and Cursor's findings:

1. **Environment design > code generation.** The scaffolding, tooling, and feedback loops matter more than which model writes the code.
2. **Constraints > instructions.** Define boundaries, not procedures. Models know engineering; tell them what's off-limits in your domain.
3. **Architecture is an agent performance variable.** Module structure, dependency direction, build times - all directly affect agent throughput. Invest in clean architecture early.
4. **Accept controlled imperfection.** Blocking on 100% correctness kills throughput. Small stable error rate + follow-up fixes outperforms perfect-or-block.
5. **Observability is non-negotiable.** Both teams invested heavily in making agent behavior visible. You can't improve what you can't see.
6. **Instructions amplify at scale.** Vague specs produce vague output. As agent throughput increases, spec quality becomes the bottleneck.

---

## Situational constraints

- **Mixed team skill.** System must work for human-first developers too. Agent infrastructure should help everyone, not just agent workflows.
- **Enterprise dependencies.** ThingsBoard, Keycloak, ERP are opaque external systems. Abstract behind clean interfaces so agents can reason about them.
- **Small team.** Every hour on agent infrastructure is an hour not shipping features. Be ruthless about what to automate and when.
