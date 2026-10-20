---
title: "Anthropic Just Shipped 10 Wall Street AI Agents, GitHub #1"
video_id: qp9uvdUGtjo
channel: "[[channels/Bitwise AI]]"
uploaded: 2026-05-08
processed: 2026-07-05
duration: "4:57"
url: https://www.youtube.com/watch?v=qp9uvdUGtjo
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [financial-services-ai-agents, vertical-ai-agent-deployment]
tools: [Claude Cowork, Managed Agents API, GitHub, FactSet, Moody's, S&P Global, LSEG, PitchBook, Daloopa, Morningstar, Aiera, MT Newswires, Chronograph, Egnyte]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Just Shipped 10 Wall Street AI Agents, GitHub #1

![thumbnail](https://i.ytimg.com/vi/qp9uvdUGtjo/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=qp9uvdUGtjo) | 📅 Uploaded [[uploaded/2026-05-08]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Anthropic open-sourced `anthropics/financial-services` — 10 named Wall Street agents, 7 vertical plugin bundles, and 11 paid MCP data connectors — one day after announcing a $1.5B joint venture with Goldman Sachs, Blackstone, and Hellman & Friedman. It hit #1 on GitHub trending with 14,000 stars in days, deployable via Claude Cowork or the new Managed Agents API, and the video frames it as the reference template every other vertical-AI industry repo will now copy.

**Watch this if:** you want to understand how Anthropic is packaging vertical AI agents (finance first) as open-source configuration wired to paid enterprise data feeds, and how the new Managed Agents API hosts them.

## Key Takeaways
- The repo hit 3,600 stars in 24 hours and #1 on GitHub trending, going from zero stars three days prior to roughly 14,000, with an unusually high 12.5% fork-to-star ratio — signaling developers cloning it to ship, not just bookmarking it.
- It's pure configuration: three top-level folders (plugins, managed agent cookbooks, scripts) built from markdown skills, JSON manifests, and Python deploy scripts — no build step, no SDK.
- Ten named agents cover a full analyst floor: Pitch, Meeting Prep, Market Researcher, Earnings Reviewer, Model Builder, Valuation Reviewer, GL Reconciler, Month-End Closer, Statement Auditor, and KYC Screener.
- Seven vertical plugin bundles (investment banking, equity research, private equity, wealth management, fund administration, operations, plus a core financial-analysis plugin) package the relevant agents, skills, and slash commands per job function, plus two partner plugins from LSEG and S&P Global.
- The real moat: 11 MCP data connectors (FactSet, Moody's, S&P Global, LSEG, PitchBook, Daloopa, Morningstar, Aiera, MT Newswires, Chronograph, Egnyte) — the repo is Apache 2.0, but the six-figure enterprise data subscriptions behind each connector are not, which is how Anthropic locks in customers without selling the lock-in directly.
- Two deployment paths: install via the Claude Cowork plugin marketplace at `anthropic.com/claude-for-financial-services`, or run a deploy script against Anthropic's new Managed Agents API (`POST /v1/agents`), which uploads skills, creates leaf-worker sub-agents, and posts a hosted orchestrator (returns `201 Created`).
- Hidden in the readme: "callable agents" let one agent hand off to another (e.g., GL Reconciler to Month-End Closer) via a steering event — real sub-agent delegation — but it's flagged as research preview, request-access only.
- Anthropic's disclaimer is blunt: these agents draft analyst work product for human review only — they don't execute trades, bind risk, or post to a ledger, and every output needs human sign-off.

## 🛠 Tools & Software
- [[topics/Claude Cowork]] — Anthropic's plugin marketplace deployment path for installing the financial-services agent bundles
- [[topics/Managed Agents API]] — Anthropic's new hosted-runtime API (`POST /v1/agents`) used to deploy the same agents as a managed, hosted service
- [[topics/GitHub]] — where the `anthropics/financial-services` repo hit #1 trending with 14,000 stars in days
- [[topics/FactSet]] — one of 11 paid MCP data connectors wired into the vertical plugin bundles
- [[topics/Moody's]] — one of 11 paid MCP data connectors, used in the deployed GL Reconciler example
- [[topics/S&P Global]] — paid MCP data connector, and also the source of one of the two partner vertical plugins
- [[topics/LSEG]] — paid MCP data connector, and the source of the other partner vertical plugin
- [[topics/PitchBook]] — one of the 11 paid MCP data connectors
- [[topics/Daloopa]] — one of the 11 paid MCP data connectors
- [[topics/Morningstar]] — one of the 11 paid MCP data connectors
- [[topics/Aiera]] — one of the 11 paid MCP data connectors
- [[topics/MT Newswires]] — one of the 11 paid MCP data connectors
- [[topics/Chronograph]] — one of the 11 paid MCP data connectors
- [[topics/Egnyte]] — one of the 11 paid MCP data connectors

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model powering the financial-services agents, deployed via Claude Cowork and the Managed Agents API

## 📡 Protocols & Standards
- [[topics/MCP]] — the 11 paid data connectors (FactSet, Moody's, etc.) are wired in as MCP connectors, described as the repo's real moat

## ✅ Action Items
- Clone `anthropics/financial-services` and inspect the plugin/skill structure as a template for building your own vertical-AI agent bundle.
- If you're in a regulated industry, study the disclaimer pattern (agents draft for human review, no execution authority) before deploying agents into production workflows.
- Try deploying one agent via the Managed Agents API script to see the leaf-worker sub-agent and orchestrator pattern firsthand.
- Watch for the same "10 agents / vertical bundles / paid data connectors / one deploy script" template appearing in other industries (legal, healthcare, insurance).

## 🔗 Related Videos
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, FactSet, GitHub, LSEG
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Cowork, MCP
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Cowork, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, GitHub, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, GitHub, MCP
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, GitHub, MCP

## Timeline
- `0:00` — Intro: Anthropic open-sources 10 Wall Street AI agents, one day after a $1.5B Goldman/Blackstone/H&F joint venture
- `0:26` — The numbers: 3,600 stars in 24 hours, #1 on GitHub trending
- `0:52` — What the repo actually is: plugins, cookbooks, scripts — pure configuration, no build step
- `1:18` — The 10 named agents covering the entire analyst floor
- `1:47` — The 7 vertical plugin bundles plus two partner plugins (LSEG, S&P Global)
- `2:16` — The MCP moat: 11 paid enterprise data connectors behind an Apache 2.0 repo
- `2:45` — Two deployment surfaces: Claude Cowork vs. the Managed Agents API
- `3:11` — Deploy script walkthrough: `201 Created`, hosted GL Reconciler with live data
- `3:36` — Callable agents: sub-agent delegation, flagged research preview
- `4:02` — The vertical-AI template: same skeleton for any other industry
- `4:28` — The disclaimer: draft-only, human sign-off required, plus outro

## Transcript
<details>
<summary>Full transcript</summary>

Anthropic just open-sourced 10 Wall Street AI agents on GitHub, Apache 2.0. And the timing is insane because 1 day earlier, Anthropic announced a $1.5 billion joint venture with Goldman, Blackstone, and Hellman and Friedman. This repo is not a demo. It is the product preview. Here's what's inside and why every other industry's repo is about to look like this one. 3,600 stars in 24 hours. Number one on GitHub trending. The repo, anthropic/financial_services. 3 days ago, zero stars. Today, 14,000. 1,800 forks. Fork to star ratio, 12 and 1/2%. Devs aren't bookmarking this. They're cloning it. Trying to ship it Monday morning. Crack it open. Three top-level folders. Plugins, managed agent cookbooks, scripts. Inside plugins, agent plugins and vertical plugins. The whole repo is markdown skills, JSON manifests, and Python deploy scripts. No build step, no SDK. This is configuration as code for AI agents.

And the configuration is everyone's job at Goldman. 10 named agents. The pitch agent. Meeting prep. Market researcher. Earnings reviewer. Model builder. Valuation reviewer. GL reconciler. Month end closer. Statement auditor. KYC screener. They handle decks, briefings, sector research, earnings, DCF and LBO models, valuations, reconciliations, and onboarding. The entire analyst floor, 10 markdown files. Seven vertical plugin bundles right on top. Investment banking, equity research, private equity, wealth management, fund administration, operations, plus a core financial analysis plugin, then two partner plugins, one from LSEG, one from S&P Global. Each vertical bundles the agents, skills, and slash commands its workflow needs. Pick the bundle, install it, you've got the team. Now the moat. 11 MCP connectors are wired in. FactSet, Moody's, S&P Global, LSEG, PitchBook, Daloopa, Morningstar, Aiera, MT Newswires, Chronograph, Egnyte. Every one of those is a six-figure enterprise data subscription. The repo is Apache 2.0. The data isn't. Open code, paid plumbing. That's how Anthropic locks in the customer without selling the lock-in.

Two ways to deploy. Path one, Claude co-work. Run Claude plugin marketplace at anthropic's slash Claude for financial services. Done. Path two, Anthropic's managed agents API. Post slash v1 slash agents hosted runtime. Same skills, different surface. The repo is the first real example of what that API was built for. Pick an agent, run scripts slash deploy managed agent.sh. The script uploads the skills, creates leaf worker sub agents, and posts the orchestrator to slash v1 slash agents. 201 created. You now own a hosted GL reconciler with Moody's data and FactSet integration. This is what agent infrastructure actually looks like. Hidden in the readme, the spicy part. Callable agents. The GL reconciler can hand off to the month-end closer through a steering event. One agent calls another. Real sub agent delegation. But it's flagged research preview, not GA, not even open beta. You request access. If you get it, congratulations, you're building the future. If you don't, wait, it's coming.

Forget finance for a second. Look at the shape. 10 agents, seven verticals, 11 data connectors, one deploy script. This is a template. Replace financial with legal or healthcare or insurance. Same skeleton, same managed agents API call. Anthropic just published the reference architecture for verticalized AI. Every other industry's repo is about to look like this one. One more thing. The red meat disclaimer is brutal. Quote, these agents draft analyst work product for human review. They do not execute trades, bind risk, or post to a ledger. Every output needs a human sign-off. Translation, Anthropic wants the analyst's hours, not the accountability. Smart. Repo's in the description. Clone it. Tell me what breaks. Subscribe.

</details>
