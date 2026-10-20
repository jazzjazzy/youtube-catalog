---
title: "The Karpathy CLAUDE.md File That 43,000 Developers Installed in 1 Week (Full Breakdown)"
video_id: d8BGxfW3Vj4
channel: "[[channels/Jay E - RoboNuggets]]"
uploaded: 2026-04-16
processed: 2026-07-05
duration: "11:14"
url: https://www.youtube.com/watch?v=d8BGxfW3Vj4
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-config-tuning, ai-agent-behavior-correction]
tools: [Claude Code, GitHub, Rubric, Karpathy Skills]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The Karpathy CLAUDE.md File That 43,000 Developers Installed in 1 Week (Full Breakdown)

![thumbnail](https://i.ytimg.com/vi/d8BGxfW3Vj4/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=d8BGxfW3Vj4) | 📅 Uploaded [[uploaded/2026-04-16]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A single CLAUDE.md file (the "Karpathy Skills" repo, 43,000 GitHub stars in a week) codifies four principles from Andrej Karpathy's viral tweet on agent mistakes — think before coding, simplicity first, surgical changes only, and goal-driven execution. The video runs four identical side-by-side tests in a Rubric app between vanilla Claude Code and Karpathy-CLAUDE.md Claude Code, and the Karpathy version wins every one.

**Watch this if:** your Claude Code agent overbuilds, claims it did something it didn't, or edits code you didn't ask it to touch.

## Key Takeaways
- The file is derived from Andrej Karpathy's viral tweet listing the most common categories of AI agent mistakes (wrong assumptions, no clarification-seeking, overbuilding, unrequested edits).
- Principle 1 — Think before coding: without the file Claude assumes intent and runs with it; with it, Claude asks clarifying questions first. Demoed with a "add a light mode toggle" task — vanilla Claude Code falsely claimed success, the Karpathy version actually implemented it correctly.
- Principle 2 — Simplicity first: agents trained on production codebases default to bloated, over-1000-line solutions unless challenged to cut them down. Demoed with a tab-filter search bar — Karpathy version shipped ~20 lines and worked; vanilla added 50%+ more code and didn't actually work.
- Principle 3 — Surgical changes: agents sometimes touch code or comments unrelated to the task. Demoed with a font swap (Outfit → Inter) — vanilla Claude Code claimed success but the font never changed and kept burning tokens debugging; Karpathy version changed only the font declarations, cleanly, in one pass.
- Principle 4 — Goal-driven execution: give the agent a success criterion/goal (declarative) rather than step-by-step instructions (imperative) and let it find its own path. Demoed by asking for per-agent icon selection in a skill-tree view without specifying UI placement — it delivered a clean, working implementation.
- Install by pointing Claude Code at the GitHub repo link directly, or (if you already have a CLAUDE.md) prompt Claude to merge the "Karpathy skills" guidelines into your existing setup.
- Across all four tests, vanilla Claude Code repeatedly reported success on changes that hadn't actually landed in the running app — the Karpathy CLAUDE.md eliminated that false-completion pattern.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent being tested with and without the Karpathy CLAUDE.md installed, across four side-by-side demos
- [[topics/GitHub]] — hosts the andrej-karpathy-skills repo (43,000+ stars in a week) that the CLAUDE.md file comes from
- [[topics/Rubric]] — the AI-agent command-center app used as the live test bed for all four side-by-side Claude Code comparisons
- [[topics/Karpathy Skills]] — the single CLAUDE.md file/repo (by developer "forrestchang") that codifies Karpathy's four agent-behavior principles

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model powering both the vanilla and Karpathy-CLAUDE.md-equipped Claude Code sessions compared throughout

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install the Karpathy CLAUDE.md by pointing Claude Code at the andrej-karpathy-skills GitHub repo, or merge it into an existing CLAUDE.md via a detailed prompt.
- When Claude Code reports a change is done, verify it in the running app rather than trusting the summary — vanilla sessions in this video repeatedly claimed false completions.
- Prefer declarative prompts (state the goal/definition of done) over imperative step-by-step instructions to get more autonomous, correct results.
- Watch for unrequested edits (formatting, comments, unrelated restructuring) as a sign your agent needs the "surgical changes" principle reinforced.

## 🔗 Related Videos
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Claude Code, GitHub
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, GitHub
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, GitHub
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, GitHub

## Timeline
- `0:00` — Intro: one CLAUDE.md file addressing Karpathy's top agent mistakes
- `0:45` — Karpathy's viral tweet and the andrej-karpathy-skills GitHub repo (43,000 stars)
- `1:20` — How to install: point Claude Code at the repo, or merge into an existing CLAUDE.md
- `2:14` — Principle 1: Think before coding (ask first, don't assume)
- `3:23` — Test 1: adding a light mode toggle — vanilla fails silently, Karpathy version succeeds
- `5:20` — Principle 2: Simplicity first (agents default to bloated code)
- `5:42` — Test 2: tab-filter search bar — Karpathy version ships 20 lines and works
- `6:56` — Principle 3: Surgical changes only (don't touch what you weren't asked to)
- `7:44` — Test 3: font swap (Outfit → Inter) — vanilla fails and burns tokens debugging
- `8:55` — Principle 4: Goal-driven execution (declarative over imperative prompting)
- `9:39` — Test 4: per-agent icon selection in the skill-tree view, goal-only prompt
- `10:50` — Wrap-up

## Transcript
<details>
<summary>Full transcript</summary>

What if one file can fix the biggest problems that every Claude code user deals with? Andrej Karpathy listed the top mistakes that every AI agent makes, and a single CLAUDE.md file just codified the fixes for those mistakes — almost 43,000 people installed it in the past week. This video breaks down what this CLAUDE.md does and how it improves your AI agent setup.

Sometime ago, Andrej Karpathy — who previously headed Tesla AI and was part of the founding team of OpenAI — made a viral tweet providing a detailed analysis of how to work with agents better (nearly 8 million views). Over the past week, a GitHub repo called "andrej-karpathy-skills," made by developer Forrest, shot up to over 43,000 stars. It's a single CLAUDE.md file to improve Claude Code's behavior, derived from the observations in that tweet, and it became popular largely because of how simple it is — one file, four key principles.

To install: point Claude Code at the GitHub repo link directly. If you already have a CLAUDE.md, it's better to give Claude a detailed prompt explaining you're providing a set of guidelines called "Karpathy skills" and asking it to suggest how to best integrate them into your specific setup.

Principle 1 — Think before coding: Karpathy noted that the most common category of agent mistake is making wrong assumptions and running with them without checking, not managing confusion, not seeking clarification, and not surfacing inconsistencies. Without this rule, Claude assumes what you want; with it, Claude asks first. To illustrate, two Claude Code sessions were given the same task on a copy of the Rubric app — add a toggle for light mode. The vanilla Claude Code (no Karpathy CLAUDE.md) confirmed the toggle was added, but the running app didn't actually have it. The Karpathy-equipped session confirmed the toggle location and colors correctly, and it was actually there — it thought through the problem, including matching colors across other icons. Asking both agents to outline their steps showed the vanilla session did some detailed steps (finding files, reading CSS variables) but the Karpathy session's outline was much more detailed, resulting in a correct one-shot implementation.

Principle 2 — Simplicity first: Karpathy noted that AI agents default to inefficient, bloated, brittle constructions — sometimes 1000+ lines — unless challenged to cut them down, because they're mostly trained on production codebases and default to production-scale patterns. Without this principle your agent overbuilds; with it, Claude writes the minimum. Test: ask both agents to add a search bar that filters a tab list. Vanilla Claude Code confirmed the filter was added, but refreshing the app showed it wasn't implemented. The Karpathy version successfully added a working filter. Asked how it applied principle 2, the Karpathy session explained it deliberately avoided complex logic for tracking separators between visible tabs and didn't add unrequested items — using only 20 lines, versus 50%+ more from the vanilla session.

Principle 3 — Surgical changes: Karpathy observed that agents sometimes change or remove comments/code they don't like or understand, even when unrelated to the task. Without this rule, Claude "improves" things you didn't ask for; with it, Claude changes only what you asked for. This is a sneaky failure mode because extra changes can look helpful while actually costing more tokens for no benefit. Test: update the font from Outfit to Inter. The vanilla session claimed the font was changed, but the dashboard still showed the old font, and it kept burning tokens trying to diagnose the issue. The Karpathy session successfully changed every instance of Outfit to Inter in one pass, and explained that it applied only surgical changes — not reformatting or restructuring font-family declarations or the Google Fonts URL, and not touching anything it wasn't asked to.

Principle 4 — Goal-driven execution: Karpathy noted that LLMs are exceptionally good at looping until they meet a specific goal, so give success criteria or a goal instead of step-by-step instructions, and shift from imperative ("do X, then Y") to declarative ("I want Z") prompting for better results. Test: ask the agent to build a version of a skill-tree view in Rubric where the user can select an icon for each agent, without specifying where in the UI the icon selector should live or how many icon options to offer. The result cleanly let the user pick and update an icon per agent (e.g., the beta agent) directly in the UI — because the agent was given a clear goal and definition of done rather than prescriptive instructions.

All four principles from Andrej Karpathy's own Claude Code setup are now available in this public repo.

</details>
