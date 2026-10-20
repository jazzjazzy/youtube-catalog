---
title: "I Tried Every Skill. These Best Claude Skills Are Bizarre"
video_id: qQ5uObNKBOU
channel: "[[channels/AI LABS]]"
uploaded: 2026-04-17
processed: 2026-07-05
duration: "11:47"
url: https://www.youtube.com/watch?v=qQ5uObNKBOU
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [claude-code-skill-discovery, coding-agent-productivity]
tools: [Claude Code, Peon Ping, Dog Food, Caveman, Git Time Travel, Pre-mortem, Mutation Testing, The Fool, Reddit Fetch, Color Expert, Agent Browser, Gemini CLI, tmux]
llms: [Claude, Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# I Tried Every Skill. These Best Claude Skills Are Bizarre

![thumbnail](https://i.ytimg.com/vi/qQ5uObNKBOU/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=qQ5uObNKBOU) | 📅 Uploaded [[uploaded/2026-04-17]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A tour of 8 community-built, open-source Claude Code skills that sound weird but solve real problems: game-character voice notifications for session babysitting, a caveman-mode token compressor, git history auditing, adversarial UI review, pre-production bug prediction, mutation testing, decision stress-testing, Reddit research via Gemini CLI, and a 100+ file color-science reference for design.

**Watch this if:** you run multiple Claude Code sessions and want practical, install-and-go community skills beyond the official ones.

## Key Takeaways
- Peon Ping notifies you with game-character voices when Claude finishes a task or hits a permission prompt — useful for tracking multiple simultaneous sessions without manually checking each one.
- Caveman rewrites Claude's responses in a stripped-down, direct style, cutting ~75% of response tokens while keeping technical accuracy; a "Wenyuan" mode compresses further using Chinese but trades off accuracy.
- Git Time Travel gives the agent expertise in navigating git history, flagging risky force-pushes and rebases, and producing a structured change-log report.
- Dog Food drives Agent Browser through a web app page by page in an adversarial-review style, producing a bug report (critical/medium/low), screenshots, and a walkthrough video.
- Pre-mortem analyzes a codebase to predict production bugs that haven't happened yet, and Mutation Testing injects deliberate bugs to score how well the test suite catches them.
- The Fool stress-tests an idea, plan, or decision across multiple failure modes and produces a report you can push back on and iterate with.
- Reddit Fetch pulls Reddit discussion for market research by driving Gemini CLI through tmux, falling back to a curl-based JSON API when that fails (since Reddit blocks bot traffic).
- Color Expert supplies 100+ markdown reference files on color science, WCAG, and palettes so agents stop defaulting to generic purple-and-white UI themes.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent all 8 community skills are built for and demoed on
- [[topics/Peon Ping]] — session-notification skill using game-character voice packs for task completion and permission prompts
- [[topics/Dog Food]] — adversarial web-app review skill that drives Agent Browser page by page and reports bugs with screenshots and video
- [[topics/Caveman]] — token-compression skill that rewrites Claude's replies in a terse, direct style with a Wenyuan (Chinese) max-compression mode
- [[topics/Git Time Travel]] — skill giving the agent git-history expertise, flagging force-push/rebase risk and producing a change-log report
- [[topics/Pre-mortem]] — skill that analyzes a codebase and predicts production bugs before they happen, with a structured report
- [[topics/Mutation Testing]] — skill that injects bugs one at a time and scores whether the test suite catches them
- [[topics/The Fool]] — decision/plan stress-testing skill that generates a multi-failure-mode risk report
- [[topics/Reddit Fetch]] — skill that fetches Reddit content for market research via Gemini CLI (through tmux) with a curl JSON API fallback
- [[topics/Color Expert]] — skill providing 100+ grounded color-science/WCAG reference files to improve agent-generated UI
- [[topics/Agent Browser]] — CLI tool that lets agents interact with web pages by sending keys and referencing elements; used by Dog Food
- [[topics/Gemini CLI]] — driven via tmux by Reddit Fetch to bypass Reddit's bot blocking
- [[topics/tmux]] — terminal multiplexer used to run Gemini CLI in parallel sessions for Reddit Fetch

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose Claude Code sessions all 8 skills are built and tested around
- [[topics/Gemini]] — driven via Gemini CLI as the primary method Reddit Fetch uses to bypass bot blocking

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Peon Ping if you juggle multiple Claude Code sessions and keep missing completion/permission-prompt notifications.
- Try Caveman on token-heavy vibe-coding workflows where you want fast, accurate answers without filler.
- Run Dog Food's adversarial review against a staging URL before shipping a web app.
- Use Pre-mortem and Mutation Testing together before a production release to catch both predicted bugs and weak test coverage.
- Point Reddit Fetch at a topic when doing market/competitor research that needs real user discussion.
- Load Color Expert before letting an agent build UI from scratch to avoid the generic purple/white default look.

## 🔗 Related Videos
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Claude Code, Gemini
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Claude Code, Gemini, Gemini CLI
- [[videos/Never hit Claudes Usage Limit Again]] — shared: Caveman, Claude, Claude Code
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Gemini CLI
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: Claude, Claude Code, Gemini
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Gemini
- [[videos/This Claude Skill Cuts Your Token Costs In HALF]] — shared: Caveman, Claude, Claude Code
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude, Claude Code, Gemini CLI

## Timeline
- `0:00` — Intro: weird community Claude Code skills that actually work
- `0:51` — Peon Ping: game-character voice notifications for session tracking
- `1:59` — Dog Food: adversarial browser review of a web app via Agent Browser
- `3:05` — Caveman: 75% token-reduction response mode, plus Wenyuan mode
- `5:08` — Git Time Travel: git history expertise and risk-flagging report
- `5:48` — Sponsor break: Freebuff
- `6:37` — Pre-mortem: predicting production bugs before they occur
- `7:39` — Mutation Testing: injecting bugs to score test-suite strength
- `8:29` — The Fool: stress-testing ideas and decisions across failure modes
- `9:51` — Reddit Fetch: market research via Gemini CLI/tmux with curl fallback
- `10:35` — Color Expert: 100+ file color-science reference for better UI

## Transcript
<details>
<summary>Full transcript</summary>

Many people have started perfecting their own agent skills and open-sourcing them for the community. While most of their skills are genuinely useful, some of them are just weird. But despite being weird, they are useful in ways you wouldn't expect. One of them solved the biggest problem we faced while handling multiple sessions, and it did it in a way that was fun but actually worked. Another one fixed the token bloat problem in a way we didn't see coming. We kept finding more like these — ones that genuinely helped even though they sounded ridiculous at first.

If you use multiple Claude sessions simultaneously on different tasks, you've had to manually keep track of which session has completed its work. There are also cases where Claude has been blocked on a permission prompt without you noticing. For this, you need Peon Ping — a skill that notifies you whenever Claude has completed a task or needs a permission prompt, using voices from popular games with multiple modes and characters instead of standard notifications. You can set it up for any coding agent, install it with the command for your OS, then use the slash command to pick your favorite voice pack. Whenever Claude finishes a task while you're busy elsewhere, you get a game-character voice notification; starting a new session also gets a voice notification indicating Claude is ready.

We always talk about adversarial review mode because it critically evaluates so many aspects, and that's what makes it effective. Dog Food explores a web app and identifies bugs and UX issues using an adversarial-review style. It uses Agent Browser, a CLI tool that lets agents interact with pages by sending keys and referencing elements properly (covered in a previous video) — make sure Agent Browser is installed before using this skill. Give it a link (hosted or localhost) and it initializes a report, then walks the app page by page. It reports all issues found, including reproduction steps, screenshots, and a critical/medium/low breakdown, and even records a video of the entire walkthrough.

If you're annoyed by Claude's unnecessarily long, filler-filled explanations, Caveman is a plugin that makes Claude talk like a caveman, cutting 75% of tokens from responses while maintaining technical accuracy — using fewer, more direct words and cutting articles and filler. The highest intensity mode is Wenyuan, which uses Chinese since it represents whole sentences in far fewer tokens than English — though model accuracy is generally lower in non-English languages, so English caveman mode is usually the safer choice. It's available for all major agents; for Claude Code, install the plugin marketplace command first, then search for and install caveman in whichever scope you want, reload plugins, and set the intensity level with the caveman command.

Git Time Travel gives your agent expertise in navigating git history, letting it understand the entire history like a time-travel log. Installing it brings a skill.md file plus references containing patterns and validations that check for issues like force-pushing to main or rebasing without proper backup. You can use it to analyze any issue in your git logs, and after going through the history it gives a detailed report pointing out what went wrong with recommendations.

[Sponsor segment: Freebuff, a free coding agent claimed to be up to 10x faster than Claude Code, with 9 sub-agents and ChatGPT/GPT-5.4 integration for plan and review.]

Pre-mortem looks at a codebase, identifies fragile areas, and predicts possible issues that could occur with the current implementation — writing realistic reports for bugs that haven't occurred yet but could once the app goes live. Installing it gives a skill.md detailing the full workflow and patterns to check; running the pre-mortem command analyzes the codebase and generates a thorough report, possibly asking which aspects to focus on.

Mutation Testing analyzes your entire test suite by introducing different bugs and mutations one at a time and checking whether test cases catch them. It uses git to revert mutations (so commit changes first), applies changes to components, checks detection, and generates a report with a mutation score, uncaught issues, and recommended improvements.

The Fool critically analyzes and stress-tests an idea, plan, decision, or proposal using multiple modes and failure stories. After installing, you provide what you want challenged, choose a challenge mode, and it loads relevant references to reason through failure modes, producing a structured report you can push back on and iterate with.

Reddit Fetch fetches content from Reddit — which normally blocks bots like Claude Code — using either the Gemini CLI (via tmux, a terminal multiplexer for running parallel sessions) or a curl JSON API fallback if that fails. Specify the topic you want researched and it returns a detailed report on what people on Reddit are actually saying, useful for market research.

Since agents tend to converge on the same purple-and-white UI theme, Color Expert acts as a guide providing understanding of color science, WCAG, palettes, and more — via 100+ markdown reference files sourced from Wikipedia, YouTube scripts, and other grounded resources. Tested on a community landing page, the agent loaded the skill, understood the codebase and guide, and produced a much more balanced UI with better white space, contrast, and a more engaging color palette than it would have without the skill.

That brings us to the end of this video. Thank you for watching.

</details>
