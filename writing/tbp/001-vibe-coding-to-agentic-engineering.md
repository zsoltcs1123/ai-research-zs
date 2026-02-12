# From Vibe Coding to Agentic Engineering

_Accountability kills vibe coding. What comes next?_

---

## The appeal of vibing

Vibe coding — the process of 'vibing' a piece of software into existence by talking to an LLM — is becoming a viable way to produce software. LLMs and the agent harnesses around them (systems that let AI act autonomously, not just answer questions) are good enough at solving programming tasks that they produce working solutions even from vague instructions.

'Vibe coder' has become a somewhat derogatory term amongst professionals, as it involves not caring too much about the code the LLM outputs. As such, vibe coding has become very popular recently, as it opens up the possibility of software development to the general public. The main goal is hasty execution, getting from zero to a working product in the least amount of time possible; a vibe coder cares less about code quality. Either because they don't even understand code, or simply because they just want to go fast.

If one thinks about it, there is a time and place for this kind of work. Throwaway software, POCs, static websites (and increasingly, any html/css work - no one liked doing that anyway, right?), personal tools & scripts - these can all benefit from the increased velocity and can sacrifice long term maintainability for it.

## Where it breaks down

The problem starts when you are liable in some way for the produced software. Accountability kills vibe coding. If I don't know the code well, how could I ever take responsibility for it?

Think about it from a team lead's perspective: someone ships a feature built entirely by vibe coding. It works in the demo. Two weeks later there's a production incident, and now you need to debug code that nobody on the team actually wrote or understands. Or a security audit comes around and you have to explain design decisions that were never consciously made.

Despite what the surface might suggest, LLMs are still not 'magic'; they are statistical/non-deterministic text generation machines that are biased to produce output that is similar to what they have been trained on. Therefore, they struggle with novel concepts (although this is less clear-cut with reasoning models as they show surprising results on that front).

They are also very goal-oriented - they must produce outcome (predict the next token) however vague or low the confidence is. This leads to a phenomenon termed 'hallucination' - mixing in content for no reason other than statistical correlation, which might be completely inadequate in the current context. This can be outright dangerous.

Hallucination can introduce subtle bugs, which can escape even rigorous human reviews - not to mention those vibe-coded codebases with little to no review at all. And even disregarding bugs - little inconsistencies will inevitably build up with every LLM-based iteration, and add up quickly, producing a huge pile of technical debt in no time.

Another big problem is the limited context window the models currently have. When the context window gets full, LLMs drift: they stop remembering instructions precisely, lose important context, compress information, etc. This is mitigated by the advances in context window sizes by the model providers. However, there will always be a ceiling.

The current frontier models offer up to 200k-1M tokens as context windows. In my experience using agents in large codebases, a 200k window is barely enough to execute a small-to-medium sized feature request, especially if you factor in unit tests, documentation, reviews etc. You need to break down the task at hand into manageable chunks and use context isolation strategies for effective work.

Context window sizes will surely grow quickly. The next few model releases will likely push for 10M size - a huge jump from current levels. Still, the need for context engineering will likely remain even at 10M windows. The windows size is just one parameter. How well a model retains and retrieves information _within_ that window is a different story.

All this points to the conclusion that an engineering mindset is still going to be relevant for the foreseeable future for any kind of serious work.

---

## Taming the beast

The capabilities LLMs offer for software development — or really any kind of digital work for that matter — are too powerful to ignore. You 'just' have to tame the beast somehow.

The answer is not to reject LLMs or slow down. It's to stop treating them as a magic box you throw prompts at, and start treating them as components in an engineered system, with the same rigor you'd apply to any unreliable but powerful dependency. You wouldn't deploy a distributed database without monitoring, retry logic, and failover. LLM agents deserve the same discipline.

**Enter Agentic Engineering.**

The core thesis is that all digital work will converge around agents. By extension, all digital work will become engineering-shaped, and will require an engineering mindset.

If a traditionally trained software developer wants to utilize the LLM for their work effectively - well beyond the "AI tooling" phase - one needs to start thinking about how to build an engineering system that views agents as the primary layer of execution. That means the job naturally shifts a few abstraction levels up. The core competencies become system design, architecture, specification, quality control, and agent coordination.

What does this look like in practice? Instead of implementing a feature yourself, you describe what it should do, define the acceptance criteria, and let an agent produce the code. Instead of doing code review line by line, you design the constraints that make bad output impossible to merge: linters, CI gates, architectural rules. Your job becomes building the system that makes agents productive, not doing the production work yourself. Early adopters like [OpenAI](https://openai.com/index/harness-engineering/) and [Cursor](https://cursor.com/blog/self-driving-codebases) have already started operating this way, and independently arrived at the same conclusion: environment design and context management are critical pieces of the puzzle.

This isn't a flip-the-switch transformation. You start small (tight constraints, heavy review, limited autonomy) and gradually extend the leash as your engineering system proves itself. Trust is earned incrementally — same as with any new team member.

---

## What's next

In this Substack I'll document what I learn: the architectures that work, the ones that don't, and the practical mechanics of shifting a development workflow from human-first to agent-first. I start with software development, but I suspect the patterns will generalize far beyond it.

Next up: the Design Principles of an Agentic Engineering System.
