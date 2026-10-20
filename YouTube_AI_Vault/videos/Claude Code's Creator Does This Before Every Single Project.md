---
title: "Claude Code's Creator Does This Before Every Single Project"
video_id: B-UXpneKw6M
channel: "[[channels/AI LABS]]"
uploaded: 2026-01-09
processed: 2026-07-06
duration: "9:54"
url: https://www.youtube.com/watch?v=B-UXpneKw6M
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [claude-code-power-user-workflow]
tools: [Claude Code, Slack, BigQuery, Sentry, Notion, GitHub, Ralph Loop, Claude Browser Extension]
llms: [Claude Opus, Claude Sonnet, Claude Haiku]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code's Creator Does This Before Every Single Project

![thumbnail](https://i.ytimg.com/vi_webp/B-UXpneKw6M/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=B-UXpneKw6M) | 📅 Uploaded [[uploaded/2026-01-09]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Boris, the Anthropic engineer who created Claude Code, shares how he actually uses it day to day: always giving Claude a way to verify its own work (tests, browser extension, screenshots), keeping claude.md lean (~2.5k tokens) and continuously updated by the whole team, always starting in plan mode before autoaccept, running five parallel sessions plus cloud background agents, and defaulting to Opus 4.5 with thinking enabled because fewer errors beat faster-but-wrong output.

**Watch this if:** you use Claude Code regularly and want the actual power-user habits of its creator instead of generic prompt-engineering tips.

## Key Takeaways
- Always give Claude a way to verify its own work (e.g., ask it to write and run tests) — this creates a feedback loop that dramatically increases output quality, and you can even ask Claude which tests to use.
- Verification is domain-specific: bash commands for scripts, the Claude Browser Extension for full site navigation/UI verification, iOS/Android simulator MCPs for mobile apps, or test-driven development (write tests first, implement second) paired with screenshots for UI work.
- claude.md should be unique per repo, cover tech stack, project structure, code conventions, and — most importantly — things Claude shouldn't do (based on past mistakes); Boris's own team edits it multiple times a week and it stays around 2.5k tokens. Full-stack apps can have a separate claude.md per microservice (frontend/backend).
- Boris avoids "dangerously skip permissions" mode, especially in production, instead configuring granular permission rules (allow/ask/deny per command) in a shareable settings.json inside the .claude folder.
- Claude Code is used as a full orchestration system, not just for coding — connecting to Slack, BigQuery, and Sentry via MCP/CLIs, and to Notion via MCP to create and populate databases from project context.
- Workflow: describe the task in plan mode first, iterate there until the plan is verified, then switch to autoaccept-edits mode (not skip-permissions) to execute — the back-and-forth happens during planning, not execution.
- Boris runs 5 Claude Code sessions in parallel (numbering terminal tabs to track notifications), plus web/cloud sessions connected to GitHub for long-running background tasks (including from his phone), using the teleport command to bring a cloud session back to the local terminal.
- Defaults to Opus 4.5 with thinking enabled for everything — slower and bigger than Sonnet or Haiku, but the much lower error rate means less total time spent steering the model.
- For long-running verification, he uses three approaches: background verification tasks that self-report, a stop hook that triggers verification automatically when Claude finishes output, and the Ralph Wiggum plugin pattern that removes the human from the loop entirely — plus linters/formatters to clean up the remaining ~10% of formatting issues models don't get right.
- Simple, longstanding built-in features still deliver ~90% of the productivity: slash commands for repetitive "inner loop" workflows (stored in the commands subfolder and committed to git for team sharing) and subagents for narrow, repeatable tasks like architecture verification, refactoring, and build validation.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the subject of the whole video; used as a full orchestration system across coding, verification, and integrations with other tools.
- [[topics/Claude Browser Extension]] — used for UI-based verification, navigating a whole site to confirm changes work as intended.
- [[topics/Slack]] — connected to Claude Code via an MCP server as part of Boris's orchestration workflow.
- [[topics/BigQuery]] — one of the tools Boris accesses through its CLI inside Claude Code.
- [[topics/Sentry]] — one of the tools Boris accesses through its CLI inside Claude Code.
- [[topics/Notion]] — connected via MCP so Claude can create and populate databases and understand project/video-idea context.
- [[topics/GitHub]] — used for the Claude Code GitHub Action (automated PR review comments) and as the repo backend for web/cloud sessions.
- [[topics/Ralph Loop]] — the Ralph Wiggum plugin pattern used as a third long-running-task verification approach that removes the human from the loop.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4.5 with thinking enabled is Boris's default model for everything, chosen for its much lower error rate despite being slower.
- [[topics/Claude Sonnet]] — referenced as faster but less careful than Opus 4.5 in Boris's comparison.
- [[topics/Claude Haiku]] — referenced as the fastest but least careful tier in Boris's model comparison.

## 📡 Protocols & Standards
- [[topics/MCP]] — the integration layer connecting Claude Code to Slack and Notion, plus the basis for iOS/Android simulator MCPs used for mobile app verification.

## ✅ Action Items
- Add an explicit verification instruction to your claude.md so every session states how it will verify its work before starting.
- Keep claude.md short (aim for roughly 2.5k tokens) and update it as a team habit whenever Claude makes a recurring mistake.
- Configure granular command permissions in .claude/settings.json (allow/ask/deny) instead of using dangerously-skip-permissions mode, and share the file with your team.
- Always draft and verify a plan in plan mode before switching to autoaccept-edits mode to execute.
- Try running multiple Claude Code sessions in parallel (numbering terminal tabs) plus a web/cloud session connected to GitHub for background long-running work.
- Set up a stop hook or background verification task so tests/checks run automatically without manual prompting each time.
- Store repetitive workflows as slash commands in the commands subfolder and commit them to git so the whole team can reuse them.

## 🔗 Related Videos
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, GitHub, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet

## Timeline
- `0:00` — Intro: why Boris, Claude Code's creator, is the person people ask for advice.
- `1:00` — Core tip: always give Claude a way to verify its own work (tests, feedback loops).
- `2:15` — Verification differs by domain: bash checks, the Claude Browser Extension, mobile simulator MCPs, test-driven development with screenshots.
- `3:20` — Why claude.md must be unique per repo, team-maintained, and kept lean (~2.5k tokens); per-microservice claude.md files.
- `4:45` — Plan mode vs. autoaccept vs. dangerously-skip-permissions, and granular permission rules in settings.json.
- `5:40` — Claude Code as a full orchestration system: Slack, BigQuery, Sentry, and Notion via MCP/CLIs.
- `6:40` — Boris's actual workflow: plan mode first, then autoaccept-edits; running 5 parallel sessions plus cloud/background agents and the teleport command.
- `7:50` — Defaulting to Opus 4.5 with thinking for fewer errors, despite being slower than Sonnet/Haiku.
- `8:10` — Three approaches to long-running verification, including the Ralph Wiggum plugin pattern, plus linters/formatters for cleanup.
- `8:50` — Simple built-in features that still deliver ~90% of productivity: slash commands and subagents.

## Transcript
<details>
<summary>Full transcript</summary>

This is Boris — he created Claude Code at Anthropic, which is why people ask him how to use it. Even though he calls his setup simple, what's simple to him is a whole system to everyone else.

One of his biggest corrections to a common misconception: people give Claude a task, hit minor errors, and get disappointed — but humans work similarly, so you should always give Claude a way to verify its own work. For Python code, tell it to use tests too — this gives Claude a feedback loop that instantly increases result quality. You can even ask it which tests it should use, and it'll propose one for everything it implements. You can bake this into claude.md (sent into every session) by telling Claude that before doing any work, it should state how it will verify that work, creating a constant feedback loop.

Verification differs by domain — sometimes it's as simple as a bash command, sometimes it needs UI-based verification via Claude's own browser extension, which navigates a whole site and can verify everything works. For something like a mobile app, there are iOS and Android simulator MCPs; if those feel too token-hungry, use verification-led techniques like test-driven development (write tests first, then implement) combined with UI screenshots.

claude.md should be unique to each repo: tech stack, project structure, code style/conventions, and — most importantly — things it shouldn't do, so it doesn't repeat past errors. Boris has his whole team contribute to claude.md multiple times a week whenever they see incorrect behavior, with each team member responsible for maintaining a specific file. Full-stack apps can have separate claude.md files per microservice (frontend, backend). Don't bloat it — his own is about 2.5k tokens.

On modes: plan mode is for planning; autoaccept mode auto-accepts file edits; dangerously-skip-permissions gives Claude permission to run everything, which Boris avoids, especially in production, since one bad terminal command can break everything. Instead he configures Claude Code's permissions system — which commands are allowed, which need confirmation, which are denied — at the project level, stored in a settings.json inside the .claude folder that he shares with his team.

Claude Code is arguably badly named because it's not just for code — people build entire content workflows, SEO pipelines, or market-analysis agents with it. Boris uses it as an orchestrator: Slack via MCP, plus BigQuery and Sentry through their CLIs, all inside Claude Code. The presenter's own biggest orchestration use is connecting Claude to Notion via MCP to create and populate databases and understand video-idea context.

Boris's actual workflow: before implementing anything, switch to plan mode and clearly describe the goal; all the back-and-forth happens there, and he only starts the agent once the plan is verified — then in autoaccept-edits mode (not skip-permissions). At scale, he runs five Claude Code sessions in parallel, numbering his terminal tabs to track which notifications come from where. He also heavily uses web sessions of Claude Code connected to GitHub, giving it access to a repo to work in the cloud — including from his phone — using background agents for long-running tasks; when done, it creates a branch and pushes changes for review. The teleport command brings a cloud session back into the local terminal to view/continue locally — treating the agent like a junior developer.

He defaults to Opus 4.5 with thinking enabled for everything: it's bigger and slower than Sonnet, and much slower than Haiku, but has a much lower error rate, so overall time spent working with and steering the model ends up lower. He also uses the Claude Code GitHub Action inside authorized repos — during PR reviews, whenever he finds a mistake, he asks Claude to add it to claude.md.

For long-running tasks he uses three approaches: (1) ask Claude to verify its work with self-generated tests, run as background tasks that report back to the main agent when done; (2) a stop hook that automatically triggers verification when Claude stops outputting; (3) the pattern the Ralph Wiggum plugin is built on, which removes the human from the loop entirely for UI verification during development. He also verifies code formatting with linters/formatters per language — models generate mostly correct code, but formatters clean up the remaining ~10%, avoiding CI errors.

On simpler, longstanding features that still save huge time: his workflow is "surprisingly vanilla," and built-in features already get most people ~90% of the productivity they want. Slash commands handle repetitive "inner loop" workflows (e.g., a simple GitHub-related command) and are stored in the commands subfolder inside .claude, so they can be committed to git and shared with the team. Subagents are another simple built-in feature — people build them for all kinds of use cases (market researchers, product validators), but Boris mainly uses them to automate narrow, differently-instructed workflows: verifying architecture correctness, refactoring code, and validating that builds actually work.

</details>
