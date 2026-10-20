---
title: "18 Claude Code Token Hacks in 18 Minutes"
video_id: 49V-5Ock8LU
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-04-02
processed: 2026-07-05
duration: "18:57"
url: https://www.youtube.com/watch?v=49V-5Ock8LU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [token-management, claude-code-cost-optimization]
tools: [Claude Code, Google Workspace CLI, Codex]
llms: [Claude, Claude Sonnet, Claude Opus, Claude Haiku]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# 18 Claude Code Token Hacks in 18 Minutes

![thumbnail](https://i.ytimg.com/vi/49V-5Ock8LU/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=49V-5Ock8LU) | 📅 Uploaded [[uploaded/2026-04-02]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A tiered breakdown of 18 token-management hacks for Claude Code, from easy wins (clear between tasks, disconnect unused MCP servers, batch prompts) to intermediate habits (lean CLAUDE.md, surgical file references, manual compact at 60%) to advanced strategies (right-sizing model choice, understanding sub-agent token cost, timing sessions around peak/off-peak demand). The core insight: every message resends the entire conversation history, so cost compounds exponentially rather than adding linearly, and context hygiene — not a bigger plan — is what actually fixes hitting usage limits.

**Watch this if:** you're burning through your Claude Code session limit faster than expected and want concrete habits to fix it instead of just upgrading your plan.

## Key Takeaways
- Every message resends the entire conversation from the start, so cost compounds exponentially, not linearly — one tracked 100+ message session found 98.5% of all tokens were spent just rereading old chat history, and "lost in the middle" means bloated context also degrades output quality, not just cost.
- Tier 1 (easy): use `/clear` between unrelated tasks, disconnect unused MCP servers (one server can cost ~18,000 tokens/message — prefer CLIs like the Google Workspace CLI over MCP where available), batch multi-step prompts into one message, use plan mode with a "95% confidence before changes" rule in CLAUDE.md, run `/context` and `/cost` to see where tokens go, set up a status line, keep your usage dashboard open, be surgical about what you paste, and actually watch Claude work instead of walking away.
- Tier 2 (intermediate): keep CLAUDE.md under ~200 lines and treat it as an index/router rather than documentation, reference specific files/functions instead of whole repos, manually `/compact` around 60% capacity (auto-compact waits until ~95%, by which point context is already degraded), avoid stepping away for more than 5 minutes since the prompt cache expires and the next message reprocesses everything at full cost, and restrict which shell commands Claude can run since full command output enters the context window.
- Tier 3 (advanced): match model to task — Sonnet for default coding, Haiku for sub-agents/formatting/simple tasks, Opus only for deep architectural planning (kept under ~20% of usage); bring in Codex via its official plugin to review a codebase Opus/Sonnet built, saving Claude tokens on the review pass.
- Sub-agents cost roughly 7-10x more tokens than a single-agent session because each spins up with its own full context reload — delegate one-off research/summarization tasks to Haiku sub-agents rather than defaulting to expensive agent teams.
- Peak hours (8am-2pm Eastern on weekdays) drain the 5-hour session window faster than off-peak (afternoons, evenings, weekends) — schedule big refactors and multi-agent sessions for off-peak, and strategically "go heavy" near a reset versus stepping away when running low with time left.
- Treat CLAUDE.md as your project's "constitution" — store stable architecture decisions and progress summaries there (not conversations) so every future prompt gets shorter, and consider a self-updating "applied learning" section for recurring failures, capped and reviewed regularly so it doesn't bloat.
- Hitting your usage limit isn't inherently bad — if you're following good context hygiene, hitting it means you're actually using the tool productively; the real problem is unnecessary reprocessing, not the plan tier.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI agent every hack in the video is about optimizing token usage for, including its `/clear`, `/context`, `/cost`, `/compact`, `/status line`, and plan-mode features
- [[topics/Google Workspace CLI]] — recommended as a lighter-weight, cheaper alternative to running the Google Workspace/Calendar MCP server, which eats significant tokens per message
- [[topics/Codex]] — suggested via its official Claude Code plugin as a way to review a codebase Opus/Sonnet built, offloading review work from Claude's own token budget

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose token-charging mechanics (rereading full history every turn) motivate every hack in the video
- [[topics/Claude Sonnet]] — recommended as the default model for most coding work
- [[topics/Claude Opus]] — recommended only for deep architectural planning, kept to roughly 20% of overall usage
- [[topics/Claude Haiku]] — recommended for sub-agents, formatting, and simple one-off tasks to cut cost

## 📡 Protocols & Standards
- [[topics/MCP]] — identified as a major invisible token cost since every connected server's tool definitions load into context on every message; recommended to disconnect unused servers and prefer CLIs where possible

## ✅ Action Items
- Run `/context` and `/cost` at the start of a session to see exactly where your tokens are going.
- Disconnect MCP servers you're not actively using each session; swap MCP for a CLI where one exists.
- Add a "don't make changes until 95% confidence, ask follow-up questions" rule to your CLAUDE.md and default to plan mode on real tasks.
- Trim CLAUDE.md to under ~200 lines and treat it as an index pointing to other files rather than a place to document everything.
- Set up a status line showing model, context percentage, and token count.
- Manually `/compact` around 60% capacity instead of waiting for auto-compact at 95%.
- Restrict which shell commands Claude can run on a given project to avoid command-output bloat.
- Match model to task: Sonnet default, Haiku for sub-agents/simple work, Opus only for architecture-level planning.
- Schedule heavy multi-agent or refactor sessions for off-peak hours (afternoons, evenings, weekends).

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Haiku, Claude Opus
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, Claude Sonnet
- [[videos/Claude Code (New Lazy-MCP Loading) They FINALLY FIXED the BIGGEST ISSUE of CLAUDE CODE]] — shared: Claude Code, Claude Opus, Claude Sonnet, Codex
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Haiku, Claude Sonnet
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet

## Timeline
- `0:00` — The token problem: people hitting Claude Code limits far faster than expected
- `0:48` — How tokens actually work: every message rereads the entire conversation
- `3:04` — Tier 1 hacks: clear, disconnect MCPs, batch prompts, plan mode, `/context`/`/cost`, status line, dashboard, precise pasting, watch it work
- `8:48` — Tier 2 hacks: lean CLAUDE.md, surgical file references, compact at 60%, cache timeout on breaks, command output bloat
- `12:15` — Is hitting your limit actually bad? A mindset reframe
- `13:17` — Tier 3 hacks: right model per task, sub-agent token cost, peak/off-peak timing, CLAUDE.md as constitution
- `17:32` — What to do right now: the action checklist
- `18:12` — Final thoughts: context hygiene over bigger plans

## Transcript
<details>
<summary>Full transcript</summary>

In the past week or so, many people have been complaining about hitting their Claude Code limit insanely fast — even on the $200/month plan, and even after an Anthropic employee mentioned adjustments to peak/off-peak hours. This video covers 18 token-management hacks, organized tier one through tier three in increasing sophistication. Understanding how tokens actually work first is key to reverse-engineering how you should work: a token is roughly the smallest unit of text an AI model reads and charges for (roughly one word as a baseline), and every message resends the entire conversation from the beginning — message one, its reply, message two, its reply, all the way to your latest prompt, every single time. This means

cost compounds rather than adds — message one might cost 500 tokens, message 30 costs 15,000 because it's rereading everything before it. One developer tracked a 100+ message chat and found 98.5% of all tokens were spent rereading old chat history. Beyond your own messages, Claude also reloads CLAUDE.md, MCP servers, system prompts, skills, and files on every turn as invisible overhead, and bloated context doesn't just cost more, it produces worse output too — the "lost in the middle" phenomenon means models pay most attention at the start and end of a session, with content in the middle getting ignored. Moving into tier one hacks (nine easy-to-implement ones): number one, start fresh conversations —

use `/clear` between unrelated tasks rather than carrying topic-A context into a topic-B conversation, since every message in a long chat is exponentially pricier than the same message in a fresh one. Number two, disconnect MCP servers — each connected server loads its full tool definitions into context on every message (one server alone can be ~18,000 tokens/message), so run MCP only at session start and disconnect what you don't need; where a CLI exists (e.g. Google Workspace CLI instead of a Google Calendar MCP server), prefer it — faster, cheaper, and likely the direction agents are heading. Number three, batch prompts into one message — three separate messages cost three times what one combined message costs, so send "summarize, extract issues, suggest a fix" as one prompt; if Claude gets something slightly wrong, edit and regenerate the original message rather than sending a follow-up correction, since follow-ups stack permanently onto history while edits replace the bad exchange (though single-task-at-a-time prompting can sometimes yield better quality — a tradeoff to weigh). Number four, use plan mode before any real task —

it lets Claude map its approach and ask the right questions, preventing the single biggest source of waste: going down the wrong path and having to scrap the work. Add something like "do not make any changes until you have 95% confidence in what you need to build; ask follow-up questions until then" to CLAUDE.md. Number five, run `/context` and `/cost` — `/context` shows exactly what's eating tokens (conversation history, MCP overhead, loaded files), `/cost` shows actual usage and estimated spend; running `/context` in a completely fresh session with MCPs cleared out still showed 51,000 tokens consumed before typing anything, from the system prompt, tools, custom agents, skills, and memory files. Number six, set up a status line —

visible only in the terminal, showing the active model, a usage progress bar, and context percentage/token count (e.g. 5%, or 52K of 1M) — set it up by running `/status line` in Claude Code and describing the layout you want. Number seven, keep your usage dashboard open so you can pace yourself by checking every 20-40 minutes rather than getting blindsided by hitting the limit (or automate a check-in that texts/Slacks you when you're getting close). Number eight, be smart with pasting — before dropping in a whole document, ask whether Claude actually needs the whole thing, or just one function or paragraph; be as precise about what you feed it as you want it to be about what it reads. Number nine, actually watch Claude Code work instead of firing a prompt and walking away — watching catches it going down a wrong path or looping on the same files early, since in a bad loop roughly 80% of tokens produce zero value. Moving into tier two

hacks (five of them): number one, keep CLAUDE.md lean — auto-read at the start of every chat, so keep it under ~200 lines covering only tech stack, coding conventions, build commands, and rules like the 95%-confidence one, treating it as an index that routes to where more detailed information lives rather than a place to document everything (the same lean-index mindset applies to skills and reference sheets — someone built a lean index pointing straight to specific Claude Code documentation URLs instead of having Claude search a whole database). Number two, be surgical with file references — say "check the verifyUser function inside auth.js" rather than "here's my whole repo, find the bug," or use `@filename` to point directly at files instead of letting Claude explore freely. Number

three, compact around 60% capacity rather than waiting for auto-compact at ~95%, by which point context is already degraded — run `/context` or check your status line, then `/compact` with specific instructions on what to preserve; after three to four compacts in a row quality starts to degrade, so at that point get a session summary, `/clear`, and feed the summary back in. Number four, short breaks cost you — Claude Code's prompt caching avoids reprocessing unchanged context, but the cache has a 5-minute timeout, so stepping away longer than that means your next message reprocesses everything from scratch at full cost; `/compact` or `/clear` before stepping away. Number five, command output bloat — when Claude runs shell commands, the full output (e.g. 200 commits' worth) enters the context window, so deny permissions for commands a project doesn't need and be intentional about what you let it run. A brief aside: hitting

your usage limit isn't inherently bad — if you're following good token hygiene rather than being wasteful, hitting the limit just means you're genuinely using the tool as a power user should; the goal is getting full value from it, not avoiding the wait. Moving into tier three (four hacks plus bonuses): number one, pick the right model — Sonnet for default coding work, Haiku for sub-agents/formatting/simple tasks, and Opus only for deep architectural planning when Sonnet falls short, kept under roughly 20% of total usage; for big codebases, bring in Codex via its official Claude Code plugin to review work that Opus and Sonnet built together, saving Claude tokens on the review pass. Number two, the cost of sub-agents — agent workflows use roughly 7-10x more tokens than a single-agent session because each sub-agent wakes up with a full separate context reload; delegate one-off research or summarization tasks to Haiku sub-agents to keep cost down, and use full "agent teams" sparingly since they're expensive despite sometimes yielding higher-quality output. Number three, understand peak hours — the

5-hour session window drains faster during peak demand (8am-2pm Eastern on weekdays) versus off-peak (afternoons, evenings, weekends), so schedule big refactors or multi-agent sessions for off-peak; a related "hack 3.5" is keeping your Claude usage dashboard open — go heavy near a reset if you have room left in your allocation, but step away and take a break if you're near your limit with lots of time left, rather than burning the last 5% on something small and losing your flow state mid-task. Number four, treat CLAUDE.md as your project's "constitution" — store stable architecture decisions and progress summaries there rather than conversations, so future prompts get shorter since you never have to retype an architectural call once it's saved. Layer in rules that tell Claude to spawn Haiku sub-agents for any exploration or multi-file

analysis and return only summarized insights, and consider a self-updating "applied learning" section (one-line bullets under 15 words, added only when something fails repeatedly or a workaround is found) — checked on frequently so it doesn't bloat unnoticed. The recap checklist: run `/context` and `/cost`, set up a status line showing model/context percentage/token count, keep your usage dashboard visible, disconnect unused MCP servers, start complex tasks in plan mode, `/clear` between unrelated tasks, manually compact around 60%, batch multi-step instructions into single messages, and schedule heavy sessions for off-peak hours. There's a real balance between quality and cost — sometimes higher quality is worth paying more for — but the core message is that most people don't need a bigger plan, they need to stop resending their entire conversation history dozens of times over. It's not a limits problem, it's a context hygiene problem.

</details>
