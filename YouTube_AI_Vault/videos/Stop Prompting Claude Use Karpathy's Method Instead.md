---
title: "Stop Prompting Claude. Use Karpathy's Method Instead."
video_id: 7zZy1QTvokM
channel: "[[channels/Austin Marchese]]"
uploaded: 2026-06-09
processed: 2026-07-05
duration: "13:18"
url: https://www.youtube.com/watch?v=7zZy1QTvokM
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-spec-driven-workflow, ai-output-verification]
tools: [Claude Code, Codex]
llms: [Claude, Gemini, Grok, ChatGPT]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Stop Prompting Claude. Use Karpathy's Method Instead.

![thumbnail](https://i.ytimg.com/vi_webp/7zZy1QTvokM/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=7zZy1QTvokM) | 📅 Uploaded [[uploaded/2026-06-09]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Austin Marchese breaks down Andrej Karpathy's three-layer method for getting far more out of Claude: writing a precise, goal-driven spec instead of relying on plan mode alone; building a verification layer (clear criteria, a second AI critic, external signal) since LLMs behave like a "robot librarian" rather than a motivated human; and building a durable environment (CLAUDE.md, a personal knowledge base, reusable skills, and hard tool-level guardrails) that compounds over time.

**Watch this if:** you keep re-explaining the same context to Claude and want a repeatable system instead of one-off prompting.

## Key Takeaways
- Karpathy's method breaks into three layers: the spec, the verifier, and the environment.
- Layer 1, the spec: AI is brilliant at measurable things but blind to context — Claude, Gemini, Grok, and ChatGPT all gave the same wrong answer to a simple context-dependent question (drive or walk 50m to a car wash). Bridge the gap by having Claude interview you to uncover the real goal (not just the task), working agile with tight, checkpointed scopes instead of one giant "waterfall" ask, and being maximally precise so AI has less room to assume.
- Layer 2, the verifier: Karpathy frames LLMs as not "animals" driven by intrinsic motivation like humans, but more like a robot librarian that can only answer from what's in its library and doesn't know what it's missing — so yelling at it or pleading doesn't help. The real lever is verification: set precise evaluation criteria up front, use a second AI model (e.g. the Codex plugin inside a Claude Code session) as an independent critic, and pull in external signal (checking an actual deployment, feeding in historical reports) to ground verification in reality.
- Claude Code creator Boris Cherney is quoted saying a feedback loop can 2-3x the quality of Claude's final output.
- Layer 3, the environment: treat your workspace like a workshop — write a real CLAUDE.md (auto-injected every prompt) describing your repo, custom skills, and knowledge architecture; build a personal "LLM knowledge base" folder of your own reference material since your data is your moat; turn repeated tasks into custom skills that improve with use; and enforce truly critical constraints as hard, tool-level guardrails (e.g. a pre-tool-use hook blocking edits to a folder) rather than soft prompt-level rules Claude can still ignore.
- Karpathy's closing point: you can outsource your thinking to AI, but you can't outsource your understanding — all three layers ultimately depend on you understanding your own goals well enough to direct the AI.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent all three layers (spec, verifier, environment) are built around
- [[topics/Codex]] — recommended as a second, independent AI critic via a plugin that lets you query Codex from within a Claude Code session

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the primary model being taught to use via the three-layer method; also one of four models tested on the car-wash question
- [[topics/Gemini]] — tested alongside Claude on the car-wash question and gave the same wrong answer
- [[topics/Grok]] — tested alongside Claude on the car-wash question and gave the same wrong answer
- [[topics/ChatGPT]] — tested alongside Claude on the car-wash question and gave the same wrong answer

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Have Claude interview you to uncover the actual goal behind a task before it starts building.
- Work agile: scope specs small, review at each checkpoint, and repeat instead of handing Claude one giant task.
- Add a second-model check (e.g. install the Codex plugin in Claude Code) to critique Claude's own output on complex builds.
- Pull external signal into verification — have Claude check the actual deployed system, or feed it historical examples as a reference format.
- Write a real CLAUDE.md describing your repo, skills, and hard rules, and enforce critical rules with pre-tool-use hooks instead of prompt-level requests.

## 🔗 Related Videos
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: ChatGPT, Claude, Claude Code, Codex
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Claude, Codex, Gemini
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: ChatGPT, Claude, Gemini, Grok
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Codex, Gemini
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Codex
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Claude Code, Gemini
- [[videos/Agent memory resolved]] — shared: Claude, Claude Code, Codex
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, Claude Code

## Timeline
- `0:00` — The Karpathy Method: why almost everyone prompts Claude wrong
- `0:28` — Layer 1, the spec: the car-wash question every model gets wrong
- `1:53` — Uncovering the real goal instead of just the task
- `3:34` — Layer 2, the verifier: "animals vs. ghosts" — why yelling at AI doesn't work
- `6:33` — Using a second AI model (the Codex plugin) as an independent critic
- `7:38` — Pulling external signal into verification
- `8:48` — Layer 3, the environment: CLAUDE.md, your knowledge base, and custom skills
- `11:52` — Hard guardrails: pre-tool-use hooks vs. soft prompt rules
- `12:36` — The one thing to focus on: understanding over thinking

## Transcript
<details>
<summary>Full transcript</summary>

Austin Marchese breaks down what he learned listening to Andrej Karpathy (former head of AI at Tesla) speak at AISN 2026: almost everyone is prompting Claude wrong, and Karpathy's method for building 10x faster comes down to three layers.

Layer one is the spec. AI models are incredibly smart but still miss something. Karpathy poses a simple question AI gets wrong: if you want to go to a car wash 50m away, should you drive or walk? State-of-the-art models say walk, because it's so close — but the person asking obviously needs the car there to wash it. Testing this himself against Claude, Gemini, Grok, and ChatGPT, Austin got the same wrong answer from all four. This reveals the foundation of the video: AI is brilliant at what can be measured, but for context-driven things it has no signal to act on. The spec is how you deliver your own understanding to Claude in a format it can use. Karpathy doesn't think Claude's plan mode goes far enough — he says he doesn't even like plan mode much; there's something more general where you work with your agent to design a spec that is very detailed.

Building a good spec has three steps. First, uncover your actual goal — "create an end-of-month report" is a task, but the goal is the conclusion or decision the report drives, and AI can never decide that for you; have Claude interview you to identify the real goal. Second, be agile: waterfall (handing over one big task and only seeing the final product) is how most people misuse AI agents; agile specking means a tight scope, a clear checkpoint, reviewing the output, adjusting, and repeating — tell Claude to bias toward smaller, more compartmentalized specs. Third, be precise and use your own brain: the more precise you are, the less AI has to assume, and every assumption is a chance to drift from what you actually want — tell Claude to "verify key decisions explicitly to ensure nothing is missed." Combining these three produces a tightly-scoped, well-thought-out spec aligned with your actual goal — a process Austin calls "modern engineering."

Layer two is the verifier, sitting on top of the spec. Reviewing and verifying AI output is one of the most frustrating parts of using it, because unlike a human it can't grasp non-measurable things. Karpathy's mental model: we're not building animals, we're summoning ghosts. Austin simplifies this: people (animals) are driven by intrinsic motivation — threaten someone's job and they'll figure out SEO in 14 days. AI isn't that; it's more like a robot librarian that can only suggest answers based on the books already in its library, and it doesn't know when it's missing a book, so it may confidently make something up. That's why AI nails math (clear answers exist) but fumbles context (no clear answer exists) — and why yelling at it, pleading, or saying "make this better" doesn't work. The only real lever is verification, focused on three places. First, set evaluation criteria up front with precision — not "make this report look good" but "the report must have three sections, each ending with a recommendation." Second, use a second AI model as the critic — like a second robot librarian from a different library grading the first one's work; tactically, if you use Claude Code, you can install the Codex plugin to ask Codex questions directly within a Claude Code session, and say something like "if this turns into a complex build, run the final output by Codex to ensure both systems agree." Third, pull external signal where possible — e.g. connect your Claude session to the actual system where an app is deployed so it can verify real deployment success, or bring in your own historical reports as a format reference for a monthly report. Claude Code's creator, Boris Cherney, has said that if Claude has a feedback loop, it will 2-3x the quality of the final result.

Layer three is the environment — the workshop that layers one and two live in. The spec is the blueprint pinned to the wall, the verifier is the quality-check station by the door, and the environment is the workshop itself. Most people rebuild this workshop from scratch every time, which is wasteful. Building a proper environment has four steps. First, set up a real CLAUDE.md file — it gets auto-injected every time you prompt Claude, so it's the first thing Claude reads; it should describe how your repo works, your custom skills and how they're routed, your knowledge architecture (where to look for information), and key working rules Claude should always follow. Second, build your own "LLM knowledge base" (a concept Karpathy went viral for) — a folder system of your own reference material that makes it easy for Claude to find information, because your data is your moat. Third, turn anything you do repeatedly into a custom skill — the more you use a skill, the more you discover where it needs fixing, and the system compounds over time ("the best way to find a leak in a hose is to run water through it"). Fourth, create explicit rules for what AI can and can't touch, and match the enforcement to the cost of getting it wrong: a line in CLAUDE.md like "don't touch the /important, don't edit folder" is only a soft request Claude can still bypass — for truly critical constraints, add a pre-tool-use hook that checks the file Claude is about to write or edit and blocks it at the tool level, not just the prompt level. Bucket tasks into always-do (autopilot), ask-first (double-check), and never-do (hard lines).

That's the Karpathy method end to end: the spec, the verifier, and the environment. Karpathy's answer to what's still worth learning deeply as intelligence gets cheap: you can outsource your thinking, but you can't outsource your understanding. All three layers ultimately center on your own understanding of the bigger picture — what your goals are and what's needed to direct AI to work for you.

</details>
