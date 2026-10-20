---
title: "This Agent Team Builds 100s of Features While You Sleep"
video_id: nKiPOxDpcJY
channel: "[[channels/Leon van Zyl]]"
uploaded: 2026-02-05
processed: 2026-07-06
duration: "21:48"
url: https://www.youtube.com/watch?v=nKiPOxDpcJY
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [autonomous-app-development]
tools: [AutoForge, Claude Code, Playwright, n8n, Ollama, SQLite, Node.js, Python, Telegram, Z.AI]
llms: [Claude Opus, Claude Sonnet, Claude Haiku, GLM, Qwen, GPT-OSS-20B]
protocols: [MCP, webhooks]
transcript: true
tags: [youtube, ai-automation]
---

# This Agent Team Builds 100s of Features While You Sleep

![thumbnail](https://i.ytimg.com/vi/nKiPOxDpcJY/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=nKiPOxDpcJY) | 📅 Uploaded [[uploaded/2026-02-05]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A full setup and feature tour of AutoForge, a free open-source tool (1,300+ GitHub stars, born from a UI wrapper around Anthropic's long-running-agent demo) that runs multiple coding agents concurrently against a Kanban/dependency-graph board to autonomously implement dozens to hundreds of app features. The video covers installation, spec generation via a Claude chat, concurrency/regression-testing settings, Mission Control monitoring, and swapping in GLM or local Ollama models plus n8n-based progress notifications.

**Watch this if:** you want to run several AI coding agents in parallel to autonomously build out an entire application's feature list while you're away from the keyboard.

## Key Takeaways
- AutoForge began as a UI layer over Anthropic's own long-running-agent harness demo (which lacked a UI and ran entirely in the terminal) and has since grown into its own project with a Kanban board, dependency graph, and "Mission Control" monitoring view.
- Setup requires Node.js, Python, and the Claude Code CLI installed; install/update via `npm install -g autoforge` (or `npm update -g autoforge-ai`), or clone the GitHub repo and run `start-ui` (or `start` for CLI-only mode without the web UI).
- New projects are defined by chatting with Claude inside AutoForge (quick mode lets Claude pick the stack/architecture; detailed mode lets a technical user drive it), producing an `app_spec` file and a full feature list (35 features in the demo) — this also works against existing codebases.
- Coding agents can test their own work via a Playwright MCP server (toggle headless mode) unless "YOLO mode" is enabled to skip testing for speed.
- Concurrency is configurable: 1-5 parallel coding agents, 1-3 regression-testing agents that re-check previously implemented features and either self-repair or mark them failed for a future agent to fix, plus how many features an agent handles per session before compacting context.
- Only Opus and Sonnet are supported as coding models (Haiku is excluded as "not a good enough coding model"), but editing the AutoForge `.env` file lets you swap the underlying models for GLM (via a Z.AI API key) or fully local Ollama models (e.g. Qwen3 Coder, GPT-OSS-20B) while the UI still shows Sonnet/Opus/Haiku labels.
- An `.env` webhook variable can POST a JSON progress payload to any endpoint (the presenter uses an n8n workflow) to relay feature-completion updates to Telegram or other messaging apps.

## 🛠 Tools & Software
- [[topics/AutoForge]] — the free open-source multi-agent orchestration app the whole video installs, configures, and tours (Kanban board, dependency graph, Mission Control, model switching).
- [[topics/Claude Code]] — the underlying coding-agent CLI AutoForge is built on and requires to be installed and signed in.
- [[topics/Playwright]] — used via an MCP server so coding agents can test their own implementations in a browser (with an optional non-headless mode to watch it work).
- [[topics/n8n]] — used to build the webhook workflow that receives AutoForge's progress notifications and forwards them to Telegram.
- [[topics/Ollama]] — used to run fully local/free models (e.g. Qwen3 Coder) as a drop-in replacement for Claude models.
- [[topics/SQLite]] — the database AutoForge's initializer agent sets up to store the project's features and their dependencies.
- [[topics/Node.js]] — required prerequisite for installing and running AutoForge.
- [[topics/Python]] — required prerequisite for AutoForge.
- [[topics/Telegram]] — the destination for the presenter's personal webhook-based progress notifications.
- [[topics/Z.AI]] — the provider used to generate the API key needed to swap AutoForge over to GLM models.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — the default/recommended coding model in AutoForge.
- [[topics/Claude Sonnet]] — the other supported coding model option in AutoForge's settings.
- [[topics/Claude Haiku]] — explicitly not supported as a coding model, deemed not good enough for the task, though it was auto-selected in an unrelated prior demo.
- [[topics/GLM]] — an alternative, cheaper model swapped in behind the scenes via Z.AI API key, shown consuming usage as agents run.
- [[topics/Qwen]] — used locally via Ollama (Qwen3 Coder) as a free inference option.
- [[topics/GPT-OSS-20B]] — mentioned as another local model option that could be swapped in through Ollama.

## ✅ Action Items
- Install AutoForge with `npm install -g autoforge` (requires Node.js, Python, and Claude Code CLI already set up) and launch it with the `autoforge` command.
- Create a new project and use AutoForge's built-in Claude chat to generate an app spec and feature list in "quick mode," or drive the architecture yourself in "detailed mode."
- Set concurrent coding agents (1-5) and regression-testing agents (1-3), and decide features-per-session to balance speed against context compaction.
- Enable the Playwright MCP testing step (or use YOLO mode to skip it) depending on whether you want agents to verify their own work.
- Edit the `.env` file to try GLM (Z.AI API key) or local Ollama models for free/cheaper inference, and optionally wire up an n8n webhook for phone notifications on feature progress.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Claude Opus, Claude Sonnet, GPT-OSS-20B
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet

## Timeline
- `0:00` — What AutoForge is: origin as a UI over Anthropic's long-running-agent demo, now its own 1,300+-star open-source project.
- `1:01` — UI overview: Kanban board, feature cards, dependency graph, and Mission Control.
- `2:30` — Supported AI models overview (Claude, GLM, Ollama).
- `2:48` — Installing AutoForge via npm, prerequisites (Node.js, Python, Claude Code CLI).
- `5:29` — Creating a new project and chatting with Claude to define features (quick vs. detailed mode).
- `8:14` — Claude generates the app spec file and a 35-feature list; also works on existing projects.
- `9:57` — YOLO mode (skip testing) vs. Playwright MCP-based testing.
- `10:25` — Configuring concurrent coding agents (up to 5) and per-session feature counts.
- `11:02` — Regression-testing agents: re-checking implemented features and self-repairing or flagging failures.
- `12:43` — Starting the build: initializer agent sets up the SQLite features DB and project scaffolding.
- `14:50` — Mission Control: watching Maestro (the orchestrator) assign features to concurrently running agents based on the dependency graph.
- `16:06` — Manually adding a feature (UI rebrand) and watching an agent pick it up; using the AI chat assistant to query/add features via MCP tools.
- `17:53` — Switching to GLM (Z.AI API key) and then Ollama (Qwen3 Coder / GPT-OSS-20B) by editing the `.env` file.
- `20:29` — Setting up webhook-based progress notifications via an n8n workflow forwarding to Telegram.
- `21:21` — Final results and next steps; call to try the free, actively-developed project.

## Transcript
<details>
<summary>Full transcript</summary>

A month earlier, the presenter made a video demonstrating long-running harnesses for coding agents, based on an Anthropic article about an effective harness for long-running agents — the idea being that agents can implement massive projects with hundreds of features, something not doable with a single agent due to context window limits. Anthropic's own sample project ran entirely in the terminal with no UI, making it hard to visualize progress, so the presenter built a UI on top of it with a local database and Kanban board. After release, the project (now renamed AutoForge) gained 1,300+ GitHub stars and an active contributing community, with lots of added functionality since.

AutoForge's Kanban board shows pending, in-progress, and done features; clicking a card shows dependencies and required steps and allows editing. A graph view shows all features and their dependencies. Mission Control shows what the orchestrator agent and each sub-coding-agent are doing, with multiple agents running concurrently on different features. By default AutoForge uses Claude Code, but also supports GLM models and Ollama for free local inference, with more providers planned.

Setup: go to autoforge.cc for docs, star the GitHub repo if you like it. Prerequisites include Node.js, the Claude Code CLI, and Python. The simplest install is a single command (`npm install -g autoforge` style), after which running `autoforge` starts the app; updating uses `npm update -g autoforge-ai`. Alternatively, clone the GitHub repo and run `start-ui.bat`/`.sh`, or run `start.bat`/`.sh` for a pure CLI experience without the web UI (the video uses the web app). You need Claude Code CLI signed in with a Claude account; GLM models (shown later) are a cheaper alternative if you don't want to use Claude.

Navigating AutoForge: light/dark mode and themes are available (the presenter picks a "Claude" theme), plus in-app docs. Creating a new project requires a lowercase-kebab-case name and selecting a target folder (works for both new and existing projects). You choose to either manually edit spec template files or have Claude help define features via an in-app chat. Describing a simple "project management" app idea, Claude asks whether to use quick mode (Claude decides the stack/architecture) or detailed mode (user drives architecture); quick mode is used for the demo, with files optionally attachable (e.g. a design screenshot). Claude proposes 35 features; once accepted, Claude generates specification files, producing an `autoforge` subfolder in the project containing prompts for the coding agent, initializer agent, and tester agents (all editable), plus an `app_spec` file describing the project name, overview, tech stack, prerequisites, security/access control, and core features. For existing projects, Claude first familiarizes itself with the existing codebase before adding an app_spec covering existing plus new features.

By default, agents test their own code using a Playwright MCP server as they work; "YOLO mode" skips testing for speed, but the presenter leaves testing enabled. Before starting, settings let you set concurrent agents (1-5 via a slider — set to 3 in the demo), an optional run schedule, auto-starting a dev server, toggling YOLO mode, and toggling Playwright's headless mode (disable to visually watch the agent's browser interactions). Model choice is Opus or Sonnet (Haiku isn't supported — deemed not a good enough coding model). Beyond coding agents, 1-3 regression-testing agents can re-test already-implemented features to catch regressions from later changes, attempting self-repair or marking a feature failed for a future coding agent to retry. You can also set how many features a coding agent implements per session before its context needs compacting (recommended: one, or maybe two).

Clicking "run" starts the process; a debug window (toggle with "D") shows the underlying Claude Agent SDK's raw output/thought process, and a dev server can be started from the same panel; multiple terminals can also be opened directly. The initializer agent sets up a SQLite database with all features and scaffolds the chosen framework (e.g. React/Next.js) with dependencies installed, visible as a `features.db` file with a dependencies array per feature. Once initialization finishes, Mission Control shows the orchestrator ("Maestro") assigning features to the three concurrently running coding agents based on the dependency graph — features without dependencies get assigned first, sometimes multiple to one agent depending on the features-per-session setting. Individual agent logs and a combined "recent activity" feed show live output streaming in.

Additional features: manually adding a feature (e.g. "rebrand the app," with an optional priority) which an agent then picks up and completes; using the Claude chat to add a batch of new features to an existing project; and a separate assistant chat window that can answer questions about the codebase and has MCP tool access to interact with the features database (e.g. checking whether light/dark mode already exists as a feature rather than duplicating it).

Switching models: editing the AutoForge `.env` file (found in the user's AutoForge folder) reveals commented-out overrides for Google Cloud Vertex, GLM, and Ollama, plus an n8n-webhook variable. Uncommenting the GLM variables and supplying a Z.AI API key (created via Z.AI's API keys page) swaps Claude for GLM behind the scenes (UI still labels models Sonnet/Opus/Haiku) after restarting AutoForge — confirmed by a GLM badge and rising usage percentage as agents run. The same pattern applies to Ollama: uncomment the relevant lines, download the desired local model (e.g. Qwen3 Coder or GPT-OSS-20B), specify its name, and restart — an Ollama logo confirms the switch, and the presenter drops concurrency to one agent since it's running locally.

Finally, uncommenting a webhook `.env` line lets AutoForge POST a JSON payload with project name and completed features to any endpoint — the presenter's own simple n8n workflow receives this webhook and forwards a Telegram notification with progress updates. The video closes with an invite to try the free, actively-developed AutoForge project and join the presenter's "Agentic Labs" community.

</details>
