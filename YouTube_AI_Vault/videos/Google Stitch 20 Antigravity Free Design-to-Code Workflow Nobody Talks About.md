---
title: "Google Stitch 2.0 + Antigravity: Free Design-to-Code Workflow Nobody Talks About"
video_id: 0rtkaioPb30
channel: "[[channels/AI Stack Engineer]]"
uploaded: 2026-04-16
processed: 2026-07-05
duration: "9:02"
url: https://www.youtube.com/watch?v=0rtkaioPb30
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [design-to-code-workflow, ai-native-ui-prototyping]
tools: [Google Stitch, Antigravity, Figma, VS Code, Gemini CLI, DESIGN.md]
llms: [Gemini]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Google Stitch 2.0 + Antigravity: Free Design-to-Code Workflow Nobody Talks About

![thumbnail](https://i.ytimg.com/vi/0rtkaioPb30/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=0rtkaioPb30) | 📅 Uploaded [[uploaded/2026-04-16]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Google rebuilt Stitch (its AI design tool) with an infinite context-aware canvas, a project-memory design agent that can run parallel sub-agents, Gemini Live voice design, clickable interactive prototypes, and a portable DESIGN.md design-system file. Stitch now connects to Google Antigravity over MCP so an agent can pull the Stitch design and code the full app — all free, with a paid tier comparison against Figma.

**Watch this if:** you want a free way to go from AI-generated UI design straight to a working coded app without Figma-to-code busywork.

## Key Takeaways
- The new Stitch canvas is infinite and multimodal — you can drag in images, screenshots, and text notes alongside prompts, and the AI reasons across everything on the canvas at once (similar to Figma's artboards, but AI-aware).
- The design agent now tracks full project history and builds on prior versions instead of starting from zero each time; a new "agent manager" lets multiple agents work on different screens in parallel.
- Gemini Live voice integration turns Stitch into a conversational design agent that asks follow-up questions (desktop vs. mobile, what data to show) and can make live edits by voice ("make the sidebar narrower").
- A new play button stitches individual screens into a clickable interactive prototype, auto-generating a logical next screen (e.g., a sign-up page) if you click an element with no linked screen yet; supports mobile/tablet/desktop views and a click-prediction heat map.
- DESIGN.md is a portable markdown file capturing colors, typography, spacing, and component patterns — generated from scratch or by crawling an existing website's URL to extract its design tokens, and importable into other Stitch projects or tools.
- Stitch now connects directly to Antigravity (Google's agentic IDE built on VS Code) via an MCP server: the Antigravity agent pulls Stitch's code, design tokens, and layout, then adds backend (auth, database, API routes) — some developers report full working apps in under 30 minutes this way.
- Google also shipped seven agent skills that work across Antigravity, Gemini CLI, and other coding tools for converting Stitch designs to React components and generating design tokens.
- Stitch is free (350 standard Gemini Flash generations/month + 200 experimental Gemini Pro generations, no credit card) versus Figma's Organization plan at $55/seat/month (~$13K/year for a 20-person team); Figma's stock dropped ~8% the day the Stitch redesign was announced, though Stitch isn't a replacement for professional design teams yet.

## 🛠 Tools & Software
- [[topics/Google Stitch]] — Google's AI design tool, rebuilt with an infinite canvas, smarter design agent, voice input, prototyping, and DESIGN.md support
- [[topics/Antigravity]] — Google's agentic IDE (built on VS Code) that connects to Stitch via MCP to turn designs into full working coded apps
- [[topics/Figma]] — used as the cost/capability comparison point; also the original export target for the old Stitch
- [[topics/VS Code]] — the base editor that Antigravity is built on top of
- [[topics/Gemini CLI]] — named as one of the coding tools that Google's new agent skills work across alongside Antigravity
- [[topics/DESIGN.md]] — the portable markdown design-system file Stitch generates/imports, letting Antigravity keep colors/fonts/spacing consistent when coding

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — powers Stitch's standard generations (Gemini Flash) and experimental generations (Gemini Pro), plus the new Gemini Live voice design feature

## 📡 Protocols & Standards
- [[topics/MCP]] — the protocol Stitch uses to connect to Antigravity (install the Stitch MCP server, add an API key, and Antigravity can pull designs/code directly)

## ✅ Action Items
- Sign in at stitch.withgoogle.com with a Google account to try the new canvas and design agent for free.
- Generate or import a DESIGN.md by pasting your company website's URL to auto-extract your existing brand colors, fonts, and spacing.
- Install Antigravity, add the Stitch MCP server from its MCP store, and plug in your Stitch API key to let an agent build the backend around a Stitch design.
- Use the agent manager to run multiple Stitch design agents in parallel across different screens of the same project instead of building screens one at a time.

## 🔗 Related Videos
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Antigravity, Gemini, Gemini CLI
- [[videos/The Last Claude Code Tutorial You'll Ever Need]] — shared: Figma, Gemini, MCP
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Antigravity, Gemini CLI, MCP
- [[videos/Your AI UI Looks Generic This Fixes It (DESIGNmd)]] — shared: DESIGN.md, Figma, Google Stitch
- [[videos/Can Claude Code Fix an Engineer's Terrible Taste]] — shared: Antigravity, Gemini
- [[videos/Claude Code + Karpathy Slides Just Changed Presentations Forever (MARP System)]] — shared: Antigravity, VS Code
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: MCP, VS Code
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: MCP, VS Code

## Timeline
- `0:00` — Intro: Stitch rebuilt from the ground up since its May 2025 Labs debut
- `0:30` — Update 1: the new infinite, multimodal canvas
- `1:20` — The canvas is AI-aware across everything placed on it (Figma-artboard-like)
- `1:37` — Update 2: the smarter design agent with project memory + parallel agent manager
- `2:35` — Update 3: Gemini Live voice-driven conversational design
- `3:43` — Interactive prototypes: the play button stitches screens together, auto-generates missing screens
- `4:12` — Device previews and click-prediction heat map
- `4:32` — Update 4: DESIGN.md portable design-system file, importable from any site URL
- `5:23` — Stitch connects to Antigravity via MCP; full apps built in under 30 minutes
- `6:50` — Seven new Google agent skills across Antigravity, Gemini CLI, and other tools
- `7:13` — Pricing: Stitch free tier vs. Figma Organization plan cost comparison
- `8:30` — Getting started: stitch.withgoogle.com and antigravity.google setup (~5 minutes)

## Transcript
<details>
<summary>Full transcript</summary>

So, Google just rebuilt Stitch from the ground up. Stitch is Google's AI design tool that came out of Google Labs back in May 2025. The original version was pretty basic — you typed a prompt, it gave you a screen, and you could export the code or send it to Figma. It felt more like a demo than an actual tool you could rely on. That version is gone; now it's a completely different product.

The first thing you notice is the canvas. It used to be a simple prompt-in, screen-out layout. Now it's an infinite canvas — you can drag images onto it, paste code snippets, throw in text notes, screenshots of competitor apps, whatever, and the AI can see all of it at once. Drag in a dashboard screenshot from Dribbble and type "make me something like this but for a logistics company," and the AI uses the screenshot as reference along with the text — a big shift from the old text-box-only workflow. The canvas also lets you keep multiple screens visible at once, works kind of like Figma's artboards, except the AI reasons across the entire canvas when generating new stuff, so outputs improve the more context you feed it.

The second update is the design agent itself. The old agent just took your prompt and spit out a result; the new agent tracks your full project history — what you tried, what you changed, what direction the project has been going — so new requests build on what already exists rather than starting from zero. There's also a new "agent manager": you can run multiple agents at the same time on different tasks (one on the landing page, another on the user profile screen), tracking progress separately without interference — a big time-saver over doing screens one by one.

The third update is voice. Stitch now has Gemini Live integration — a full conversational agent, not just voice-to-text. Say "I need a CRM dashboard for an AI company, dark mode" and the agent asks follow-up questions like desktop vs. mobile and what data to show, then generates based on the conversation. You can also use voice inside a design to request live changes — "make the sidebar narrower" or "show me three color options for the header." Tested with a simple landing page request; quality was solid, usable as a starting point.

Before, Stitch gave you individual screens with no way to link them into a previewable flow. Now there's a play button that stitches all your screens into a clickable interactive prototype. Click an element with no connected screen yet (like a sign-up button) and Stitch auto-generates the next logical screen based on project context — letting you map entire user journeys without manually designing every screen. You can preview at mobile, tablet, and desktop sizes, and there's a heat map predicting where users are most likely to click, useful for optimizing layout before handoff to development.

Design system support comes via DESIGN.md — a markdown file capturing your design rules: colors, typography, spacing, component patterns. Create one from scratch, or import a design system from any website by pasting its URL — Stitch crawls the site and extracts the design tokens automatically (great if you have an existing brand guide). DESIGN.md is portable — export it, import it into another Stitch project, and because it's standard markdown, coding tools and AI agents can read it too.

Which brings it together: Stitch now connects directly to Google Antigravity, Google's agentic IDE (launched November 2025, built on VS Code) with AI agents that plan, write code, debug, and test apps in a browser autonomously. The connection works through MCP (model context protocol) — install the Stitch MCP server inside Antigravity, plug in your API key, and the Antigravity agent can pull designs directly from your Stitch projects: code, design tokens, layout metadata, everything. Workflow: design the UI in Stitch, then tell the Antigravity agent to fetch the Stitch design and build the actual app — it adds the backend (auth, database connections, API routes). Some developers report building full working apps in under 30 minutes this way. Because Stitch generates the DESIGN.md file, Antigravity reads your exact design rules and keeps colors, fonts, and spacing consistent as it builds, without manual checking.

Google also released seven agent skills that work across Antigravity, Gemini CLI, and other coding tools — install with a single command, and they handle things like converting Stitch designs into React components or generating design tokens automatically. The ecosystem is starting to feel like one connected pipeline rather than separate glued-together tools.

Stitch is free: 350 standard generations per month using Gemini Flash, plus 200 experimental generations using the Pro model, no credit card needed — design to working coded app at no cost. Compare that to Figma's organization plan at $55/seat/month — over $13,000/year for a 20-person team — and Figma doesn't write code for you. Figma's stock actually dropped about 8% the day Google announced the Stitch redesign, which tells you the market is taking this seriously. But Stitch won't replace Figma for professional design teams yet — Figma still has real-time collaboration, advanced component libraries, plugins, and developer handoff tools. Stitch is still a Google Labs product (which could get shut down anytime), and its outputs, while good for ideation and prototyping, usually need manual cleanup before production; some users report the agent forgetting design choices or reinterpreting elements unexpectedly.

To get started, just sign in with a Google account at stitch.withgoogle.com. To connect Antigravity, download it from antigravity.google, install the Stitch MCP server from the MCP store inside the IDE, and add your API key from Stitch settings — the whole setup takes about 5 minutes.

</details>
