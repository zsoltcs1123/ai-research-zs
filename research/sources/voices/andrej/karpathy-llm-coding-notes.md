# LLM Coding Techniques (from Karpathy, Jan 2026)

[Post on X](https://x.com/karpathy/status/2015883857489522876)

Practical techniques and mindset shifts for agent-assisted development.

---

## Core Workflow

**Setup**: Agent sessions (terminal/ghostty) on left, IDE on right for viewing + manual edits.

**Ratio shift**: ~80% agent coding, ~20% manual edits/touchups. Accept this—the leverage is too high to ignore.

---

## Leverage Techniques

### 1. Declarative over Imperative
Don't tell the agent *what to do*—give it **success criteria** and let it loop until met.

### 2. Tests First
Write tests (or have agent write them), then have agent implement until tests pass. Self-verifying loop.

### 3. Browser/MCP Loops
Put agent in feedback loop with browser or other tools. Let it iterate autonomously.

### 4. Naive-then-Optimize
Have agent write naive/obviously-correct algorithm first, then optimize while preserving correctness.

---

## Watching for Agent Mistakes

Agents don't make syntax errors anymore. Watch for:

| Issue | Mitigation |
|-------|------------|
| **Wrong assumptions** | Force clarification: "What assumptions are you making?" |
| **No tradeoff discussion** | Ask: "What are the tradeoffs? Alternatives?" |
| **Overcomplicated code** | Challenge bloat: "Can this be simpler?" |
| **Abstraction bloat** | Push back: "Do we need this abstraction?" |
| **Dead code accumulation** | Request cleanup passes |
| **Unrelated code changes** | Review diffs carefully, reject scope creep |
| **Sycophancy** | Ask for pushback: "What's wrong with this approach?" |

**Use Plan Mode** for anything non-trivial. Forces the agent to think before acting.

---

## Mindset Shifts

- **Tenacity**: Agents don't tire. Let them struggle—they often succeed after 30+ minutes where humans would quit.
- **Expansion > Speedup**: The real gain isn't doing old tasks faster—it's doing tasks you wouldn't have attempted.
- **Courage**: Less fear of unfamiliar codebases. Always a way forward with agent help.
- **Watch for atrophy**: Writing code and reviewing code are different skills. Stay sharp on generation.

---

## Anti-Patterns to Avoid

- Trusting agent output without review (watch like a hawk)
- Letting agents run unsupervised on code you care about
- Accepting first solution without asking "can this be simpler?"
- Not using Plan mode for complex tasks

---

## Quick Reference

```
┌─────────────────────────────────────────────────────┐
│  BEFORE CODING                                      │
│  • Define success criteria (tests, acceptance)      │
│  • Use Plan mode for complex tasks                  │
│  • Ask: "What could go wrong?"                      │
├─────────────────────────────────────────────────────┤
│  DURING CODING                                      │
│  • Let agent loop against criteria                  │
│  • Watch diffs in IDE                               │
│  • Challenge bloat early                            │
├─────────────────────────────────────────────────────┤
│  AFTER CODING                                       │
│  • Request cleanup pass                             │
│  • Ask for simplification                           │
│  • Review for unrelated changes                     │
└─────────────────────────────────────────────────────┘
```

---

*Source: Andrej Karpathy notes, January 2026*
