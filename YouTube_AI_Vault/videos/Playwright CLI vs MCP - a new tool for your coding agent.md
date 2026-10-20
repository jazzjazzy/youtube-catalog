---
title: "Playwright CLI vs MCP - a new tool for your coding agent"
video_id: Be0ceKN81S8
channel: "[[channels/Playwright]]"
uploaded: 2026-02-06
processed: 2026-07-06
duration: "6:12"
url: https://www.youtube.com/watch?v=Be0ceKN81S8
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [browser-automation-agents]
tools: [Playwright CLI, Playwright, Claude Code, GitHub Copilot]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Playwright CLI vs MCP - a new tool for your coding agent

![thumbnail](https://i.ytimg.com/vi/Be0ceKN81S8/sddefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Be0ceKN81S8) | 📅 Uploaded [[uploaded/2026-02-06]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> The Playwright team introduces Playwright CLI, a new alternative to Playwright MCP, and runs the same identical task (open playwright.dev, search locators, screenshot each language's docs) through both. MCP consumed 114,000 tokens because accessibility snapshots and screenshot bytes get pushed straight into the LLM's context, while CLI used only 26,800 tokens by saving everything to disk and letting the coding agent decide what actually needs to reach the model.

**Watch this if:** you're using Playwright MCP with a coding agent and want to know when switching to Playwright CLI would save significant context/tokens.

## Key Takeaways
- Playwright CLI is installed globally, then initialized per-workspace (`playwright-cli install`), with each workspace getting its own isolated set of browsers.
- Skills can be installed into a CLI workspace (`install skills`) to give Claude Code project-specific Playwright knowledge, making CLI interoperable with other skill-based tooling.
- Running the identical demo task, Playwright MCP used 114,000 tokens versus Playwright CLI's 26,800 tokens — over 4x more for MCP.
- The token gap comes from how results are delivered: MCP replies with the full accessibility snapshot and raw screenshot bytes directly into the LLM's context (even hitting "result exceeds maximum tokens"), while CLI saves snapshots/screenshots to disk and only sends data to the LLM if the coding agent decides it's actually needed.
- All of Playwright CLI's capabilities also exist in MCP, but MCP disables most of them by default specifically because enabling them would consume too much context; CLI has no such restriction and exposes everything.
- CLI is token-efficient specifically because it requires a coding agent (like Claude Code or GitHub Copilot) that can read/write files and decide what to send to the LLM — it's headless by default, assuming background-agent use.
- MCP remains the better fit for building a generic agentic loop (not tied to a file-editing coding agent) since it's a strict, standardized protocol any tool can call, with configurable (if more manual) control over which tools are enabled.
- Recommendation: use CLI for coding/testing tasks inside agents like Claude Code or GitHub Copilot; use MCP when authoring a custom agentic loop for specific scenarios.

## 🛠 Tools & Software
- [[topics/Playwright CLI]] — the new tool demoed end-to-end: install, initialize a workspace, install skills, and run a browser-automation task with far lower token usage than MCP.
- [[topics/Playwright]] — the parent browser-automation project both CLI and MCP belong to.
- [[topics/Claude Code]] — the coding agent used to run the identical demo task through both CLI and MCP, showing the token-consumption difference.
- [[topics/GitHub Copilot]] — mentioned as another coding agent for which Playwright CLI's token efficiency applies.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose context window absorbs MCP's full snapshot/screenshot replies (114k tokens) versus CLI's disk-first approach (26.8k tokens).

## 📡 Protocols & Standards
- [[topics/MCP]] — directly compared against Playwright CLI; shown consuming far more context because tool results flow straight into the LLM rather than being filtered through file storage first.

## ✅ Action Items
- Install Playwright CLI globally and run `playwright-cli install` to initialize a per-project workspace with its own browser set.
- Install relevant skills into your CLI workspace to give your coding agent Playwright-specific knowledge.
- If you're driving Playwright through a file-editing coding agent (Claude Code, GitHub Copilot, etc.), switch to CLI to cut context/token usage significantly.
- Keep using Playwright MCP if you're building a standalone agentic loop that isn't a general file-editing coding agent.
- Check your agent's context/token stats after a browser-automation run to compare actual CLI vs. MCP consumption for your own workflows.

## 🔗 Related Videos
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/ShadCN is Way too Powerful Now]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, MCP

## Timeline
- `0:00` — Intro: Playwright CLI as a new tool in the Playwright family, video roadmap (demo, token efficiency, capabilities).
- `0:25` — CLI demo setup: global install, `playwright-cli install` to create a per-workspace folder, installing skills.
- `1:10` — Giving Claude Code a task (open playwright.dev, search "locators," screenshot docs per language) via CLI, shown as a 16x timelapse.
- `2:00` — Same task run via Playwright MCP instead, also as a 16x timelapse.
- `2:20` — Token comparison: MCP used 114,000 tokens vs. CLI's 26,800 tokens.
- `2:45` — Digging into why: MCP pushes the full accessibility snapshot and raw screenshot bytes into the LLM context, even hitting a max-token error.
- `3:40` — Contrasting CLI's behavior: navigates, takes a screenshot, saves to disk — no snapshot/image tokens reach the LLM at all.
- `4:15` — Capabilities: all CLI features exist in MCP too, but most are disabled by default in MCP specifically to limit context use.
- `4:50` — When CLI shines: requires a file-editing coding agent (Claude Code, GitHub Copilot); skill-based and headless by default.
- `5:20` — When MCP still wins: generic/standalone agentic loops needing a strict, standardized protocol, with configurable tool allow/disallow lists.
- `5:50` — Recap recommendation: CLI for coding-agent tasks, MCP for custom agentic loops.

## Transcript
<details>
<summary>Full transcript</summary>

The Playwright team introduces Playwright CLI, a new tool in the Playwright family, covering what it is, how it compares to MCP, token efficiency, and capabilities. In the demo, starting from an empty folder, Playwright CLI is installed globally, then `playwright-cli install` initializes the workspace (creating a `.playwright` folder used to differentiate workspaces on disk, each with its own set of browsers). Skills are also installed into the workspace to give the coding agent Playwright-specific knowledge. Starting Claude Code, the task given is: open playwright.dev, search for "locators," verify the doc is available for each language (JavaScript, Python, Java, .NET), and take a screenshot of each language's doc page — shown as a 16x timelapse of Claude talking to a browser via the CLI utility. After completion, context/token stats are checked, and the same exact task is then run via Playwright MCP instead (with no skills installed, just the MCP server), also as a 16x timelapse.

The token comparison: MCP consumed 114,000 tokens for the task — quite costly — compared to CLI's 26,800 tokens. Digging into why: MCP first navigated to playwright.dev (a doc-heavy page with lots of DOM, scripts, etc.), and even though Playwright MCP is efficient about sending only an accessibility snapshot (not the full DOM) to the LLM, that snapshot's full content still landed in context, at one point exceeding the maximum token limit. Then, when taking a screenshot, because the LLM itself requests the screenshot, the raw image bytes are returned to the LLM and its tokens end up in context too — even though all that was needed was to save the file to disk. By contrast, CLI navigated to the location and, without capturing or reading a snapshot file created on disk, immediately took a screenshot and saved it to a file — no snapshot or image tokens entered the context at all, since the LLM never needed them.

On capabilities: the demo only showed MCP using a couple dozen commands, but that's not because those capabilities don't exist — all CLI capabilities are also present in MCP, they're just not enabled by default because they consume context. CLI has no such default restriction and can expose all commands and more.

Given the numbers, it might seem CLI is a no-brainer, but it depends on use case. CLI shines specifically as part of a coding agent (Claude Code, GitHub Copilot, or any agent that can edit files and access your workspace) — snapshots and screenshots get saved to disk, and the coding agent decides whether to read them in full or send them to the LLM, which is what makes it token-efficient; CLI requires a coding agent to get that efficiency. It's also skill-based (interoperable with other skill-based tools) and headless by default, assuming heavy use of background agents.

MCP, on the other hand, works with any generic agent as a strict standard — tools know exactly what to expect, how to call MCP tools, and what results look like — but everything is in the LLM's hands, so replies are likely to make their way back into context and can overwhelm it. MCP still supports multiple browsers, and its efficiency can be configured by allowing/disallowing specific tools, though this is more manual; MCP has also historically been the default choice.

Recap: if you're using a coding agent for coding/testing tasks (Claude, GitHub Copilot, etc.), CLI is probably the better choice. If you're authoring a custom agentic loop for specific scenarios, MCP is still the way to go.

</details>
