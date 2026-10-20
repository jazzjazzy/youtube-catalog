---
title: "Anthropic Just Added These Features to Claude Code"
video_id: IiA4Ku5viyg
channel: "[[channels/Ray Amjad]]"
uploaded: 2025-12-10
processed: 2026-07-06
duration: "13:11"
url: https://www.youtube.com/watch?v=IiA4Ku5viyg
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [keeping-up-with-claude-code-updates]
tools: [Claude Code, Slack, Sentry, Supabase]
llms: [Claude, Claude Sonnet, Claude Haiku, Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Just Added These Features to Claude Code

![thumbnail](https://i.ytimg.com/vi_webp/IiA4Ku5viyg/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=IiA4Ku5viyg) | 📅 Uploaded [[uploaded/2025-12-10]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A roundup of recent Claude Code releases: instant auto-compacting backed by a per-session memory file, async subagents and bash commands that run in the background and wake the main agent when done, a `/stats` command, richer session management (renaming, grouping forked sessions), hierarchical "Claude rules" for modular CLAUDE.md files, MCP quick enable/disable, running Claude Code as a specific subagent via `--agent`, and a new Claude-in-Slack integration.

**Watch this if:** you use Claude Code daily and want a fast catch-up on what changed in the last two weeks without digging through the changelog yourself.

## Key Takeaways
- Auto-compacting is now near-instant because Claude Code continuously writes a session-memory summary (title, status, completed work, open questions, learnings, work log) to `.claude/projects/.../session memory` after every message — compacting just loads that running summary into a fresh session instead of resummarizing from scratch.
- Subagents and long bash commands (e.g. `npm install`, ffmpeg) can now run asynchronously in the background (Ctrl+B to background a task, `/tasks` to check token usage/progress) and will "wake up" the main agent with results via a new agent-output tool when finished.
- `/stats` surfaces favorite model, total tokens used, longest session, and daily per-model token usage, shareable as a copyable summary (e.g. to paste into a tweet).
- Session management improvements: `/rename` (buggy at time of recording) and renaming from `/resume` (press R), plus `/resume` now groups forked sessions (sessions spawned from a compaction point) together with preview/rename shortcuts, and an "all projects" view (press A).
- "Claude rules" add a four-tier hierarchical memory structure (enterprise, project CLAUDE.md, project rules, user memory) letting you modularize CLAUDE.md into rule files scoped to specific paths (e.g. only apply to an APIs folder) — comparable to Cursor rules, useful for monorepos.
- Smaller additions: multi-choice prompts now highlight a recommended option at the top; commits now note which model wrote the code; `/mcp enable|disable <server>` toggles MCP servers quickly; `--disable-slash-commands` gives a minimal chat-only mode.
- `--agent <name>` lets you run Claude Code manually as any specific subagent (custom ones you've built, like a Haiku-based macOS log analyzer, or Anthropic's built-in ones like `plan`) instead of only letting the main agent spawn them invisibly — useful for diagnosing a subagent's behavior directly.
- Claude Code can now be added to Slack (via the app directory), connected to your Anthropic account, and tagged with @Claude in a channel to delegate coding tasks directly from chat, with the ability to add custom connectors (e.g. a Sentry MCP server) for extended context.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the subject of the whole video: auto-compact/session memory, async subagents/bash, `/stats`, session renaming, Claude rules, MCP toggling, `--agent`, and the new Slack integration are all Claude Code features.
- [[topics/Slack]] — Claude Code is installed as a Slack app, connected to an Anthropic account, and tagged with @Claude in a channel to delegate a coding task.
- [[topics/Sentry]] — mentioned as an example custom connector you can add to extend Claude-in-Slack with more context.
- [[topics/Supabase]] — used as the live example MCP server enabled/disabled via `/mcp enable` and `/mcp disable`.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model family underlying every feature demoed throughout Claude Code.
- [[topics/Claude Sonnet]] — shown as the host's "favorite model" in `/stats` (Sonnet 4.5), largely from subagent usage.
- [[topics/Claude Haiku]] — used as the model for a lightweight custom macOS log analyzer subagent, run directly via `--agent`.
- [[topics/Claude Opus]] — referenced via Anthropic's political-bias research: Opus 4.1 scored best at considering opposing perspectives, with Opus 4.5 speculated to score similarly well.

## 📡 Protocols & Standards
- [[topics/MCP]] — demoed via `/mcp enable`/`/mcp disable` for quickly toggling servers like Supabase, and via adding custom MCP connectors (e.g. Sentry) to the Slack integration.

## ✅ Action Items
- Ask Claude Code "where is your session memory stored?" to inspect the live summary it's building of your current session.
- Try backgrounding a long-running subagent or bash command (Ctrl+B) so you can keep working while it finishes and wakes the main agent.
- Run `/stats` to see your favorite model and token usage, and share it if you want to compare usage with teammates.
- Set up path-scoped Claude rules to split a large CLAUDE.md into modular, folder-specific rule files, especially in a monorepo.
- Use `/mcp enable`/`/mcp disable <server>` instead of reconfiguring MCP servers manually when you just need to toggle one off temporarily.
- Try `claude --agent <name>` to manually run and diagnose a specific subagent (built-in like `plan`, or one you've created) in isolation.
- If your team fields bug reports in Slack, install Claude Code's Slack app and tag @Claude directly in the relevant channel.

## 🔗 Related Videos
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, Claude Sonnet
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Haiku, Claude Sonnet
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus

## Timeline
- `0:00` — Intro: recent Claude Code feature roundup.
- `0:27` — Instant auto-compacting, powered by continuous per-session memory summaries.
- `2:13` — Async subagents and bash commands: backgrounding tasks and waking the main agent on completion.
- `4:02` — `/stats`: favorite model, total tokens, usage streak, shareable summaries.
- `4:56` — Enhanced session management: `/rename`, grouped forked sessions in `/resume`, "all projects" view.
- `6:20` — Claude rules: hierarchical, path-scoped modular CLAUDE.md files.
- `7:43` — Multi-choice questions get a recommended-option indicator.
- `7:54` — Commit messages now note which model wrote the code.
- `7:58` — MCP management: `/mcp enable`/`/mcp disable <server>`.
- `8:14` — `--disable-slash-commands` for a minimal chat-only mode.
- `8:32` — Running Claude Code as a specific subagent via `--agent`.
- `10:09` — Claude in Slack: installation, account connection, and tagging @Claude in a channel.
- `11:47` — Anthropic's political-bias research: Opus 4.1's strength at considering opposing perspectives.

## Transcript
<details>
<summary>Full transcript</summary>

Okay, so earlier today, some interesting new features were added to Claude Code, so we will be going over them, as well as many of the new features from the last two weeks.

First of all, they made auto-compacting instant. Usually compacting conversations would take about two minutes, but now it's much faster. Behind the scenes, your .claude folder in your home directory has a projects folder, and inside any project you can click into any session, go to session memory, and see a summary of that session — a session title Claude Code came up with itself, the current status (completed work, discussion points, open questions), some learnings, key results, and a work log that's automatically updated every time you send a message. So every time you're using Claude Code, it's automatically keeping a memory of the entire session. What's happening when compact is instant is that it just loads the summary of that session into a brand new session that it was writing as you went along. You can ask Claude Code "where is your session memory stored?" and it will tell you the exact location, since it knows its own session ID.

Okay, so now agents and bash commands can run asynchronously and send messages to wake up the main agent. I can spawn a subagent to do research online, press Enter, then Ctrl+B to move it into the background. I can continue chatting normally — the sub agent runs async in the background, and I can do `/tasks` to see it running and check token usage. Once the sub agent is done, it wakes the main agent again and uses a new "agent output" tool to look at the response, combining it into the main agent's task. This is useful when you're coding on something and want a subagent to search for information in the background and resume once it's found. The same applies to bash commands like npm install or ffmpeg that take a while — you can leave them running in the background and continue other work.

`/stats` now provides interesting Claude Code stats: favorite model, usage graph, usage streak. My favorite model is Sonnet 4.5, probably from a lot of Sonnet 4.5-based subagents. I've used 10 million tokens so far, my longest session was one day and eight hours. You can copy these stats and paste them straight into a tweet. Pressing Tab goes to a Models tab showing tokens used per day across all model types — also copyable for sharing, maybe fun for comparing usage within a team.

They now added named session support via `/rename`, though it seems to be broken right now — it doesn't recognize the command. But `/resume` shows all previous sessions and lets you rename them there (press R), and then `claude --resume <name>` resumes that named session. The resume screen now also groups forked sessions together with keyboard shortcuts for preview and rename — pressing P previews a session, and pressing B on a session shows any previous sessions forked out of it (created when you compact a conversation). You can resume any of those pre-compaction sessions, which is handy. Press A to show all your projects, since resume normally only shows sessions in your current folder.

We've now also added support for Claude rules. Claude's memory has four types of memory locations in a hierarchical structure: enterprise, the project CLAUDE.md file, project rules, and user/project memory local. Enterprise loads first, then the project CLAUDE.md, then you can now define project-based rules, letting you modularize your rules files better — kind of like Cursor rules. In your .claude folder you have your CLAUDE.md plus rules for different things; if you don't define a path at the top of a rule it applies all the time, but if you define a path like an APIs folder, the rule only applies to files within that folder. So for a big monorepo, you can extract rules that only apply to Cloudflare Workers, others that only apply to a macOS application, others to a website, and so on.

For multiple choice questions, Claude Code will now use a recommended indicator with the recommended option moved to the top of the list — useful in planning mode when you're not sure which option to take. Whenever Claude Code makes a commit, it will now say which model actually wrote the code. You can enable and disable MCP servers quickly with `/mcp enable <server>` / `/mcp disable <server>` — for example disabling a Supabase MCP server I have installed. If you want to launch Claude Code without any slash commands, you can use `claude --disable-slash-commands`, giving a more minimal, just-chatting-with-Claude experience.

They also added a `--agent` CLI flag to override the agent settings for the current session — meaning if you have a subagent in your project, you can run Claude Code as that particular subagent. I have a macOS log analyzer subagent that uses a Haiku model since it doesn't need a more powerful one; running `claude --agent <name>` runs as that subagent directly, and asking "what do you do?" confirms it identifies itself for macOS unified log analysis. You can also run Claude Code as any default built-in subagent, like `claude --agent plan`, the planning subagent built into Claude Code. By default, leaving out the agent flag runs the main agent; specifying one lets you manually control and diagnose any subagent — installed, custom-built, or default — directly, rather than only letting Claude Code spawn them invisibly.

They also now added the ability to delegate tasks to Claude Code from Slack. In Slack, go to the app section, search for Claude, add it to your workspace, grant permission, connect your Anthropic account, choose a model for conversation, choose code-only or code-plus-chat, and set the organization. Inside a channel you can tag @Claude with a request like adding a translation to a landing page, and Claude Code will get started — though it may need to be added to the channel first and may ask which repo to work in if it can't identify one automatically. This is useful for team bug fixes or issue channels where you can just tag Claude Code. You can extend it further by connecting custom connectors, like a Sentry MCP server or your own logging system, via the Slack connector settings.

Just before ending, I remember reading Anthropic's "measuring political bias in Claude" article — the graph was interesting, showing Opus 4.1 was the best at considering opposing or counter arguments to political problems. The fact that Claude is better at considering opposing perspectives and counter-arguments may carry over to making better decisions when coding, and since Opus 4.1 scored best here, it's quite likely Opus 4.5 scores similarly well or slightly higher on this eval.

Anyways, hopefully that video was useful — if you like this kind of content, subscribe, and check out my Claude Code masterclass and other apps linked below.

</details>
