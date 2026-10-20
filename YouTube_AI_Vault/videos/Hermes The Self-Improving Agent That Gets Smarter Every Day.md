---
title: "Hermes: The Self-Improving Agent That Gets Smarter Every Day"
video_id: HdxtLpL9CC8
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-15
processed: 2026-07-05
duration: "6:08"
url: https://www.youtube.com/watch?v=HdxtLpL9CC8
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [ai-agent-memory-management, personal-ai-assistant-evaluation]
tools: [Hermes, Open Claw, Nano Claw, Claude Agent SDK, OpenRouter, SQLite, Supermemory, Mem0, Open Viking]
llms: [GLM, Gemma]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Hermes: The Self-Improving Agent That Gets Smarter Every Day

![thumbnail](https://i.ytimg.com/vi/HdxtLpL9CC8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=HdxtLpL9CC8) | 📅 Uploaded [[uploaded/2026-04-15]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Hermes is Nous Research's open-source, self-improving AI agent that remembers everything across sessions, full-text-searches past conversations, and writes its own reusable skills. The creator tests it by having it learn his tweet-writing style from past scripts, switches models mid-session, and confirms in a brand-new session that Hermes recalls his preferences without any file re-upload — while weighing whether it's mature enough to replace Open Claw.

**Watch this if:** you're evaluating self-improving, memory-persistent AI agent alternatives to Open Claw or Claude Agent SDK-based tools.

## Key Takeaways
- Hermes is an open-source agent by Nous Research that reflects, learns, and evolves — it never forgets prior conversations and can write its own skills from experience.
- Setup mirrors Open Claw's flow: pick a model provider (the creator used OpenRouter with Gemma), connect messaging platforms/tools, and run via CLI; installed on a VPS in this demo but works locally too.
- Memory lives in an external memory.md file (or a pluggable processor like Supermemory, Mem0, or Open Viking), preloaded each session as a compacted ~3,500-character (~700-token) summary, not the full history.
- All sessions are stored in an SQLite database using FTS5 full-text search, so asking Hermes what you said yesterday triggers a database search rather than relying on preloaded context alone.
- Hermes compresses context at 50% of the window (vs. Claude Code's 80%), preserving the head and tail of a session while compressing the middle and discarding old tool-call output before saving to SQLite.
- It self-nudges roughly every 10 turns to save important information to memory and to write a new skill when appropriate — the creator prompted it to turn the tweet-writing process into a reusable skill, which it then used successfully.
- You can hot-swap the model mid-session with the `/model` command (switched from the default to GLM 5 Turbo for faster responses) without losing session memory.
- A brand-new session, on a different model, correctly recalled the creator's tweet style, target length, and even emoji preferences — demonstrating cross-session memory persistence without manual re-context.

## 🛠 Tools & Software
- [[topics/Hermes]] — the open-source, self-improving Nous Research agent under review; memory, skill-writing, and model-switching are all tested live
- [[topics/Open Claw]] — the more mature, better-sandboxed incumbent agent the creator is deciding whether Hermes can replace
- [[topics/Nano Claw]] — mentioned as a smaller-feature-set alternative built on the Claude Agent SDK that the creator previously tried
- [[topics/Claude Agent SDK]] — the SDK Nano Claw is built on; the creator notes usage restrictions around it with third-party tools
- [[topics/OpenRouter]] — the model provider chosen during Hermes setup (paired with Gemma) instead of running a model locally
- [[topics/SQLite]] — the database (with FTS5 full-text search) Hermes uses to persist compacted session history for later recall
- [[topics/Supermemory]] — named as one of the external memory processors Hermes can be configured to use instead of the default memory.md file
- [[topics/Mem0]] — named alongside Supermemory as a configurable external memory processor option
- [[topics/Open Viking]] — named as a third configurable external memory processor option

## 🤖 LLMs Mentioned
- [[topics/GLM]] — switched to mid-session (GLM 5 Turbo) via the `/model` command for faster responses on the tweet-writing task; the creator plans to use it as a cheap daily-driver model
- [[topics/Gemma]] — the initial model (Gemma 4) selected through OpenRouter when first setting up Hermes

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- If evaluating agent memory systems, test cross-session recall directly: start a fresh session and ask the agent to recall style/preferences without re-uploading files.
- Use the `/model` slash command to swap models mid-session when a task is taking too long or burning excess context, without losing accumulated memory.
- If token cost matters, configure a cheap model (like GLM) as the daily driver for a personal-assistant-style agent instead of a frontier model.
- Consider an external memory processor (Supermemory, Mem0, Open Viking) if the default memory.md compaction isn't capturing enough detail for your use case.

## 🔗 Related Videos
- [[videos/Hermes Agent Full Setup Tutorial How to Setup Your First AI Agent (Gemma 4)]] — shared: Gemma, Hermes, Open Claw
- [[videos/How Hermes Agent Can Save You 85 (Or More) in BG Task Token Cost]] — shared: GLM, Hermes, OpenRouter
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Agent SDK, Gemma, OpenRouter
- [[videos/7 new open source AI tools you need right now]] — shared: Gemma, Open Viking
- [[videos/Agent memory resolved]] — shared: GLM, Open Claw
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Open Claw, OpenRouter
- [[videos/Clawdbot Mac Mini VPS The ULTIMATE LOCAL AI Assistant Agent has ARRIVED]] — shared: GLM, Open Claw
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: GLM, Open Claw

## Timeline
- `0:00` — Intro: is Hermes, the self-improving agent, enough to replace Open Claw?
- `0:37` — Why Hermes: dissatisfaction with Open Claw's bloat and Nano Claw/Claude Agent SDK restrictions
- `1:16` — Installing Hermes (OpenRouter + Gemma, VPS setup)
- `1:50` — Starting a new session and prompting it to write tweets from past scripts
- `2:35` — Hermes analyzes writing style and proposes a tweet strategy
- `3:10` — Switching models mid-session to GLM 5 Turbo via `/model`
- `3:45` — Generating and refining tweets, saving preferences to memory
- `4:15` — Prompting Hermes to turn the process into a reusable skill
- `4:35` — New session, different model: Hermes recalls tweet style and emoji preferences
- `4:55` — How memory works: memory.md, external processors, SQLite + FTS5
- `5:35` — Context compression behavior (50% threshold, head/tail preservation)
- `5:50` — Wrap-up and plans to trial Hermes as a main personal assistant

## Transcript
<details>
<summary>Full transcript</summary>

Hermes is an open-source AI agent created by Nous Research that is self-improving — the more you use it, the better it gets. It reflects, learns, and evolves on its own, never forgets anything you said, and even creates its own skills. But is that enough to replace something like Open Claw, which supports more channels, has better sandboxing, and is much more mature?

The name Hermes comes from the Greek messenger god. The creator previously made videos about Open Claw (great, but with a lot of unused features) and Nano Claw (a much smaller feature set, built on the Claude Agent SDK, which has become less usable due to rules around using the Claude description with third-party tools). So he's on the lookout for a new AI assistant and testing whether Hermes can fill that void — specifically by using it to create promotional tweets based on past video scripts, testing whether it remembers his writing style and feedback without repeating himself.

Hermes was installed via a simple command, walking through model selection (OpenRouter with Gemma 4 — locally would be preferred with the right hardware), messaging platforms, and CLI tools — a setup flow that will feel familiar to Open Claw users. Installed on a VPS here, though local installation works too. Running the Hermes command starts a new chat (not resuming the previous one unless specified, same as Claude Code) showing the Hermes symbol with available tools/skills.

First prompt: help write tweets based on video scripts. After an initial response, a follow-up directs it to study scripts in a scripts folder to learn writing style and voice, plus target audience and desired tweet length. Hermes searches the files and returns a style breakdown (pragmatic, skeptical, developer-centric, transparent, relatable) plus an audience strategy. After changing his mind about tweet length (210 → 400 characters) and noticing the response was slow, the creator switched models mid-session using `/model` to GLM 5 Turbo — getting faster responses, plus Hermes automatically saved the new length/style preferences to memory without being told to.

Hermes then generates tweet drafts; after some editing feedback (avoiding phrases like "breaking a sweat" or "incredible"), it produces a tweet the creator would actually use, saving it to memory. Prompting it to create a skill for future tweet-writing invokes its skill-manager skill, and the resulting skill successfully writes multiple tweet options plus a full thread. To prove memory persistence, a brand-new Hermes session (on a different model) is asked how the creator likes to write tweets — and it answers correctly, down to preferred emoji usage.

How Hermes achieves this without burning tokens: memory is stored in an external memory.md file (or an external processor like Supermemory, Mem0, or Open Viking), preloaded each session as a compacted summary limited to about 3,500 characters (~700 tokens depending on model) rather than full history. All sessions are stored in a SQLite database using FTS5 for full-text search — so asking what was discussed yesterday triggers an actual database search. Hermes also compresses context earlier than some agents: at 50% of the context window (vs. Claude Code's 80%), keeping the head and tail of a session and compressing the middle while discarding old tool-call output — this compressed version, not the full conversation, is what's saved to SQLite. It also self-nudges roughly every 10 turns to save important information to memory and write new skills when useful.

Acknowledging the demo is short, the creator plans to use Hermes more — potentially as a main personal assistant paired with a cheap model like GLM — and will report back on how it goes.

</details>
