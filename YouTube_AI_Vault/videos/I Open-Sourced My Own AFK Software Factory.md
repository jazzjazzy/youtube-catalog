---
title: "I Open-Sourced My Own AFK Software Factory"
video_id: E5-QK3CDVQM
channel: "[[channels/Matt Pocock]]"
uploaded: 2026-04-30
processed: 2026-07-05
duration: "11:25"
url: https://www.youtube.com/watch?v=E5-QK3CDVQM
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [afk-agent-orchestration, automated-code-review-merge]
tools: [Sandcastle, Claude Code, Codex, Docker, GitHub, Vitest, Commander, npm, Claude Skills]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# I Open-Sourced My Own AFK Software Factory

![thumbnail](https://i.ytimg.com/vi/E5-QK3CDVQM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=E5-QK3CDVQM) | 📅 Uploaded [[uploaded/2026-04-30]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Matt Pocock open-sources Sandcastle, a TypeScript library for running Claude Code, Codex, or any coding agent unattended (AFK) inside sandboxes like Docker without constant permission prompts. He live-builds a full pipeline — a planner agent that reads GitHub issues, parallel implementer agents, a reviewer agent, and a merger agent that resolves conflicts and merges back to main — and shows it completing a real scaffolding task end to end.

**Watch this if:** you want your coding agents to run genuinely unattended on backlog tickets instead of babysitting Yolo-mode permission prompts.

## Key Takeaways
- Running agents fully AFK requires sandboxing, not just "Yolo mode" — bypassing permission prompts entirely risks Claude deleting a home directory or, in enterprise settings, exfiltrating code to a third party.
- Sandcastle is a TypeScript library where you call `Sandcastle.run`, passing an agent, a sandbox provider, and a prompt; it's agent-agnostic (Claude Code, Codex, or others) and ships Docker as a first-class sandbox provider with room to add more.
- Setup is `npm install ai-hero sandcastle` then `npx sandcastle init`, which scaffolds a `.sandcastle` directory with a Dockerfile, environment file, and one of five starter templates (the video uses "parallel planner with a review step").
- The demoed pipeline: a planner agent reads open GitHub issues labeled `sandcastle`, filters to unblocked ones, and emits a JSON plan; an implementer agent is spawned per issue on its own branch; if there's more than one commit, a reviewer agent checks the diff against project standards; a merger agent then resolves any merge conflicts and merges everything back to main, closing the issue.
- The review prompt borrows a syntax from Claude Skills — an `!` before backticks executes a shell command (e.g. `git diff`) while the prompt is being resolved, injecting live results into the prompt.
- Because Sandcastle is agent-agnostic, you can run adversarial setups: one agent implements while a different agent (e.g. Codex) reviews, or multiple agents each propose an implementation and a reviewer picks or merges the best one.
- The whole pipeline is unopinionated glue code, not a prescribed framework — Matt explicitly frames the planner/implementer/reviewer/merger flow as "just a workflow I use," fully editable via markdown prompt files in the scaffolded template.

## 🛠 Tools & Software
- [[topics/Sandcastle]] — the open-sourced TypeScript library that orchestrates AI coding agents inside isolated sandboxes; the video's central subject, built and demoed live
- [[topics/Claude Code]] — the coding agent selected during `npx sandcastle init` and used to run the planner/implementer/reviewer/merger agents in the demo
- [[topics/Codex]] — named as a drop-in alternative agent for any Sandcastle role (e.g. running the planner or acting as an adversarial reviewer instead of Claude Code)
- [[topics/Docker]] — the first-class sandbox provider chosen in the demo; Sandcastle builds a Dockerfile installing system deps, GitHub CLI, and the agent itself
- [[topics/GitHub]] — used as the backlog manager: agents pick up work via labeled GitHub issues, and GitHub CLI/tokens are used from inside the sandbox
- [[topics/Vitest]] — the test framework requested in the scaffolded TypeScript template and used by the implementer agent's test-first workflow
- [[topics/Commander]] — the CLI framework requested for the scaffolded template's command-line interface
- [[topics/npm]] — used to install Sandcastle (`npm install ai-hero sandcastle`) and to run it via `npx`
- [[topics/Claude Skills]] — its `!` backtick shell-execution syntax was copied into Sandcastle's review prompt template

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Try `npm install ai-hero sandcastle` and `npx sandcastle init` on an existing repo to scaffold a Docker-sandboxed agent pipeline.
- Label backlog tickets in GitHub issues (e.g. `sandcastle`) so a planner agent can autonomously pick up unblocked work.
- Add a reviewer agent step whenever an implementer produces more than one commit, and consider using a different agent (e.g. Codex reviewing Claude Code's work) for adversarial review.
- Use a strong agent specifically for the merge step since resolving conflicts across multiple parallel agent branches can get gnarly.

## 🔗 Related Videos
- [[videos/OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)]] — shared: Claude Code, Claude Skills, Codex, GitHub
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, GitHub
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Claude Skills, GitHub
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Codex, GitHub, npm
- [[videos/Continual Learning in Claude Code]] — shared: Claude Code, Claude Skills, GitHub
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Codex, GitHub
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude Code, Docker, GitHub
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Docker, GitHub

## Timeline
- `0:00` — The AFK-agent permissions problem and why Yolo mode is too risky to run unattended
- `1:22` — Introducing Sandcastle: a TypeScript library for orchestrating agents in isolated sandboxes
- `2:07` — Setup: `npm install`, `npx sandcastle init`, choosing Claude Code and Docker as the sandbox
- `2:29` — Backlog manager: GitHub issues filtered by a `sandcastle` label, five starter templates
- `3:07` — The generated Dockerfile and building the sandbox image
- `3:40` — Environment setup: Anthropic API key vs. Claude subscription, GitHub token
- `5:13` — Creating a GitHub issue and kicking off the planner agent
- `6:18` — Inside main.mts: how the planner's plan feeds per-issue implementer sandboxes
- `7:57` — Reviewer and merger agents: adversarial review, conflict resolution, merge to main
- `9:55` — Wrap-up: watching the run complete, merged code, and closing thoughts

## Transcript
<details>
<summary>Full transcript</summary>

One of my goals for the last 6 months have been trying to get my coding agents to run totally AFK. These AFK agents have been picking up backlog tasks, implementing features, doing QA, and crucially running in parallel — lots of them running at the same time. However, in order to get them to run properly, you need to handle the permissions requests that they make. A question you probably have right now is how do I get my agent to run without it constantly battering me with requests for permissions. Of course you could just go into Yolo mode and have it totally bypass any permissions requests. But if you do that, Claude will do mad things on your system like delete your home directory, or if you're in an enterprise setup, it might exfiltrate data or send your code off to a random third party. So in order to get agents to run properly AFK, you need them to be sandboxed.

There are a bunch of solutions for this, but I wasn't particularly happy with any of them. The one I really tried to use and make work was Docker sandboxes, but there were so many problems running it AFK that I won't bore you with now. What I wanted was a simple TypeScript function I could run and say "run this prompt inside this sandbox using this agent." All the tools I found were trying to sell me some third-party service. So I realized I needed to build something here. And that thing is Sandcastle, a TypeScript library for orchestrating AI coding agents in isolated sandboxes. You build TypeScript scripts where you simply say run, passing in the agent, passing in the sandbox, and passing in the prompt. If you look in any of my open source repos, you'll see a `.sandcastle` directory with a `main.ts` file full of these `Sandcastle.run` functions. With this simple function you can build really complex systems — systems that parallelize agents running side by side, systems that review their own code and merge it in.

Let me show you how to get this set up inside a repo. We first run `npm install ai-hero sandcastle`. Once that's done, we run `npx sandcastle init` and you'll first be asked to select an agent. Let's select Claude Code, why not. You can then select between first-class sandbox providers — my plan is to add many more, and you can implement your own. For now, let's choose Docker. Sandcastle also uses a backlog manager because AFK agents need some way of picking up tickets and knowing what to do next; my preferred way is GitHub issues. We ship five templates currently — let's max out and go for a parallel planner with a review step. Since we chose GitHub issues, we create a Sandcastle GitHub label; the issues get filtered by this label so only labeled issues get picked up by the agents.

A bunch of stuff gets thrown into the `.sandcastle` directory. The key thing to know about now is the Dockerfile — the instructions for setting up the Docker container Sandcastle runs inside, so you can install anything you like: system dependencies, the GitHub CLI, renaming the home directory to "agent," installing Claude Code, and we're ready to go. Building the default Docker image is fast. Next we set required environment variables in `.sandcastle/.env` — the `.env.example` shows an Anthropic API key and a GitHub token are required. If you want to use your Claude subscription instead of an API key, there's a linked GitHub issue with up-to-date advice, since Anthropic is a little particular about subscription use for this kind of thing.

Once configured, commit and push, then create a new GitHub issue: "Scaffold me a basic TypeScript template in the repo. Give me a basic TypeScript application that uses Vitest, that uses type checking, that has a very simple CLI. Use Commander for the CLI. Add a CI script that does type checking and runs the tests." Add a small script to `package.json` that runs `npx tsx .sandcastle/main.mts` (tsx runs TypeScript directly as a script), then run it.

Immediately it kicks off a planner agent — you can control-click the logs to see it set up the sandbox, run as a planner agent on Docker, look at the open issues (one open issue here), and spit out a plan of issues to work on, along with the context window used. Then an implementer agent kicks off: it calls `gh issue view`, gets a clear picture of the ask, and starts running bash commands — installing dependencies, doing red-green-refactor by writing the test first and running Vitest. You can watch it or go make a cup of tea while it works without you.

While it's running, look at `main.mts`: the planner `Sandcastle.run` call takes an agent name (swap in Codex instead of Claude Code if you want) and a plan prompt file. That prompt takes all open issues labeled `sandcastle`, grabs their labels and comments, works out which are unblocked right now, and outputs its plan as JSON wrapped in plan tags. Back in `main.mts`, that JSON plan is parsed and, for each issue, a separate sandbox runs an implementer with an implement prompt that takes the issue title and task ID and works on a specific branch. This whole flow is just a workflow Matt cooked up for his own repos, not something Sandcastle prescribes — it's fully editable in the template.

If more than one commit results, a reviewer agent runs — this pattern is powerful because the implementer can make mistakes that the reviewer generally catches. You can run an adversarial review with a different agent, e.g. `Sandcastle.codex`, reviewing another agent's code, or spawn multiple different agents to each produce an implementation and have a reviewer pick or merge the best one — the power of an agent-agnostic setup. The review prompt uses a syntax borrowed from Claude Skills: an exclamation mark before backticks executes a shell command while resolving the prompt, e.g. running `git diff` between branches live. The review prompt itself just understands the change, checks for improvements and correctness, and is a great place to add your own project coding standards.

After all branches are created, they're passed to a merger agent that takes all branches and their resulting issues, understands the changes made, and merges them back to the main branch — using an agent here because merge conflicts between parallel branches can be gnarly, and a powerful agent handles that well. The result: multiple agents running at once, all committing to their own branches, then a "senior merger developer" agent pulling them back into main. This setup has massively increased Matt's velocity. Sandcastle is unopinionated — you could just as easily make these into PR branches instead of merging directly.

Checking in on the run: an implementer kicked off, then a reviewer found the code already clean and well-structured with minimal, clearly-named scaffolding. The merger ran type checks, merged the branch, and closed the issue with a comment. The repo now has a `tsconfig.json`, a `vitest.config.ts`, and a few CLI files. You can build relatively complicated flows this way using ergonomic markdown prompts, run on different branches, and merge back into main or do full PR flows. It's just code — a programmatic way to run Claude Code, run Codex, and build these workflows into mini software factories. Matt's been really happy with it and is excited to see what people build with it. He points to his newsletter on AI skills for real engineers, following the skills repo that went viral a few days earlier, with more tips on getting the most out of agents using solid software fundamentals.

</details>
