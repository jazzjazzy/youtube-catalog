---
title: "Agent memory resolved?"
video_id: pAIF7vZm5k0
channel: "[[channels/AI Jason]]"
uploaded: 2026-02-18
processed: 2026-07-06
duration: "15:28"
url: https://www.youtube.com/watch?v=pAIF7vZm5k0
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [agent-memory]
tools: [Claude Code, Codex, Open Claw, OneContext]
llms: [Claude, GLM, GPT-4o Mini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Agent memory resolved?

![thumbnail](https://i.ytimg.com/vi/pAIF7vZm5k0/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=pAIF7vZm5k0) | 📅 Uploaded [[uploaded/2026-02-18]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Coding agents degrade over long tasks because their effective context window (~120-200k tokens even on "1M token" models) fills up and gets compacted, losing prior learnings. The video walks through Git Context Control (GCC), a file-based memory framework using branch/commit/merge semantics, and demos the CLI tool OneContext, which implements GCC to share persistent memory across different coding agents and folders.

**Watch this if:** you're tired of Claude Code or other coding agents "forgetting" earlier context on long-running projects and want a session- and agent-agnostic memory system.

## Key Takeaways
- Even "1M token" models have an effective usable context window of roughly 120k-200k tokens, which is why coding agents compact conversations and lose earlier details.
- Claude Code's built-in memory (a per-project MD file) is limited: it's Claude Code-specific and can balloon on complex projects.
- Git Context Control (GCC) proposes a git-like memory structure: a `main.md` for global project context, plus per-branch `commit.md` (milestones), `log.md` (raw conversation/OTA history), and metadata files.
- GCC defines four actions — branch, commit, merge (and implicit retrieval) — letting an agent fork into an approach, log progress, and later merge learnings back into `main.md`.
- Reported results: using this memory method made Claude Code ~13-14% better on software engineering tasks and let cheaper/smaller models perform closer to frontier-model level.
- OneContext (`npm i -g one-context-ai`) is a CLI tool implementing GCC: it groups sessions into shared "contexts," works across Claude Code and Codex sessions in different folders, uses a stop hook to save conversation history into a local DB, and defaults to a GPT-4o Mini call to summarize each session.
- OneContext can retrieve memory across multiple past sessions/agents at once (e.g., comparing how Open Claw, Codex-based research, and prior OneContext sessions each handle memory) and can generate a shareable link to a chatbot loaded with that context.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose default memory system is critiqued, and one of the agents driven through OneContext sessions.
- [[topics/Codex]] — used as an alternate coding agent option inside OneContext sessions (e.g., researching Open Claw's memory mechanism).
- [[topics/Open Claw]] — referenced as another agent/memory setup the presenter has a session research and compare against OneContext and Claude Code memory.
- [[topics/OneContext]] — the CLI tool demoed end-to-end (install, add context, add sessions, retrieve memory across folders, share a context link) implementing the Git Context Control framework.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model behind Claude Code sessions used throughout the demo; also the model shown improving ~13-14% with GCC-style memory.
- [[topics/GLM]] — cited as an example of a cheaper, smaller model that can reach near-frontier performance when paired with this memory method.
- [[topics/GPT-4o Mini]] — the default model OneContext uses under the hood to generate session summaries.

## ✅ Action Items
- Try `npm i -g one-context-ai` and set up a context per project to test git-style branch/commit/merge memory logging.
- Turn off Claude Code's own memory feature when testing OneContext to avoid double-logging/conflicting memory.
- Use OneContext's shareable context link to let a teammate or a Slack/Telegram bot query accumulated project memory.
- Read the Git Context Control paper/methodology to design your own lightweight main.md + branch folder memory structure even without adopting the CLI tool.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Codex, GPT-4o Mini
- [[videos/You NEED to try these open-source AI projects right now]] — shared: Claude, Claude Code, Codex, Open Claw
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Codex
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, Open Claw
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, Codex, Open Claw
- [[videos/Clawdbot Mac Mini VPS The ULTIMATE LOCAL AI Assistant Agent has ARRIVED]] — shared: Claude Code, GLM, Open Claw
- [[videos/LiteParse - The Local Document Parser]] — shared: Claude Code, Codex, Open Claw
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: Claude Code, Codex, Open Claw

## Timeline
- `0:00` — The core problem: coding agents get "dumber" over long tasks due to limited effective context windows and lossy compaction.
- `1:00` — Claude Code's built-in memory MD file is described and its limitations (per-project, tool-specific, can bloat) explained.
- `3:16` — Introduction of Git Context Control (GCC): main.md, branch folders, commit.md, log.md, metadata.
- `5:30` — Walkthrough of the four GCC actions: branch, commit, merge, and how they fork/preserve context.
- `7:10` — Concrete LinkedIn-scraper example showing branch (Playwright) vs. an alternate API-based branch, and progressive retrieval from main → branch → commit → log.
- `8:31` — Setting up OneContext: `npm i -g one-context-ai`, opening the split session/agent view.
- `9:40` — Creating a context, adding a coding-agent session (Claude or Codex), and testing memory persistence of a name across folders.
- `11:30` — Turning off Claude Code's native memory so only OneContext handles retention; confirming the .claude memory file is empty.
- `12:40` — Cross-folder retrieval demo: asking "what is my name" from a brand-new folder and getting the correct answer via OneContext search.
- `13:40` — Multi-session research demo comparing Open Claw, Context Repositories, and OneContext memory mechanisms, then asking a new session to synthesize pros/cons from memory alone.
- `14:40` — Sharing a context via a generated link that opens a chatbot loaded with the session's context.

## Transcript
<details>
<summary>Full transcript</summary>

So one of the key limitation factor for cloud code or any coding agent is a context management. If you use coding agent enough you will often notice that agent just seems to become dumber as it works on longer and more complex tasks. It'll make the same mistakes and forget about stuff it tried before. Fundamentally it's limited by the context window of the model. Even though modern models can take around 1 million tokens, the actual effective context window is somewhere between 120 to 200k. That's why coding agents design conversation-compacting mechanisms around those context window limitations. Ideally you want the agent to remember every single trace it did before. Claude Code introduced a memory feature where the agent can log information into a shared memory file of the project, but fundamentally the way it works is still somewhat limited — it keeps a separate memory MD file per project, so if your project is complicated this document can blow up quickly, and it's specific to Claude Code. In an ideal world you want knowledge and memory shared across any possible agent session, no matter which agent — only then does your team's knowledge actually accumulate.

The presenter found a project called OneContext, released this week, built around a method called Git Context Control that defines a simple memory framework where the agent manages context just like git, persisting across any session and any coding agent — even shareable via Slack or Telegram. With this method, Claude Code performed 13% better on software engineering tasks, and even smaller/cheaper models like GLM performed at a similar level to frontier models.

The Git Context Control structure has four main files: main.md stores the global context of the project; each branch (a different approach/path the agent explored) has commit.md (high-level milestones logged like a git commit), log.md (the full raw conversation history — observation, thought, action), and metadata (project metadata for quick lookup). Four actions operate on this structure: branch (triggered when the agent explores an alternative strategy), commit (logged at milestones or completed subtasks), and merge (combining a branch's history back into main once a task or exploration completes). This lets an agent fork conversations without losing overall context on complex, long-running tasks.

Walking through an example: building a web scraper for LinkedIn, the agent sets up main.md with the global roadmap, then decides to try a Playwright script first, creating a branch/playwright folder with its own commit.md, log.md, and metadata. As it hits milestones (like a working v1 script), it commits — updating commit.md with a summary and optionally revising main.md. After finishing, it can merge, folding commit.md and log.md back into main.md as a high-level summary. If the Playwright approach turns out wrong, the agent can create a new branch for an API-based approach instead, keeping learnings separate. Later, asking "where are we on the LinkedIn scraper project" lets the agent progressively retrieve: main.md for overall scope, then a specific branch's commit.md for milestones, then log.md for the raw conversation of a specific commit.

Just this week the same author also introduced a "context repositories" feature — a similar concept with a different memory structure but the same overall approach of using the file system to layer information so any coding agent can access memory progressively, and multiple agents on the same project can share context in real time.

Setting up OneContext: run `npm i -g one-context-ai`, then run `one-context` to open a split view — agent sessions on the left, the actual agent interface on the right. First, add a context (a named group of shared memory, e.g. one per project), then add a session choosing a coding agent (Claude or Codex) and a workspace. Testing memory: asking a fresh session "what's my name" returns nothing; telling it "my name is Jason" gets remembered — but this ran via Claude Code's own memory, which isn't wanted, so that gets removed, confirmed by checking the .claude folder's memory file is empty. Creating an entirely new folder and asking "what is my name using OneContext" runs a command-line "align" search (Align is the company behind OneContext) that searches memory and correctly returns "Jason" — demonstrating shared memory across totally different folders.

Under the hood, running `code align` opens the memory folder, which contains a skill file describing how the agent should search: first a broad search across the context folder, then narrowing by session (`-s`) or turn, down to the raw conversation of a specific turn. Knowledge is saved locally in a DB folder ("align.db"), replicating the Claude Code conversation history plus summary information. Every new session is captured by a watcher service with an automatic stop hook that saves conversation info to the DB and triggers an LLM call — defaulting to GPT-4o Mini — to generate a summary.

For a real-world demo: creating a "memory research" context with multiple sessions — one Claude Code session researching how Open Claw's memory mechanism works, one researching how context repositories work, another researching how OneContext's own memory mechanism works. Then, a new session is asked to compare pros and cons of all three approaches purely from memory, without using the internet. It searches across relevant sessions and turns, then returns a pros-and-cons comparison — though it makes a small factual mistake about Open Claw's memory path, possibly due to retrieval noise from Claude Code's own memory system interfering. Still, this cross-session retrieval is presented as valuable for teams working collectively, since everyone can contribute to the same knowledge graph. OneContext also has a share button that generates a link opening a simple chatbot loaded with that session's context, so others can query it directly (e.g. "how does context repositories work") and get an accurate summary.

The core takeaway: this is fundamentally a file-system approach to store and progressively summarize an agent's past actions, cheap to set up, and reusable as a skill for Claude Code to manage its own memory locally.

</details>
