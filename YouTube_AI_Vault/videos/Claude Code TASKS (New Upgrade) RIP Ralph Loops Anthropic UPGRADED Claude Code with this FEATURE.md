---
title: "Claude Code TASKS (New Upgrade): RIP Ralph Loops! Anthropic UPGRADED Claude Code with this FEATURE!"
video_id: Qh6jg3FymXY
channel: "[[channels/AICodeKing]]"
uploaded: 2026-01-23
processed: 2026-07-06
duration: "8:50"
url: https://www.youtube.com/watch?v=Qh6jg3FymXY
playlist: "[[Agents skills n8n]]"
type: news
difficulty: advanced
use_case: [claude-code-task-management, ai-agent-orchestration]
tools: [Claude Code, Ralph Loop, Ralphie]
llms: [Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code TASKS (New Upgrade): RIP Ralph Loops! Anthropic UPGRADED Claude Code with this FEATURE!

![thumbnail](https://i.ytimg.com/vi/Qh6jg3FymXY/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Qh6jg3FymXY) | 📅 Uploaded [[uploaded/2026-01-23]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Claude Code replaced its in-memory Todos with file-backed Tasks that persist across sessions, support dependency metadata, and can be shared live across multiple sub-agents/sessions via a `CLAUDE_CODE_TASK_LIST_ID` environment variable — effectively productizing what hack-y community tools like the Ralph Loop and Ralphie were built to do, though the presenter flags sparse documentation and no visual dashboard yet.

**Watch this if:** you rely on the Ralph Loop, Ralphie, or similar autonomous-loop tooling and want to know what Claude Code's native Tasks feature does differently.

## Key Takeaways
- Todos lived only in session memory: closing a session wiped the list, sub-agents had no visibility into what the main agent was doing, and coordinating multiple Claude Code sessions meant "yelling into the void."
- Tasks are stored as files under `~/.claude/tasks`, so they persist across sessions/restarts and can even be inspected or manipulated by your own tooling since they're just files.
- Tasks support dependency metadata (task C blocked by A and B, etc.) instead of Todos' flat list, mirroring how real project planning actually works.
- The headline feature: multiple sub-agents or Claude Code sessions can collaborate on the same task list in real time, with updates broadcast instantly — enabling one sub-agent to work on auth, another on the DB schema, and a third on tests without duplicate work or collisions.
- Tasks are framed as the "official, architectural evolution" of the Ralph Loop plugin's stop-hook-based "keep going until it's actually done" philosophy, but with proper multi-task dependency and coordination support instead of a single loop hack.
- Set the same `CLAUDE_CODE_TASK_LIST_ID` env var across sessions (also works with `claude -p` CLI mode and the Claude Agent SDK) to have them collaborate on one shared task list.
- Recommended usage threshold: skip Tasks for small asks (a quick refactor or bug fix); use them for larger multi-file features, big refactors, or test-suite builds where you can define dependencies and split work across sub-agents.
- Ralphie (which added parallel execution, git worktree isolation, and task dependencies on top of the Ralph Loop) isn't fully obsolete — its git worktree isolation and automatic PR creation still add value — but its core task-coordination role is now handled natively by Claude Code.
- Noted drawbacks: documentation is sparse (pieced together from an X announcement plus experimentation), there's no visual dashboard for task progress/dependencies (only a terminal view toggled with Ctrl+T), and sharing a task list currently requires a somewhat clunky environment variable instead of a slash command.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose new file-backed, dependency-aware Tasks system (replacing Todos) is the subject of the video
- [[topics/Ralph Loop]] — the stop-hook-based "keep going until done" plugin that Tasks is described as the official architectural evolution of
- [[topics/Ralphie]] — a tool built on top of the Ralph Loop adding parallel execution, git worktree isolation, task dependencies, and automatic PR creation; still useful for the git-isolation piece even though Tasks now handles core coordination

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — cited as the model whose improved long-horizon autonomy (Opus 4.5) made the old per-session Todo checklist unnecessary for smaller tasks, motivating the shift to Tasks for bigger, multi-session work

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Reserve Tasks for larger, multi-file, multi-session work; keep quick fixes and refactors as plain prompts without a task list.
- Set matching `CLAUDE_CODE_TASK_LIST_ID` values across sessions/sub-agents (including `claude -p` and the Agent SDK) to have them collaborate on the same shared task list.
- If you already use Ralphie, keep it for git worktree isolation and automatic PR creation, but rely on native Tasks for the underlying dependency/coordination logic.
- Use Ctrl+T in the terminal to toggle the task view while waiting for a visual dashboard tool to emerge from the community.

## 🔗 Related Videos
- [[videos/I Can't Believe Anthropic Messed Up The Ralph Wiggum]] — shared: Claude Code, Claude Opus, Ralph Loop, Ralphie
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Opus

## Timeline
- `0:00` — Intro: Claude Code replaces Todos with Tasks
- `0:31` — Why now: Opus 4.5's longer autonomy made per-session Todos unnecessary for small work
- `1:03` — Todos' limitations: no persistence, no sub-agent visibility, no cross-session coordination
- `1:27` — What Tasks fix: file-backed storage in `~/.claude/tasks`, persistence across sessions
- `2:12` — Dependency metadata: tasks can block/be blocked by other tasks
- `2:23` — Cross-session/sub-agent collaboration: shared task list, broadcast updates, parallelization
- `3:08` — Tasks as the official evolution of the Ralph Loop's stop-hook philosophy
- `4:27` — Sharing task lists via `CLAUDE_CODE_TASK_LIST_ID`, including CLI and Agent SDK support
- `5:06` — When to use Tasks: small asks vs. larger multi-file/multi-agent projects
- `6:09` — Ralphie comparison: what's now native vs. what Ralphie still adds (git worktrees, PR creation)
- `6:39` — Nitpicks: sparse documentation, no visual dashboard, clunky env-var-based sharing

## Transcript
<details>
<summary>Full transcript</summary>

Hi, welcome to another video. So, Claude Code just got a pretty significant upgrade. They're replacing todos with something called tasks. And before you roll your eyes and think, "Great, another fancy name for the same thing." Let me tell you why this actually matters. Tasks are basically the evolution of todos, but they solve problems that todos never could. Here's the deal. As Opus 4.5 got better at running autonomously for longer periods, Anthropic noticed something interesting. The todo write tool became kind of unnecessary for smaller tasks. Claude already knew what it needed to do. It didn't need a checklist for simple stuff. But for bigger projects, for stuff that spans multiple sessions, or involves multiple sub agents, todos were completely useless.

Think about it. With todos, everything lived in memory. If you closed your session, your todo list was gone. If you spun up a sub agent, it had no idea what the main agent was working on. If you tried to coordinate work across multiple Claude Code sessions, you were basically yelling into the void. Tasks fix all of that.

Now, let me explain what makes tasks different. First, tasks are stored in the file system. They live in tilde/.claude/tasks. This means they persist between sessions. You can close Claude Code, grab a coffee, come back, and your tasks are still there. You can even build your own utilities on top of them because they're just files.

Second, tasks support dependencies. With todos, everything was just a flat list. Task A, task B, task C. But real projects don't work like that. Sometimes task C can't start until task A and task B are done. Sometimes task D depends on task C, but task E doesn't. Tasks let you define these relationships in the metadata, which mirrors how actual projects work.

Third, and this is the big one. Tasks enable collaboration across sessions and sub agents. When you spin up multiple sub agents or run multiple Claude Code sessions, they can all work on the same task list. When one session updates a task, that change is broadcasted to all other sessions working on the same list. This is huge for parallelization. You can have one sub agent working on the auth system, another on the database schema, and a third on the tests. They all see the same task list. They all know what's been completed and what's still pending. No more duplicate work. No more agents stepping on each other's toes.

Now, here's where it gets interesting. Remember my video on the Ralph Wiggum loop? That plugin where you trap Claude Code in a loop until it actually finishes the job? Well, tasks are essentially the official version of what Ralph was trying to do, but built directly into Claude Code. Let me explain. Ralph Wiggum uses a stop hook to intercept Claude's exit attempts. Every time Claude tries to stop, the hook blocks the exit and re-injects the original prompt. It keeps going until the task is actually complete. The problem was, Ralph was essentially a hack. A clever hack, but still a hack. It didn't have any concept of multiple tasks, dependencies, or coordination. Tasks take that same philosophy of keep going until it's actually done and integrate it properly into Claude Code's architecture. Instead of one task in a loop, you can have 10 tasks with complex dependencies. Instead of one session banging its head against a problem, you can have multiple sessions and sub agents dividing and conquering.

And the best part? You can control this with an environment variable. If you want multiple sessions to collaborate on the same task list, you just set CLAUDE_CODE_TASK_LIST_ID equals whatever name you want, and then start Claude. All sessions using that same ID will see and update the same tasks. This also works with claude -p for the CLI mode and with the agent SDK. So, if you're building automation on top of Claude Code, you can coordinate work across multiple instances.

Now, let me talk about when you'd actually use this. For small tasks, you probably don't need tasks at all. If you're just asking Claude to refactor a function or fix a bug, just ask it. Claude's smart enough now to handle that without needing a task management system. But for bigger projects, like building a full feature across multiple files, or doing a large refactor, or creating a test suite, that's where tasks shine.

Here's my workflow. I'll define my project requirements, ask Claude to break it down into tasks with proper dependencies, then spin up multiple sub agents to work on independent branches of the task tree. Each sub agent works in its own context window, but they're all seeing the same task list. When one finishes a task, the others see that update and can start working on tasks that were blocked. This is the kind of orchestration that used to require tools like Ralphie, which I covered in a previous video. Ralphie added parallel execution, git work trees, and task dependencies on top of the Ralph loop. But now, tasks handle a lot of that natively. You still might want Ralphie for the git work tree isolation and automatic PR creation, but the core task coordination, that's built in now.

I do have a couple of nitpicks, though. First, the documentation is pretty sparse right now. The Claude Code team announced tasks on X, but there's not much official documentation yet. I had to piece together how it works from the announcement and some experimentation. Hopefully, they'll add proper docs soon. Second, I wish there was a visual interface for tasks. Right now, you can see them in the terminal, and you can control plus T to hide them, but a proper dashboard showing task progress and dependencies would be really nice. Maybe someone in the community will build that. Third, the fact that you need to set an environment variable to share tasks across sessions is a bit clunky. I'd prefer if there was a slash command or a config option for this. Something like /tasks share groceries to start collaborating on a task list called groceries. But these are minor complaints. The core functionality is solid, and it's exactly what power users have been asking for.

If you've been using the Ralph Wiggum plugin or Ralphie for autonomous loops, tasks won't completely replace those. Ralph is still useful for that single-minded don't stop until it's done behavior. But for coordinating work across multiple agents and sessions, tasks are the proper solution now. I think this is the direction AI coding tools should be going. We're moving from AI as a helper to AI as a team. And when you have a team, you need proper project management. Tasks are Claude Code's answer to that.

Overall, it's pretty cool. Anyway, share your thoughts below and subscribe to the channel. You can also donate via super thanks option or join the channel as well and get some perks. I'll see you in the next video. Bye.

</details>
