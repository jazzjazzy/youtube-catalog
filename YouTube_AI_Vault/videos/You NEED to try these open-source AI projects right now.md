---
title: "You NEED to try these open-source AI projects right now..."
video_id: sXVbWkoCVaA
channel: "[[channels/Matthew Berman]]"
uploaded: 2026-03-26
processed: 2026-07-05
duration: "14:58"
url: https://www.youtube.com/watch?v=sXVbWkoCVaA
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [ai-coding-agent-tooling, autonomous-company-orchestration]
tools: [Claude Code, Codex, Gstack, Hermes, Open Claw, Superpowers, Paperclip, GitHub]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# You NEED to try these open-source AI projects right now...

![thumbnail](https://i.ytimg.com/vi_webp/sXVbWkoCVaA/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=sXVbWkoCVaA) | 📅 Uploaded [[uploaded/2026-03-26]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A tour of four fast-growing open-source agent projects: Gstack (Y Combinator president Garry Tan's startup-focused prompt/role framework for Claude Code/Codex), Hermes Agent (Nous Research's Open Claw-like personal agent OS with a built-in self-improving learning loop), Superpowers (Obra's TDD/YAGNI/DRY-focused Claude Code plugin, already 115,000 GitHub stars), and Paperclip (a Node.js/React orchestrator that runs a "zero-human company" of AI agents with an org chart, ticketing system, and cost tracking).

**Watch this if:** you want a quick scan of the most-starred new open-source agent frameworks before deciding which to actually try.

## Key Takeaways
- Gstack, by Y Combinator president Garry Tan, packages his startup-advising experience (office hours, CEO review, 10-star product framing referencing Airbnb's Brian Chesky) into individual role-based markdown prompts (engineering manager, senior designer, staff engineer, debugger) that sit on top of Claude Code, Codex, or any coding agent — install by copy-pasting a prompt into Claude Code, then invoke sub-tools like `/office-hours`.
- Gstack is described as a process, not a tool collection — its purpose is fine-tuning your idea and market opportunity before any code gets written, using six "forcing questions" under `/office-hours` to reframe the product first.
- Hermes Agent (Nous Research) is an Open Claw-like framework/personal-agent operating system with a TUI, multi-line editing, chat-app integrations (Telegram, Discord, Slack, WhatsApp, Signal, CLI) via a single gateway, scheduler/cron, and parallel sub-agent delegation — plus direct migration from Open Claw so existing workflows and memories don't have to be rebuilt from scratch.
- Hermes Agent's standout feature is a closed, built-in self-improving learning loop: agent-curated memory with periodic nudges, autonomous skill creation after complex tasks, skills that self-improve during use, and search over its own past conversations to build a deepening model of the user across sessions.
- Superpowers (by Obra, 115,000+ GitHub stars) gives Claude Code a structured development workflow emphasizing TDD, YAGNI, and DRY — it moves through brainstorm (refining rough ideas, exploring alternatives, saving a design doc), work-tree-based parallelization, plan writing, TDD-enforced execution, code review, and branch completion.
- Superpowers installs as a plugin (`claude plugin install superpowers@claude-plugins-official`) rather than a copy-pasted prompt, making it notably easier to set up than Gstack, and exposes its workflow via `/superpowers` sub-commands like `/superpowers brainstorm`.
- Paperclip is open-source orchestration for a "zero-human company" — if Open Claw is an employee, Paperclip is the company: a Node.js server and React UI where you bring your own agents, assign goals, and track work/cost from a dashboard showing an org chart (e.g. a Claude CEO, a Claude CMO, and a CTO overseeing both Claude and Codex engineer agents).
- Paperclip uses atomic work units, a human-team-style ticketing system for issues, token/cost tracking (since this can get expensive fast), and ties all agent work back to a high-level company goal — get started with `paperclip ai onboard --yes`.
- Clear caveat on Paperclip and similar "zero-human company" projects (including the closed-source Pulsia): the odds of actually making money from clicking a button and walking away are low, and rough edges/limitations are likely — treat it as an early, experimental glimpse of where agent orchestration is heading rather than a working business-in-a-box.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent Gstack's role-based prompts and Superpowers' plugin workflow are both built to run inside
- [[topics/Codex]] — named alongside Claude Code as a coding agent Gstack can sit on top of, and shown as one of the engineer agents inside Paperclip's org chart
- [[topics/Gstack]] — Garry Tan's open-source, startup-advising role/process framework (office hours, CEO review, engineering manager, designer, debugger) layered on top of Claude Code or Codex
- [[topics/Hermes]] — Nous Research's Open Claw-like personal agent framework/OS with a built-in self-improving learning loop and chat-app gateway
- [[topics/Open Claw]] — repeatedly used as the comparison point for both Hermes Agent (a close alternative with migration support) and Paperclip (described as "the employee" to Paperclip's "the company")
- [[topics/Superpowers]] — Obra's TDD/YAGNI/DRY-focused Claude Code plugin workflow (brainstorm → work trees → plan → TDD execution → code review), installed via `claude plugin install`
- [[topics/Paperclip]] — the Node.js/React zero-human-company orchestrator with an agent org chart, ticketing system, and cost dashboard
- [[topics/GitHub]] — all four projects' star counts and repos are referenced/browsed directly as evidence of their rapid growth

## 🤖 LLMs Mentioned
- [[topics/Claude]] — shown filling the CEO and CMO agent roles in the Paperclip org-chart demo, and the model Gstack's and Superpowers' prompts are designed to run against

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Try Gstack by copy-pasting its install prompt into Claude Code, then explore its role-based sub-tools like `/office-hours`.
- Consider Hermes Agent if you're already using Open Claw and want to test its built-in self-improving learning loop — migration support means you don't have to rebuild workflows from scratch.
- Install Superpowers via `claude plugin install superpowers@claude-plugins-official` and run `/superpowers brainstorm` before your next coding project.
- If experimenting with Paperclip or similar "zero-human company" tools, go in with realistic expectations — track token/cost spend closely since agent-run orchestration can get expensive fast.

## 🔗 Related Videos
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, GitHub, Gstack
- [[videos/Agent memory resolved]] — shared: Claude, Claude Code, Codex, Open Claw
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, Codex, GitHub, Open Claw
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: Claude Code, Codex, GitHub, Open Claw
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Codex, GitHub
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: Claude, Claude Code, GitHub, Open Claw
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude, Claude Code, Codex, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, GitHub, Superpowers

## Timeline
- `0:00` — Intro: four open-source agent projects shaping where AI is headed
- `0:20` — Gstack: Garry Tan's startup-advising role framework for Claude Code/Codex
- `2:40` — Gstack's office-hours forcing questions and role-based markdown prompts
- `4:35` — Sponsored segment
- `7:45` — Hermes Agent: Open Claw-like framework with a built-in self-improving learning loop
- `10:30` — Superpowers: TDD/YAGNI/DRY workflow plugin for Claude Code, 115,000+ stars
- `12:20` — Paperclip: zero-human company orchestration, org chart, and ticketing
- `14:20` — Closing thoughts: early but rapidly advancing agent orchestration

## Transcript
<details>
<summary>Full transcript</summary>

Four open-source projects showing where agents are headed. First: Gstack, by Y Combinator president Garry Tan, already near 50,000 GitHub stars just weeks after release. Tan has overseen thousands of startups (including Airbnb and DoorDash) and packaged that experience, combined with a goal of giving solo developers the power of a full development team, into a package that layers on top of Claude Code, Codex, or any other coding agent. He quotes Karpathy's remark about not having typed a line of code since December — "how does one person ship like a team of 20?" — as the question Gstack tries to answer. Installation is a simple copy-pasted prompt into Claude Code (which then asks a few questions and permissions), after which typing `/gstack` reveals sub-tools like `/office-hours`, each documented individually. Gstack

is described as a process, not a collection of tools — the goal is fine-tuning your idea and market opportunity before writing any code, drawing on Tan's YC experience: `/office-hours` runs six forcing questions to reframe the product before coding begins, echoing the actual YC office-hours format where founders meet partners for advice. Other roles include CEO review (rethink the problem, aim for a "10-star product," referencing Airbnb's Brian Chesky on why five stars isn't enough), engineering manager, senior designer, design partner, staff engineer, and debugger — each broken into individual markdown prompts that give Claude Code specific lenses through which to view a codebase, rather than relying on one general-purpose agent for everything. Being fully open source means anyone can read the documentation and effectively see how Garry Tan thinks about startups; the project updates frequently despite being a part-time effort alongside his full-time YC role, and is starting to accept outside contributors. [Sponsored segment: Microsoft 365 Copilot, discussed via the presenter's own use of it for research, document review, and automation to help a small team punch above its weight.] Next: Hermes

Agent by Nous Research, already at 13,500+ stars within days of release. Described as Open Claw-like but especially good at self-improving, Hermes Agent is a full framework/personal-agent operating system rather than just a coding agent or assistant — a strong alternative for anyone already deep into Open Claw. Features include a terminal UI (multi-line editing, command autocomplete, conversation history, interrupt-and-redirect, streaming tool output) and — mirroring what Open Claw popularized — chat-app integrations across Telegram, Discord, Slack, WhatsApp, Signal, and CLI through a single gateway. What sets it apart, in a lineage of self-improving-loop projects inspired by Andrej Karpathy's "auto research" work, is a closed learning loop: agent-curated memory with periodic nudges, autonomous skill creation after complex tasks, and skills that self-improve during use — described as the only agent with a built-in learning loop, creating skills from experience, persisting knowledge, searching its own past conversations, and building a deepening model of the user over time. It also carries Open Claw's

usual feature set (scheduler/cron, parallel sub-agent delegation, run anywhere locally/cloud/hybrid) plus a migration path from Open Claw so existing workflows and memories don't need to be rebuilt from scratch — a genuinely useful feature, and a hint that the industry may need a standard for testing agents without starting from zero each time. Next, the most popular of the four: Superpowers, at 115,000 GitHub stars, by author Obra, which "gives Claude Code superpowers." Similar in spirit to Gstack but far more development-focused, its self-description is memorable: it produces implementation plans clear enough for "an enthusiastic junior engineer with poor taste, no judgment, no project context, and an aversion to testing" to follow. It emphasizes TDD (test-driven development), YAGNI (you aren't gonna need it), and DRY as core coding-best-practice patterns. Its

workflow: brainstorm (activated before writing code, refining rough ideas, exploring alternatives, presenting design in sections for validation, saving a design document — echoing Gstack's and YC office-hours' idea-refinement step in a different flavor), then git worktrees by default for parallelized coding agents, then plan-writing, TDD-enforced plan execution, code review, and finishing the branch. Unlike Gstack, Superpowers installs as a plugin (`claude plugin install superpowers@claude-plugins-official`), making setup noticeably simpler — running `/superpowers` reveals its tools, and `/superpowers brainstorm` walks through its idea-refinement workflow step by step. Finally, arguably the most interesting: Paperclip, at 33,000 stars, aiming to be an entire AI-run, zero-human company. A caveat up front: expecting to make real money by simply running one of these zero-human-company projects is unrealistic without real effort — this is not a "click go and wake up rich" tool, and the same skepticism applies to similar closed-source projects like Pulsia (Ben Sara's "AI that runs your company while you sleep"). Rough edges and

real limitations are likely in this whole category, so treat it as a glimpse of what's coming rather than a finished product. Paperclip itself is open-source orchestration for zero-human companies — if Open Claw is an employee, Paperclip is the company: a Node.js server and React UI orchestrating a team of AI agents, letting you bring your own agents, assign goals, and track work and cost from a single dashboard. The demo shows a polished org-chart UI where the engineering team automatically picks up issues and builds them out — a Claude-powered CEO agent, a Claude-powered CMO agent, and a CTO overseeing two engineers (one Claude, one Codex), all across multiple projects. All work is atomic,

token/cost spend is tracked (since this can get expensive fast), and a human-team-style ticketing system handles issue submission, building, and deployment, all tied back to a high-level company goal the agents continuously reference. Getting started is a single command: `paperclip ai onboard --yes`. The roadmap includes a plugin system (knowledge base, custom tracing queues), Open-Claw-style agents you can chat with directly via Telegram, full company export/import via `companies.sh`, a skills manager, scheduling routines, and better budgeting. It's a very cool but experimental project the presenter hasn't personally tested yet, though others have reported good results — again, not a path to overnight money, but a real signal of where agent capability and the harnesses around them are heading. Being early and experimenting with these projects now offers a meaningful advantage over people still just using ChatGPT for basic Q&A.

</details>
