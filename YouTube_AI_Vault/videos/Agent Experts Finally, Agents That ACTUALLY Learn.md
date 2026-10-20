---
title: "Agent Experts: Finally, Agents That ACTUALLY Learn"
video_id: zTcDwqopvKE
channel: "[[channels/IndyDevDan]]"
uploaded: 2025-12-15
processed: 2026-07-06
duration: "18:54"
url: https://www.youtube.com/watch?v=zTcDwqopvKE
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [self-improving-agent-expertise]
tools: [Claude Code, Chrome]
llms: [Claude, Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Agent Experts: Finally, Agents That ACTUALLY Learn

![thumbnail](https://i.ytimg.com/vi_webp/zTcDwqopvKE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=zTcDwqopvKE) | 📅 Uploaded [[uploaded/2025-12-15]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A sneak peek at IndyDevDan's Agentic Horizon lesson 5, arguing that today's agents "execute and forget" instead of learning like traditional software does. The fix is "agent experts": prompts paired with a per-domain expertise file (a working mental model) that the agent reads, validates against the actual code, and self-improves after every task — demoed live with a database expert and a websocket expert running inside a multi-agent orchestration system, scaled up to three parallel experts answering the same question for higher confidence.

**Watch this if:** your agents keep re-discovering the same codebase facts every session and you want them to accumulate and reuse domain expertise automatically, with no manual memory-file upkeep.

## Key Takeaways
- The core problem: memory files force globally-loaded context and require manual updates, while prime prompts/sub-agents/skills are powerful but still need you to manually steer them with new information every time — none of them make agents actually learn on their own.
- An "agent expert" is described as a self-improving template metaprompt: it must accumulate and manage its own expertise without being told to, the same way a real expert's mental model evolves with every useful action.
- Meta-agentics (meta prompts that write prompts, meta agents that build agents, meta skills that build skills) are the foundational building tools behind agent experts, but are not themselves agent experts — nothing in a meta prompt/agent/skill updates automatically after use.
- A concrete agent expert = a question prompt + a paired expertise file (YAML/markdown) that acts as a working mental model of one problem domain — demoed with a database expert whose question prompt first reads its expertise file, then instantly validates that understanding against the actual code before answering.
- Critical distinction: the expertise file is explicitly NOT a new source of truth — the code always remains the true source of truth; the expertise file is closer to a working memory/mental model, same as what a human engineer keeps in their head.
- A three-step workflow (plan → build → self-improve) runs after every task: the self-improve step is what updates the expert's expertise file to reflect what changed, so no one has to manually track and document the change afterward.
- Demoed scaling compute: firing the same question at three parallel websocket-expert agents inside a multi-agent orchestrator to "co-locate" on the right answer — one of the three agents failed to complete, illustrating why deploying multiple experts against an important question increases confidence in the combined result.
- Context stays protected across the chain: the plan step alone used ~80k tokens but the top-level orchestrator only passes the resulting plan into the builder, and only the diff into the self-improve step, rather than carrying the full context forward.

## 🛠 Tools & Software
- [[topics/Claude Code]] — runs the entire demo: the `.claude` commands directory holds the meta prompts, expert question prompts, and self-improve prompts fired via `/quest`, `/pl`, and related commands.
- [[topics/Chrome]] — the multi-agent orchestration app's front end is opened in Chrome via a meta-built "start orchestrator" skill and used to observe live UI updates as agent experts complete work.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying every agent, sub-agent, and orchestrator demoed throughout.
- [[topics/Claude Opus]] — referenced specifically as running the orchestrator agents coordinating the parallel websocket experts.

## 📡 Protocols & Standards
- [[topics/MCP]] — mentioned as one option among several ("build your own MCP servers... skills... sub-agents") for implementing the underlying abstraction, with the core four (context, model, prompt, tools) as what actually matters.

## ✅ Action Items
- Build a small stack of meta prompts, meta agents, and meta skills so you can quickly spin up new agentic layers instead of hand-writing every prompt from scratch.
- For any codebase domain you rely on heavily, create a dedicated expert: a question prompt paired with an expertise file the agent reads first and validates against the code.
- Add a self-improve step to your task workflow (plan → build → self-improve) so the expertise file updates automatically after every change instead of relying on manual documentation.
- When correctness on a specific question really matters, fire the same prompt at multiple parallel agent experts and synthesize their combined answers rather than trusting a single response.
- Keep passing only reduced artifacts (plans, diffs) between workflow steps rather than full context, to protect your top-level agent's context window.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, Claude Opus, MCP

## Timeline
- `0:00` — Intro: agents execute and forget instead of learning, unlike traditional software.
- `1:36` — Defining the agent expert: a self-improving template metaprompt that learns with zero human intervention.
- `4:03` — Meta-agentics introduced: meta prompts, meta agents, meta skills as the foundational atoms.
- `4:56` — Meta prompt demo: building a "question with mermaid diagrams" prompt.
- `6:50` — Are meta-agentics themselves agent experts? No — they don't update or learn automatically.
- `7:45` — Database expert demo: question prompt reads its expertise file, then validates it against the actual code.
- `7:49` — Why the expertise file is a working mental model, not a new source of truth.
- `11:45` — Websocket expert demo: adding a session-based event counter using its existing mental model.
- `11:39` — The self-improve prompt explained as the third step of the plan → build → self-improve workflow.
- `12:50` — Scaling up: firing the same question at three parallel websocket agent experts to co-locate on the right answer.
- `18:40` — Closing: the "core four" (context, model, prompt, tools) as what really matters, regardless of abstraction (skill, agent, MCP server).

## Transcript
<details>
<summary>Full transcript</summary>

Agents of today have many problems. Most of them can be solved with great context engineering and great agentic prompt engineering. But there is one massive problem that persists no matter how great your context engineering or agentic prompt engineering becomes. Traditional software improves as it's used, storing user analytics, usage data, and patterns that create algorithms. Agents of today don't. Your agents forget. And that means your agents don't learn. There are a few solutions, but each has their own problems. Memory files are globally forced context that always loads, and expertise requires breaking rules when the time is right — memory files must also be manually updated. Prime prompts, sub-agents, and skills are powerful agentic tools, but again, they all have to be manually updated when you want to add new information and steer your agents in a different direction.

So what if you could teach your agents to act, learn, and reuse their expertise at runtime? What if you could create agent experts? The difference between a generic agent and an agent expert is simple: one executes and forgets, the other executes and learns. You'll learn to build agents that turn actions into expertise automatically, storing the right information and reusing it with no human in the loop. Real experts don't relearn their craft every time — they're always updating their mental model, a data structure that evolves over time. With each useful action, experts accumulate information, examples, and expertise around a specific topic — you're not trying to solve every problem, just the one that matters most to you, your business, and your customers. The expert understands the game never ends, except for one condition: the moment they stop learning.

So what is an agent expert exactly? It's a concrete form of a self-improving template metaprompt. If you understand meta prompts, you'll understand agent experts. We'll walk through meta-agentics — meta prompts, meta sub-agents, and meta skills — the atoms that make up the agent expert. We'll use our orchestrator agent from lesson 4 to showcase agent experts operating on specific areas of a codebase extraordinarily well, and then look at a product-focused agent expert for adaptive user experiences.

At their core, meta-agentics help you build the elements of the system that builds the system: meta prompts, meta agents, meta skills. These greatly increase your output as an agentic engineer with or without agent experts. We'll start with our meta prompt and have it create a new version of a question prompt called "question with mermaid diagrams." Then we'll fire off the meta agent — the agent that builds the agent — to create a new planner agent that directly reads and executes the plan prompt, scaling up planning to multiple agents in parallel. Finally we'll use the meta skill to create a "start orchestrator" skill that kicks off the front end and back end of our multi-agent orchestration application from lesson 4.

We have our question-with-mermaid-diagrams prompt built out here in classic agentic prompt format — variables take in the user question, and based on the purpose you can see it's always going to create mermaid diagrams that enhance understanding. Our meta agent built out a new planner agent that simply reads an existing prompt and fires it as a sub agent — a powerful way to reuse and scale existing prompts into their own agents. Our meta-skill took our existing process of kicking off the orchestrator's front end and backend and turned it into a concrete skill — you can see its purpose, its flags, where to go, how to start things, and it even opens Chrome for us when finished.

Now, an important question: are these meta-agentics themselves agent experts? They're acting, but they're missing a key piece — they're not learning at all. Nothing inside the meta prompt, meta agent, or meta-skill has updated automatically. Our meta tools are not becoming more proficient. Therefore these are not agent experts. Agent experts must learn on their own — you teach them to learn, but after that they accumulate and manage their own expertise.

Let's look at a concrete example: inside our `.claude` commands directory where our prompts are stored, we have an "experts" directory with a database expert — two prompts making up this expertise file. Before diving in, let's execute a question to our database agent: `/quest`, tab to database question, and ask how information flows between our database tables, reporting into a temp file. The first thing this agent does, critically, is read the expertise file — the mental model of the problem space for the agent expert. It then instantly starts comparing its understanding against the actual code — it didn't need to search or find these files, it already knew where they were. This is the differentiating factor of an agent expert: it contains a working mental model, just like any engineer on your team would.

To be ultra clear about what we've built in this YAML file: this is NOT another source of truth. You don't have a source of truth in your own mind — you have a working memory file, a mental model. The agent produced a comprehensive database information flow report: the system uses six Postgres tables tracking orchestrator agent commands, communications, and logging, with a parent-child cascading-delete pattern, an entity relationship diagram, and information flow patterns showing three-way communication between the user, the orchestrator, and the agent. The key point: the agent very quickly used its mental model and validated it against the source of truth — the true source of truth is always the code, never comments, documentation, or plans. But that doesn't mean auxiliary documents, memory, and mental models — expertise — aren't valuable; you'll see that over and over.

At a high level, the question prompt takes in an argument, has a static variable referencing the expertise file, reads it first, then validates its assumptions against the codebase (a critical line, present twice in the prompt for emphasis), and only then reports. Now, what is the expertise and how do we build it? Running the self-improve step for the database expert lets the agent sync its mental model with the working codebase.

Before that, let's look at a websocket expert. We'll kick off the three-step agentic workflow (`/pl`): add a session-based counter to the app navbar displaying the total number of websocket events — perfect for a websocket expert, since there's no searching here, just validating its mental model against known locations, then quickly updating the code.

Let's have some fun with the multi-agent orchestration tool: asking what websocket events exist in the system, then scaling this up — create three agents and run this. Since this is an agent orchestration system, we can quickly scale up more agents against a specific problem — a great way to co-locate on the right answer. Instead of one agent answering, have three, five, or ten, depending on how important it is that the answer is correct. We've now deployed three websocket agent experts to answer one question, firing the exact same prompt to every agent — when they come back with their answers, we'll be a lot more confident they're giving us the right answer.

This prompt actually composes other prompts: a three-step workflow where each step kicks off a different sub agent — a classic planning step, a build step against the plan (classic prompt chaining via an agentic workflow using sub agents), and then a self-improve step. This is where things get interesting: we're not just planning and building codebase updates, we're keeping track of what changed via the self-improve step, so the engineer doesn't have to manually jump in, validate what happened, and write review documentation themselves. Opening the self-improve prompt for the websocket expert shows a very similar structure — almost as if a meta expert had generated it (which, in fact, exists once you start building the same thing repeatedly — three times marks a pattern worth automating).

All three websocket agents completed, and the application starts live-updating. Asking for a concise bullet-point summary of websocket events shows all consumed files from that agent — and interestingly, one of the three agents (websocket 3) didn't complete the task. This is another key value proposition of scaling compute: sometimes only one of five agents finds something the others missed, and composing those results together gives a better outcome. The mental model validates the resulting count — 21 websocket event types across roughly seven categories (agent lifecycle, agent communication, orchestrator, chat, system, etc.).

Notice the context reduction happening across the chain: the plan step alone took 80k tokens, but the top-level agent's context stayed completely protected — it only passed the returned plan into the builder, and only the diff into the self-improve step. Three agent experts completed the work; you could scale this up further by creating three more experts on the same prompt to further validate. The websocket build step used 61k tokens and 41 tool uses, with the Opus orchestrator agents firing off the final self-improve step, making updates as things changed in the system.

We're entering a phase where you can truly create high-performance agents with just the right information, the right prompts, composed into whatever you want. Build a skill if that's your abstraction of choice, build a custom agent, build your own MCP servers — it doesn't matter. Always focus on the foundational units: context, model, prompt, tools — the core four. Everything else is just fancy tooling and a bit of code structure on top of that.

</details>
