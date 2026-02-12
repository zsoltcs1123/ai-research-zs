# Design Principles of Agentic Engineering Systems

Agentic Engineering can be applied to any problem

three scenarios: software engineering vs financial analysis vs creating a presentation deck

workflow steps:

software:
goal: integrate new change into codebase

1. define task
2. plan
3. implement
4. review
5. verify (qa)
6. document
7. finalize (commit, push & pr)

at a minimum. can be more
each step can have its loop

consider vs financial analysis
goal: ccessing, processing analyzing & storing an earnings report a company have produced

1. define task
2. plan
3. implement: here's where its different: instead of editing code, it goes and:
   - gets the report
   - maybe transforms it
   - feeds to an LLM for analysis or to extract the numbers
   - run the numbers through another system
   - maybe cross reference with other data
   - enrich
   - push to database
   - etc etc
4. review
5. verify
6. document
7. finalize (send report etc)

3 creating a presentation deck
.... same idea

The point is: each area is different, yet it can be defined within an general Agentic Engineering Framework. All of it is a mix of code editing, api calls, LLM calls etc. the workflow steps can be largely the same.

Another point: most will try to build 'THE' financial analysis tool for the problem above. But I think it is the wrong approach. No matter how hard you try, your solution will end up being opiniated and specific to YOUR ideas. another analyst might have a totally different approach. then your tool you built is worthless to them, unless u tried and built in customization for everything... lot of hassle

the Solution is to provide a lightweight Agentic Framework which can be customized ot any workflow.
it must be:

- Truly portable - not specific to any model/agent provider like claude code, cursor, gemini etc. This alone is a challenge as each company has their own ecocystem which they try to lock you into. some specs like agentskills are being standardized, but generally each agent has their own way of doing the same thing...
- So you need a generic source with agent-specific installer
- For now to be portable the workflow steps must be defined as skills, as all agents understand them. this however is problematic, because your orchestrators are non-deterministic.
- All the domain specifc behaviour must come from user defined rules. you cannot bake rules into the system because each person will have their own ideas when it comes to anything. also rules depend on the project. so plugin=based rules system
- A workflow customization tool that lets users add/remove workflow steps beyond the default ones
