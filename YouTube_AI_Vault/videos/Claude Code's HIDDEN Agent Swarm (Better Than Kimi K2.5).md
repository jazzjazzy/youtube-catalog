---
title: "Claude Code's HIDDEN Agent Swarm (Better Than Kimi K2.5?)"
video_id: eRu5kIYAAz8
channel: "[[channels/Better Stack]]"
uploaded: 2026-01-30
processed: 2026-07-06
duration: "6:48"
url: https://www.youtube.com/watch?v=eRu5kIYAAz8
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [multi-agent-orchestration]
tools: [Claude Code, Claude Sneak Peek, BMAD, x-dl]
llms: [Kimi, Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code's HIDDEN Agent Swarm (Better Than Kimi K2.5?)

![thumbnail](https://i.ytimg.com/vi_webp/eRu5kIYAAz8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=eRu5kIYAAz8) | 📅 Uploaded [[uploaded/2026-01-30]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Kimi K2.5's agent-swarm mode lets an orchestrator dynamically spawn up to 100 specialized subagents for a complex task with no manual setup. This video shows that Claude Code has a nearly identical feature hidden behind an undocumented flag — discovered by Mike Kelly and demoed via a fork called Claude Sneak Peek — where an orchestrator automatically creates a growing team of specialized subagents (front-end builder, backend builder, QA tester, etc.) to complete a task.

**Watch this if:** you use Claude Code's custom subagents or task feature and want to know about the dynamic, auto-spawning "swarm" mode Anthropic hasn't shipped publicly yet.

## Key Takeaways
- Kimi K2.5 is an open-source model with benchmarks that beat Opus on some measures, and its standout feature is an agent-swarm mode where an orchestrator dynamically spawns up to 100 specialized subagents for a complex task.
- Claude Code's existing custom subagents (announced last year) require manually defining a role, tools, skills, and permissions — and each subagent only sees a snippet of context, resetting after finishing its task; people work around this by having subagents write findings to shared markdown files.
- Claude Code's newer "tasks" feature can fan work out to subagents in parallel, but those subagents are general-purpose, not automatically matched to specialized custom subagents.
- A hidden flag discovered by Mike Kelly enables a genuine dynamic agent-swarm mode in Claude Code: the orchestrator automatically creates specialized subagents on the fly based on the task, with no manual setup required.
- Demoed via "Claude Sneak Peek" (a fork of Claude Code): asking it to execute a plan spawned a growing team — starting at 5 agents (team lead, QA tester, backend builder, component builder, front-end builder) and expanding to 8 as more specialized work was identified.
- The swarm produces a "swarm project complete" file and a "swarm execution report" listing every specialized agent used, its role, and whether it completed its task.
- The presenter doesn't think Anthropic copied Kimi — more likely they saw implementations like the community Agents repo and BMAD and built a native version — but suspects it's hidden because of unresolved complexity: how should the orchestrator decide whether to reuse a user's existing subagents/skills versus creating new ones?

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose hidden dynamic agent-swarm flag is the subject of this video, compared against its existing custom-subagent and task features.
- [[topics/Claude Sneak Peek]] — a fork of Claude Code (by Mike Kelly) used to demo the hidden swarm feature: reading a plan, generating tasks, and auto-spawning a growing team of specialized subagents.
- [[topics/BMAD]] — referenced as a community multi-agent framework the Claude Code team may have drawn inspiration from.
- [[topics/x-dl]] — the terminal tool (for downloading videos from X/Twitter) used as the example project the demoed agent swarm builds a web front end for.

## 🤖 LLMs Mentioned
- [[topics/Kimi]] — Kimi K2.5, the open-source model whose agent-swarm orchestrator (spawning up to 100 subagents) is the comparison point for Claude Code's hidden feature; its benchmarks reportedly beat Opus in some areas.
- [[topics/Claude Opus]] — referenced as the model Kimi K2.5's benchmarks are compared against.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try Claude Code's existing task feature to fan a job out to general-purpose subagents in parallel and compare against your manually defined custom subagents.
- Look up Mike Kelly's tweet and the `claude-sneakpeek` GitHub repo to try the hidden dynamic agent-swarm flag yourself.
- If experimenting with dynamic subagent spawning, check the generated swarm execution report to see exactly which specialized agents were created and what each did.
- Compare community multi-agent frameworks like the Agents repo and BMAD against Claude Code's native subagent tooling for your own projects.

## 🔗 Related Videos
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: BMAD, Claude Code, Claude Opus
- [[videos/Opus 4.6 + Agent Teams Makes Claude Code Insane]] — shared: Claude Code, Claude Opus, x-dl
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Opus
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Opus
- [[videos/9 NEW Claude Mods that can truly change how you work]] — shared: Claude Code, Claude Opus
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Claude Opus

## Timeline
- `0:00` — Intro: Kimi K2.5's agent-swarm mode vs. a hidden feature in Claude Code.
- `0:30` — Recap of Claude Code's existing custom subagents — manual setup, fresh context each run.
- `1:24` — How Kimi K2.5's agent swarm works: orchestrator dynamically spawns up to 100 specialized subagents.
- `2:05` — Claude Code's task feature fans work to subagents in parallel, but they're general-purpose, not auto-specialized.
- `2:47` — Demo of Claude Sneak Peek: reading a plan, generating tasks, and watching the subagent team grow from 5 to 8 agents.
- `4:58` — Did Anthropic copy Kimi? Presenter's take: more likely inspired by community projects like Agents and BMAD.
- `5:16` — Why this feature is likely still hidden: complexity of deciding when to reuse vs. create subagents and skills.

## Transcript
<details>
<summary>Full transcript</summary>

People are going crazy over Kimi 2.5 — an open-source model with benchmarks that beat Opus in some areas, and an agent-swarm mode where an orchestrator can spawn up to 100 specialized agents for a complex task. But this feature also exists in Claude Code behind a hidden flag, discovered by a user on Twitter. Did Anthropic just steal this idea from Kimi?

Anthropic announced custom subagents last year, and people have used them for specialized tasks since. But subagents only see a snippet of the wider context (they're designed for a specific task), return their data, and reset to a fresh slate — so people implemented memory by having subagents write findings to a markdown file and update a shared context file so other subagents could see where things were left off. You still have to manually create each subagent: role, skills, tools, permissions, and so on.

Kimi's new agent swarm takes this further: the orchestrator dynamically creates a specialized subagent for a specific task with no manual setup. Subagents work in parallel, and when done, hand results back to the orchestrator, which decides if new subagents need spinning up to complete the overall complex task. It's still a research project but already shows big improvements over single-agent workflows — task complexity stays roughly consistent to solve because of parallel subagents.

Honestly, you can kind of already do this in Claude Code with the newish task feature — creating a list of tasks and fanning them to subagents. The problem: those subagents are general-purpose, not specialized, and it's unclear whether Claude automatically assigns tasks to the right custom subagent. But it turns out the Claude team has been working on letting an orchestrator automatically create subagents on the fly based on the task — hidden behind a flag found by Mike Kelly, who demoed it in a tweet linking to a fork of Claude Code called Claude Sneak Peek.

Demo: a plan document describes building a web front end for x-dl, a terminal tool for downloading videos from X/Twitter. With Claude Sneak Peek running (confirmed: no custom subagents currently configured), the presenter asks it to read the plan and create tasks executable by a swarm of subagents, then execute them. It automatically adds a front-end-builder subagent for front-end tasks. Viewing the team shows five agents: team lead, QA tester, backend builder, component builder, and front-end builder, all working simultaneously — each showing live status (QA tester searching for patterns, backend builder reading files, etc.). Drilling into an agent shows its system prompt; the team lead is the main Claude Code orchestrator. As work continues, the team grows to eight agents — adding a components creator, an API server builder, someone doing Vite setup, someone integrating the API, and someone doing CSS. When complete, the swarm produces a project-complete file plus a swarm execution report listing every specialized agent used, its role, and completion status, with full detail on what each agent did.

The presenter doesn't think Anthropic copied Kimi — more likely they saw community implementations like the Agents repo and BMAD and wanted a native version in Claude Code — but understands why it's not released yet. It probably hasn't had the extensive training Kimi's orchestrator has, and things get complicated once a user already has existing subagents: how does the orchestrator decide whether to create a brand-new front-end subagent or reuse the user's own? Skills add more complexity too — should the orchestrator use a user's downloaded skills, or fetch its own more appropriate ones? Before deciding whether to spin up a new subagent, this kind of orchestrator would need to reason over a user's existing agents, tools, and skills — a lot of surface area to get right before shipping.

</details>
