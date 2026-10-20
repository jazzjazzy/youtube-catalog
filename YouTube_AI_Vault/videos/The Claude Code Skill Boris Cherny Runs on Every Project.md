---
title: "The Claude Code Skill Boris Cherny Runs on Every Project"
video_id: AhXfI1rSUPc
channel: "[[channels/AI LABS]]"
uploaded: 2026-04-03
processed: 2026-07-05
duration: "12:17"
url: https://www.youtube.com/watch?v=AhXfI1rSUPc
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-skills-workflow, engineering-workflow-automation]
tools: [Claude Code, GitHub, Remotion, Chrome]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# The Claude Code Skill Boris Cherny Runs on Every Project

![thumbnail](https://i.ytimg.com/vi_webp/AhXfI1rSUPc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=AhXfI1rSUPc) | 📅 Uploaded [[uploaded/2026-04-03]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A reverse-engineering breakdown of the exact skills and slash commands the Anthropic Claude Code team (including Boris Cherny) uses internally, pieced together from tweets, open-source plugin repos, and leaked source code. Covers open-source plugins you can install today (frontend-design, batch, code-simplifier) and internal-only skills (verify, skillify, tech-debt, dedupe) you can recreate yourself with the skill-creator skill.

**Watch this if:** you want to replicate the actual internal Claude Code workflow of the team that builds it, not just generic skill advice.

## Key Takeaways
- The frontend-design plugin (official Claude Code plugin marketplace, open source) exists specifically to stop AI-generated UI from converging on "generic AI aesthetics" and is invoked via slash command or automatically whenever Claude judges it relevant.
- The batch skill parallelizes work like library migrations by entering plan mode, splitting the task into units, then spawning one agent per unit — each running in its own isolated git worktree — before merging all worktrees back to main and optionally opening the PR.
- Code-simplifier (open source plugin, one agent) and the built-in Simplify skill (three agents, rigorously evaluating multiple metrics) both refine code for clarity without changing functionality; Simplify is the more thorough of the two and both are heavily used internally.
- Verify is an internal-only skill (hidden behind a CLI flag, its system prompt injected into the environment rather than shipped in the product) that runs the app, tests changes from multiple angles, and auto-fixes failures — you can build your own with the skill-creator skill, tailored to your project's verification methods (linters, npm test, or visual checks via the Claude Chrome extension).
- Skillify is another internal-only skill that captures an entire brainstorming session with Claude and converts the workflow discussed into a reusable skill.md file, asking clarifying questions before finalizing it.
- The security-scan command (now a public Claude Code feature, originally internal) checks input validation, auth issues, secret management, injection, code execution, and endpoint exposure, then can be prompted to implement the fixes directly.
- The team uses slash commands for every repetitive inner-loop workflow, including an open-source commit-push-PR command that generates commits from staged/unstaged changes and opens the pull request.
- Tech-debt is an internal, project-specific skill run at the end of every session to detect duplicated code, consolidate it into a shared library, and update call sites — recreate it yourself via the skill-creator skill with your own project's file-structure and verification rules.
- Dedupe (internal, reverse-engineered from a linked GitHub issue) checks new GitHub issues against existing ones via the GitHub CLI and comments when it finds roughly 70%-confidence duplicates, though it still requires human confirmation.
- Remotion is used by Anthropic's marketing team, inside Claude Code, to generate the motion graphics used in product announcement and marketing videos — one of their most-used non-development skills.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the platform every skill/command in the video runs inside; plugins are installed via its plugin marketplace and invoked with slash commands
- [[topics/GitHub]] — the batch skill can open pull requests when a remote is configured; the dedupe skill searches existing issues via the GitHub CLI for duplicates
- [[topics/Remotion]] — the skill Anthropic's marketing team uses inside Claude Code to generate motion graphics for product announcement and marketing videos
- [[topics/Chrome]] — recommended for the verify skill's visual verification step via the Claude Chrome extension

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying Claude Code and every skill described; its agents are spawned per-worktree by the batch skill and per-metric by the Simplify skill

## 📡 Protocols & Standards
- [[topics/MCP]] — cited as one possible verification method ("Playwright MCP verification tests") a project's verify skill could use

## ✅ Action Items
- Install the frontend-design and code-simplifier plugins from the official Claude Code plugin marketplace.
- Use the batch skill for any parallelizable task (library migrations, bulk refactors) so agents work in isolated worktrees instead of stepping on each other.
- Build a project-specific verify skill with the skill-creator skill, wiring in your linters, test runner, and (if relevant) the Claude Chrome extension for visual checks.
- Create a Skillify-style skill that captures brainstorming sessions and turns them into reusable skill.md files.
- Run the built-in security-scan command on large or AI-generated-heavy codebases before shipping.
- Adopt the open-source commit-push-PR slash command to standardize your commit/PR inner loop.
- Build a tech-debt skill that runs at end-of-session to find and consolidate duplicated code.

## 🔗 Related Videos
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Chrome, Claude, Claude Code, GitHub
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP

## Timeline
- `0:00` — Introduction: reverse-engineering the Claude Code team's actual skill workflow
- `0:28` — Frontend Design plugin: avoiding generic AI aesthetics
- `1:25` — Batch skill: parallelizing work across isolated git worktrees
- `2:47` — Code Simplifier plugin vs. the built-in Simplify skill
- `4:35` — Verify skill: internal automated testing and auto-fixing
- `5:55` — Skillify: turning a session into a reusable skill
- `7:02` — Security Scan command: vulnerability scanning and patching
- `8:07` — Commit-Push-PR slash command
- `8:57` — Tech Debt skill: end-of-session duplicate cleanup
- `10:26` — Dedupe skill: auto-flagging duplicate GitHub issues
- `11:34` — Remotion skill: powering Anthropic's marketing videos

## Transcript
<details>
<summary>Full transcript</summary>

The creator of Claude Code previously revealed his entire workflow in an earlier video; this one goes further by digging through the team's posts, open-source repos, and the official plugin marketplace to pull out the specific skills and commands his team actually uses daily — some installable right now, others internal tools reverse-engineered from what they do. One skill they use is the frontend-design plugin, developed to convert designs from simple prompts while enhancing UI/UX and specifically avoiding the "generic AI aesthetics" models tend to converge toward. It's open source in the official Claude Code plugin repo, installed via the plugins marketplace (or the `plugins add marketplace` command if not already present), and invoked via slash command — though it can also be

triggered automatically whenever Claude determines it's necessary. Another daily-use skill is batch, built directly into the product to automate easily parallelized tasks like migrating code between libraries. Giving it an instruction after the batch command triggers plan mode first — identifying the task, breaking it into subtasks, and exploring the implementation before executing. Unlike Claude's default agent parallelism, batch uses separate git worktrees (isolated repo copies) so agents can't affect each other's work. The generated plan covers the app's current state, the division of work into units, required additions, and end-to-end verification instructions; once approved, it spawns one agent per unit

of work, each in its own worktree with a dedicated prompt, reporting progress back to a main agent that merges all worktrees into the main branch and can even manage the pull request if a remote is configured. They also frequently use the code-simplifier plugin — open source, installed the same way, refining code for clarity while preserving functionality by spawning a single agent to remove duplicates and unnecessary files and returning a summary of changes. This is similar to the built-in Simplify skill shipped in Claude Code, but Simplify spawns three agents and evaluates code across multiple metrics more rigorously, making it the more thorough version; both are heavily used

by the team. [Sponsored segment: Airtop, a no-code cloud-browser automation tool, demonstrated monitoring competitor pricing and posting a daily summary to Slack.] Another skill used internally is verify — not mentioned in any tweets, but visible in leaked source code as an internal-only skill hidden behind a CLI flag, with its system prompt injected directly into the environment

rather than shipped in the product code (likely because it's highly project-specific). You can build your own version using the skill-creator skill or the repo as a template — it scans your codebase and generates a tailored verify skill. Verification methods vary by project; some use Playwright MCP tests or other approaches, but the core idea is giving the agent a way to confirm its own changes work. The skill's instructions cover step-by-step guidance for handling code changes, reporting results, and example tool integrations like linters, exit codes, and npm test files, ideally paired with test cases and visual verification via the Claude Chrome extension. Another internal-only skill is Skillify, which captures an entire session and converts it into a reusable skill; like verify it's gated behind an environment flag, but unlike verify its system prompt is visible in the source. Skillify's purpose is to record a session where you brainstorm a workflow with Claude, refine it

across multiple conversations, and save it as a skill — identifying repeatable processes, tools and permissions mentioned, and the agents involved, then interacting with you to clarify intent before finalizing a skill.md and detailed guide. You don't need the internal version — you can recreate it from source: once invoked, it analyzes the session, confirms its deductions, asks follow-up questions, generates a skill.md, and lets you review before saving it as a reusable skill for your project. Another tool the team uses is the Claude Code security-scan command, which scans for vulnerabilities and suggests patches. Used internally first to catch multiple real security issues, it was later released as a public Claude Code feature. Its (leaked) system prompt covers input validation, authentication issues, secret management, injection and code execution risks, endpoint exposure, and more, with an in-depth

analysis methodology built in. It's a built-in feature you can run directly for a security review of all files; after it reports findings, you can prompt Claude to implement the fixes — especially valuable for large-scale, AI-generated-heavy codebases where vulnerabilities can otherwise slip into production unnoticed. The Claude Code team uses slash commands for every repetitive inner-loop workflow — for example, a commit-push-PR command that pushes code and opens a pull request. This command is open source on the Claude Code plugins marketplace, generates commits from staged and unstaged changes following a specific series of steps, and matches the exact command the creator described in an X post. Install it via the plugins marketplace by searching for the commit command;

once installed, all its commands are available to streamline repetitive workflows. The creator also mentioned their team uses a tech-debt skill, run at the end of every session to find duplicated code. It's not open source and is highly project-specific, but you can build your own equivalent using the (open source) skill-creator skill — writing instructions covering how to identify changes, detect duplicates, track accumulated tech debt, handle your project's file structure, and finish with verifications like npm test and linting. Running it walks the entire codebase with multiple analysis agents, reports redundant duplication in detail, creates a shared library components can draw from, and updates those components to

reference the shared location — ending the session with a proper cleanup and a more organized, lower-tech-debt codebase. Another skill the Claude Code team uses is Dedupe, also internal and not available in open-source or product form, but reverse-engineered from a GitHub issue they linked in a tweet. It checks whether a new GitHub issue duplicates an existing one, using the GitHub CLI to parse and search for similar issues against a similarity threshold; when it finds a duplicate with roughly 70% certainty, it comments explaining the match — though it still requires human verification. This is useful on multi-person projects where duplicate issue reports waste time re-explaining that something's already been handled. A final skill Anthropic uses frequently is Remotion inside Claude Code, which generates motion graphics and videos from simple prompts — it's used across all of Anthropic's product announcement and marketing videos, making it one of the most important skills in the marketing team's non-development workflow.

</details>
