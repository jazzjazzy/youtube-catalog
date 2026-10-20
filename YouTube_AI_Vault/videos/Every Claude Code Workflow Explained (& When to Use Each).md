---
title: "Every Claude Code Workflow Explained (& When to Use Each)"
video_id: 38t5UBCa4OI
channel: "[[channels/Simon Scrapes]]"
uploaded: 2026-04-07
processed: 2026-07-05
duration: "17:49"
url: https://www.youtube.com/watch?v=38t5UBCa4OI
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-multi-agent-orchestration, agentic-workflow-design]
tools: [Claude Code, VS Code, GSD, Ralph Loop]
llms: [Claude, Claude Haiku, Claude Sonnet, Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Every Claude Code Workflow Explained (& When to Use Each)

![thumbnail](https://i.ytimg.com/vi/38t5UBCa4OI/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=38t5UBCa4OI) | 📅 Uploaded [[uploaded/2026-04-07]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A structured breakdown of five escalating Claude Code agentic patterns — sequential flow, the operator (parallel terminals/worktrees), split & merge (in-session sub-agents), agent teams (experimental cross-communicating agents), and headless (fully autonomous, unattended runs) — plus the three built-in sub-agents (explore, plan, general-purpose) Claude Code already uses behind the scenes in every conversation.

**Watch this if:** you only ever use Claude Code as one long back-and-forth conversation and want to know when to escalate to parallel or autonomous workflows.

## Key Takeaways
- Claude Code already uses three built-in sub-agents automatically: `explore` (runs on Claude Haiku, read-only file search, keeps main context clean), `plan` (activates in plan mode, also read-only, researches the codebase before proposing a strategy), and `general-purpose` (runs on Claude Sonnet, full read/write tool access, used for complex multi-step tasks) — each with its own separate context window.
- Pattern #1, Sequential Flow: one terminal, one growing conversation where each task builds on the last; it's capped by the context window, and long sessions eventually hit "context rot" — mitigated with well-structured CLAUDE.md/skills and `/clear`/`/compact`.
- Pattern #2, The Operator: multiple terminal windows, each its own isolated Claude instance/git worktree (`claude -w "task"`), used for independent tasks that don't depend on each other; you manually coordinate and merge, and Claude auto-cleans unused worktrees on window close — practically caps out around 4-5 terminals before coordination gets unwieldy.
- Pattern #3, Split & Merge: within a single session, Claude itself fans a task out to multiple sub-agents (built-in or custom, defined in `.claude/agents`) running in parallel, then merges their results — capped at 10 concurrent sub-agents (additional ones queue), and sub-agents can only report to the main agent, never talk to each other directly (hub-and-spoke), enabling patterns like a builder-validator review chain.
- The GSD ("Get Sh*t Done") framework by Tash is a planning framework built on this pattern — it splits a project brief into subtasks with named agents (each with its own description, context, and tool access) that Claude routes work to automatically or on request.
- Pattern #4, Agent Teams: an experimental (Claude Opus 4.6 research preview, enabled via a `settings.json` environment flag) pattern where teammates share a task list, message each other directly, and coordinate without funneling through a team lead — genuinely powerful for cross-collaborating roles (e.g., frontend/backend/testing developers) but uses an estimated 4-7x more tokens than a single session, so reserve it for tasks sub-agents genuinely can't handle.
- Pattern #5, Headless: fully autonomous, no terminal interaction, run via `claude -p "prompt"` with full permissions and no approvals — becomes powerful when scheduled via cron/Task Scheduler for unattended jobs (e.g., a daily morning report, transcript-to-social-posts pipeline); best restricted to easily verifiable, easily undoable tasks, optionally scoped with `--allow-tools`, and can be pushed further with self-iterating loops like the "Ralph Loop."
- General rule of escalation: use the simplest pattern that solves the task — most work doesn't need agent teams, and headless/autonomous runs should only handle work whose output is trivial to verify.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose five escalating agentic patterns (sequential, operator, split & merge, agent teams, headless) and three built-in sub-agents are the entire subject of this video
- [[topics/VS Code]] — the editor shown hosting multiple terminal windows/git worktrees for the operator pattern
- [[topics/GSD]] — the "Get Sh*t Done" planning framework by Tash, built on the split & merge / named sub-agent pattern for large (non-enterprise) projects
- [[topics/Ralph Loop]] — mentioned as a community technique that repeatedly re-feeds the same prompt so Claude iterates on its own headless output until it's correct, used to ship entire projects overnight

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model family powering Claude Code across all five patterns discussed
- [[topics/Claude Haiku]] — powers the built-in `explore` sub-agent, chosen for being Anthropic's fastest/cheapest model for read-only file search
- [[topics/Claude Sonnet]] — powers the built-in `general-purpose` sub-agent used for complex, full-tool-access multi-step work
- [[topics/Claude Opus]] — the experimental Agent Teams pattern shipped as a research preview with Opus 4.6

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Watch your terminal's context bar during long sequential sessions and reach for `/clear`/`/compact` or well-structured skills/CLAUDE.md before context rot sets in.
- Use `claude -w "task"` to spin up isolated git-worktree sessions for independent tasks (the operator pattern) instead of letting one conversation's context balloon.
- Let Claude's built-in split & merge handle parallelizable research/analysis tasks (e.g., "research 5 competitors") rather than doing them sequentially yourself.
- Only enable the experimental Agent Teams flag for genuinely cross-collaborative, complex projects — expect 4-7x the token cost of a single session.
- Reserve headless (`claude -p`) runs for easily verifiable, easily reversible tasks, and scope permissions with `--allow-tools` before scheduling anything via cron.

## 🔗 Related Videos
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Never hit Claudes Usage Limit Again]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet

## Timeline
- `0:00` — Intro: why one-conversation-at-a-time is the wrong way to use Claude Code
- `0:45` — Claude's Built-in Sub-Agents (explore, plan, general-purpose)
- `2:44` — Pattern #1: Sequential Flow
- `4:38` — Pattern #2: The Operator (parallel terminals/worktrees)
- `7:34` — Pattern #3: Split & Merge (in-session sub-agents, GSD framework)
- `11:50` — Pattern #4: Agent Teams (experimental, cross-communicating agents)
- `14:22` — Pattern #5: Headless (autonomous, scheduled, Ralph Loop)

## Transcript
<details>
<summary>Full transcript</summary>

Most people use Claude Code one conversation at a time, waiting for each task to finish before moving to the next — but Claude Code is built to work more like a coordinated team, running things in parallel and bringing in specialists as needed. This video covers five ways to use it, from simple to fully hands-off.

Even in a basic conversation, Claude Code already uses built-in sub-agents automatically. `explore` is a fast, cheap, read-only scout running on Claude Haiku (Anthropic's fastest/cheapest model) — it searches files and folder structures but can't change anything, spinning up behind the scenes (visible in the terminal) to keep the main conversation's context clean. `plan` activates in plan mode (`/plan` or shift-tab twice) and similarly researches the codebase read-only, in its own context window, before presenting a strategy. `general-purpose` runs on Claude Sonnet with full read/write tool access, handling complex multi-step tasks that require both exploring and making changes — Claude decides automatically which sub-agent to route to based on task complexity, each with its own separate context window so the main conversation never bloats.

Pattern #1, Sequential Flow: one terminal, one Claude Code session, where each task builds on the growing shared context (e.g., build a landing page, then add a hero image, then add a contact form). Even here, Claude may spin up explore/plan/general-purpose sub-agents behind the scenes to offload context. The ceiling is the context window (shown by the terminal's green bar) — the longer the session runs, the more it accumulates, eventually causing "context rot" where Claude starts forgetting or failing to find things. Well-structured CLAUDE.md and skills, plus `/clear` and `/compact`, help manage this, but eventually you hit a wall.

Pattern #2, The Operator: you act as orchestrator across multiple terminal windows, each running its own isolated Claude instance with its own context window — ideal for independent tasks (e.g., a new onboarding flow, a checkout bug fix, and a settings page redesign) that don't depend on each other. Claude Code has a built-in flag for this: `claude -w "task description"` in each terminal creates a separate git worktree (an isolated copy of the project with its own branch) per task, visible under the `.claude` folder. Each stays clean of context rot from the others; you check in on each, coordinate/copy findings between them, and decide when to merge back. Closing a worktree session triggers automatic cleanup (or asks what to do if there's unmerged work to keep). This pattern practically caps out around 4-5 terminals before manual coordination becomes unwieldy.

Pattern #3, Split & Merge: within a single Claude Code session, Claude itself splits a task across multiple sub-agents running in parallel, then merges the results — the built-in explore/plan/general-purpose sub-agents are examples, but you can also define custom sub-agents in your `.claude` folder. Given a task, Claude recognizes it can be broken into independent pieces, fans out to sub-agents (each with its own context, focused on one piece), and merges results automatically — e.g., researching 5 competitors by spinning up 5 sub-agents in parallel instead of one at a time. The concurrent limit is 10 sub-agents at once (Boris Cherny of Anthropic has mentioned spinning up 15, but additional ones beyond 10 queue). Critically, sub-agents can only report to the main agent — they can't talk to each other (hub-and-spoke). The GSD ("Get Sh*t Done" by Tash) framework builds on this pattern for large (but non-enterprise) projects, splitting a brief into subtasks handled by named agents, each with its own description, context, and tool access, that Claude routes to automatically or on request. One powerful application is the builder-validator chain: one sub-agent builds something, passes results back to the main agent, which routes it to a second sub-agent to review — giving a built-in quality check without manual review, all funneled through the main agent since sub-agents can't communicate directly.

Pattern #4, Agent Teams: addresses split & merge's limitation that sub-agents can't talk to each other. An agent team shares findings, challenges each other, and adapts together via a shared task list rather than only reporting to a team lead — agents know what teammates are doing and can message each other directly. This is the newest, most advanced coordination pattern, still experimental (shipped as a research preview with Opus 4.6), requiring a `settings.json` environment flag (`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`) to enable. Unlike sub-agents, you must explicitly request an agent team in your prompt (describing the task and team structure, or letting Claude determine structure); Claude then spawns and coordinates teammates, each a full Claude Code instance with its own context window (seeded from the shared task list and team lead). You can navigate between teammates in the terminal (shift up/down) and message any teammate directly, bypassing the team lead. Token cost is roughly 4-7x a single session due to the cross-agent back-and-forth, so it should only be used when sub-agents or a single session genuinely can't do the job (e.g., a frontend developer, backend developer, and testing developer that need to communicate as they build) — not just as a way to produce large volumes of work quickly, since the work still needs to be the right work.

Pattern #5, Headless: fully autonomous operation with no terminal interaction, no back-and-forth, and no human in the loop — run via `claude -p "prompt"` with full permissions and no approval prompts, returning a result (e.g., a `report.json`) when done. This becomes especially powerful when scheduled via cron or a Windows/Mac scheduler (e.g., "every day at 7am, fire this command") to create fully unattended workflows — reviewing yesterday's work and writing a morning report, or pulling a video transcript and generating social media posts, with skills invoked automatically. The major limitation is trust: since you're not checking each step, this works best for tasks whose output is easy to verify and easy to undo; guardrails like `--allow-tools` can restrict what it's permitted to do (e.g., read-only). Some in the community push this further with the "Ralph Loop" — repeatedly feeding the same prompt back in so Claude iterates on its own prior work until it gets it right, used to ship entire projects overnight.

That's five agentic patterns for Claude Code — use the simplest one that solves your task, and reserve agent teams and headless autonomy for genuinely complex or easily-verified work respectively.

</details>
