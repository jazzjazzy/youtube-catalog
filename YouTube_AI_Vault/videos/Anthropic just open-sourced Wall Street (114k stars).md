---
title: "Anthropic just open-sourced Wall Street (11.4k stars)"
video_id: E4GNZxJQqfM
channel: "[[channels/Indie Hacker News]]"
uploaded: 2026-05-08
processed: 2026-07-05
duration: "6:51"
url: https://www.youtube.com/watch?v=E4GNZxJQqfM
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [financial-services-ai-agents, open-source-vertical-ai-architecture]
tools: [GitHub, Claude Code, Managed Agents API, FactSet, S&P Global, PitchBook, Moody's, LSEG, Bloomberg Terminal, CapIQ, Excel, GitLeaks]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic just open-sourced Wall Street (11.4k stars)

![thumbnail](https://i.ytimg.com/vi/E4GNZxJQqfM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=E4GNZxJQqfM) | 📅 Uploaded [[uploaded/2026-05-08]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A deep architectural dive into Anthropic's `anthropics/financial-services` repo (11.4k stars, Apache 2.0), which just restructured into 10 named end-to-end analyst agents wired to 11 licensed MCP data connectors. The video walks the actual plugin architecture (agent.md, skills, .mcp.json, sync scripts, GitLeaks secret scanning) and argues Anthropic just published the analyst workflow itself — the prompts and conventions, not just the data access.

**Watch this if:** you build vertical AI, sell into financial services, or want a concrete architectural template (agent.md + skills + .mcp.json + sync scripts) for packaging AI agents as Claude Code plugins.

## Key Takeaways
- Three days before this video, the repo restructured from a generic skills bundle into 10 named, job-titled agents (Pitch Agent, Market Researcher, Earnings Reviewer, Model Builder, Meeting Prep, GL Reconciler, Month-End Closer, Valuation Reviewer, Statement Auditor, KYC Screener) — hitting 11,400 stars and trending #1 in Python the day it shipped.
- The README frames every output as a draft for human sign-off, not investment advice — positioning that lets Anthropic ship something this aggressive without appearing to replace the analyst.
- What's actually being open-sourced isn't the data (11 connectors like FactSet, S&P Global, PitchBook, Moody's, and LSEG still require paid licensed seats) — it's 20 years of closed-shop methodology: the modeling conventions, prompts, and audit checklists that used to live only inside the banks.
- Architecturally, every named agent is a self-contained Claude Code plugin: an `agent.md` system prompt, a `skills` folder, a `commands` folder, and a `.mcp.json` declaring exactly which connectors that agent may call — skills are authored once in the vertical plugins and synced per-agent via `sync_agent_skills.py`.
- Supporting tooling includes `check.py` (manifest linting), `deploy_managed_agent.sh` (pushes an agent to the `/v1/agents` Managed Agents API), `orchestrate.py` (the reference event loop for agent-to-agent handoffs), and a GitLeaks-based secret scan added because everyone using this will be holding licensed terminal credentials.
- Model Builder runs DCF/three-statement/comps live in Excel (via a headless "XL Author" integration in managed-agent mode); the fund-admin/operations agents (GL Reconciler, Month-End Closer, KYC Screener) are notable because middle-office workflows are rarely open-sourced at all.
- Install is three Claude Code commands: add the marketplace, install the core financial-analysis plugin (which carries the data connectors), then cherry-pick whichever named agents and verticals match your job function.
- The real tradeoff: connectors still require paid licensed seats, so you can't clone this into a turnkey terminal stack for free — but as a reference implementation, it resets what enterprise financial-services prospects will expect you to already have.

## 🛠 Tools & Software
- [[topics/GitHub]] — where the `anthropics/financial-services` repo hit 11.4k stars and trended #1 in Python
- [[topics/Claude Code]] — the plugin architecture (agent.md, skills, commands, .mcp.json) that every named agent is packaged as
- [[topics/Managed Agents API]] — the `/v1/agents` hosted-runtime API that `deploy_managed_agent.sh` pushes agents to
- [[topics/FactSet]] — one of the licensed MCP data connectors wired into the agents
- [[topics/S&P Global]] — one of the licensed MCP data connectors, and the source of one of the two partner-built vertical plugins
- [[topics/PitchBook]] — one of the licensed MCP data connectors
- [[topics/Moody's]] — one of the licensed MCP data connectors
- [[topics/LSEG]] — one of the licensed MCP data connectors, and the source of the other partner-built vertical plugin
- [[topics/Bloomberg Terminal]] — cited as the ~$25k/year legacy tool this repo's methodology used to be locked behind
- [[topics/CapIQ]] — cited alongside Bloomberg Terminal as part of the old closed-shop analyst toolkit
- [[topics/Excel]] — where Model Builder runs its DCF, three-statement, and comps models
- [[topics/GitLeaks]] — the secret-scanning workflow added to catch leaked licensed terminal credentials

## 🤖 LLMs Mentioned
- [[topics/Claude]] — Anthropic's underlying model; the repo (Claude for financial services) packages it into named, job-specific analyst agents

## 📡 Protocols & Standards
- [[topics/MCP]] — the 11 licensed data connectors are wired in as MCP connectors, each declared per-agent in that agent's `.mcp.json`

## ✅ Action Items
- Read the `anthropics/financial-services` repo like a textbook if you build vertical AI or sell SaaS into financial services — study the agent.md/skills/.mcp.json pattern as a template.
- Install only the core financial-analysis plugin plus the specific named agents and verticals relevant to your role rather than the whole repo.
- If adapting this pattern for your own vertical, add a GitLeaks-style secret scan before letting agents hold any licensed or credentialed data access.
- Treat the shipped agents as reference templates, not finished products — expect to tune prompts and swap in your own firm's data sources before production use.

## 🔗 Related Videos
- [[videos/Anthropic Just Shipped 10 Wall Street AI Agents, GitHub 1]] — shared: Claude, FactSet, GitHub, LSEG
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude, Claude Code, GitHub, MCP

## Timeline
- `0:00` — Intro: Anthropic's repo that could end Wall Street's monopoly on its own workflow
- `1:04` — The README: disclaimer framing, agents draft, humans approve
- `1:55` — Why this matters: 20 years of closed-shop methodology now public
- `2:31` — Engineering depth: forks, commits, partner plugins since launch
- `2:44` — Coverage and modeling: what each of the 10 named agents actually does
- `4:11` — Architecture: agent.md, skills, .mcp.json, sync scripts, GitLeaks
- `5:04` — Install: three Claude Code commands to cherry-pick agents and verticals
- `5:27` — What shipped May 5th: the restructure commit, tightened tool grants
- `6:11` — The verdict: real tradeoffs, but a new ceiling for reference implementations

## Transcript
<details>
<summary>Full transcript</summary>

3 days ago Anthropic dropped a repo on GitHub that might end Wall Street's monopoly on its own analyst workflow. Anthropic, the company that makes Claude, quietly shipped a repo called Claude for financial services. 3 days ago they restructured it from a generic skills bundle into 10 named end-to-end agents with job titles you would see on a Goldman analyst's business card, names like pitch agent, market researcher, earnings reviewer, model builder, GL reconciler, and KYC screener. The repo is Apache 2.0, hit 11,400 stars, and trended number one in Python the day it shipped. 11 licensed MCP data connectors are wired in, including SP Global, FactSet, PitchBook, Moody's, and LSEG. Every named agent ships its own skills bundle and deploys two ways. Let me show you what's inside.

Okay, so the read me and the framing matters. The page opens with a disclaimer that none of this constitutes investment advice, and that every output is staged for human sign-off. The agents draft, the humans approve. That positioning is what lets Anthropic ship something this aggressive without sounding like they are replacing the analyst. The agent table is organized by function, grouping coverage and advisory at the top, then research and modeling, then the fund admin and finance ops cluster, then operate. Below that, the vertical plugin section lists seven bundles, the core financial analysis bundle that ships shared modeling skills, plus six verticals running from investment banking and equity research through private equity, wealth management, and the back office stack. Two partner-built plugins also ship, one from LSEG and one from S&P Global.

For 20 years the analyst workflow has been a closed shop. To build a pitch deck or run a DCF, you needed a Bloomberg terminal at $25,000 a year, an Excel template owned by a bulge bracket bank, a CapIQ subscription, and 3 years of unpaid weekends learning the modeling conventions. None of those vendors ever shipped the methodology. The methodology lived inside the banks. What Anthropic just published is the entire skill ladder, the workflow itself, the prompts and conventions, the audit checklist, and the plumbing that lets a properly licensed seat actually pull the data once you have it.

Okay, the named agents. Pitch agent runs comps, presidents, and an LBO end-to-end, outputs a branded pitch deck, the full thing a banking analyst would build over a weekend. Meeting prep generates a briefing pack before client meetings, pulling from your CRM, the news desk, and recent filings. Market researcher takes a sector or theme and produces an industry overview, competitive landscape, peer comps, and a short list of investment ideas. Earnings reviewer ingests the call audio, the press release, and the 10-Q, then updates the model and drafts the research note. Model builder runs DCF, three statement, and comps live in Excel, hitting XL author headlessly when in managed agent mode. The fund admin and operations side is where this gets interesting because nobody usually open-sources middle office workflows. GL reconciler finds breaks in the general ledger, traces the root cause, routes for sign-off. Month-end closer handles accruals, roll forwards, and variance commentary. Valuation reviewer ingests GP packages, runs the firm's valuation template, stages LP reporting. Statement auditor audits LP statements before distribution. KYC screener parses onboarding documents, runs the rules engine, flags compliance gaps. Every one of these is something a junior accountant or a compliance analyst was getting paid 80,000 a year to do 6 months ago.

Under the hood, the architecture is what other indie builders should study. Every named agent is a self-contained Claude Code plugin, a folder with an agent.md file declaring the system prompt, a skills folder with bundled markdown files, a commands folder with slash commands, and a .mcp.json declaring which connectors that agent is allowed to call. Skills are authored once in the vertical plugins, then synced into each agent by a script called sync_agent_skills.py. There is a check.py that lints manifests, a deploy_managed_agent.sh that pushes the same agent to the /v1/agents API, and an orchestrate.py showing the reference event loop for routing handoff requests between agents. The whole thing is markdown and JSON, no build step.

Install on Claude Code is three commands: add the marketplace, install the financial analysis core, which carries the data connectors, cherry-pick whichever agents and verticals match your work. Pitch agent for IB coverage, GL reconciler for fund admin, wealth for the advisor stack. Each agent bundles its own skills, so there is no manual dependency tracking.

The May 5th restructure commit is what flipped this repo. Every vertical moved from the repo root into a plugins/vertical-plugins folder. The 10 named agent plugins landed under plugins/agent-plugins, each one self-contained. The team added managed agent cookbooks with one folder per agent, including sub-agent isolation and steering examples for headless deployment. They added a fund admin and operations vertical, so the finance ops and onboarding agents shipped with real domain skills. They tightened tool grants — no agent can shell out to bash, hit web fetch, or call an undeclared connector. And they added a GitLeaks-based secret scan workflow because everyone using this is going to be holding licensed terminal credentials.

The tradeoffs are real. The connectors all require licensed seats, and those subscriptions still cost real money. So you cannot clone this repo and walk away with a turnkey terminal stack out of the box. The agents are reference templates, not finished products, so you have to tune the prompts and swap in your firm's data sources before any of this runs in production. But if you build software for the financial industry in 2026, this is the new ceiling for what an open reference implementation looks like, and the conversation with your enterprise prospects just changed. They can spin up the analyst stack themselves and compare it to whatever you're charging for.

</details>
