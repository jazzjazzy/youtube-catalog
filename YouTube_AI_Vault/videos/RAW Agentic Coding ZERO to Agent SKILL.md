---
title: "RAW Agentic Coding: ZERO to Agent SKILL"
video_id: X2ciJedw2vU
channel: "[[channels/IndyDevDan]]"
uploaded: 2025-12-08
processed: 2026-07-06
duration: "50:23"
url: https://www.youtube.com/watch?v=X2ciJedw2vU
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [agent-skill-authoring]
tools: [Claude Code, Gemini CLI, Codex CLI, Cursor, VS Code, uv, GitHub]
llms: [Claude, Claude Haiku, Claude Sonnet, Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# RAW Agentic Coding: ZERO to Agent SKILL

![thumbnail](https://i.ytimg.com/vi_webp/X2ciJedw2vU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=X2ciJedw2vU) | 📅 Uploaded [[uploaded/2025-12-08]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> IndyDevDan builds a complete Claude Code Agent Skill from scratch, live, with no orchestration frameworks or meta-prompts — just pen-and-paper planning followed by hand-written prompts. The result is a "Fork Terminal" skill that lets an agent spawn brand-new terminal windows running Claude Code, Gemini CLI, or Codex CLI, complete with a conversation-summarization prompt so the new agent inherits context from the one that forked it.

**Watch this if:** you want to see the actual raw process of designing and hand-writing a reusable Agent Skill (pivot file, tools directory, prompts directory, cookbook) rather than watching a polished highlight-reel demo.

## Key Takeaways
- Planning starts on paper, not in the editor: define purpose, problem, and solution, then the concrete file/output structure you're aiming for, before writing a single prompt.
- A skill's structure centers on the "pivot file" (skill.md), plus a `tools/` directory (single-file scripts, e.g. built with Astral uv), a `prompts/` directory (explicitly labeled as user prompts vs. system prompts), and a "cookbook" of per-use-case markdown docs for progressive disclosure.
- Everything ultimately reduces to the "core four": context, model, prompt, tools — skills are just a reusable, composable structure wrapped around those four primitives.
- The Fork Terminal skill's purpose: spin up a brand-new terminal window running either a raw CLI command (e.g. FFmpeg, gcloud, aws) or a new agentic coding tool (Claude Code, Gemini CLI, Codex CLI), offloading context/work to a fresh window.
- This is "in-loop" agentic coding (high presence, high effort, live in the editor) as opposed to "out-loop" cloud-based agent execution — a distinction the host says matters for where you should spend your attention.
- Cookbook entries teach the agent tool-specific operating rules, e.g. for Claude Code: always use interactive terminals (no `-p`), a fast/base/heavy model mapping (Haiku/Sonnet/Opus), and running with `--dangerously-skip-permissions`.
- True "forking" required a dedicated fork-summary user prompt: the base agent summarizes conversation history into a YAML template (history + summarized user prompt + response summary) and hands that off as the new fork agent's starting prompt — mirroring what a `/compact` does, but to bootstrap a brand-new agent instead of resetting the current one.
- Tested live across Claude Code (Haiku ping test), then Codex CLI (forking a session with a history summary and a new "summarize this codebase into a README" request), successfully carrying conversation context into the new forked agent.

## 🛠 Tools & Software
- [[topics/Claude Code]] — one of the three CLIs the Fork Terminal skill can spawn; tested directly with a Haiku-model ping and with fast/base/heavy model routing rules.
- [[topics/Gemini CLI]] — one of the "big three" agentic coding tools the skill's cookbook is built to launch in a forked terminal.
- [[topics/Codex CLI]] — the third supported CLI, used in the live fork-summary demo to inherit conversation history and write a README summary.
- [[topics/Cursor]] — the editor used to hand-write the skill's files and prompts, with its tab-completion and inline Command-K prompting used to speed up mirroring cookbook entries.
- [[topics/VS Code]] — mentioned as an editor the host alternates with Cursor.
- [[topics/uv]] — used to build the Fork Terminal tool as a single-file Python script.
- [[topics/GitHub]] — the finished Fork Terminal skill is hosted here publicly so viewers can access the full repo.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model family driving Claude Code throughout the build and demos.
- [[topics/Claude Haiku]] — set as the "fast" model in the skill's model-routing rules; used for the live ping test.
- [[topics/Claude Sonnet]] — set as the "base"/default model in the skill's model-routing rules.
- [[topics/Claude Opus]] — set as the "heavy" model in the skill's model-routing rules.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Before writing any prompt or skill, write out the purpose, problem, solution, and concrete output structure on paper first.
- Structure your own skills around a pivot file (skill.md), a tools directory for scripts, a prompts directory (clearly separating user vs. system prompts), and a cookbook of per-use-case docs for progressive disclosure.
- Add explicit enable/disable flags and model-routing variables (fast/base/heavy) to your skill.md so behavior is easy to tune without rewriting prompts.
- If you need agents to "fork" context to a new instance, build a dedicated summary prompt (YAML history + next request) rather than assuming the new agent will have any memory.
- Clone the host's Fork Terminal skill from GitHub (disler/fork-repository-skill) as a working reference implementation.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Cursor, GitHub
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Claude Opus, Claude Sonnet, Cursor
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Claude Opus, Cursor, Gemini CLI

## Timeline
- `0:00` — Intro: building a Claude Code Agent Skill completely from scratch, no frameworks or meta-prompts.
- `2:13` — Begin with the end in mind: pen-and-paper planning of purpose, problem, solution, and file structure.
- `9:17` — Initialize the skill codebase in Cursor; agent scaffolds the empty file/folder structure.
- `13:24` — Writing skill.md's core structure using a personal prompt snippet, plus cookbook enable/disable flags.
- `26:34` — Building out per-tool "agent files": Claude Code rules, fast/base/heavy model mapping, `--dangerously-skip-permissions`.
- `27:57` — Live test: forking a new Claude Code terminal running the Haiku model with a ping prompt via AppleScript.
- `30:20` — Extending the cookbook pattern to Codex CLI and Gemini CLI docs using Cursor's inline autocomplete.
- `41:28` — Forked Summaries: designing the YAML fork-summary user prompt (history, summarized prompt, response summary).
- `46:28` — Live test: forking a Codex CLI session with a conversation summary and a new "summarize this codebase" request.
- `49:00` — Wrap-up: the "core four" (context, model, prompt, tools) as the real primitives behind every skill.

## Transcript
<details>
<summary>Full transcript</summary>

What's up engineers? Andy DevDan here. So, I thought it would be cool to take a step back from our normal type of video and kind of go back to the root of this channel where we just sit down and we just build. Let's write a skill from scratch. I've been building software for over 15 years and I've been building with language models since GPT 3.5 was released, back when we were running Aider, the original AI coding tool. I've written thousands of prompts by hand and even more with agents. So I think it's important to always ask: why are skills becoming more important and more popular? Skills let you deploy prompts and code against any problem in a consistent, reusable way. In this video we'll be building a fork terminal tool and breaking down why that's valuable as we progress. This is a real, raw agentic coding video — no flashy demo, no spicy hook. I want to go back to the roots of this channel as we push into 2026.

Before I even start touching the computer, using agents, using generative AI, using orchestrators, I go back to the fundamentals of engineering — I think and I plan. The first thing we do is push the laptop aside. We never start by just blasting out prompts; we start by thinking through the problem. I have a whole stack of notebooks — this is an engineer's most important tool. I'm on the agentic engineering train, I think the future is all agent-forward, but none of that matters if you don't begin with the end in mind, if you don't fully understand what you want to see.

So the first thing I do when building something new — down to a skill, down to a prompt — is understand the purpose, the problem, the solution. Beginning with the end in mind, for engineering work, often means defining the concrete output structures, the assets you're going to generate. Here we're going to have a new agent skill, so we start by writing out the file structure. We have the .claude/skills directory, and the meat of it — I call this the pivot file: the skill.md file, where we define and progressively disclose how the skill works to the operating agent.

One of the consistent directories I build under my skills is a tools directory — single-file scripts, command line tools, entire programs — the commands we give our agent to extend its capability. We're going to use a fork terminal Python script, built with Astral uv, the best Python tooling. What else do we need? Prompts — the most important piece of it all. Remember the core four: context, model, prompt, tools. Skills encapsulate this structure against a specific use case, but everything always boils down to that. We're going to have a prompts directory, and what we need here is a fork summary user prompt — I make it super clear this is not a system prompt, this is a simple user prompt that fires off inside the system at some point.

One more directory: the cookbook — additional documentation on a per-use-case basis, where we progressively disclose new information to our agent given the incoming prompt. In our fork terminal skill: it starts brand new terminal instances and has our agent kick off either a raw CLI command (FFmpeg, gcloud, aws, whatever) or a new agentic coding tool — we're focusing on the big three: Gemini CLI, Codex CLI, Claude Code. So we'll bundle stuff under a CLI command markdown file, a Gemini CLI markdown file responsible for kicking off brand new Gemini CLI agents with a forked terminal — that's why we have the fork summary prompt, to summarize the existing terminal then fork it, handing off to a new agent — and likewise Codex CLI.md and Claude Code.md.

I think that's all we'll need for this proof of concept. Once we build this, I'm going to host it on GitHub publicly so you can access the full process beginning to end. The purpose: take an existing executing agent and fork a brand new window, either running brand new CLI commands or kicking off brand new agentic coding tools, effectively forking the existing conversation — letting us offload context to new agents or offload processes to new windows. Those who plan the future tend to create it.

Now let's start building. Brand new code base, terminal projects, make dir, fork terminal skill, cd in. I'm using Cursor here, but the UI doesn't really matter since everything is converging on agents. Right away we hand off work to our agent — booting up the best agentic coding tool. I'm just going to rewrite the directory structure we planned: .claude/skills/skill.md, tools/fork-terminal, prompts/fork-summary (user prompt), and cookbook, with cli-command, gemini-cli, codex-cli, and claude-code files. We also have .gitignore, .env.sample, and a README. Let's fire this off and have the agent build the empty file structure.

To be clear about what type of agentic coding we're doing: this is in-loop agentic coding — our presence is highest, our effort is highest, our tooling capability is highest because we're operating right here in the loop. Out-loop agentic coding tools are more for production codebases where you don't need to step in for small bugs or chores — we talk about this a lot in Tactical Agentic Coding.

Now let's dial into the actual skill.md, the pivot file everything else is centered around — once you build this, everything else falls into place and you can scale your impact by throwing agents at the problem. I'm not using meta prompts, meta skills, or orchestrator agents — I'll walk through the whole process. I highly recommend setting up prompt code snippets; I have a snippet for writing skills. Activating it gives the skill structure: name, a one-sentence description of what it does, and a one-sentence description of when it should be used — "when user requests fork terminal, create new terminal, new terminal."

The purpose: fork a new terminal session to a new window using a raw CLI command. I like a variable section with simple enable flags — enable Gemini CLI, enable raw CLI commands, and so on, as booleans, all enabled. Starting with spinning up a command via the raw CLI: for brand new terminals on Mac we use AppleScript (osascript). Let's scale this up to our agent files. We want to open brand new terminal windows with prompts executed — first testing in the loop inside a terminal, a brand new instance (never be afraid to start fresh, you always want a fresh context window). I want this to kick off a brand new Claude Code terminal running the Haiku model in "yolo" mode.

So our agent learns to use Claude — using AppleScript to fire a new terminal and prompt the Haiku model with a ping test, running in non-interactive mode with `-p`. Good start — now let's encode this: copy the CLI command, open Claude Code, create rules for how this agent should operate. I want it to always use interactive terminals (leave off `-p`). Variables: fast model = Haiku, base model = Sonnet, and soon our heavy/slow model = Opus. Default model = Sonnet for the `-m` argument; use the fast model if fast is requested, the heavy model if heavy is requested. I trust my models, so I'll add: always run with `--dangerously-skip-permissions`.

Now we add the other cookbook docs for our other use cases — this is how we push on progressive disclosure. For Claude Code: if the user enters a Claude Code agent and "enable Claude Code" is true, read the Claude Code docs, with three simple examples like "fork terminal, use Claude Code to XYZ." Using Cursor's inline Command-K prompting, I mirror this pattern for Codex CLI and Gemini CLI docs. Now we have all our docs, our cookbook properly routes and progressively discloses information to the right place when needed.

Let's try spinning up a brand new Claude Code instance — not quite "forked" yet since we don't have the summarization prompt. Fork terminal, new Claude Code, "list your current working directory" — it reads the documentation, understands we want a Claude Code instance, runs the help command, and forks with the settings we requested.

Now, what does "fork" actually mean? We need to create a summary just like the `/compact` command does — it summarizes all existing messages and resets the context window. You always lose information doing this, but it's a good stopgap for resetting context while maintaining the current task. We want the same for our fork summary user prompt: program our agent to use this when we say "summarize," having it summarize the work done and pass that summary into the new agent along with the new request. The relationship: a base agent writes to a fork agent. We set this up as a YAML-format prompt template — history (a summarized user-prompt/response-summary sequence) plus the next user request — filled out by the base agent and passed as the fork agent's starting prompt, giving the fork agent a concise history to understand the user's next request.

We update skill.md with a dedicated instruction: if the user requests a fork terminal with a summary, include the history of the conversation so far plus the next request, only for agentic coding tools that are enabled. Testing this: some setup prompts about FFmpeg to build history, then "fork session Codex CLI, fast, summarize work done: understand this codebase then write a 20-line summary in the README." First attempt actually overwrote the skill file directly, which we didn't want — so we add an "important, information-dense" instruction: don't update the file directly, just read it and use it to craft a new prompt for the fork agent.

Rewinding with Claude Code's history-rewind feature and retrying: this time it doesn't overwrite the file, and we see a new Codex agent kick off with the properly filled-in prompt — a nice summarization of the previous conversation plus the next user request (understand this codebase, write a 20-line README summary). The formatting from Codex's high model isn't great, so we just ask it to improve formatting.

Here we created a skill from scratch and walked through all the pieces: a reusable prompt our agent can operate, a dedicated tools directory, a cookbook of specific use cases and tooling, and the central skill.md pivot file with static variables our agent tunes. Skills are important because they put together reusable code and reusable prompts. Don't let any new feature release or model confuse you — the only things you need to focus on are the primitives that make it all up: context, model, prompt, and tools, the core four. If you master these, you'll master the agent, you'll master engineering in 2025 and 2026. This will be linked in the description so you can give it a shot. If you like this raw, less-hype agentic coding format, let me know — you know where to find me every Monday. Stay focused and keep building.

</details>
