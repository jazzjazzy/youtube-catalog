---
title: "7 Tools That Make Claude Code + Codex Dangerous"
video_id: dBhNEVEXOxc
channel: "[[channels/Eric Michaud]]"
uploaded: 2026-04-30
processed: 2026-07-05
duration: "11:13"
url: https://www.youtube.com/watch?v=dBhNEVEXOxc
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [self-hosted-agent-stack, avoiding-vendor-lock-in]
tools: [GitHub CLI, Google Workspace CLI, Obsidian, Superpowers, Browser Use, Huashu Design, FFmpeg, Claude Code, Codex, Antigravity, Playwright, Firecrawl]
llms: []
protocols: [OAuth, CDP]
transcript: true
tags: [youtube, ai-automation]
---

# 7 Tools That Make Claude Code + Codex Dangerous

![thumbnail](https://i.ytimg.com/vi_webp/dBhNEVEXOxc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=dBhNEVEXOxc) | 📅 Uploaded [[uploaded/2026-04-30]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Eric Michaud lists the 7 tools he'd install first to rebuild a self-hosted AI developer stack around Claude Code and Codex: GitHub CLI as the workflow engine, Google Workspace CLI to reach outside the sandbox into Gmail/Calendar/Docs, Obsidian as a memory/context layer, Superpowers to enforce a structured planning methodology, Browser Use for undetectable web automation, Huashu Design to teach agents brand guidelines, and 25-year-old FFmpeg for all media handling.

**Watch this if:** you want a practical, vendor-light tool stack to give your coding agents real-world reach instead of leaving them sandboxed to just editing files.

## Key Takeaways
- GitHub CLI does the most heavy lifting: it gives an agent direct terminal access to repos, issues, pull requests, GitHub Actions automation, and deployment triggers (e.g. auto-syncing to Vercel/AWS on push), which the presenter prefers over separate hosting-provider CLIs since GitHub already gives rollback control and backups.
- Google Workspace CLI hands an agent Gmail, Calendar, Docs, Drive, Tasks, and Sheets through the terminal, normalizing OAuth authentication (cached, auto-refreshing credentials) across all those products instead of wrestling with each one's API separately — used for things like emailing a finished report or auto-generating a morning briefing from unread email, to-dos, and calendar.
- The Obsidian Skills repo (by Obsidian's CEO, Kepano) teaches agents to use Obsidian itself and its CLI; the presenter treats Obsidian less as a notes app and more as a shared memory layer where projects, daily notes, research, and skills aggregated from Claude Code, Antigravity, and Codex all live in one discoverable, tagged place.
- Superpowers is a complete software development methodology built on composable skills that force an agent through brainstorm → clean workspace → write a plan → test the plan → review the test output → push to development, preventing agents from going off on unstructured tangents; the presenter rates it above similar planning plugins like GSD.
- Browser Use (called "Browser Harness" here) is a thin harness built directly on the Chrome DevTools Protocol (CDP) via remote debugging rather than a flagged browser like Chromium, so it avoids anti-bot detection; it's self-healing, has learned domain-specific skills (e.g. posting to TikTok/Instagram), and has fully replaced the presenter's prior Firecrawl + Playwright scraping combo — with an explicit warning that it can easily cross into ToS/ethical gray areas since it bypasses Cloudflare and similar bot detection.
- Huashu Design (the newest tool on the list) is a skill that trains a coding agent to follow consistent brand guidelines with real assets, references, scripts, and demos, addressing the common gap where design-capable agents can't code well and code-capable agents can't design.
- FFmpeg, a 25-year-old command-line media library, still gets used daily for captions, transcoding, compression, audio extraction, video cleanup, and assembling clips — most newer AI video tools are themselves built on top of it; the presenter's closing point is that the best tools are the ones that keep working, not the newest or loudest.

## 🛠 Tools & Software
- [[topics/GitHub CLI]] — the top pick; gives an agent direct terminal access to repos, issues, PRs, GitHub Actions, and deploy triggers
- [[topics/Google Workspace CLI]] — connects an agent to Gmail, Calendar, Docs, Drive, Tasks, and Sheets with normalized OAuth handling
- [[topics/Obsidian]] — used as a shared memory/context layer aggregating notes, research, and skills across every agent harness
- [[topics/Superpowers]] — enforces a structured brainstorm-plan-test-review development methodology on coding agents
- [[topics/Browser Use]] — CDP-based browser automation harness for scraping and site interaction that avoids anti-bot detection; replaced the presenter's Firecrawl + Playwright combo
- [[topics/Huashu Design]] — newly released skill that teaches a coding agent to follow consistent brand/design guidelines
- [[topics/FFmpeg]] — 25-year-old media toolkit used daily for captions, transcoding, compression, and video editing tasks
- [[topics/Claude Code]] — one of the two primary agent harnesses (alongside Codex) this entire tool stack is built around
- [[topics/Codex]] — the other primary agent harness this tool stack targets
- [[topics/Antigravity]] — named as another agent harness the presenter pulls skills from into a unified Obsidian source of truth
- [[topics/Playwright]] — the browser automation tool the presenter used before switching to Browser Use
- [[topics/Firecrawl]] — previously combined with Playwright for web scraping before being replaced by Browser Use

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/OAuth]] — Google Workspace CLI normalizes OAuth authentication and credential refresh across Gmail, Calendar, Docs, and other Google products
- [[topics/CDP]] — Browser Use is built directly on the Chrome DevTools Protocol via remote debugging, which is why it avoids the anti-bot flags that hit Chromium-based automation

## ✅ Action Items
- Install GitHub CLI first and wire agent actions to GitHub Actions/deployment triggers before reaching for separate hosting CLIs.
- Set up Google Workspace CLI so an agent can email results, generate docs/sheets, or build a morning briefing from your inbox and calendar.
- Aggregate skills and notes from every agent harness you use into one Obsidian vault as a single source of truth.
- Install Superpowers (or an equivalent planning methodology plugin) before letting an agent run unsupervised on real work.
- Evaluate Browser Use as a replacement for a Playwright/Firecrawl scraping stack, but be mindful of ToS and privacy boundaries since it bypasses bot detection.
- Keep FFmpeg in your stack for any media-handling automation rather than reaching for newer wrapper tools built on top of it.

## 🔗 Related Videos
- [[videos/This is The Most Powerful Tool to Give to Claude Code]] — shared: Claude Code, Codex, GitHub CLI, OAuth
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Codex, Google Workspace CLI
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Playwright, Superpowers
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, Superpowers
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Browser Use, Claude Code, Playwright
- [[videos/Claude HeyGen Just Changed Content Creation Forever]] — shared: Claude Code, FFmpeg, Playwright
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Codex, Google Workspace CLI, OAuth
- [[videos/Google's New CLI Is The Missing Piece for Claude Code]] — shared: Claude Code, Google Workspace CLI, OAuth

## Timeline
- `0:00` — Intro: rebuilding an AI stack from scratch, cutting through the noise
- `0:28` — GitHub CLI: repos, issues, PRs, GitHub Actions, and deploy triggers from the terminal
- `1:48` — Google Workspace CLI: Gmail, Calendar, Docs, Drive with normalized OAuth
- `3:17` — Obsidian Skills & CLI: the shared memory layer for AI agents
- `5:05` — Superpowers: enforcing a structured development methodology
- `6:21` — Browser Use ("Browser Harness"): CDP-based scraping that avoids bot detection
- `7:58` — Huashu Design: teaching coding agents brand/design guidelines
- `8:44` — FFmpeg: the 25-year-old media powerhouse still used daily
- `10:22` — Summary: the full seven-tool functionality stack recapped
- `10:57` — Outro and where to get the Obsidian framework

## Transcript
<details>
<summary>Full transcript</summary>

In this video, we're going to talk about the very first tools and plugins I would reach for if I was just getting started with Codex, Claude Code, and rebuilding my stack from scratch. There's a lot of noise out there, conflicting opinions, and every day something new is supposedly killing the old thing. So today we're going through the things I've found actually useful, in order.

Starting with the one that does the most heavy lifting: GitHub CLI. GitHub isn't just where the code lives anymore — it's the repo, the task tracker, the pull request system, the automation runner, the deployment trigger. GitHub CLI gives your agent direct access to take actions in GitHub: PR commands, browsing repos, looking for issues, writing gists, and the like. You can set up GitHub Actions straight away too — for example, a friend has one that pulls a video's transcript and writes a blog post every time he posts. You can also sync to a web host like AWS or Vercel, and every push updates your backend automatically. There are CLIs for Vercel and AWS, but I don't use them nearly as much, because if I'm pushing to GitHub I've already got rollback control and backups, and everything else syncs from there anyway.

The second thing I'd install is the Google Workspace CLI. This gives you hands through the terminal into Gmail, Calendar, Docs, Drive, Tasks, and Sheets — a direct connection your agent has to the Workspace, which is the first step in moving your agent outside its sandbox. I'll have an agent do research and then say "email this to me," or "turn this into a Google Doc," "generate a spreadsheet," "make a calendar note." An article from Mind Studio sums up how this differs from raw API access: authentication is a one-off command, credentials cache locally and refresh automatically, and error handling is normalized across every product instead of wrestling with Google OAuth separately for each one. Practically, I've got a `/today` command that pulls in unread emails, to-dos, and calendar every morning so I'm not spending 45 minutes building a to-do list by hand.

The next one is the Obsidian Skills repo from Kepano, the CEO of Obsidian, which includes an Obsidian CLI. I don't think of Obsidian as a notes app anymore — it's a modular chassis you can add anything to. This teaches your agents how to use Obsidian and helps with plugin/theme development. But outside of being a customizable platform, Obsidian is best used as a memory layer for AI agents — it fills gaps left by harnesses like Claude Code and Codex. All my projects, daily notes, tasks, research, and scripts live here, tagged so they're discoverable by my AI agent. All my skills and workflows from Claude Code, Antigravity, and Codex are aggregated here too, so there's one single source of truth regardless of what I'm running — I bring my AI to my workflows rather than my workflows to different AI agents. The window in this video is actually Obsidian itself — browser, terminal, agent frameworks, content and video editing plugins, all built into one window.

Number four is Superpowers. This is less about giving the agent new capabilities and more about making it behave. Similar plugins exist, like GSD, and they matter because a lot of people just go in guns-blazing on a Claude Code or Codex instance and hope for the best. Superpowers is a complete software development methodology built on composable skills and initial instructions that force consistent, well-thought-out output: brainstorm, work in a clean space, write a plan, test the plan, review the test output, then push to development. I even use just the brainstorming skill in isolation sometimes to plan out content or website/funnel design. Of the agent-planning-behavior plugins out there, this is a cut above in detail and consistency.

Number five is Browser Harness from Browser Use — I liked it enough to do a whole video on it. It's a browser AI agent that gets better the more it's used, built directly on top of the Chrome DevTools Protocol (CDP), using remote debugging to run real Chrome rather than something like Chromium that usually gets flagged for anti-bot detection. Before this, I used Playwright, sometimes combined with Firecrawl, to pull information off the web — Browser Use has replaced that combo wholesale. It's self-healing and has already picked up domain skills, like posting videos or carousels to TikTok or Instagram, where the Meta Graph API is a nightmare to connect to directly — Browser Use just does it manually, like a person at the desk. It's also great for scraping directories and databases, but be careful: it's extremely easy to violate terms of service since it bypasses Cloudflare and other bot detection, and it's easy to slip into ethical and privacy gray areas. Be good with it.

Number six is Huashu Design, the newest one on the list and one I haven't used as extensively as the others. Design has been a weak spot for AI agents — you get design-specific agents that are bad at code, or code-specific agents that are bad at design. This is a skill that trains a coding agent to be good at design, or at least follow consistent brand guidelines, giving it assets, references, scripts, and demos — a real framework instead of just telling your assistant to "make this look better."

Number seven, last on the list, is FFmpeg — a 25-year-old command-line workhorse for editing media: captions, transcodes, compression, audio extraction, video cleanup, adding voiceovers or music, stitching videos together, whatever it is. Plenty of newer video editors and AI tools are built on FFmpeg under the hood. This is core to my content workflow — filming, clipping, captioning — every single day. AI can now drive FFmpeg for you without writing the commands yourself, which is the whole point of this video: the best tools aren't the newest or loudest, they're the ones that actually keep working. Once something does the job, don't chase every new thing just because someone argued about it on Twitter.

Recap of the full stack: GitHub CLI as the workhorse for getting things done, Google Workspace for connections, Superpowers as the process/execution layer, Obsidian as the environment and memory layer, Browser Use for everything browser, Huashu for design, and FFmpeg for media manipulation. A few honorable mentions — Supabase, or hosting CLIs like Vercel or AWS — are more niche. With these seven (or equivalents), you can do just about anything.

</details>
