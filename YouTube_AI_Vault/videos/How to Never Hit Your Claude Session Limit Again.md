---
title: "How to Never Hit Your Claude Session Limit Again"
video_id: _qZvORxGqI0
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-04-20
processed: 2026-07-05
duration: "24:49"
url: https://www.youtube.com/watch?v=_qZvORxGqI0
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [token-management, context-engineering]
tools: [Claude Code, Docling, GitHub, Context Mode, Claude Context]
llms: [Claude Opus, Claude Haiku]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# How to Never Hit Your Claude Session Limit Again

![thumbnail](https://i.ytimg.com/vi_webp/_qZvORxGqI0/sddefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=_qZvORxGqI0) | 📅 Uploaded [[uploaded/2026-04-20]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Claude Code rereads your entire conversation on every message, so cost compounds rather than adds — one developer found 98.5% of a 100+ message session's tokens were spent just rereading old history. This video walks through why that happens (context rot, late auto-compaction), the five things you can do about it (continue, rewind, clear, compact, sub-agents), a custom token dashboard, and 10 practical habits — from markdown conversion to a 120K-token personal ceiling — that cut token burn without a subscription upgrade.

**Watch this if:** you keep hitting Claude Code session limits and want concrete habits, not just "buy the bigger context window," to fix it.

## Key Takeaways
- Every message resends the entire conversation history, so cost grows exponentially, not linearly — message 1 might cost 500 tokens while message 30 costs 15,500 purely from rereading everything before it; a fresh Claude Code session can already burn 8,000-62,000+ tokens before you type anything, so run `/context` first to check your baseline.
- Context rot is real and measurable: retrieval accuracy drops from 92% at 256K tokens to 78% at 1M tokens, and a GitHub analysis of 18,000 thinking blocks found thinking depth dropped 67% and "edit without reading" jumped from 6% to 34% as sessions got longer.
- Auto-compaction fires at ~95% of the context window (Claude's least intelligent point) and keeps only 20-30% of the original detail — manual compaction around 60% is better, but the creator's actual habit is a custom `/session-handoff` skill: summarize decisions/files/next-steps, `/clear`, then paste the summary back in for a fully reoriented fresh context.
- After every response you effectively have five choices — continue, `/rewind` (drop everything after a chosen point, cleaner than just telling Claude "try again" and leaving the failed attempt polluting context), `/clear`, `/compact`, or delegate to a sub-agent with its own fresh context window (which can run on a cheaper model like Haiku for big savings with similar quality).
- Practical tips covered: watch your session-limit meter and be strategic about when to push it; convert PDFs/DOCX/HTML to Markdown before feeding them to Claude (e.g. ~65-70% fewer tokens for PDF, ~90% fewer for HTML) using a tool like Docling; use `/by the way` (`/btw`) for side questions that don't pollute conversation history; start every session in plan mode (a habit borrowed from Claude Code creator Boris Cherny); and keep CLAUDE.md under ~200 lines/2,000 tokens since it loads every session.
- The creator built and is open-sourcing a token dashboard (via GitHub, shared in his Skool community) showing sessions, turns, input/output tokens, cache read/create, and per-prompt/per-file/per-command breakdowns to spot where tokens are actually going.
- Philosophy on the 1M-token window: it's "insurance, not a goal to fill" — bigger windows just invite worse habits and more room for context rot; the creator personally never goes above ~120K tokens (~12%) even on Opus with a 1M window, and recommends session chaining (discovery session → planning session → execution session) for big projects instead of one giant session.
- A curated list of 10 community GitHub repos claiming 60-90% token reduction is mentioned as a starting point, with the advice to feed the list to Claude Code and ask which 2-3 fit your specific project rather than installing all of them.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the entire video's subject: its context window, `/context`, `/rewind`, `/compact`, `/clear`, `/by the way`, plan mode, CLAUDE.md discipline, and sub-agent delegation are all walked through in detail
- [[topics/Docling]] — recommended as a tool to convert PDFs/DOCX/HTML into token-efficient Markdown before feeding documents to Claude
- [[topics/GitHub]] — hosts the creator's token-dashboard repo, which he's making public for the community to set up themselves
- [[topics/Context Mode]] — named in the 10-repo token-reduction roundup as a tool that sandboxes raw tool output into SQLite instead of dumping it into context
- [[topics/Claude Context]] — named in the same 10-repo token-reduction roundup as one of the community tools for reducing token usage

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — the model the creator runs with the full 1M-token context window, though he personally caps his own usage around 120K tokens regardless
- [[topics/Claude Haiku]] — recommended as the cheaper model to assign to sub-agent tasks (e.g. summarization) since quality stays comparable at a much lower cost

## 📡 Protocols & Standards
- [[topics/MCP]] — named as one of the context-window occupants (alongside skills and agents) that contributes to a session's fixed startup token overhead

## ✅ Action Items
- Run `/context` in a fresh Claude Code session to see your real startup token overhead before assuming your CLAUDE.md/skills/MCP servers are lean.
- Build a session-handoff habit (manual summary + `/clear` + paste back in) instead of waiting for auto-compaction at 95%.
- Convert PDFs/DOCX/HTML to Markdown with a tool like Docling before feeding large documents into a session.
- Delegate research/verification/summarization work to sub-agents, and explicitly request a cheaper model (like Haiku) for those sub-agent tasks.
- Keep CLAUDE.md under ~200 lines and move specialized instructions into on-demand skills or context files instead of loading everything every session.

## 🔗 Related Videos
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Haiku, Claude Opus, GitHub
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, GitHub, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Haiku, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, MCP
- [[videos/Planning In Claude Code Just Got a Huge Upgrade]] — shared: Claude Code, Claude Haiku, Claude Opus, GitHub

## Timeline
- `0:00` — Intro: session limits are a community-wide problem
- `0:27` — How tokens actually work: exponential cost from rereading full history
- `3:24` — Context rot and why auto-compaction at 95% is too late
- `5:45` — The five post-response options: continue, rewind, compact, clear, sub-agents
- `11:35` — Practical token tips: watching your limit, Markdown conversion, `/by the way`, plan mode, CLAUDE.md discipline
- `16:06` — Walkthrough of the custom token usage dashboard
- `18:30` — Why the creator skips the 1M-token window and caps at ~120K
- `22:16` — 10 community GitHub repos for 60-90% token reduction
- `24:00` — Final thoughts

## Transcript
<details>
<summary>Full transcript</summary>

If you use Claude, this video is going to save you money today. Hitting session limits has been a huge issue lately across the entire community, so today I'm going to show you everything I know about how to make sure you don't hit your limit — a custom token dashboard I built, custom skills to help manage session limits, the best free tools to reduce tokens, and Anthropic's actual best practices.

Context is basically everything Claude Code can see at one time: the system prompt, the full conversation, every tool call and output, every file read, every skill, MCP server, or agent in the project — think of it as Claude's current working memory. Claude Code gives a 1 million token context window, but before you type anything you're already burning around 8,000 tokens from startup overhead (system prompts, CLAUDE.md, context files, MCP tools, skills) — it could be way more; the creator once found 62,000 tokens on a fresh session. Run `/context` in a fresh session to see your own number.

One key thing about how tokens work: every time you send a message, Claude rereads the entire conversation from the beginning, and all of that is charged. So message 1 might cost 500 tokens, message 30 might cost 15,000+ because it's rereading everything before it — cost compounds, not adds. One developer tracked a 100+ message chat and found 98.5% of all tokens were spent just rereading old history. After 30 messages you might already be at nearly a quarter million cumulative tokens.

Context rot is basically "AI dementia" — as a session grows, the model's attention spreads across every token ever sent, and it gets distracted, forgets things, contradicts itself, edits files without reading them, and gets vague. Retrieval accuracy drops from 92% at 256K tokens to 78% at 1 million — so even filling the window makes the model measurably worse at finding what it needs, meaning token efficiency actually goes down as sessions grow.

Auto-compaction kicks in around 95% of the way through the window — way too late, per community consensus — keeping only about 20-30% of original detail, and it happens at the model's least intelligent point (deep in context rot). Manual compaction around 60% through beats that every time. Anthropic's own framing: after every response you have five options — continue (just keep messaging), `/rewind` (jump back to a previous message and drop everything after), `/clear` (start fresh), `/compact` (summarize and replace history), or delegate to a sub-agent (fresh context window, returns a result).

`/rewind` is Anthropic's top recommendation — double-tap escape or run it directly, jump back to any previous message, and everything after gets dropped. It's more powerful than it seems: when Claude does something wrong and you just say "that didn't work, try this instead," the failed attempt is still sitting in context, still being reread every time, polluting future responses. Rewinding keeps context clean, and there's a "summarize from here" option that creates a handoff message for the next context.

On compact/clear: the documented rule of thumb is `/clear` for a new task and `/compact` for continuing the same task, but the creator doesn't use `/compact` at all — instead, around 120,000 tokens (~12% of a 1M window on Opus), he asks Claude for a full summary of everything done and the current status, takes that summary, runs `/clear`, and pastes it back in — a reset that doesn't feel like one because the context is preserved. This requires storing data externally too (tracking sheets, activity logs, task lists) so nothing is lost. He built a `/session-handoff` skill for this: it reads the whole conversation, analyzes it, and outputs where it started, decisions locked, what shipped, key files for the next session, running state, verification notes, deferred/open questions, and a pick-up point — copy that, `/clear`, paste it in, and the project is fully reoriented with a fresh context window.

Sub-agents get their own fresh context window, do their own work/research, synthesize results, and return output to the main session — like a research intern you don't watch work, you just want the summary back. You can explicitly say "spin up a sub-agent to verify this" or "review the codebase and summarize," and each sub-agent can use a cheaper model — e.g. explicitly requesting Haiku for a summarization sub-agent task can be much cheaper than Opus doing it, with comparable quality. The key is knowing which tasks are safe to delegate.

Practical tips: watch your session-limit meter constantly (keep it visible on a second monitor) and be strategic — if you're close to the limit near the end of a long session, take a break; if you have plenty left before a reset, use it aggressively on heavy work. Converting documents to Markdown is a huge token reduction: HTML to Markdown is about 90% fewer tokens, PDF to Markdown about 65-70% fewer, DOCX to Markdown about 33% fewer — meaning roughly 3x more content fits in the same context window (a 40-page PDF could take the same space as a 130-page Markdown file). Use a tool like Docling to convert files in seconds, since tokenizers process plain text far more efficiently than layout/metadata/formatting noise. Use `/by the way` (`/btw`) for quick side questions that open an overlay without entering your conversation history. Start every session in plan mode — Boris Cherny, Claude Code's creator, does this, and spending tokens upfront to nail the plan before building means you don't have to correct course later, ultimately cheaper overall; the creator uses things like Ultra Plan and Superpowers for this. Keep CLAUDE.md under roughly 200 lines / 2,000 tokens since it loads every session — move specialized instructions into on-demand context files or skills, and use a `.claudeignore` file to exclude folders/files Claude shouldn't read, especially on large repos. Output tokens cost more than input tokens, but simply telling Claude to "be concise" doesn't move the needle much in practice — a tested "caveman" terseness plugin saved less than expected, since so many output tokens are spent outside the visible reply.

Knowing where your tokens actually go matters, so the creator built a token dashboard (to be made public via GitHub through his Skool community) showing sessions, turns, input/output tokens, and cache read/create across the past 7 or 30 days, broken down by model, project, and tool. It surfaces things like a project with unusually more input than output tokens (traced back to having Claude read and reorganize an entire project), lets you inspect which prompts consumed the most tokens and drill into the full session/tool-call history, and includes project and (early-stage) skill/tips breakdowns showing which files and bash commands were used most often.

Some stats: a GitHub analysis of 18,000 thinking blocks across 7,000 sessions found thinking depth dropped 67% and edit-without-reading rose from 6% to 34% as sessions lengthened. One user's token spend went from $345/month to $42,000/month with completely flat output quality — pure bad context management. And the retrieval-accuracy stat again: 92% at 256K tokens down to 78% at 1 million. Just because you can fill a million tokens doesn't mean you should — people see "1 million" and get wasteful, stop using sub-agents, stop being intentional, and dump everything into one giant session because the progress bar looks half full. But the underlying rules haven't changed: a bigger window doesn't mean better output, just more room for context rot. The 1M window is insurance, not a goal to fill. The creator personally never goes above about 120K tokens (~12%) even running Opus with a 1M window — a habit carried over from the 200K-window era when he'd clear/compact at about 60% (120K then too). He also uses session chaining for big projects: a discovery session (read PDFs/codebase, produce a summary doc), a planning session (reads that summary, creates a plan), and an execution session (implements the finished plan) — like an assembly line where each session has a specialized task. Beginners might stick with the 200K window to build discipline before graduating to 1M — more space just invites worse habits.

There's also a curated list of 10 community GitHub repos claiming 60-90% token reduction in Claude Code, each tackling context management differently: a CLI proxy that filters terminal output before it hits context, a tool that sandboxes raw tool output into SQLite instead of dumping it into context, a code-review-graph tool, a terseness-focused CLAUDE.md file, a couple of "token optimizer" MCP-based tools, and a vector-search-based context tool. The advice is not to install all 10, but to feed the list to Claude Code and ask which 2-3 fit your specific project best. Finally: if a session goes off the rails, even if you're not deep into context rot, just clear it or start a new one — for your sanity and the session's.

</details>
