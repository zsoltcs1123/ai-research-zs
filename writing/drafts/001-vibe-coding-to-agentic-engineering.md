From Vibe Coding to Agentic Engineering

Accountability kills vibe coding. What comes next?

Vibe coding — the process of 'vibing' a piece of software into existence by talking to an LLM — is certainly viable for some limited use cases. LLMs and the agent harnesses around them are good enough at solving programming tasks that they produce working solutions even from vague instructions.

'Vibe coder' has become a somewhat derogatory term as it involves not caring too much about the code the LLM outputs. As such, it has become very popular recently, as it opens up the possibility of software development to the general public. The main goal is hasty execution, getting from zero to a working product in the least amount of time possible; a vibe coder cares less about code quality. Either because they don't even understand code, or because they just want to go fast.

If one thinks about it, there is a place and time for this kind of work. Throwaway software, POCs, static websites (and increasingly, any html/css work - no one liked doing that anyway, right?), personal tools & scripts - these can all benefit from the increased velocity and can sacrifice long term maintainability for it.

The problem starts when you are liable in some way for the produced software. Accountability kills vibe coding. If I don't know the code well, how could I ever take responsibility for it?

Think about it from a team lead's perspective: someone ships a feature built entirely by vibe coding. It works in the demo. Two weeks later there's a production incident, and now you need to debug code that nobody on the team actually wrote or understands. Or a security audit comes around and you have to explain design decisions that were never consciously made.

Despite what the surface might suggest, LLMs are still not 'magic'; they are statistical/non-deterministic text generation machines that are biased to produce output that is similar to what they have been trained on. Therefore, they struggle with novel concepts. They are also very goal oriented - they must produce outcome (predict the next token) however vague or low the confidence is. This leads to a phenomenon termed 'hallucination' - mixing in content for no reason other than statistical correlation, which might be completely irrelevant to the current context. This can be outright dangerous.

Hallucination can introduce subtle bugs, which can escape even rigorous human reviews - not to mention those vibe-coded codebases with little to no review at all. And even disregarding bugs - little inconsistencies will inevitably build up with every LLM-based iteration, and add up quickly, producing a huge pile of technical debt in no time.

Another big problem is the limited context window the models currently have. When the context window is getting full, LLMs drift: they stop remembering instructions precisely, lose important context, compress information, etc. This is mitigated by the advances in context window sizes by the model providers. However, there will always be a ceiling.

The current frontier models offer up to 200k tokens as context windows. From experience in using agents in large codebases, the 200k window is barely enough to execute a small-to-medium sized feature request, especially if you factor in unit tests, documentation, reviews etc. You need to break down the task at hand into manageable chunks and use context isolation strategies for effective work. This will surely advance quickly. The next few model releases will likely push for 1M context windows - a 5x increase. Still, the need for context engineering will likely remain - even at 10M windows.

With all that being said, the capabilities LLMs offer for software development — or really any kind of digital work for that matter — are too large to ignore. You 'just' have to tame the beast somehow.

The answer is not to reject LLMs or slow down. It's to stop treating them as a magic box you throw prompts at, and start treating them as components in an engineered system — with the same rigor you'd apply to any unreliable but powerful dependency. You wouldn't deploy a distributed database without monitoring, retry logic, and failover. LLM agents deserve the same discipline.

Enter Agentic Engineering.

The core thesis is that all digital work will converge around agents. By extension, all digital work will become engineering-shaped, and will require an engineering mindset.

If a traditionally trained software developer wants to utilize the LLM for their work effectively - well beyond the `AI tooling` phase - one needs to start thinking about how to build an engineering system that views agents as the primary layer of execution. That means the job naturally shifts a few abstraction levels up. The core competencies become system design, architecture, specification, quality control, and agent coordination.

What does this look like in practice? Instead of implementing a feature yourself, you describe what it should do, define the acceptance criteria, and let an agent produce the code. Instead of doing code review line by line, you design the constraints that make bad output impossible to merge — linters, CI gates, architectural rules. Your job becomes building the system that makes agents productive, not doing the production work yourself. Early adopters like OpenAI and Cursor have already started operating this way, and independently arrived at the same conclusion: environment design matters more than prompt engineering.

This isn't a flip-the-switch transformation. You start small — tight constraints, heavy review, limited autonomy — and gradually extend the leash as your engineering system proves itself. Trust is earned incrementally — same as with any new team member.

In this Substack I'll document what I learn: the architectures that work, the ones that don't, and the practical mechanics of shifting a development workflow from human-first to agent-first. I start with software development, but I suspect the patterns will generalize far beyond it.
