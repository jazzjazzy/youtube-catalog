---
title: "Multica: The Open Source Tool That Makes Claude Code 10x Better"
video_id: WdGSXQPwwmo
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-21
processed: 2026-07-05
duration: "9:57"
url: https://www.youtube.com/watch?v=WdGSXQPwwmo
playlist: "[[Agents skills n8n]]"
type: review
difficulty: advanced
use_case: [agent-task-management, self-hosted-agent-orchestration]
tools: [Multica, Claude Code, OpenCode, Docker, Hetzner, GitHub, Tailscale]
llms: [Big Pickle]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Multica: The Open Source Tool That Makes Claude Code 10x Better

![thumbnail](https://i.ytimg.com/vi_webp/WdGSXQPwwmo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=WdGSXQPwwmo) | 📅 Uploaded [[uploaded/2026-04-21]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Multica is an open-source, self-hostable alternative to Anthropic's Claude routines and managed agents: it turns terminal coding agents (Claude Code, OpenCode, and others) into assignable teammates with their own system prompts, skills, Kanban-style task tracking, and scheduled "autopilot" runs. The video self-hosts Multica on a Hetzner VPS via Docker, works around undocumented auth setup issues, and demos assigning a real task and a recurring scheduled task to a custom agent.

**Watch this if:** you want Claude-routines-style task assignment and scheduling for your coding agents without paying for Anthropic's managed infrastructure, and you're comfortable self-hosting.

## Key Takeaways
- Multica installs via Docker as three containers (backend, frontend, and a Postgres-backed session store) and needs a separate `multica setup self-host` step that, per this video, has undocumented auth quirks — setting `APP_ENVIRONMENT=development` and clearing the reCAPTCHA API key in the env file sidesteps a broken sign-in flow.
- Each machine you want to use needs a terminal coding agent (Claude Code, OpenCode, etc.) already installed; you connect it to Multica by generating an API token in the UI and running `multica login --token`, after which the daemon polls for tasks and spawns agents in git worktrees to do the work.
- You can connect multiple VPS machines to a single Multica UI using separate API tokens per machine — useful for running several agents/projects from one dashboard.
- Custom agents get their own system prompt, skills (either from the CLI's installed skills or added directly in the UI), environment variables, and custom CLI arguments (e.g. forcing a specific model); by default an agent uses whatever model the underlying CLI tool defaults to.
- Assigning a task to an agent starts it working immediately, so the video recommends fully writing and reviewing the task before assigning it; agents move their own tasks to "in review" (never straight to "done") and wait for a human to close them out.
- Multica's "autopilot" is the open-source equivalent of Claude routines — scheduled recurring prompts run against a chosen agent — but currently lacks the API/GitHub-event trigger options that Claude routines has.
- Honest take: the presenter dislikes Kanban-style task-tracking as an interaction model (prefers a live dialogue with the agent) but likes the scheduled-tasks feature and the ability to self-host cheaply with any model; the tradeoff is a much more technical setup and losing built-in Slack/Telegram/mobile connectors that Anthropic's managed offering provides out of the box.

## 🛠 Tools & Software
- [[topics/Multica]] — the self-hosted task-assignment and scheduling platform for coding agents under review, set up and demoed end-to-end on a VPS
- [[topics/Claude Code]] — one of the terminal coding agent CLIs Multica can drive; installed on the VPS as a candidate runtime
- [[topics/OpenCode]] — the CLI agent actually used to execute the demoed tasks (medical Q&A and newsletter research), run via `opencode run`
- [[topics/Docker]] — used to install and run Multica's three containers (backend, frontend, database) on the VPS
- [[topics/Hetzner]] — the VPS provider used to self-host Multica for this demo
- [[topics/GitHub]] — the private repo holding the presenter's medical information, cloned directly onto the VPS for the Medibot agent to read
- [[topics/Tailscale]] — recommended for exposing a self-hosted Multica instance to the internet without leaving the server fully open

## 🤖 LLMs Mentioned
- [[topics/Big Pickle]] — the default model shown running via OpenCode Zen when no custom model override is set on the demoed agent

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Before self-hosting Multica, set `APP_ENVIRONMENT=development` and clear the reCAPTCHA key in the env file to avoid the broken default auth flow.
- Always fully write and double-check a task before assigning it to an agent, since assignment triggers immediate execution.
- Use `multica hook`-style git worktree spawning to run multiple agents per machine, and separate API tokens to connect multiple VPS machines to one dashboard.
- If self-hosting and exposing the UI to the internet, put it behind Tailscale rather than a raw public port.

## 🔗 Related Videos
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude Code, Docker, GitHub
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Docker, GitHub
- [[videos/I Open-Sourced My Own AFK Software Factory]] — shared: Claude Code, Docker, GitHub
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, GitHub, OpenCode
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Claude Code, Docker, GitHub
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude Code, GitHub, OpenCode
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, GitHub

## Timeline
- `0:00` — Intro: can Multica turn coding agents into real teammates?
- `0:32` — Setup plan: self-hosting on a VPS instead of the intended local + cloud UI route
- `1:05` — Installing Multica via Docker on a Hetzner VPS: three containers
- `1:28` — Auth setup problems and the env-file workaround
- `2:14` — Connecting a runtime (Claude Code / OpenCode) via API token and the daemon
- `3:22` — Creating a custom agent (Medibot): system prompt, cloned GitHub repo, skills, model override
- `4:52` — Creating and assigning a task; why to write it fully before assigning
- `5:33` — Autopilot: the open-source Claude-routines equivalent, scheduling a recurring research task
- `6:20` — Checking results: medical answer, execution history, and autopilot output
- `7:36` — Workflow quirk: agents move tasks to "in review," never straight to "done"
- `8:16` — Honest take: dislikes Kanban-style interaction, likes self-hosting and scheduling
- `8:53` — Tradeoffs vs. managed agents: setup complexity, missing connectors, and security via Tailscale

## Transcript
<details>
<summary>Full transcript</summary>

Multica claims to be the tool that can turn your agents into real teammates. So Claude Code, OpenCode, Codex CLI, Hermes, and more can be set up with their own system prompts and their own skills and be assigned tasks with status updates. They can alert you if they need your help, schedule recurring tasks, and you can talk directly to your agent. But is this open-source version of Claude routines and managed agents actually worth your time?

The intended way to use Multica is to install it on your working machine, which ideally has a terminal coding agent like Claude Code or OpenCode, and connect that to the Multica Cloud UI. But we're going completely self-hosted instead — installing Multica on a VPS. I usually skip the setup stage, but for self-hosting there were a few things not in the documentation. I've already set up Multica on a fresh Hetzner VPS by running a command that uses Docker to install it — make sure you have Docker installed on your VPS. You should end up with three containers running: the Multica backend (written in Go), the Multica frontend (TypeScript/Next.js), and the Postgres database used to store session information.

Next you run `multica setup self-host`, but I had issues with that. If you reset your configuration and workspace, it asks you to authenticate with a URL — add your email and hit continue, then you have to put in a recent code, and I had a lot of trouble with that section. I'd recommend avoiding the reCAPTCHA side of things by going into the `.multica-server` directory, opening the env file, making sure `APP_ENVIRONMENT` is set to development, and making sure the reCAPTCHA API key value is empty. Stay in that directory and run the command to restart the containers with the updated env file — after that you should be able to log in.

From here, go to runtimes — you should have none set up yet. If you run `multica daemon status`, yours should show an error, because first you need a terminal coding tool installed on your VPS. I have Claude Code and OpenCode installed; to connect that runtime, go into settings, API tokens, create a new API token, then run `multica login --token` and paste it in. Then stop and restart the Multica daemon. The daemon checks for installed harness binaries, polls for tasks from Multica to give to the agents, and spawns multiple agents using git worktrees to get tasks done. Once done, the daemon shows your available runtimes — and the beauty of connecting it this way is you can add multiple machines to a single Multica instance, each with its own API token.

With setup out of the way, some simple tasks: before doing anything you have to create an agent — I've made one called Medibot, similar to the one from my Claude managed agents video, which gets my medical information from a private GitHub repo and lets me talk to it via Slack. Because I have my own VPS here, instead of having the agent clone the repo from GitHub, I cloned it myself into the directory. As well as the system prompt, you can give your agent custom skills — it'll have access to skills installed on your CLI, but you can also add skills directly in the UI (I've added a test skill but won't attach it here). There are also environments and custom arguments — since the agent uses the CLI tool (OpenCode run in this case), I can add custom flags to force a specific model, but by default the agent uses whatever model is set in your CLI — right now that's the Big Pickle model from OpenCode Zen.

I can create a task or issue — calling this one "medical question" with the prompt "can you check my medical information and let me know if I can eat calamari?" This looks like any issue tracker: priorities, assignees, due dates. I'd highly recommend fully writing the issue before assigning someone, because the second you assign a bot, it starts working right away. Assigning it to Medibot and creating the issue, the bot gets started immediately, trackable under issues.

While that runs, clicking on autopilot — the open-source version of Claude routines — you can start from scratch, select an agent, and set how often the task runs. Unlike Claude routines there's no API or GitHub event trigger option yet. I gave it a prompt similar to the Claude routine video: fetch the latest issues of three newsletters via RSS, then find the best 10 articles usable in a YouTube video, running daily at 9am London time. Ideally you'd want a research-specific agent, but sticking with Medibot for now. Clicking "run now" creates a new issue in to-do, and after a few minutes the original medical issue has moved to "in review" — the agent responded that based on my medical records I have a shellfish allergy (true) and shouldn't eat calamari, with more allergy detail. Expanding the execution history shows the bash tool calls it made searching for the medical info directory across the whole home directory before finding and checking it.

I can leave a reply asking why it was put in review instead of moved to done, and get notifications from the agent — here's the medical agent's response, and an update from autopilot showing the run that finished, listing the top 10 picks. Interesting detail: an agent will never move a task from "in review" back to "in progress" or "to do," and also never straight to "done" — that's the standard workflow step, waiting for the human to close it out; you as a human can drag it around manually.

Honestly, I'm not the biggest fan of communicating with agents by assigning tasks and watching a Kanban board — I don't care about priorities or due dates, I tend to work on one or two projects with agents and prefer more of a dialogue, seeing the tools they use and debugging alongside them. But I do like Multica's scheduled-tasks feature and that you can fully self-host it, and it's a much cheaper tool if you use a different model than Claude's managed agents or routines. It is fairly technical to set up though — you need to know what you're doing, especially around security, which is exactly what managed agents/routines handle for you by hosting on Anthropic's infrastructure, plus their connectors (Slack, Telegram, Discord) make communication easier. In Multica you'd have to wire that together manually, or use the responsive web UI on your phone. I went the self-hosted route purely for security — anything connected to the internet is hackable. You could run Multica completely locally with no internet exposure, but if you do want to connect it to the internet, go through Tailscale so your server isn't fully exposed, and keep it up to date.

</details>
