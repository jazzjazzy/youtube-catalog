---
title: "Your CLAUDE.md Is Making Claude Code Dumber (Here's the Fix)"
video_id: aUvBevrlMtU
channel: "[[channels/Josh Pocock]]"
uploaded: 2026-04-03
processed: 2026-07-05
duration: "36:07"
url: https://www.youtube.com/watch?v=aUvBevrlMtU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [context-engineering, claude-md-optimization]
tools: [Claude Code, GitHub]
llms: [Claude, Claude Sonnet]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Your CLAUDE.md Is Making Claude Code Dumber (Here's the Fix)

![thumbnail](https://i.ytimg.com/vi_webp/aUvBevrlMtU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=aUvBevrlMtU) | 📅 Uploaded [[uploaded/2026-04-03]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> An ETH Zurich study found auto-generated CLAUDE.md files (`/init` output) decrease coding-agent success by 3% and raise cost 20%, while a SkillBench study found curated skills beat the best developer-written CLAUDE.md by 4x. The video explains the prompt hierarchy CLAUDE.md sits in, why Claude is explicitly told to ignore irrelevant context, and walks through a six-section template plus a live demo trimming a 288-line file to 46 lines.

**Watch this if:** your CLAUDE.md file has grown past 100 lines and you suspect it's hurting more than helping.

## Key Takeaways
- Claude Code injects CLAUDE.md with a system message telling the model "this context may or may not be relevant to your task... you should not respond to this context unless it is highly relevant" — bloated or generic files get silently skipped rather than followed.
- CLAUDE.md rides along on every single message in a session (it "resends" with the full history on each turn), so one bad instruction cascades through every plan, spec, and implementation for the rest of that session — unlike a single bad line of code.
- ETH Zurich's "Evaluating Agent MDs" study (hundreds of real GitHub issues, Claude Code/Codex/Qwen Code) found auto-generated (`/init`) context files cut success rate 3% and raised cost over 20%; developer-written files averaged only 4% improvement, and that 4% was inconsistent — Claude Code with Sonnet 4.5 actually showed a 2% drop.
- SkillBench found curated skills improve pass rates by 16.2 percentage points (4x the best CLAUDE.md gain) because of progressive disclosure — content loads only when relevant instead of eating tokens on every message; self-generated skills added zero benefit, mirroring the auto-generated CLAUDE.md failure.
- There are four hierarchy levels — managed policy (org-wide, unbeatable), user (`~/.claude/CLAUDE.md`, keep to 10-15 lines), project (checked into Git, the shared team brain), and subdirectory (loads only when Claude works in that folder) — and when rules conflict, more specific wins.
- A six-section template (Commands, Code Standards, Architecture, Workflow, Common Mistakes, Don'ts) answering What/Why/How in under 80 lines covers what production CLAUDE.md files actually need; Anthropic's own team keeps theirs to 60-80 lines and updates it multiple times a week.
- Boris Cherny's setup: one Git-checked-in CLAUDE.md the whole team edits, failure-driven iteration (add a rule only after Claude actually gets something wrong), `@Claude` on PRs auto-updates it via GitHub Actions, and his personal file is just two lines pointing at the team version.
- The "canary test" (add a line like "always call me Mr. Tinkerbell" to the top of CLAUDE.md) reveals whether the file is still being read — if Claude stops using the canary phrase mid-session, that's the signal context has drifted and it's time to `/clear`.
- Compliance with CLAUDE.md decays over a session: ~95% for the first 1-2 messages, 60-80% by 3-5 messages, 20-60% by 6-10, and mostly gone beyond that — which is why Boris starts sessions in plan mode and clears between them rather than letting one session run long.
- CLAUDE.md is advisory (~80% compliance per Anthropic), not enforcement — anything that must happen every time (running a formatter, blocking a dangerous command) belongs in a hook, not a CLAUDE.md rule.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the entire video is about optimizing its CLAUDE.md context file; live demo uses `/context`, `/compact`, `/clear`, and an optimizer prompt to shrink a real file
- [[topics/GitHub]] — Boris's team checks CLAUDE.md into Git and uses `@Claude` on pull requests with GitHub Actions to auto-update it after code review; also browsed for the "awesome-CLAUDE.md" curated repo of examples

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model the whole prompt hierarchy and research is framed around; its system prompt already consumes ~50 of the ~150-200 instructions a frontier model can reliably follow
- [[topics/Claude Sonnet]] — called out specifically in the ETH Zurich study as showing a 2% performance drop with developer-written CLAUDE.md files, undercutting the average 4% improvement figure

## 📡 Protocols & Standards
- [[topics/MCP]] — cited as one of the context-consuming additions (MCP servers) that grows the token baseline on top of the system prompt and tool definitions

## ✅ Action Items
- Run `/context` in Claude Code to see your actual baseline token cost before adding anything to CLAUDE.md.
- Rewrite your CLAUDE.md around the six sections (Commands, Code Standards, Architecture, Workflow, Common Mistakes, Don'ts) and target under 80-100 lines.
- Delete 80% of what `/init` auto-generates rather than keeping it as-is.
- Add a canary line (a fake instruction like a nickname) to the top of CLAUDE.md to detect when Claude stops reading it mid-session.
- Move domain-specific or rarely-needed knowledge out of CLAUDE.md into skills or plain-text pointers (progressive disclosure) instead of `@`-importing large docs.
- Add a "common mistakes" section and append a rule every time Claude actually gets something wrong (failure-driven iteration).
- Move anything that must happen every time (formatting, blocking dangerous commands) into a hook instead of a CLAUDE.md rule.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Sonnet, GitHub
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Sonnet, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Sonnet, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Sonnet, MCP
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Sonnet, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Sonnet, GitHub, MCP

## Timeline
- `0:00` — Hook: ETH Zurich and SkillBench research on CLAUDE.md performance
- `2:22` — How instructions actually reach Claude (the layer hierarchy)
- `4:23` — Why Claude is explicitly instructed to ignore irrelevant CLAUDE.md content
- `7:30` — The four-level hierarchy: managed, user, project, subdirectory
- `11:23` — The research: ETH Zurich's Evaluating Agent MDs + SkillBench
- `16:55` — The What/Why/How mental model
- `17:53` — Section-by-section template (Commands through Don'ts)
- `21:24` — Boris Cherny's actual CLAUDE.md setup and habits
- `22:50` — The canary test for detecting context drift
- `28:46` — Progressive disclosure: the three-tier loading system
- `30:59` — Live demo: optimizing a 288-line file down to 46 lines
- `32:41` — Starter templates and further resources

## Transcript
<details>
<summary>Full transcript</summary>

Your Claude MD is probably making Claude code dumber. A study from ETH Zurich tested this across hundreds of real coding tasks and found that most context files actually decrease performance and increase cost by 20%. But the answer isn't deleting your Claude.md file or your agents.md. It's writing it correctly because a second study from Skill Bench with 105 researchers, 7,000 plus test runs proved that carefully written context improves performance by 16 percentage points. The difference between a bad Claude.md and a good one is massive. So here's what we're going to be diving into in today's video: the actual research on why most Claude.md files hurt performance rather than help, the system prompts hack that explains why Claude ignores your instructions, a section-by-section template you can copy within 5 minutes, real-life examples from the creator of Claude Code, Boris, and how Next.js, OpenAI, and Humanloop structure their agent.mds and Claude.mds, a live demo of taking a 300-line bloated file down to 60 lines or less, and a free optimizer prompt to test your own CLAUDE.md.

This is all based on Anthropic's official documentation, tweets and threads from Boris (the creator of Claude Code), analysis of real production CLAUDE.md files on GitHub, and the actual research papers covered below. Before you can understand CLAUDE.md, you need to understand how instructions reach Claude in the first place — this discussion focuses on Claude since it's the top model right now, but the same logic applies to OpenAI, Codex, whatever the case is. Above everything sits the model's pre-built training (safety guardrails baked into the weights, not a prompt, and not overridable). The next layer you can interact with is Claude Code's system prompt and built-in tools — on a clean session, `/context` shows about 6,000 tokens for the system prompt plus 8,000 for tool definitions, so about 15,000 tokens before you type a character, before skills, MCP servers, and memory files add more. Layer two is where CLAUDE.md lives — injected below the system prompt, above your conversation, and advisory rather than enforced (Anthropic says it works about 80% of the time). Layer three is your actual messages, tool results, and conversation history. Humanloop discovered, by putting a proxy between Claude Code and the API, that Claude Code injects CLAUDE.md with a system message that says:

"Important, this context may or may not be relevant to your task. You should not respond to this context unless it is highly relevant to your task." Claude is explicitly told to ignore CLAUDE.md or agents.md if it decides the content isn't relevant — so the more generic or bloated your file, the more likely it gets skipped entirely. Every single message resends the entire conversation from the beginning plus your CLAUDE.md plus every MCP server definition and skill metadata — one dev tracked a 100-plus message session where 98.5% of tokens were literally just rereading old conversation history. That means CLAUDE.md rides along on every one of those reads, making it one of the highest-leverage files in your entire project: a bad instruction doesn't cause one mistake, it degrades the entire session, cascading through every spec, plan, and implementation from minute 5 to minute 30.

Token strategies aside (using `/compact`, keeping sessions shorter), CLAUDE.md fully survives `/compact` and rereads from disk every time — it never gets lost, and it's always eating tokens on every message of every project, which is exactly why keeping it lean matters. There are really four levels to CLAUDE.md, not just one file: the first is the managed policy — organization-wide, the nuclear option, living in the system directory (e.g. Program Files on Windows), unoverridable, mostly irrelevant to individuals. Level two is user instructions at `~/.claude/CLAUDE.md` — personal preferences like "always use two-space indentation" or "ask before committing," kept to 10-15 lines since it loads into every conversation across every project. The third layer is project instructions living at the project's CLAUDE.md or `.claude/CLAUDE.md` in the project root.

This is the big one most people mean when they say CLAUDE.md — checked into Git, shared with the team as the project's shared brain. Boris says the Claude Code team shares one CLAUDE.md that the whole team contributes to multiple times a week; keeping it current functions like an onboarding document for new team members, and letting it go stale is like hiring someone and never giving them an employee handbook. The fourth layer is subdirectory CLAUDE.md files, loaded only on demand when Claude is working in that specific directory — great for monorepos where, say, a Next.js frontend and Python backend

each get their own scoped rules so front-end conventions don't pollute back-end context. Context is precious and needs to be protected; when rules conflict, more specific wins (managed beats everything, project beats user, subdirectory loads only when relevant). Knowing this hierarchy alone puts you ahead of 90% of Claude Code users. Now to the research: two papers, both published in 2026. The first, ETH Zurich's "Evaluating Agent MDs" (published in February), is the first rigorous study of whether context files actually help coding agents — tested with Claude Code, Codex, and QwenCode across hundreds of real GitHub issues, comparing dev-provided instructions, no instructions, and AI-generated auto

instructions from `/init`. The auto-generated ones decreased success rate by 3% and increased cost by over 20% on average — one possible explanation for rising usage costs beyond any Anthropic-side bugs. Developer-written files only showed a 4% average improvement, and — the part nobody mentions — that 4% was inconsistent: Claude Code with Sonnet 4.5 actually showed a 2% drop with developer-written files, a finding one of the paper's authors confirmed on Hacker News. The reason: agent-generated CLAUDE.md files cause the agent to explore more, read more files, and make more tool calls on its own, but don't help it find the actually relevant files any faster — the "project overview" section everyone includes is usually useless, since agents found the right files just as fast without it. The paper's conclusion: unnecessary requirements in context files make tasks harder and degrade performance; provide minimal requirements only.

A month later, SkillBench tested something different: not CLAUDE.md files, but skills — the progressive disclosure system. Curated skills improved pass rates by 16.2 percentage points, four times the benefit of the best developer-written CLAUDE.md files, while self-generated skills added zero benefit — the same pattern as auto-generated CLAUDE.md. What you put in the context matters more than where you put it: auto-generated garbage hurts everywhere, carefully crafted knowledge helps everywhere, and skills outperform CLAUDE.md because they only load when relevant instead of eating tokens on every message. You can implement this same progressive disclosure inside CLAUDE.md itself. SkillBench also found that focused skills with two to three modules outperform comprehensive documentation — less is more. Frontier LLMs can follow roughly 150

to 200 instructions with reasonable consistency; Claude Code's system prompt already uses about 50 of those slots, leaving 100-150 for your entire CLAUDE.md. A bloated CLAUDE.md doesn't just waste tokens, it actively makes Claude worse at following its own built-in instructions, since every added line competes with every other line — domain-specific knowledge belongs in a skill, not CLAUDE.md, per the SkillBench findings. Compliance also decays within a session: 95% at 1-2 messages, 60-80% at 3-5, 20-60% at 6-10, and downhill beyond that — which is why Boris starts most sessions in plan mode and uses `/clear` between sessions for fresh context. The single biggest takeaway: `/init` is a starting point, not a final product — expect to delete 80% of what it generates, backed by the ETH Zurich research across hundreds of real-world tasks. Enough theory — here's exactly what goes into

the perfect CLAUDE.md section by section. The mental model: it needs to answer What, Why, and How. What is the tech stack and project structure (especially important in monorepos); Why is the purpose of each part; How is how Claude should actually work — Bun or pnpm, how to verify changes, how to run tests. Answer all three in under 80 lines and you're in great shape. The section-by-section template distilled from production files has six parts. Section one, Commands (5-8 lines): things Claude can't guess, like `pnpm dev`/`build`/`test`, custom type-check and lint invocations — skip things Claude already knows like `npm install`.

Section two, Code Standards (5-10 lines): rules that differ from defaults, like "must use TypeScript strict mode," "functional components with hooks," "prefer early returns," "max function length 50 lines" — don't waste lines on conventions Claude already knows. Section three, Architecture (3-5 lines): brief, just enough to orient Claude, using `@`-import syntax to point to a separate architecture doc (e.g. "see @docs/architecture.md") rather than inlining detail. Section four, Workflow (3-5 lines): branch-from-main, run type checks and lint before committing, never commit directly to main, conventional-commit PR titles — customize to your project. Section five, Common Mistakes (3-5 lines), an underrated

section: anytime Claude repeats a mistake you've seen before, add it here — what Boris calls compound engineering, the file getting smarter over time, echoing the direction of Andrej Karpathy's "auto research" work on models developing their own skills. Section six, Don'ts (3-5 lines): explicit negative instructions like "never modify package.json without asking" or "never use `any`, use `unknown` and narrow" — "never" is stronger than "prefer not to," so use must/should/may/never language. Total: roughly 30-40 lines, maybe 50 for complex projects; Boris's team at Anthropic keeps theirs at 60-80 lines. Anthropic's own docs recommend staying under 200 lines, with under 80 being most optimal; going over 200 actively hurts the project.

Boris's own setup, surprisingly vanilla: a single CLAUDE.md checked into Git that the whole team contributes to, roughly 60-80 lines, failure-driven iteration (add a rule only when Claude does something wrong), and `@Claude` on pull requests auto-updates it via GitHub Actions during code review — what he calls compounding engineering. His personal CLAUDE.md is just two lines pointing to the team's shared version. The lesson: if the creator of Claude Code doesn't need 400 lines, you don't either. One of his biggest tips: give Claude a way to verify its own work — a feedback loop can 2-3x output quality, echoing Karpathy's auto research findings. Verification commands — type check, test, lint —

might be the most important lines in your entire CLAUDE.md. A trick from a Hacker News dev: the canary test. Add a line at the top of CLAUDE.md like "always refer to me as Mr. Tinkerbell in all communications," then start a session — if Claude uses the canary phrase, it's reading the file; if not, something's wrong. Used during long conversations, it reveals exactly when Claude starts "being dumb," tying directly into the compliance decay curve (95% at 1-2 messages, fading after 10) — if Claude stops using the canary mid-session, that's the signal context is drifting and it's time to `/clear`. On self-updating CLAUDE.md files: some people add a rule telling Claude to append new learnings to the

bottom of the file automatically. The recommendation instead is a separate memory file referenced via progressive disclosure, so CLAUDE.md itself doesn't bloat. If you do want self-updating behavior, use guardrails — a provided prompt limits it to one-line bullets under 15 words, no explanations, only time-saving additions, pruning unneeded rules, and a max of 10 bullets (replacing the least useful when full). Claude Code actually has a built-in auto-memory system doing something similar in a separate location (`.claude/projects/memory`), which is the safest version of this. Advanced techniques that separate power users from beginners: first, imports — CLAUDE.md supports `@path/to/file.md` syntax to pull in external files, but

unlike progressive disclosure, an `@`-import actually gets loaded fully into CLAUDE.md's context (recursive up to five levels deep) — a 500-line README imported this way dumps 500 lines into context, so use sparingly. Next, Claude "rules" — path-scoped YAML rule files that only activate for specific file paths, so front-end rules don't pollute back-end context and vice versa; a powerful and underused feature. Many developers maintain an `agents.md` file instead since it's the open-source standard working across Claude Code, Codex, Cursor, Gemini CLI, and other tools — rather than maintaining two files, symlink CLAUDE.md to agents.md, or `@`-import agents.md from CLAUDE.md. Every company except Anthropic has adopted agents.md as the shared convention, but the symlink/import approach means one file works

for every tool regardless of whether a team member uses Claude, Gemini CLI, or Codex — check both into Git either way. HTML comments are another trick: block-level HTML comments in CLAUDE.md get stripped before injection into Claude's context, so they're free, zero-token, human-readable notes for you or your team that Claude never sees. Progressive disclosure is the single most important concept in the video — the same idea skills are built on. CLAUDE.md should be a lean index pointing to detailed information, not a document containing everything Claude needs to know, like a new employee's day-one orientation rather than the entire handbook. It breaks into three tiers: tier one is always loaded

(system prompt, CLAUDE.md, imports, memory) — high token cost, every message, keep minimal. Tier two is on-demand (rule files, skills, subdirectory CLAUDE.md) — low token cost, loads when relevant. Tier three is reference-only (docs, READMEs, source code) — zero cost until Claude searches for and accesses it. Rather than `@`-importing a 500-line doc, write a plain-text pointer like "for database schemas, see docs/schema.md" — Claude reads the cheap pointer every message and only reads the actual file when working on that area, instead of cramming schema, API docs, and workflow into CLAUDE.md and bloating everything. Remember CLAUDE.md is advisory (~80% compliance) — anything that must happen every time, like running a formatter or blocking a

dangerous command, belongs in a hook, not a CLAUDE.md rule; rules are requests, hooks are laws. Common mistakes to avoid: making it too long, treating it like documentation, including things Claude already knows, vague language, putting style rules in CLAUDE.md, auto-generating without pruning, including sensitive information, not checking it into Git, stuffing everything into one file, and not iterating (write once, never update, and rules go stale — Boris's team updates theirs weekly, multiple times). A live example of a bad CLAUDE.md at nearly 300 lines gets run through an optimizer prompt (linked in the resources) that rewrites it into a separate "after" file for direct before/after comparison.

The result: an 84% reduction, from 288 lines down to 46, removing things like the project overview and redundant tech-stack detail with reasons given for each removal — though the recommendation is to still manually cross-reference the AI-generated result against the actual codebase rather than trusting it blindly. The linked GitHub repo also includes three starter CLAUDE.md templates — Python, TypeScript/Next.js, and a generic universal version — plus the full research papers, Anthropic's "Effective Context Engineering for AI Agents" writeup, Humanloop's blog posts, a CLAUDE.md starter kit, and the "awesome-CLAUDE.md" repo, a curated collection of high-quality CLAUDE.md files from projects like OpenAI's Agents Python, Basic Memory, Pydantic, Claude Flow, Cloudflare Workers, and Anthropic Quickstarts, covering

the foundation for understanding how Claude Code and agentic harnesses work and how to actually do context engineering well.

</details>
