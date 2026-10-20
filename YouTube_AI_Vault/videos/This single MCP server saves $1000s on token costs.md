---
title: "This single MCP server saves $1000s on token costs"
video_id: Lj6GAVmqkOo
channel: "[[channels/Indie Hacker News]]"
uploaded: 2026-05-06
processed: 2026-07-05
duration: "7:59"
url: https://www.youtube.com/watch?v=Lj6GAVmqkOo
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [context-window-management, token-cost-reduction]
tools: [Context Mode, Claude Code, Cursor, Codex, Antigravity, Gemini CLI, OpenCode, SQLite, Bun]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# This single MCP server saves $1000s on token costs

![thumbnail](https://i.ytimg.com/vi/Lj6GAVmqkOo/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Lj6GAVmqkOo) | 📅 Uploaded [[uploaded/2026-05-06]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Context Mode is an MCP server that sandboxes every tool call so only the distilled result enters your coding agent's context window, cutting a 315 KB Playwright snapshot to 5.4 KB and output tokens by ~70%. It works across 14 agent platforms including Claude Code and Cursor, uses a SQLite FTS5/BM25 retrieval engine to survive context compaction, and shipped 111 releases in its first 10 weeks under a source-available Elastic License 2.0.

**Watch this if:** you run a coding agent for more than an hour at a stretch and keep hitting compaction, or you're paying real money for tokens burned on raw tool output.

## Key Takeaways
- Context Mode intercepts MCP tool calls, runs them in a sandbox, and only lets the final distilled result enter your context window — turning a 315 KB raw Playwright snapshot into 5.4 KB.
- It supports 14 coding agent platforms (Claude Code, Cursor, Codex, Antigravity, Gemini CLI, and more), installs in about two commands, and adds 11 new MCP tools plus four automatic hooks.
- Session continuity is solved by tracking every file edit, git operation, task, and decision in a SQLite database indexed with FTS5, so when the agent compacts, it re-retrieves only relevant history via BM25 search instead of losing state.
- "Think in code" mode has the agent write a script to count/analyze things instead of reading dozens of files into context — turning 47 read calls into one logged result and 700 KB of file content into 3.6 KB of output.
- A system-prompt rewrite forces terser, "caveman"-style model output — dropping articles, hedging, and pleasantries — for roughly a 70% cut in output tokens without losing accuracy.
- It's a single-maintainer project (MK) that hit #1 on Hacker News, pulled 12.9k GitHub stars and 893 forks in 10 weeks, and has shipped 111 releases (roughly two a day) since launch.
- Real trade-offs: it's Elastic License 2.0 (source-available, not OSI open source, so it's a no-go under strict MIT/Apache-only company policies), hook setup on some platforms needs manual config, and the fast release cadence means occasional regressions.

## 🛠 Tools & Software
- [[topics/Context Mode]] — the MCP server itself: sandboxes tool calls, indexes session state in SQLite, and rewrites output for token efficiency
- [[topics/Claude Code]] — one of the 14 supported agent platforms; install is two commands via a marketplace plugin
- [[topics/Cursor]] — supported platform; noted as needing manual hook config rather than push-button setup
- [[topics/Codex]] — supported platform; also flagged as needing manual hook config
- [[topics/Antigravity]] — supported coding agent platform named among the 14 integrations
- [[topics/Gemini CLI]] — supported coding agent platform named among the 14 integrations
- [[topics/OpenCode]] — listed among the 14 supported coding agent platforms
- [[topics/SQLite]] — backs the knowledge base with FTS5 full-text search and BM25 ranking for session-state retrieval
- [[topics/Bun]] — auto-detected in the sandbox for 3-5x faster JavaScript execution

## 🤖 LLMs Mentioned
- [[topics/Claude]] — cited as a typical agent used to research a repo and burn ~100,000 tokens reading irrelevant files, the exact problem Context Mode targets

## 📡 Protocols & Standards
- [[topics/MCP]] — Context Mode is itself an MCP server that intercepts and sandboxes every MCP tool call before it reaches the model's context

## ✅ Action Items
- If you run an agent for more than an hour at a time, install Context Mode and watch the built-in status line for real-time token/dollar savings.
- Check your company's OSS license policy before adopting it — Elastic License 2.0 is source-available, not MIT/Apache, and may be a blocker.
- On Cursor or Codex, budget time for manual hook config since it isn't push-button on every platform.
- Run `ctx upgrade` periodically given the ~2-releases-a-day cadence, and expect occasional regressions.

## 🔗 Related Videos
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Codex, Cursor, Gemini CLI
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Codex, Cursor
- [[videos/The HTTP Header Trick That Cuts AI Agent Costs in Half!]] — shared: Claude Code, Codex, Cursor, Gemini CLI
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude, Claude Code, Codex, Cursor
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Codex, MCP
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor, Gemini CLI, OpenCode
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor, MCP, OpenCode
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Cursor, MCP

## Timeline
- `0:00` — The leak: Context Mode hits #1 on Hacker News, 570 points, 12.9k stars in 10 weeks
- `1:14` — The README: framed as "the other half of the context problem" — what fills the window, not just its size
- `2:04` — Why it's different: unlike summarization or compaction, it sandboxes tool output entirely
- `2:48` — The four sides: context saving, session continuity, "think in code," output compression
- `4:20` — Architecture: SQLite FTS5 + BM25 ranking, Porter stemming, trigram matching, reciprocal rank fusion, 11 sandboxed language runtimes
- `5:08` — Install: two commands on Claude Code, or MCP-only install without routing enforcement
- `5:37` — Latest release: v1.0.11, part of a 111-release, ~2-per-day cadence since launch
- `6:22` — Who it's for: heavy agent users, repo-research burners, and MCP/skill builders studying the architecture
- `7:02` — Honest verdict: Elastic License 2.0 caveats, manual hook setup on some platforms, fast-moving regressions

## Transcript
<details>
<summary>Full transcript</summary>

Your coding agent is leaking context and someone finally fixed it. Here's something kind of weird that's been quietly trending on GitHub the last couple weeks. There's a project called context mode that just hit number one on Hacker News with 570 points, and it's already running across 14 different coding agents from Claude code to cursor to Codex to anti-gravity. 12.9 thousand stars, 893 forks, and it shipped its first version about 10 weeks ago.

The pitch is very specific. Every MCP tool call you make is dumping raw data into your context window. A Playwright snapshot costs 56 kilobytes. 20 GitHub issues cost 59 kilobytes after 30 minutes of agent work. 40% of your context is gone, and then your agent compacts the conversation and forgets what file it was editing. 12.9 thousand stars on the repo, 570 points on Hacker News, 14 agent platforms supported, and a 98% context reduction on real workloads. The numbers are not subtle. And the wild part is this isn't a research paper, it's an MCP server you install in about 30 seconds and your agent starts using it the next session. Let me show you what's actually inside.

Okay, so this is the read me and the framing here matters. The author calls this the other half of the context problem. Most people fixate on context windows getting bigger, 200,000, 1 million tokens, and assume the problem is solved. The argument here is that the real problem is what fills the window. Every tool call dumps raw output. The agent compacts, the agent forgets, you start over. Context mode is an MCP server that intercepts those tool calls, runs them in a sandbox, and only the result enters your context.

The list of companies running it on the read me is honestly wild. Microsoft, Google, Meta, Amazon, Stripe, Notion, GitHub, Cursor, Superbase all listed at the top. The HN front page bumped it to 10,000 stars in about a week and it kept climbing.

Here's why this is different from every other context optimization people have tried. The usual approach is summarize. You finish a tool call, you summarize the output before it hits the context. That works for pros. It falls apart on logs and snapshots. The other approach is compaction, which every coding agent already does. And the compaction ironically destroys the working memory you needed. Context mode does neither of those things. The repo specs in one frame, 12.9 thousand stars, 893 forks, an elastic license 2.0, which is source available, and 111 shipped releases in 2 and 1/2 months. That last one is the tell — two releases a day every day since launch.

Okay, so the four sides of the context problem and what context mode does about each one. Side one is context saving and this is the obvious one. Tool output gets sandboxed in a subprocess and only the final result enters your context. 315 kilobytes of raw output becomes 5.4 kilobytes. Side two is session continuity. Every file added, every get operation, every task, every error, every user decision gets tracked in SQLite. When the conversation compacts, instead of dumping all that data back into context, context mode indexes it into FTS5 and lets the model pull only what's relevant via BM25 search. The model picks up exactly where you left off without reprompting.

Side three is the one I find most interesting. They call it think in code. Instead of reading 50 files into your context to count something, the agent writes a script that does the counting and only logs the answer. So 47 read calls becomes one CTX echo call. 700 kilobytes of file content becomes 3.6 kilobytes of output. The framing is the LLM shouldn't be a data processor. It should be a code generator that programs the analysis. Side four is output compression. The system prompt itself rewrites how the model talks. Drop articles, drop hedging, drop pleasantries, technical substance exact. They quoted as terse like caveman and it cuts output tokens by about 70% without losing accuracy.

Under the hood, the architecture is genuinely interesting. The knowledge base is built on SQLite FTS5 with BM25 ranking, which is a classic information retrieval algorithm that scores documents by term frequency and document length. Search runs two strategies in parallel, Porter stemming and trigram substring matching, and the results get merged with reciprocal rank fusion. Multi-term queries get a proximity re-ranking pass so passages where your terms appear close together rank higher. They threw in fuzzy correction with Levenshtein distance so Kubernetes finds Kubernetes. The sandbox supports 11 language runtimes including JavaScript, TypeScript, Python, Shell, Ruby, Go, Rust, PHP, Perl, R and Elixir. Bun is auto-detected for three to five times faster JS execution.

Install on Claude code is two commands. You add the marketplace, you install the plugin and the next session your agent has 11 new MCP tools and four hooks running automatically. No config file, no project edits. The session start hook injects the routing instructions at runtime. There's an MCP only path if you want it without the routing enforcement. Just Claude MCP add context mode and you get the tools. The model just won't be nudged to prefer them over raw bash and read.

Version 1.0.11 shipped two days ago and gives you a clean look at the release cadence. The change is one line, a refactor of how route pre-tooling picks up the platform parameter plus a CI test alignment, so the rebuild test stops failing on three operating systems. They've shipped 111 releases since launch, which is roughly two per day, every single day. The status line is opt-in and shows you context savings in real time. Dollars saved this session, dollars saved across sessions, percent efficient. The personal analytics dashboard, CTX Insight, opens to a local web UI with 90 metrics, 37 insight patterns, and four composite scores covering productivity, quality, delegation, and context health.

Okay, so who should actually be paying attention to this? If you write code through an agent for more than an hour at a time, you've already hit the compaction problem. You're the target. If you've ever asked Claude or Cursor to research a repo and watched it burn 100,000 tokens reading files that didn't matter, you're the target. If you build agentic skills or MCP servers, the architecture choices in here, FTS5, BM25, RRF merging, sandbox isolation, are an open textbook for how to build context-efficient tools. And if you're paying for tokens, the 70% output compression alone pays for the install in about a week.

Okay, let's be real about the tradeoffs. The license is Elastic License 2.0, which is source available, not open source. So if your company has a strict MIT or Apache only policy, you can't ship this. The hook setup on a few platforms like Cursor and Code X needs manual config files. It's not all push button. And the project is moving fast. Two releases a day means you'll occasionally hit a regression and need to run CTX upgrade. But for everything that's wrong with it, the project is real. 12.9 thousand stars in 10 weeks. 111 shipped releases. 14 agent platforms covered. Full SQLite FTS5 retrieval engine. All built by one maintainer named MK with PRs landing from contributors at companies on the list. If you write code through an agent in 2026 and you're not at least testing this, you're paying token costs that other people aren't. Links are in the description. Thanks for watching. I'll catch you tomorrow.

</details>
