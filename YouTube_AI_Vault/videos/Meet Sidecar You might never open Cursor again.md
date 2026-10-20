---
title: "Meet Sidecar: You might never open Cursor again"
video_id: 5QZxWmDl_tc
channel: "[[channels/Marcus Vorwaller]]"
uploaded: 2026-02-07
processed: 2026-07-06
duration: "9:58"
url: https://www.youtube.com/watch?v=5QZxWmDl_tc
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [terminal-based-coding-agents]
tools: [Sidecar, Claude Code, Codex, Cursor, Gemini CLI, Warp, OpenCode, GitHub, ripgrep, iTerm2]
llms: [Claude Opus, GPT-5.3]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Meet Sidecar: You might never open Cursor again

![thumbnail](https://i.ytimg.com/vi_webp/5QZxWmDl_tc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=5QZxWmDl_tc) | 📅 Uploaded [[uploaded/2026-02-07]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Sidecar's creator demos a terminal-based control center for running Claude Code, Codex, Gemini CLI, Warp, and OpenCode agents without leaving the terminal: an AI-focused task manager (TD), an inline Git diff/blame/merge viewer, a fast fuzzy file search with markdown rendering, a unified conversation log across agents (including Cursor and Codex app sessions), and one-shortcut Git worktree creation/merging for parallel feature branches, all wrapped in a themeable UI with per-project context switching.

**Watch this if:** you juggle multiple terminal AI coding agents and IDEs and want one place to manage tasks, diffs, files, conversations, and git worktrees without switching to Cursor.

## Key Takeaways
- TD (to-dos) is an AI-agent-oriented task manager (unlike human-focused tools like Jira/Linear): agents pick up tasks, work on them, and pick up review tasks, with a full activity log.
- The Git plugin shows inline/side-by-side diffs, staging/committing, pulling, merging remote branches, a git worktree graph view, and git blame — all keyboard-shortcut driven with a fully themeable UI (453+ community themes).
- The Files plugin gives fast fuzzy file search (powered by ripgrep), in-file and global search, and inline markdown rendering, avoiding the need to open Cursor just for context.
- The Conversations plugin aggregates AI agent conversations across tools — not just Claude Code, but Opus and GPT-5.3 sessions too, including conversations held inside the Codex app or the Cursor IDE — with adapters supported for Gemini CLI, Warp, and OpenCode, and more addable.
- Workspaces combine an inline terminal (create/name new shells, optionally attach or start an agent) with one-shortcut Git worktree creation — spinning up an isolated full checkout for a feature (e.g. "Spotify integration") without manual git commands.
- Finishing a worktree feature has a guided merge flow (review diff, pick target branch, merge directly or open a GitHub merge request) with automatic cleanup, or you can just delete the worktree/branch if you decide not to merge.
- Sidecar can fetch existing GitHub merge requests (even ones created from a phone via the Claude app) and attach an agent to continue work on them.
- Projects can be switched with an "@" shortcut, letting you jump between entirely separate repos/contexts within the same interface and terminal tab.

## 🛠 Tools & Software
- [[topics/Sidecar]] — the terminal-based hub for AI coding agents demoed throughout: tasks, git, files, conversations, and workspaces/worktrees.
- [[topics/Claude Code]] — one of the primary coding agents run and tracked inside Sidecar (including its own conversation history).
- [[topics/Codex]] — a supported coding agent, shown started in a workspace shell with "danger mode" and via its own app's conversation history appearing in Sidecar.
- [[topics/Cursor]] — the IDE Sidecar aims to reduce reliance on; has a dedicated adapter so Cursor conversations also surface inside Sidecar.
- [[topics/Gemini CLI]] — listed as a supported agent whose conversations Sidecar can display.
- [[topics/Warp]] — listed as a supported agent/terminal whose conversations Sidecar can display.
- [[topics/OpenCode]] — listed as a supported agent whose conversations Sidecar can display.
- [[topics/GitHub]] — used to fetch and open merge requests created from Sidecar's guided merge workflow.
- [[topics/ripgrep]] — the search engine powering Sidecar's fast global file search.
- [[topics/iTerm2]] — referenced as the baseline terminal experience Sidecar's inline shells replace/improve on.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — shown as one of the models behind a logged conversation in the Conversations plugin.
- [[topics/GPT-5.3]] — shown as another model behind a logged conversation (via the Codex app) in the Conversations plugin.

## ✅ Action Items
- Install Sidecar (github.com/marcus/sidecar) and try the TD task manager for agent-oriented (not human-oriented) task tracking.
- Use Sidecar's inline Git diff/merge view instead of switching to an IDE to review agent-made changes.
- Create a Git worktree from within a workspace to let an agent build an isolated feature branch, then use the guided merge shortcut to bring it back or open a GitHub merge request.
- Browse Sidecar's 453+ community themes (or build your own) and set per-project or global themes.
- Use the "@" project-switch shortcut to manage multiple repos from a single Sidecar/iTerm session.

## 🔗 Related Videos
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Cursor, Gemini CLI
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Codex, Cursor
- [[videos/The HTTP Header Trick That Cuts AI Agent Costs in Half!]] — shared: Claude Code, Codex, Cursor, Gemini CLI
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude Code, Codex, Cursor, Gemini CLI
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor, Gemini CLI, OpenCode
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Claude Opus, Codex, Gemini CLI
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, Cursor, GitHub

## Timeline
- `0:00` — Intro to Sidecar and the first screen, TD (an AI-agent-focused task manager).
- `1:00` — Git plugin: inline/side-by-side diffs, staging/committing, pulling, merging, worktree graph, git blame, discoverable shortcuts via "?", and theming (453+ community themes).
- `3:00` — Files plugin: fuzzy file search, markdown rendering, in-file and global ripgrep-powered search, Cursor adapter mentioned.
- `3:50` — Conversations plugin: unified log of agent conversations across Claude Code, Opus, GPT-5.3, Codex app, Cursor IDE, plus Gemini, Warp, OpenCode support.
- `5:20` — Workspaces: inline terminal/shell creation, starting Codex with danger mode.
- `6:00` — Creating a Git worktree ("Spotify integration") without manual command-line steps, optionally passing a TD task/prompt.
- `7:30` — Merge workflow: reviewing diff, picking target branch, merging directly or opening a GitHub merge request, automatic cleanup.
- `8:20` — Fetching an existing GitHub merge request (created via the Claude phone app) and attaching an agent to it; switching into a worktree to inspect its diff/commit.
- `9:10` — Switching between projects with the "@" shortcut, moving to a separate "night shift" project within the same interface.
- `9:45` — Brief mention of an unreleased Notes feature, saved for a future video.

## Transcript
<details>
<summary>Full transcript</summary>

Marcus introduces Sidecar with a quick feature demo. The first screen is TD (to-dos), a task manager built for AI agents rather than humans (unlike Jira or Linear) — tasks are created, agents pick them up and work on them, agents can pick up review tasks, and a full activity log shows everything that's happened; it's described as advanced in features but simple in usability.

The next feature is Git: instead of switching to Cursor to view an agent's changes, you get a full diff view (inline and side-by-side) directly in Sidecar, mostly shortcut-driven with some mouse-interactive elements. You can pull, stage and commit changes, merge in remote branches, see a graph view of the git worktree, and view git blames, among many other features — most discoverable via a "?" shortcut that searches for the action you want and shows its keyboard shortcut. A full theming system includes standard themes plus 453 community themes, themeable per-project or globally.

The Files plugin lets you view files inline instead of going to Cursor for context; files load quickly, with fuzzy search across all files, nice rendering for markdown files, in-file search via "/", and fast global search powered by ripgrep under the hood — useful for searching for something like "Cursor" since Sidecar has a built-in Cursor adapter.

The Conversations plugin shows all AI agent conversations, not just Claude Code — you can see a conversation with Opus and one with GPT-5.3 inline. Sidecar supports Gemini, Warp, and OpenCode among others, and building adapters for other agentic workflows is fairly straightforward. This isn't limited to command-line conversations: a GPT-5.3 conversation shown was actually held inside the Codex app, and Cursor IDE conversations show up here too.

Workspaces has two main features: an inline terminal (equivalent to opening a new iTerm tab, but viewable inline) — pressing "N" creates a new shell you can name, optionally attaching or starting an agent (demoed starting Codex with danger mode on); and Git worktree creation without command-line steps — creating a new workspace/worktree (named e.g. "Spotify integration," based on the main branch, optionally passing a prompt or an attached TD task) spins up a completely separate directory with the full codebase to work on in isolation. This inline-interactive-terminal-in-a-pane view is described as fairly unique to Sidecar. Once an agent (e.g. Claude Code) makes changes in that worktree, a diff tab shows what changed, and merging back uses the "M" shortcut: review the diff, pick the target branch (defaulting to the one branched from), then merge directly or create a GitHub merge request (which can open GitHub to view it) — cleanup happens automatically afterward, and even failed/complex merges can be revisited and cleaned up later, including handing a complex merge to Claude.

Sidecar can also fetch existing merge requests from GitHub — including one created the night before from a phone via the Claude app — load it in, and attach an agent to continue the work, or switch directly into that worktree (via capital "W") to inspect the diff and commit history in full context.

Sidecar also supports switching between entirely separate projects using the "@" shortcut or by clicking the repo name — demoed switching from the Sidecar repo itself into a separate "night shift" project, all within the same interface and the same single iTerm tab. An unreleased Notes feature is teased for a future video.

</details>
