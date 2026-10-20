---
title: "I Tested Every Claude Code Feature, These 12 Are the Best"
video_id: vfWTyEreOEc
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-06-03
processed: 2026-07-05
duration: "20:14"
url: https://www.youtube.com/watch?v=vfWTyEreOEc
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [claude-code-feature-selection, ai-personal-operating-system]
tools: [Claude Code, Claude Cowork, VS Code, Google Workspace CLI, Glaido, ClickUp, Excalidraw]
llms: [Claude, Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# I Tested Every Claude Code Feature, These 12 Are the Best

![thumbnail](https://i.ytimg.com/vi_webp/vfWTyEreOEc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=vfWTyEreOEc) | 📅 Uploaded [[uploaded/2026-06-03]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> After 500+ hours in Claude's ecosystem, Nate Herk ranks every Claude Code feature from D to S tier and counts down his top 12 — skills, status line, routines, remote control, /loop, sub agents, agent teams, /rewind, auto memory, /insights, ultra plan, and /goal — explaining why each earns its spot for knowledge-work and automation use (not heavy software engineering).

**Watch this if:** you use Claude Code daily and want to know which of its many features are actually worth learning first.

## Key Takeaways
- Rankings are based on how much a feature changes actual day-to-day knowledge-work/automation output, not novelty — heavy software engineers will likely rank these differently.
- #1 Skills are reusable markdown "recipes" stored in `.claude` that make repeatable tasks (Excalidraw presentations, thumbnails, video trims, session handoff) far more consistent than re-prompting every time, shareable across Claude Code/chat/Cowork, and installable as plugins that bundle hooks and MCP servers.
- #2 Status line plus `/context` and `/usage` give constant visibility into model, effort level, and context-window consumption (e.g. Opus 4.8 at 27%/274k of a million tokens) — critical for knowing when to run session handoff, `/clear`, or `/compact`.
- #3 Routines and #4 remote control let you schedule an actual agent session (not a deterministic script) and then drive or check in on a running Claude Code session from your phone.
- #6 Sub agents (parallel, no cross-talk, report only to the main session) and #8 agent teams (personas that debate each other in rounds until they converge) are two distinct multi-agent patterns worth knowing apart.
- #7 `/rewind` rolls conversation and code back to an earlier checkpoint — often a cleaner fix than telling Claude mid-conversation that it got something wrong.
- #12 `/goal` and #11 ultra plan both offload extended or ambiguous work (an objective "definition of done," or cloud-based parallel planning agents) so Claude keeps working while you step away.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the core CLI/terminal agent that every ranked feature belongs to
- [[topics/Claude Cowork]] — Anthropic's other agent surface; ranked C-tier because Claude Code covers nearly everything it does with more capability
- [[topics/VS Code]] — used via the Claude Code IDE extension, mainly for cleaner copy/paste than the terminal
- [[topics/Google Workspace CLI]] — an honorable-mention tool letting the agent navigate Sheets, Docs, Drive, Gmail, and Calendar directly
- [[topics/Glaido]] — a faster voice-to-text alternative to Claude Code's built-in `/voice` dictation
- [[topics/ClickUp]] — mentioned as where most of his non-Google work lives, alongside the Google Workspace environment
- [[topics/Excalidraw]] — used as the example of a skill-driven repeatable task (auto-generating Excalidraw presentations)

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying assistant/brand behind Claude Code, Claude chat, and Claude Cowork
- [[topics/Claude Opus]] — shown in the status line demo as "Opus 4.8," the model in use

## 📡 Protocols & Standards
- [[topics/MCP]] — mentioned as one of the components (alongside hooks) bundled into installable skill plugins

## ✅ Action Items
- Build a library of custom skills for anything you do repeatedly (presentations, thumbnails, video trims, session handoff) instead of re-prompting each time.
- Set up a custom status line and check `/context` and `/usage` regularly to know when to clear, compact, or hand off a session.
- Try `/goal` with an objective "definition of done" instead of a vague instruction, and use `/rewind` instead of correcting Claude mid-conversation.
- Experiment with sub agents for parallel independent work and agent teams for multi-persona debate on the same problem.
- Schedule a real agent routine (not just a script) for a recurring task, and enable remote control so you can check in from your phone.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus, Google Workspace CLI
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Cowork, Claude Opus
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude, Claude Code, ClickUp, VS Code
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Claude Code 2.0 Has Arrived (It's Insane)]] — shared: Claude Code, Claude Cowork, Google Workspace CLI, MCP

## Timeline
- `8:09` — #12: /goal — a clear definition of done, not marathon runtimes
- `10:01` — #11: Ultra plan — offloading big/ambiguous planning to the cloud
- `10:54` — #10: /insights — an HTML report on your last 30 days of usage
- `11:43` — #9: Auto memory — Claude re-reviews and updates its own memory
- `12:18` — #8: Agent teams — multiple personas debating in rounds
- `13:18` — #7: /rewind — rolling code and conversation back to a checkpoint
- `13:47` — #6: Sub agents — parallel background work reporting to the main session
- `14:26` — #5: /loop — repeating a prompt on a local cron-backed interval
- `15:18` — #4: Remote control — driving a session from your phone
- `16:09` — #3: Routines — scheduling an actual agent, not just a script
- `16:45` — #2: Status line — model, effort level, and context usage at a glance
- `17:55` — #1: Skills — reusable markdown recipes for repeatable work

## Transcript
<details>
<summary>Full transcript</summary>

Nate Herk has spent over 500 hours inside Claude's ecosystem — chat, Cowork, and Claude Code — so he ranks every feature from D tier up to S tier and walks through his top 12 in order. The ranking is based on how much each feature changes his actual day doing knowledge work and automation, not global popularity or novelty — since he's not doing heavy software engineering, viewers who are will likely disagree with some placements.

**D tier** (very useful, but nobody's favorite): CLAUDE.md setup (essential groundwork), context lifecycle commands (`/clear`, `/compact`, resuming conversations), native web search/fetch, file uploads, fast mode, permissions, custom themes (`/theme` — auto dark mode, colorblind-friendly, custom themes), and the VS Code IDE extension (useful for those who don't want the terminal).

**C tier** (great, but not used a ton): voice mode (`/voice` for dictation, though a tool like Glaido is faster), Claude Cowork (a great product, but Claude Code covers nearly everything it does with more capability — Cowork is better suited to non-technical users just getting started), interactive connectors (quick logins for tool calls instead of terminal setup), and local file access.

**B tier** (super useful, just missed the top 30): dynamic workflows (token-intensive but great parallel processing; still new, hasn't found its permanent place in his day-to-day), deep research (`/deep research` invokes a dynamic workflow automatically), git worktrees (isolated copies of a codebase for parallel work that merge back together), ultra review (a `/command` that spins up a cloud code review), interactive charts in Claude Chat, the session recap feature (shows what an idle Claude Code session was working on), and quick mentions of Claude for Microsoft 365, Claude in Chrome, and computer use.

**A tier** (honorable mentions, hardest cut from the top 12): the Google Workspace CLI (not a Claude feature itself, but lets his agent navigate Sheets, Docs, Drive, Gmail, and Calendar, with skills built around it); Dispatch (channel-based continuation, letting you talk to Claude from your phone, especially for Cowork/Claude Code sessions); the Claude desktop app (good for managing routines and seeing multiple projects/sessions visually, and for cleaner copy/paste than the terminal); Claude design (used by his team for shared design systems and quick POCs); auto mode as a permission level; ultra code; hooks; effort levels; agent view (a dashboard of all running terminals); asking questions without interrupting the main terminal; `/context`; and prompt caching (saves tokens silently in the background).

**The Top 12:**

**#12 — `/goal`**: tells Claude to keep working until a specific condition is met — e.g. "research the best riddles, don't stop until you find three very hard to solve ones." The key is giving as objective a "definition of done" as possible; you don't need marathon 24-48 hour runs (a common demo trope) — a `/goal` can finish in 43 seconds or, in his real example of optimizing a website's globe element to load instantly, about an hour and a half, and you can walk away with confidence it will actually be done because it includes verification.

**#11 — Ultra plan**: offloads planning to the cloud using multiple planning agents in parallel, useful for big or highly ambiguous tasks (e.g. "help me figure out how to make 5x monthly recurring revenue"). It runs in the cloud on a shareable link while you keep working locally in the terminal.

**#10 — `/insights`**: generates an HTML report on your past ~30 days of Claude Code usage — message/session counts (e.g. 1,500+ messages across 153 sessions), what's working, what's hindering you, quick wins, and ambitious workflows to try, with a table of contents to jump around.

**#9 — Auto memory** (formerly "auto dream"): Claude periodically reviews recent sessions and updates its own memory without being prompted to. Check `/memory` to confirm it's turned on.

**#8 — Agent teams**: an experimental feature (enabled in `.claude` settings) that spins up multiple personas — e.g. a complete beginner and a CEO — to analyze or brainstorm something together, running rounds of debate until they converge, invoked with natural language.

**#7 — `/rewind`**: rolls code and conversation back to an earlier checkpoint. Often better than telling Claude "no, that was wrong, do it this way" — you rewind to the exact prior prompt and redo it cleanly.

**#6 — Sub agents**: background agents that run in parallel and can be invoked automatically or on request; unlike agent teams, sub agents can't talk to each other — they only report back to the main terminal session. They're defined as markdown files in `.claude` alongside skills, rules, and workflows.

**#5 — `/loop`**: repeats a prompt on an interval (e.g. "every minute, remind me to use the restroom"), implemented via a local cron tool tied to that terminal session — closing the terminal kills the cron, and loops auto-expire after 7 days if left running. You can also just describe a recurring loop in natural language instead of typing the slash command.

**#4 — Remote control**: drive a local Claude Code session from your phone or the web. Useful for stepping away (a walk, the gym) while keeping a session running — actions and messages sync between phone and computer in both directions.

**#3 — Routines**: schedule an actual agent session (not a deterministic script) via `/schedule`, viewable and manageable in the desktop app on a calendar or list view, as either local or cloud routines.

**#2 — Status line**: one of the most slept-on features — shows model (e.g. Opus 4.8), effort level, and context-window usage (e.g. 27%, 274,000 of a million tokens) at the bottom of the screen. Fully customizable via `/statusline` (you can even hand Claude a screenshot of what you want shown). Paired with `/context` (visualizing what's eating tokens) and `/usage` (session/weekly stats across models).

**#1 — Skills**: markdown files living in `.claude` that act like recipes — write the steps once (how to do Excalidraw presentations, make thumbnails, trim videos, hand off a session) and Claude follows them consistently instead of needing the same prompt repeated every time. Skills can be simple (a four-sentence session-handoff prompt turned into one slash command) or complex (chained together, using multiple tools), can be built yourself or pulled in from others as plugins bundling skills, hooks, and MCP servers, and work across Claude Code, Claude chat, and Claude Cowork — making this the single feature that gives him the most leverage day to day.

</details>
