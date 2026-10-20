---
title: "15 Claude Code Tricks That Feel Like Cheating"
video_id: qGAuqbbj1Ls
channel: "[[channels/Sean Kochel]]"
uploaded: 2026-04-29
processed: 2026-07-05
duration: "21:59"
url: https://www.youtube.com/watch?v=qGAuqbbj1Ls
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-workflow-optimization, reducing-token-costs]
tools: [Claude Code, Chrome, Git, GitHub, Superpowers, Compound Engineering]
llms: [Claude Opus, Claude Sonnet]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# 15 Claude Code Tricks That Feel Like Cheating

![thumbnail](https://i.ytimg.com/vi_webp/qGAuqbbj1Ls/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=qGAuqbbj1Ls) | 📅 Uploaded [[uploaded/2026-04-29]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Sean Kochel distills 15 workflow rules that Boris (Claude Code's creator) actually uses to build Claude Code itself — from `--chrome` browser verification and conversation forking with `/branch`, to remote/teleport sessions, heavy git-worktree parallelism, defaulting to Opus over Sonnet, automated PR-fix loops, sub-agent verification, the power-user `/batch` command, and disciplined planning with grill-me-style interrogation. Each trick is explained and then demoed live in Claude Code.

**Watch this if:** you use Claude Code daily and want the creator's own habits for getting more reliable output with fewer wasted tokens.

## Key Takeaways
- Launching with `--chrome` gives Claude Code live browser access so it can iterate on front-end changes and visually verify the result instead of guessing — one of the creator's highest-impact habits.
- `/branch` forks a conversation so you can explore a tangent without muddying your main context, and `/resume <id>` gets you back to the original thread afterward.
- Remote control makes a desktop session accessible from the Claude mobile app; teleport pulls a session started on phone or web back onto your desktop machine — together they let you move work between devices.
- Git worktrees let multiple Claude Code instances work on separate directories/branches truly in parallel without stashing or overwriting each other's changes; a Superpowers skill automates creating worktrees, running a clean-baseline test pass, and guarding against going off the rails.
- The creator uses Opus for everything rather than the common Opus-for-planning/Sonnet-for-implementation split, reasoning that a slower-but-correct model is often faster and cheaper overall; the `effort` parameter can push this further, though anything below "extra high" reportedly makes Opus 4.7 error-prone.
- PR loops (the creator's version, and the presenter's own "ship and watch" command) commit, open a pull request, then poll it every 5 minutes to auto-diagnose and fix CI/lint failures until it's green.
- Sub-agents dedicated to code simplification and app verification (and libraries like Compound Engineering's 18-persona code review, six of which always run) catch maintainability and correctness issues right after a change is made.
- The `/batch` command scales the worktree idea further, planning and spinning up many parallel work units (13 in the demo) from one instruction — powerful but token-hungry, so it needs judgment about when it's actually worth it.
- Planning discipline matters most: pour effort into the plan itself, have adversarial sub-agents challenge it, keep the CLAUDE.md file concise and pruned regularly, and use a "grill me" style command to interrogate every ambiguous decision before building — because unresolved ambiguity gets silently decided by the model at build time.
- Token-usage analytics (`/status line`, auditing globally-installed skills that silently load 30-40k tokens per session) and building in "explain what you did and why" instructions both help catch runaway costs and build real understanding, especially for non-engineers who vibe code.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI coding agent the entire video is built around; every trick is a workflow habit for using it
- [[topics/Chrome]] — launched via `--chrome` so Claude Code can visually iterate on and verify front-end changes in a real browser
- [[topics/Git]] — git worktrees are used to run multiple Claude Code instances on separate branches truly in parallel
- [[topics/GitHub]] — pull requests are the target of the automated PR-fix loop that polls and resolves CI/lint failures
- [[topics/Superpowers]] — its git-worktree skill automates worktree setup with a clean test baseline and guardrails; also referenced for a red-green-refactor TDD skill
- [[topics/Compound Engineering]] — a library providing an 18-persona code review process and feature-ideation skills, chained together with slash commands

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — recommended for use on everything, not just planning, since Opus 4.7 arriving at the correct answer first is often cheaper overall than a faster-but-wrong Sonnet pass; needs "extra high" effort to avoid mistakes
- [[topics/Claude Sonnet]] — named as the model many other workflows reserve for implementation after Opus plans, a split the creator explicitly departs from

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Launch sessions with `--chrome` for any front-end work so Claude Code can verify its own changes visually.
- Use `/branch` to fork a conversation before exploring a risky tangent, and `/resume` to get back to the original thread.
- Set up git worktrees (or a Superpowers-style skill) to run multiple Claude Code instances in true parallel without branch-switching pain.
- Build a "ship and watch" style PR loop that polls every 5 minutes and auto-fixes CI/lint failures until the PR is green.
- Add code-simplification and app-verification sub-agents (or a multi-persona review library) that run automatically after each change.
- Keep CLAUDE.md concise, review it weekly, and don't be afraid to nuke it if it stops working.
- Add a "grill me" style planning command that interrogates every ambiguous decision before implementation starts.
- Check `/status line` regularly and move heavily-used skills from global to per-project installs to avoid burning tens of thousands of tokens per session on context you don't need.

## 🔗 Related Videos
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, Claude Sonnet, Git
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Claude Sonnet, GitHub, Superpowers
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude Code, Claude Opus, Git, GitHub
- [[videos/I Can't Believe Anthropic Messed Up The Ralph Wiggum]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/Planning In Claude Code Just Got a Huge Upgrade]] — shared: Claude Code, Claude Opus, Git, GitHub
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Claude Code, Git, GitHub, Superpowers

## Timeline
- `0:00` — Intro: 15 of Claude Code creator Boris's own workflow rules
- `0:37` — Chrome verification: `--chrome` gives live browser access for iterative front-end fixes
- `2:18` — Forking conversations with `/branch` and returning with `/resume`
- `3:57` — Remote control (desktop session on mobile) and teleport (pull a session back to desktop)
- `6:06` — Git worktrees for true parallel work, automated by a Superpowers skill
- `7:05` — Why the creator uses Opus for everything instead of Opus-plan/Sonnet-implement
- `9:12` — PR loops: auto-polling and fixing pull request CI/lint failures every 5 minutes
- `11:52` — Verification sub-agents: code simplification, app verification, and Compound Engineering's persona-based review
- `13:25` — `/batch`: worktrees at scale, planning and running many parallel units from one instruction
- `16:00` — Keeping CLAUDE.md concise and reviewed regularly
- `16:59` — `/grill-me`: interrogating the plan to resolve ambiguity before building
- `18:27` — Token analytics: auditing global skill costs and reading `/status line`

## Transcript
<details>
<summary>Full transcript</summary>

Over the last 4 months or so, Claude Code's creator has shared probably dozens of different rules that he follows in his own workflows to build Claude Code itself — not what Anthropic wants you to do or what people on Twitter think you should do, but what he actually does himself. Fifteen of the best are covered here for vibe coders and day-to-day Claude Code users, each explained and then demoed.

Starting with using Chrome as a verification step for all front-end work — one of his highest-impact habits. If you asked a human to build a website but told them they couldn't use a browser, the result wouldn't be great; it works the same for a coding model. Typing `--chrome` when kicking off Claude Code opens it with browser access, so you can ask it to extract a modal into its own settings page, and it will spin up Chrome, iterate, and verify the change actually looks right — a simple verification loop that's been extracted into its own slash command.

Next: forking conversations. It was historically a pain to fork a conversation in Claude Code or Claude's desktop app without muddying your context, but the `/branch` command now creates a fork so you can explore a tangent (e.g. "what other info would make sense in our preferences?") without disturbing your main thread, and `/resume <id>` takes you right back to where you were.

Remote control and teleport solve working away from your desktop in two ways: `remote control` makes the current session accessible from the Claude mobile app so you can pick up exactly where you left off from your phone; `teleport` pulls a session started on your phone or in the Claude Code web browser back onto your desktop machine. Together they create a triangle between desktop, mobile, and web you can move between depending on your situation.

That workflow gets smoother with git worktrees used extensively. Managing several parallel efforts (better test coverage, backend performance work, a new feature) with plain git branches gets messy fast since you're working out of one directory and constantly stashing and switching. Git worktrees spin up multiple directories so several Claude Code instances can work fully in parallel with no overwriting. The Superpowers plugin has a dedicated worktree skill that creates the worktrees, runs tests to confirm a clean baseline, and includes guardrails to keep you from going off the rails.

For how to actually work inside those worktrees: use Opus for everything, departing from the common pattern of Opus for planning and Sonnet for implementation. The reasoning is that even though Opus is bigger, slower, and pricier, arriving at a correct solution faster is often both faster and cheaper overall. The `effort` parameter can tune this, and with Opus 4.7 specifically, anything below "extra high" effort tends to produce noticeably more mistakes.

On non-negotiable quality-of-life rules: PR loops. When pushing to develop on GitHub kicks back test failures, a loop can check the pull request every 5 minutes and automatically fix code review issues until it resolves — the presenter built his own version called "ship and watch," which commits changes, opens a PR, and triggers a loop that polls status every 5 minutes, diagnoses failures like lint errors, fixes them, and lets you merge once green.

Slash commands remain powerful even after skills rolled out — chaining skills from different plugins (like Superpowers' red-green-refactor TDD skill and Compound Engineering's feature ideation) together via slash commands, exactly like "ship and watch," which itself invokes a separate looping command that tracks state, checks guardrails, polls PR status, and fixes failures.

After building something, sub-agents dedicated to verification matter: code simplification (finds opportunities to make a session's output more maintainable) and app verification (uses tools like the Chrome extension to confirm things actually work). Libraries like Compound Engineering's code review use 18 different reviewing personas — six always called (maintainability, adherence to your CLAUDE.md/agent file standards, etc.) and others called conditionally, e.g. a security reviewer triggered by touching an authentication endpoint.

The `/batch` command is git worktrees on steroids: given an instruction to migrate an app to a new design and component system (fetch the design file, read its README, implement relevant aspects), it plans and spins up many parallel units — 13 in this demo — to execute simultaneously. Someone with effectively unlimited Claude tokens could spin up hundreds of worktrees this way; for everyday use it needs a token budget and judgment about when it's worth it.

Planning discipline: pour your energy into the plan and have adversarial sub-agent personas review it, the same pattern seen in every good spec-driven or agent-orchestration library — even "never look at the code" vibe coders need to look at the plan. The CLAUDE.md file deserves similar care: don't be afraid to nuke it if it's going sideways, keep it concise rather than documenting everything, and check in on it weekly or daily as your project evolves.

Even a bulletproof CLAUDE.md won't stop models from occasionally doing something unwanted, which is where a "grill me" style command (Matt Pocock's version is popular) helps — it interrogates you about every aspect of your plan, walking every branch of the system design and its dependencies, until you and the model share a common understanding, since any ambiguity left in the plan gets silently decided by the model at build time.

On token savings: using Claude Code for analytics on its own token consumption reveals waste — globally installed skills can silently load 30-40k tokens into every new session before you've asked a single question, so installing heavy skill libraries per-project rather than globally can save enormous amounts of tokens across a team. A data-analytics exercise like this is how the presenter discovered Opus 4.7 (with Superpowers) was ignoring the sub-agent-driven execution slash command and running everything in the main thread, spiking token usage. `/status line` gives a snapshot of context-window usage percentage, proximity to the 5-hour limit, and proximity to the 7-day limit — useful enough that nearing 15-20% of a 1M-token context window is a cue to save and clear.

The last and most valuable rule is learning with Claude: instructing it in CLAUDE.md to explain the principles behind decisions it makes and how they connect to the rest of the system counters the tendency, especially for non-engineers who vibe code, to never actually look at the generated code — which becomes a problem the moment something breaks and you need to know where to look.

</details>
