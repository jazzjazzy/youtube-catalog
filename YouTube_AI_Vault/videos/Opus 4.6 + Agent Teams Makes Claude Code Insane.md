---
title: "Opus 4.6 + Agent Teams Makes Claude Code Insane"
video_id: LZyWuPqvvjU
channel: "[[channels/Better Stack]]"
uploaded: 2026-02-07
processed: 2026-07-06
duration: "4:52"
url: https://www.youtube.com/watch?v=LZyWuPqvvjU
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [multi-agent-coding]
tools: [Claude Code, tmux, iTerm2, OpenCode, x-dl]
llms: [Claude Opus, Claude Haiku]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Opus 4.6 + Agent Teams Makes Claude Code Insane

![thumbnail](https://i.ytimg.com/vi_webp/LZyWuPqvvjU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=LZyWuPqvvjU) | 📅 Uploaded [[uploaded/2026-02-07]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Claude Code's "Agent Teams" feature — previously an unofficial hack — has been officially released under an experimental flag, letting a team lead spawn multiple teammate agents (each with an independent Claude context) that can talk to each other, share a task list, and even challenge each other's approaches. The video demos building a web UI for the x-dl Twitter-video-downloader tool with a front-end and designer teammate, viewable via tmux split panes, and compares the feature against sub-agents and OpenCode's existing parallel-agent support.

**Watch this if:** you want to understand what Claude Code's officially released Agent Teams feature does differently from sub-agents, and whether the token cost is worth it.

## Key Takeaways
- Agent Teams requires Claude Code version 2.1.32+ and an experimental flag added to `settings.json`.
- Unlike sub-agents (which only report summaries back to a single main agent), teammates in Agent Teams run as independent Claude instances, communicate with each other, and share a task list — using far more tokens as a result.
- Teammates can be viewed and interacted with live via tmux (or iTerm2) split panes, or in a single switchable window when run outside tmux.
- In the demo, a team lead read a plan, created tasks, and spawned a front-end teammate and a UI/designer teammate to build a web interface for x-dl (a Twitter video downloader), which worked end-to-end (paste tweet URL, download, view video).
- The team lead automatically selected Haiku as its own model for the run without being explicitly told to, and each project gets a `.claude/teams/<project>/<branch>/config.json` recording the team lead and model used.
- Using two teammates (excluding the lead) on one Opus 4.6 run consumed 29% of the presenter's usage (~13,000 tokens), making the presenter cautious about routine use versus reserving it for research or agent-checking-agent verification tasks.
- Parallel/multi-agent orchestration isn't unique to Claude Code — OpenCode and other agent harnesses have supported similar patterns for a while.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose newly officially-released Agent Teams feature is demoed end-to-end.
- [[topics/tmux]] — used to view each teammate agent in its own split pane during the live demo.
- [[topics/iTerm2]] — mentioned as an alternative terminal for the same split-pane teammate view.
- [[topics/OpenCode]] — cited as already having supported parallel-agent workflows before Claude Code's Agent Teams.
- [[topics/x-dl]] — the open-source Twitter video downloader tool the demo adds a web interface to via the spawned teammates.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4.6, the model driving the demo and the one whose token usage (29% for two teammates) is called out as costly.
- [[topics/Claude Haiku]] — the model the team lead auto-selected for itself during the run, apparently chosen as best for that role without explicit instruction.

## ✅ Action Items
- Upgrade to Claude Code 2.1.32+ and add the Agent Teams experimental flag to `settings.json` to try the feature.
- Run a team inside tmux (or iTerm2) split panes to watch each teammate's live progress and intervene directly if needed.
- Check `.claude/teams/<project>/<branch>/config.json` after a run to see which model the team lead selected.
- Reserve Agent Teams for token-heavy use cases like independent research or having one agent double-check another's work, rather than everyday coding, given the token cost versus sub-agents.

## 🔗 Related Videos
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Claude Opus, OpenCode, iTerm2
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus
- [[videos/Claude Code CMUX The Ultimate AI Coding Terminal]] — shared: Claude Code, Claude Haiku, OpenCode
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus
- [[videos/Claude Code's HIDDEN Agent Swarm (Better Than Kimi K2.5)]] — shared: Claude Code, Claude Opus, x-dl

## Timeline
- `0:00` — Intro: Agent Teams (formerly a hidden/hacked feature) is now officially released with docs and teammate-to-teammate communication.
- `0:28` — Explaining how Agent Teams works: version requirement (2.1.32+) and the settings.json flag needed.
- `1:00` — Demo setup: a plan to add a web interface to x-dl, spawning a front-end and a designer teammate.
- `1:15` — Using tmux split panes to watch each teammate's work live, with the ability to send them commands directly.
- `2:20` — Team finishes; the resulting web UI is tested by downloading a tweet's video.
- `2:35` — Inspecting `.claude/teams/` config.json, showing the team lead auto-selected Haiku as its model.
- `2:45` — Running the same prompt outside tmux, showing the single-window switchable teammate view instead.
- `3:30` — Comparing Agent Teams vs. sub-agents: independent contexts and shared task lists vs. summarized single-context communication.
- `4:00` — Final thoughts: token cost concerns (29% usage for two teammates on Opus 4.6), and noting OpenCode already had parallel-agent support.

## Transcript
<details>
<summary>Full transcript</summary>

Last week's video covered Claude Code's "agent swarm" feature, where specialized sub-agents communicate back to a main orchestrator/team lead — back then a hidden feature exposed via clever hacking. Now it's officially released under an experimental flag with official docs, team-up support, and the ability for teammates to challenge and argue with each other. Anthropic has been busy this week (Opus 4.6, Super Bowl ads), but Agent Teams is called one of the biggest Claude Code features, combining the earlier tasks feature with parallel sub-agents — and teams are said to be much better than sub-agents alone.

To use Agent Teams you need Claude Code version 2.1.32 or above, plus a line added to `settings.json` in the Claude directory. The demo: a plan to add a web interface to a tool called x-dl, which downloads videos from Twitter. The agents are told to read the plan, create tasks, and spawn a front-end and a designer teammate. The demo runs inside tmux, since agents can use tmux (or iTerm2) to create split panes showing exactly what each teammate is doing. After hitting enter, the team lead reads the plan and creates tasks before spawning teammates in parallel — a front-end teammate and a UI-styling teammate appear in their own panes, and the presenter can interact with each teammate directly, giving specific commands as they work. Once a teammate finishes, the main team lead automatically shuts it down; once both are done, the resulting web UI is tested by pasting a tweet URL, hitting download, and viewing the extracted video in browser.

Looking in the `.claude/teams` directory reveals a folder per project/branch containing a `config.json` with the project, the team lead, and the model the team lead used — in this run, Haiku, chosen automatically without being explicitly requested, apparently as the best fit for that role. Running the same prompt outside tmux shows a similar flow but in one window with a switcher between team members (designer, front-end developer, main lead) instead of separate panes; pressing enter on a member shows exactly what they're doing and allows direct communication. When a teammate finishes, they're shut down and the team lead summarizes completed tasks.

Comparing to sub-agents: agent teams get independent contexts, and teammates communicate with each other and share a task list, whereas sub-agents only report to the main agent, which manages everything and receives summarized results. Because teammates are separate Claude instances, they use far more tokens. The presenter notes that while officially released, they don't expect to use Agent Teams often — the cost of Anthropic models plus heavy token usage make it better suited to special cases like research or having one agent check another's work. As evidence, two teammates (excluding the main one) consumed 29% of the presenter's usage on Opus 4.6, around 13,000 tokens. It's also noted that parallel agents aren't new — OpenCode and other agent harnesses have had this for a while — so it'll be interesting to see how Claude Code users adopt Agent Teams, especially given tmux's less-than-friendly shortcuts.

</details>
