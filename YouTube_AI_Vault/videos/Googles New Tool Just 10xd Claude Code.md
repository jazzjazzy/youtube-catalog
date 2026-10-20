---
title: "Google’s New Tool Just 10x’d Claude Code"
video_id: Wu67lLD8bB0
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-03-10
processed: 2026-07-05
duration: "11:49"
url: https://www.youtube.com/watch?v=Wu67lLD8bB0
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [google-workspace-automation, ai-executive-assistant]
tools: [Claude Code, Google Workspace CLI, Chrome, GitHub]
llms: [Claude, Nano Banana]
protocols: [MCP, OAuth]
transcript: true
tags: [youtube, ai-automation]
---

# Google’s New Tool Just 10x’d Claude Code

![thumbnail](https://i.ytimg.com/vi_webp/Wu67lLD8bB0/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=Wu67lLD8bB0) | 📅 Uploaded [[uploaded/2026-03-10]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Google released an open-source Google Workspace CLI (GWS CLI) that gives Claude Code direct, bash-command-level control over Gmail, Drive, Docs, Sheets, Calendar, and Slides, plus 100+ pre-built multi-step "recipe" workflows. The video walks through what it can do, why a single CLI beats juggling API calls or multiple MCP configs, a full manual OAuth installation via Google Cloud Console, and live demos including a formatted Google Doc resource guide, email triage/scoring, and a Google Slides deck with Chrome DevTools-based visual validation.

**Watch this if:** you want Claude Code to directly read, create, and manage your Gmail/Drive/Docs/Sheets/Calendar/Slides without MCP servers or manual API wiring.

## Key Takeaways
- GWS CLI (Google Workspace CLI) gives Claude Code a single tool that can search, list, upload, download, move, copy, and share across Drive, Gmail, Calendar, Docs, Sheets, and Slides, plus over 100 built-in "recipe" workflows (e.g. creating docs from templates, reading sheet data into a report, finding free time and scheduling a meeting).
- Actions run via actual bash/terminal commands talking to Google, not via API calls or MCP — demoed by having Claude Code pull a YouTube transcript and generate a fully formatted Google Doc resource guide (header image, links, CTA) instead of the usual raw-markdown API output.
- Benefits over MCP/API alternatives: one unified interface across all Workspace tools, JSON-first structured responses that are easy for an agent to parse, auto-discovery that keeps the CLI current as Google adds endpoints, and much lower context overhead than maintaining separate MCP configs per tool.
- It's an open-source, free, "not officially supported" Google product still under active development pre-v1.0 — expect breaking changes, but functionality is already extensive and improving.
- Installation has two paths: automatic setup via the Google Cloud CLI, or a full manual path through Google Cloud Console — create a project, configure the OAuth consent screen, create a desktop-app OAuth client ID, download the client secret JSON to the CLI's global config directory, then run `gws auth login` and enable each required Workspace API individually.
- Claude Code itself can drive most of the installation by reading the CLI's documentation and walking through prerequisites, install steps, and troubleshooting when auth doesn't work on the first try.
- Demoed live: finding a specific Google Doc from a vague natural-language request; scoring 30 unread emails against business-context priorities and auto-marking low-priority ones as read; and generating a branded Google Slides deck.
- For the Slides demo, Claude Code initially couldn't visually inspect its own output (it can only build programmatically) — giving it Chrome DevTools access let it screenshot each slide, identify spacing issues, and iteratively update its own Google Slide Creator skill with a visual-validation step.
- Presented as a potential low-cost or free alternative to tools like Gamma for slide generation, and as a natural fit for building an executive-assistant-style Claude Code project on top of full Workspace access.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent driving every GWS CLI action in the video, from installation and OAuth setup to generating docs, triaging email, and building slide decks
- [[topics/Google Workspace CLI]] — the open-source CLI at the center of the video, giving Claude Code bash-level control over Gmail, Drive, Docs, Sheets, Calendar, and Slides plus 100+ recipe workflows
- [[topics/Chrome]] — Chrome DevTools access is given to Claude Code so it can screenshot and visually validate the Google Slides it generates, then fix spacing issues
- [[topics/GitHub]] — the GWS CLI's GitHub repository is walked through directly, including its skills/recipes folder and development-status notices

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model behind Claude Code, which drives the entire GWS CLI installation and every demoed workflow
- [[topics/Nano Banana]] — used to generate the custom on-brand images inserted into the demoed Google Slides deck

## 📡 Protocols & Standards
- [[topics/MCP]] — contrasted directly with the GWS CLI approach: actions run via bash commands rather than MCP tool calls, avoiding the context overhead of maintaining separate MCP configs per Workspace service
- [[topics/OAuth]] — the manual installation path is a full walkthrough of Google's OAuth consent screen setup, desktop-app client ID/secret creation, and `gws auth login` authentication flow

## ✅ Action Items
- Install the GWS CLI by handing Claude Code the GitHub repo link and asking it to read the docs and walk you through setup.
- If automatic Google Cloud CLI setup doesn't work cleanly, follow the manual path: create a GCP project, configure the OAuth consent screen, create a desktop-app client ID, and save the client secret JSON to the CLI's global config path.
- Enable each Google Workspace API you need individually in the Cloud Console project before running `gws auth login`.
- Try a low-stakes first task (e.g. "find a doc I made last year") to confirm auth and access are working end-to-end.
- Give Claude Code Chrome DevTools access when generating visual output (like Slides) so it can screenshot and self-correct instead of guessing blind.
- Consider building an executive-assistant-style project on top of GWS CLI for tasks like email triage and scoring.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Google's New CLI Is The Missing Piece for Claude Code]] — shared: Claude, Claude Code, Google Workspace CLI, MCP
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/The Claude Code Skill Boris Cherny Runs on Every Project]] — shared: Chrome, Claude, Claude Code, GitHub
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Google Workspace CLI, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude, Claude Code, MCP

## Timeline
- `0:00` — What GWS CLI can do across Gmail, Drive, Docs, Sheets, Calendar, Slides
- `1:00` — Demo: generating a formatted Google Doc resource guide from a YouTube link
- `2:03` — Why use this over API calls or MCP configs
- `3:06` — GitHub repo walkthrough: skills/recipes and development status
- `4:08` — Full installation guide: Google Cloud Console, OAuth consent screen, client ID/secret
- `7:57` — Demos: finding a doc, email triage/scoring, Google Slides generation with visual validation
- `10:50` — Final thoughts: early but powerful, recommended next step of building an executive assistant

## Transcript
<details>
<summary>Full transcript</summary>

Google just dropped an open-source Google Workspace CLI (GWS CLI) that some are already calling the most powerful workspace CLI available. Any Claude Code project can now access Gmail, Drive, Docs, Sheets, Calendar, and Slides after installing one tool — it can search, list, upload, download, move, copy, and share across all of them, plus over a hundred built-in "recipe" multi-step workflows for common tasks like creating docs from templates, turning sheet data into a report doc, or finding free time and scheduling a meeting. Where past attempts to get Claude or similar tools to generate a Google Doc via API produced ugly raw markdown, GWS CLI

lets Claude Code create the doc via an actual bash command talking to Google rather than an API call or MCP — demoed by dropping a YouTube link into Claude Code and asking for a formatted resource guide: it pulls the transcript, creates the Google Doc, and populates it with a header image, links back to the channel, and a CTA, fully formatted rather than raw text. The benefits: one unified interface across Gmail, Drive, Docs, Sheets, Calendar, and Admin; JSON-first structured responses that are easy for an agent to work with; auto-discovery so the CLI stays current automatically as Google adds new API endpoints or methods; built-in skills for triage, prep, and generation (a hundred-plus of them); and much lower context overhead than maintaining a pile of separate API endpoints or MCP configs. (A quick aside on what a CLI even is: a command-line interface, as opposed to the buttons-and-forms GUI most people are used to — computers fundamentally navigate via text and commands.) This is

an open-source, completely free Google product, with the GitHub repo linked for anyone who wants to dig in. The repo's skills folder shows the full library of pre-made recipes — creating events from sheets, creating presentations, creating meet spaces, labeling and archiving emails, and many more. It's explicitly marked "not an officially supported Google product," meaning it's more open-source beta/developer playground than enterprise-backed software, and is under active development with breaking changes expected before v1.0 — already strong out of the box and expected to keep improving, with new Workspace API endpoints picked up automatically. Installation walkthrough: copy the GitHub repo link, give it to Claude Code, and ask it to read the documentation and install everything needed. Claude Code checks existing prerequisites, installs the CLI, and then offers two auth paths — automatic setup via Google Cloud CLI, or manual setup by creating your own Google Cloud project. The automatic

path required extra installs beyond a single command, so the manual path is demoed instead: create a new project in Google Cloud Console, then under APIs and Services configure the OAuth consent screen (giving the app a name, choosing an "internal" audience for personal/org-only use, adding a test user email if using external/testing), then create a client ID under Credentials, choosing "desktop app" as the type. This produces a client ID and

client secret, downloaded as a JSON file that needs to be saved to the CLI's global config directory (Claude Code can supply the exact full path if you're unsure where that is). With credentials in place, the last step is running `gws auth login`, which opens a browser tab to authenticate with the chosen Google account and confirm access permissions. First-attempt hiccups are common, but going back and forth with Claude Code (since it can read the actual documentation) resolves them — after auth succeeds, the remaining step is enabling each needed Workspace API individually inside the Cloud Console

project, one click each. With everything enabled, GWS CLI can now take action anywhere in Google Workspace — demoed by asking it to find a specific Google Doc from an intentionally vague description, which it does successfully. Live use in an ongoing executive-assistant project has been going well: asking it to pull the day's unread emails, score them against business-context priorities, and automatically mark anything scoring below a threshold as already-read — it processes 30 unread emails and returns scored priorities based on business context. A second demo explores Google Slides as a potential low-cost alternative to Gamma: after feeding it brand guidelines and a logo,

the first generated deck had spacing issues Claude Code couldn't see on its own since it can only build slides programmatically, not view them. Giving it access to Chrome DevTools let it open the deck, screenshot each slide, and identify problems — leading to a plan to add visual validation to the Google Slide Creator skill itself. After iterating, the resulting deck showed brand colors, a logo, better (if imperfect) spacing, and custom on-brand images generated with Nano Banana 2. A follow-up request to audit the deck again for future skill improvements has it opening a browser tab, screenshotting every slide in

sequence, and reading each screenshot before returning an audit with suggested improvements (noting that a smaller browser window reduced screenshot quality, and that presentation-mode screenshots would likely work better). The tool is very new — some online reactions call it overpowered, others find it finicky (particularly around repeated re-authentication) — but the experience here has been consistently reliable for finding, scheduling, and creating things across Workspace. The recommended next step is connecting GWS CLI to a broader Claude Code project like a personal executive assistant.

</details>
