---
title: "How OpenClaw Works (and why you should build your own)"
video_id: Bo4Shk2FCvk
channel: "[[channels/Agentic Lab]]"
uploaded: 2026-02-24
processed: 2026-07-05
duration: "10:59"
url: https://www.youtube.com/watch?v=Bo4Shk2FCvk
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [custom-agent-harness-design]
tools: [Open Claw, Telegram, Discord]
llms: [Claude]
protocols: [webhooks, WebSocket, RAG]
transcript: true
tags: [youtube, ai-automation]
---

# How OpenClaw Works (and why you should build your own)

![thumbnail](https://i.ytimg.com/vi/Bo4Shk2FCvk/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Bo4Shk2FCvk) | 📅 Uploaded [[uploaded/2026-02-24]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A technical breakdown of Open Claw's architecture — the gateway, session persistence, context compaction, memory, tool calling ("agentic loop"), and autonomy mechanisms (heartbeat, cron, webhooks) that make it feel like an autonomous assistant. The video distills this into four universal principles for any agent harness (triggers, context injection, tools, output), then argues you should build a narrow, single-purpose "sniper agent" instead, given Open Claw's severe context bloat, cost, and security tradeoffs.

**Watch this if:** you want to understand what's actually happening under the hood of an "always-on" AI agent like Open Claw before deciding whether to run it or build your own narrower harness.

## Key Takeaways
- Open Claw is essentially an "exoskeleton" of building blocks around an LLM — a gateway (WebSocket/HTTP server) ties chat channels like Telegram and Discord to the model and runs 24/7.
- Since LLMs are stateless between calls, Open Claw persists sessions by appending every message to a JSONL file and replaying it into each API call; when the context overflows, a compaction system summarizes chunks via the LLM and retries until context drops below 50%.
- The model's identity comes from markdown system-prompt files (soul, agents, memory) plus skill metadata and tool schemas, so it knows what it can call without loading full tool/skill definitions into context.
- Memory has two layers: a memory.md file the model writes critical facts to, and a RAG-style hybrid retrieval system the model can query via a memory tool for older conversation nuggets.
- Tool calls form the "agentic loop": the model emits tokens that trigger an external action, the tool returns results, and the model decides its next step — this is what turns an LLM into an agent, and Open Claw's computer/browser control (via a Chrome extension relay) is what most differentiates it, with real security tradeoffs.
- Autonomy comes from two mechanisms: a heartbeat timer (default every 30 minutes) that tells the agent to check heartbeat.md — which the agent itself can edit, effectively programming its own future behavior — and cron jobs plus webhooks for scheduled or externally-triggered wake-ups.
- Any agent harness reduces to four categories: what triggers it, what's injected into context every turn, what tools it can call, and what it outputs — understanding this is framed as one of the highest-leverage skills of the next decade.
- Because Open Claw is a generalist agent, its context is consistently overkill for any single task: fixed overhead grows from ~7,000 tokens on day one to ~45,000+ tokens after a month of use, driving up to a 40-90% performance decrease from context rot, plus real cost and security downsides (including Anthropic banning Open Claw use on Max plans) — the video argues for building narrow, single-purpose "sniper agents" instead.

## 🛠 Tools & Software
- [[topics/Open Claw]] — the AI agent whose gateway, memory, tool-calling, and autonomy architecture is broken down in detail, along with its context-bloat and security downsides.
- [[topics/Telegram]] — cited as one of the chat channels routed through Open Claw's gateway for interacting with the agent.
- [[topics/Discord]] — cited as one of the channels the agent can output messages to.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — implied as the underlying model in context (Anthropic's Max plan banning Open Claw usage).

## 📡 Protocols & Standards
- [[topics/webhooks]] — one of Open Claw's two autonomy mechanisms: external events that wake the agent with context about the trigger.
- [[topics/WebSocket]] — Open Claw's gateway is described as typically a WebSocket and HTTP server tying channels to the model.
- [[topics/RAG]] — Open Claw's hybrid retrieval memory system, queried via a memory tool for relevant past details.

## ✅ Action Items
- Map any agent you're building (or evaluating) against the four categories: triggers, context injection, tools, and output.
- If running Open Claw, actively manage context hygiene (prune skills/plugins, watch fixed overhead) to limit context rot over time.
- Consider building a narrow, single-purpose "sniper agent" for a specific recurring task instead of relying on a generalist harness like Open Claw.
- Study Open Claw's heartbeat + cron + webhook pattern as a template for adding autonomy to your own custom agent.

## 🔗 Related Videos
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, Open Claw, Telegram, webhooks
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: Claude, Discord, Open Claw, Telegram
- [[videos/You Need To Know This Before Installing OpenClaw]] — shared: Claude, Discord, Open Claw
- [[videos/Agent memory resolved]] — shared: Claude, Open Claw
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude, RAG
- [[videos/Clawdbot Mac Mini VPS The ULTIMATE LOCAL AI Assistant Agent has ARRIVED]] — shared: Discord, Open Claw
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: Open Claw, Telegram
- [[videos/Hermes Agent Full Setup Tutorial How to Setup Your First AI Agent (Gemma 4)]] — shared: Open Claw, Telegram

## Timeline
- `0:00` — Intro: Open Claw is called "AGI" by some; the video breaks down its actual architecture.
- `0:46` — Motivating example: a fully autonomous agent that wakes up, browses X, and sends a morning briefing on its own.
- `1:09` — Core building blocks: an LLM plus a gateway (WebSocket/HTTP server) tying chat channels together, running 24/7.
- `1:45` — Session persistence: every message appended to a JSONL file and replayed into each API call.
- `2:10` — Handling context overflow: Open Claw's compaction system summarizes chunks and retries until context is below 50%.
- `2:49` — Giving the model identity: soul/agents/memory system-prompt files plus skill metadata and tool schemas.
- `3:10` — Memory: a memory.md file for critical facts plus a RAG-style hybrid retrieval memory tool.
- `4:11` — Computer control: browser access via a Chrome extension relay, plus full terminal/camera control and its security tradeoffs.
- `4:44` — Autonomy mechanisms: the heartbeat timer, agent-editable cron jobs, and webhooks.
- `6:30` — The four universal principles behind any agent harness: triggers, context injection, tools, output.
- `7:37` — Why build your own "sniper agent" instead: Open Claw's context bloat, cost, security risk, and up to 90% context-rot performance loss.

## Transcript
<details>
<summary>Full transcript</summary>

Open Claw is an AI agent that's taken the world by storm — so much so that people are calling it AGI. In this video, I'll show you exactly how it works under the hood and the fundamentals that let you build your own agents that outperform it 5-10x on your specific use case.

So, what is Open Claw really? At its core, it's a set of building blocks around an LLM that gives it the ability to perform a variety of tasks — think of it like an exoskeleton built around the LLM, giving it the capacity to perform complex tasks on a computer. Here's a motivating example: your agent wakes up on its own, opens your browser while logged into your account, starts scouring X for the latest AI discourse, reads through the posts, pulls out key takeaways, and sends you a message — "here's your morning briefing" — completely autonomously.

But this isn't magic. First, we start with an LLM — typically a simple external API call or local model, the entire brains of the operation. To talk to it from a chat interface, especially your phone, we route Telegram or other channels to it via a gateway, typically a WebSocket and HTTP server that runs 24/7 and ties everything together.

Since LLMs forget everything between API calls, we need session persistence. Open Claw does this by appending every message as a line to a JSONL file on disk; on each API call, that file is parsed into a messages array and passed back to the LLM. But long conversations eventually overflow the context window — when the API rejects the request as too large, Open Claw's compaction system kicks in, summarizing each chunk of prior messages via the LLM, merging the summaries, and retrying until context is below 50%.

So now we have a basic chatbot. We need the model to understand it isn't just a simple LLM, that it has tools and a personality — we give it a system prompt: a set of markdown files (soul, agents, memory) that tell it how to work in the Open Claw harness. On top of that, we give the LLM skills metadata and tool schemas so it knows which tool it can call without loading the entire tool/skill definition into context. We also inject safety and runtime prompts to help it operate safely.

To make it remember who we are and previous conversations, the model writes to a memory.md file for critical information, and Open Claw also adds RAG-style memory using a hybrid retrieval system to store tons of previous conversations and nuggets, letting the model call a memory tool to search that database for relevant details. We also have an output function — where the LLM talks to us, via Telegram, Discord, or elsewhere.

Since we've given the model an identity, we have to tell it which actions it can take and how — this is the exoskeleton, and we call these tool calls. The model outputs tokens that call a tool, the tool triggers an external action (like writing code), and returns tokens back to the model — a feedback loop we call the agentic loop. Your Open Claw is now an agent.

One of the most critical tools that makes Open Claw different from most agents is computer control — it controls your browser via a Chrome extension relay, meaning it can stay logged in. It's not just browser access either — it's full computer control, from terminal to camera. Obviously this level of access comes with heavy security tradeoffs, so use it at your own risk with heavy guardrails.

The big thing Open Claw gets so much praise for is its autonomous behavior, built on two mechanisms. First, the heartbeat: a timer (default every 30 minutes) that fires a standard prompt telling the agent to recall heartbeat.md and follow its instructions — the agent itself can write to heartbeat.md, effectively programming its own future behavior. On top of this, there are cron jobs — scheduled tasks the agent can create, modify, and delete using a cron tool, with full cron expressions, one-time triggers, or intervals. The other method is webhooks — external events that wake the agent with context about the trigger; something happens, the model wakes up with that context, and acts on it.

That's the entire architecture behind Open Claw, mostly wired to the model through various scripts and hooks (multi-agent methods, hooks, sandboxing, and more go beyond this video's scope). You can notice a distinct pattern: agents are comprised of four categories — what triggers the agent, what's injected on every turn, what tools it can call, and what it outputs. The final piece is giving agents the ability to run in a loop: the LLM calls a tool, gets feedback, and decides the next step. Putting this together is what we call a harness, and learning to build your own is one of the highest-leveraged skills going into the next decade — think of it like the newer version of coding.

Breaking down each zone: what triggers the LLM — cron and heartbeats, core methods to wake Open Claw up. What gets injected into context every turn — the system prompt (soul.md, personality files), JSONL conversation history, tool schemas; you want just enough information for the model to operate well without causing context rot. The tools the LLM can call — memory retrieval via RAG, computer control skills, plugins, all executing in a sandboxed environment with results flowing back in an agentic loop, making your model an actual agent. And finally, what the agent outputs or writes — what it can actually do and how it communicates with the world and remembers.

So Open Claw is genuinely impressive, but the truth is it's a generalist model — its architecture is a roundabout way of giving one agent the power to do many things. As a result, the context given to Open Claw is consistently overkill for a given task, and it has to jump through many hoops. This is the core reason Open Claw doesn't perform as well as you'd like and tends to be very expensive. On top of this, Anthropic banned Open Claw use on Max plans, it has a massive security vulnerability, and it's very difficult to truly customize and see what's going on inside.

For this reason, I implore you to build your own version that serves just one purpose — I call these sniper agents. On day one, you're looking at about 7,000 tokens of fixed overhead before you say a word — comprised of soul.md, agents, workspace files, skill descriptions, tool schemas, and more. But after a month of daily use, memory files grow, the agent creates skills, sessions reset and save summary files, and the more skills/plugins you install, the more bloated things get — around 45,000 tokens of fixed overhead before even sending a prompt. Based on a paper measuring context rot, this results in up to a 40% performance decrease.

Compare that to a single-purpose email reader agent: it only needs about 1,400 tokens and works like a charm. After 6 months, workspace files cap around 37,000 tokens, skills cap at 7,500 tokens, and tools can bloat to tens of thousands of tokens, resulting in 50-90% performance decreases and about 52 cents of extra usage per message — again, before even sending the first message, which will trigger almost instant compaction.

On top of all this, Open Claw has hard limits on memory, heartbeat, skills, and more, causing catastrophic forgetting after months of daily use via very basic truncation — the model forgets what you told it because Open Claw directly prevents those memories from getting into context. The takeaway: learning how agents and harnesses work enables performance gains far above a one-size-fits-all model, and at minimum, understanding Open Claw's internals lets you prevent context rot through good context hygiene and limited plugin usage.

</details>
