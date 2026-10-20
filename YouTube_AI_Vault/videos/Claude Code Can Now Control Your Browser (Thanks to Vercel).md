---
title: "Claude Code Can Now Control Your Browser (Thanks to Vercel)"
video_id: P7JrP57AxR0
channel: "[[channels/Better Stack]]"
uploaded: 2026-01-13
processed: 2026-07-05
duration: "6:52"
url: https://www.youtube.com/watch?v=P7JrP57AxR0
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [browser-automation, coding-agent-tool-comparison]
tools: [Agent Browser, OpenCode, Cursor, Claude Code, Playwright, Browser Use]
llms: [GLM]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Can Now Control Your Browser (Thanks to Vercel)

![thumbnail](https://i.ytimg.com/vi_webp/P7JrP57AxR0/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=P7JrP57AxR0) | 📅 Uploaded [[uploaded/2026-01-13]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Better Stack demos Vercel's Agent Browser — an open-source headless browser CLI built by a single engineer (Chris Tate) in a weekend — showing it fix a dark-mode bug and add form validation on a React app via OpenCode + GLM 4.7. The video also breaks down its Rust/Node architecture and compares it against Browser Use and the Playwright MCP server.

**Watch this if:** you want a fast, CLI-only way to let a coding agent (Claude Code, Cursor, OpenCode) drive a real Chromium browser to test and fix its own frontend changes.

## Key Takeaways
- Agent Browser is an open-source headless browser CLI (Rust binary + Node.js daemon) built by Vercel's Chris Tate in a single weekend; agents call it via plain CLI commands like `open`, `click`, `fill`, and `snapshot` — no MCP server or skill required.
- It uses a reference-based system (`@e1`, `@e2` style element references) and semantic locators (by role, text, label) instead of brittle CSS selectors, making element targeting deterministic and agent-friendly.
- Live demo: an agent (OpenCode running GLM 4.7) uses `agent-browser --help` to discover commands, snapshots a login page, fixes a broken dark-mode toggle, and separately adds missing login form validation — writing its own bash test script that uses `agent-browser eval` to verify the fix.
- Architecture: a CLI command is parsed by the Rust binary into JSON, sent over a Unix socket to a Node daemon (one per session) that drives headless Chromium via Playwright under the hood, then returns JSON output back to the agent.
- Compared to Browser Use: Browser Use can run a full autonomous plan-action-observe-replan loop on its own (with Python/TypeScript SDKs, a skills marketplace, and its own MCP server), whereas Agent Browser is simpler and only works when an external agent (Cursor, Claude Code, OpenCode) drives it via CLI.
- Compared to Playwright MCP: Agent Browser currently only supports Chromium (no Firefox/Safari), while Playwright MCP supports everything Playwright can do; but piling on many MCP tools can confuse an agent into picking the wrong one, whereas Agent Browser's CLI-only surface avoids that.
- The presenter's personal take: he prefers Agent Browser's simplicity and ease of install (`npm install -g`) since he mainly targets Chromium anyway.

## 🛠 Tools & Software
- [[topics/Agent Browser]] — Vercel's open-source headless browser CLI, the video's main subject; demoed fixing dark mode and login validation on a real app.
- [[topics/OpenCode]] — the coding agent harness used to run the demo, paired with GLM 4.7 and Agent Browser.
- [[topics/Cursor]] — mentioned as one of the coding agents developers can pair with Agent Browser.
- [[topics/Claude Code]] — mentioned as one of the coding agents developers can pair with Agent Browser (title's framing of the story).
- [[topics/Playwright]] — powers Agent Browser's actual browser execution under the hood, and is separately compared via the Playwright MCP server.
- [[topics/Browser Use]] — competing browser-automation framework compared against Agent Browser (full autonomous loop, SDKs, skills marketplace, own MCP server).

## 🤖 LLMs Mentioned
- [[topics/GLM]] — GLM 4.7 is the model driving the OpenCode agent in the demo; presenter notes a multimodal model would have been a better choice for reading screenshots.

## 📡 Protocols & Standards
- [[topics/MCP]] — discussed via the Playwright MCP server (and Browser Use's own MCP server) as the alternative integration path compared against Agent Browser's plain-CLI approach.

## ✅ Action Items
- Install Agent Browser globally (`npm install -g`) and run `agent-browser --help` inside an agent session so it discovers the available commands without needing a skill or MCP config.
- Point any coding agent (OpenCode, Cursor, Claude Code) at a running dev server and ask it to use Agent Browser to snapshot, click, and screenshot as part of verifying a bug fix.
- Prefer a multimodal model when using Agent Browser so the agent can actually read the screenshots it captures, rather than working blind.
- If you need full autonomous browsing without an external agent loop, evaluate Browser Use instead; if you need cross-browser (Firefox/Safari) support, evaluate Playwright MCP instead.

## 🔗 Related Videos
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Agent Browser, Claude Code, MCP, OpenCode
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Code, GLM, MCP, Playwright
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude Code, Cursor, MCP, OpenCode
- [[videos/Your AI Coding Workflow NEEDS This New Agent Browser CLI]] — shared: Agent Browser, Claude Code, MCP, Playwright
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor, OpenCode
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Browser Use, Claude Code, Playwright
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, MCP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, MCP, Playwright

## Timeline
- `0:00` — Intro: Agent Browser, a weekend project from a single Vercel employee.
- `0:22` — 2026 as the year of AI agents writing, reviewing, and testing code from the terminal.
- `0:52` — Introducing agent-browser by Vercel — CLI commands, accessibility snapshots, reference-based actions.
- `1:30` — Demo 1: fixing a broken dark-mode toggle on a React + Vite project.
- `3:00` — Agent Browser fixes login form validation and writes its own bash test script.
- `4:17` — How Agent Browser works: Rust CLI, Unix socket, Node daemon, headless Chromium via Playwright.
- `5:06` — Agent Browser vs. Browser Use vs. Playwright MCP server comparison.
- `6:30` — Presenter's closing thoughts on Agent Browser.

## Transcript
<details>
<summary>Full transcript</summary>

This is Agent Browser, an open-source headless browser CLI built in a weekend by a single Vercel employee that lets your agent do anything in the browser from dragging and dropping to uploading an image and even toggling offline mode. But why would anyone use this over something like Browser Use, which has way more features? And is Vercel getting into the agent browser space? Hit subscribe and let's get into it.

2026 is the year of AI agents writing, reviewing, and testing all of your code. No more tab completions. In fact, developers are even moving away from IDEs entirely in favor of doing everything in the terminal since all we're really doing now is reviewing code. And to help with this movement, we need the agents to actually interact with and test the code they've written. Because the last thing you want to do as a developer is to open up the browser to test each feature an army of agents have written one by one because that's just tedious.

This is where Vercel's new Agent Browser comes in handy. Written by Chris Tate in both Rust and TypeScript — I'll explain why later. This tool makes it so easy for an agent to interact with the browser using CLI commands that do a bunch of things like creating an accessibility snapshot that provides an accessibility tree and references to elements of a page, reference-based actions that take the references from the tree and apply relevant actions to them. There's also semantic locators if you don't want to use references that allow you to find an element based on its role, its text content, its label, and so much more.

In fact, let's go through a quick demo of how it works. Now, here is a little login page with an email and password. And it's built with shadcn/ui + React + Vite — not because of Vercel or anything, it just happened to be built that way. Now, there's one problem with this whole page and it's that right now I'm blinding my users because it's in light mode. So I want there to be a dark mode which I've actually gone ahead and asked the agent to do but as you can see it hasn't done it correctly. I mean, okay, this text changes but nothing else. So let's go ahead and get the agent to fix this using Agent Browser.

So right now I'm using OpenCode with the GLM 4.7 model, but of course Agent Browser can work with any agent and any model. I've gone ahead and told it that dark mode is broken and it should test it with agent-browser on the specific port. What's important is this part of the command to run `agent-browser --help` to see the available commands because there's no slash commands, no skills. I've just installed Agent Browser globally with npm. I'm going to hit enter and then it checks the available commands, uses the agent-browser snapshot functionality to create a snapshot of the page which shows document, heading, paragraph, text, and even images. It's then clicked on the relevant element and taken a screenshot to see if dark mode is working. And this is the screenshot if you're curious. From here, it's gone ahead and fixed the issue before taking another screenshot of the fixed dark mode. And it's finally finished the task, which we can test by clicking up here. And we have a page with perfect dark mode.

Let's try another test. Actually, while this was running, I had another agent in the background fix another issue. You may have noticed that if I press the login button, it will take me straight here without any validation, which of course isn't good. So I went ahead and asked it to fix the issue with the validation in this project and it did something actually really interesting. It first checks the available commands from Agent Browser and then, if we scroll down, it fixes the issue and even makes a bash script. So it's over here to test that it works. So it echoes the first test, adds an empty input, clicks the login button and then expects these errors. It's made a few tests here, but it's actually made an even better bash test down below, which we can see over here that makes use of agent-browser eval to run some JavaScript code. So now we can see if I press the login button, we get some validation. This looks like an email, but it's actually a placeholder. If I give it an email over here, just a made up one, and hit login, it says enter a valid email, which I can do like this. And then I can enter a password before it takes me to this dashboard.

So, basically, agents have addressed two issues with this app and tested it themselves to validate it works using the Agent Browser plug-in. I would say if I could do it again, I'd go with a model that has multimodal support so you can actually read the screenshots it takes instead of using GLM 4.7.

But now, let's get into some architecture. How does Agent Browser actually do all of these things? Well, after an agent runs a command like `agent-browser click @e2`, this gets sent to a Rust binary that parses that command and converts it to JSON. The benefit of it being Rust is that it's fast, resource efficient, and stays running after it's spawned. This JSON then gets sent to a Node daemon through a Unix socket, and this daemon manages the Chromium browser. What's cool about this is that a daemon is run per session, meaning multiple browsers can be controlled. Once the daemon validates the output, it launches the browser, which is headless by default, and executes the action using Playwright. And once it's completed, it sends the output also in JSON back to the agent. So the CLI, and from here, the agent can do whatever it wants — it can send even more commands to the Rust binary or it can end the whole loop. All of this is super impressive for a weekend's project.

But how does it compare to Browser Use or even using the Playwright MCP server? Well, Browser Use can be used with or without an external agent because it can run the full agent reasoning loop — so, plan, action, observe, and replan all on its own without the use of anything else. It also has a Python and TypeScript SDK for fine-grained control. It has a skills marketplace, an MCP server, and uses Better Stack to track the API status, which is very cool. Agent Browser, on the other hand, is much simpler and can only be used with an external agent. So you, the developer, have to provide an agent like Cursor, Claude Code, OpenCode, and the agent only interacts with Agent Browser through CLI commands.

When it comes to comparing Agent Browser with the Playwright MCP server, right now Agent Browser only supports Chromium browsers, so no Firefox or Safari, which I believe the Playwright MCP server does support. In fact, it supports everything that Playwright can do, but with an MCP server that is perfect for agents. The only kind of downside is if you already have loads and loads of MCP tools, then adding a bunch more could confuse the agents since it has more tools available to choose from autonomously, and it might not choose the right one the first time.

Basically, choosing between Browser Use, the Playwright MCP server, and Agent Browser really depends on your use case and what you want from your agent. For me personally, I like the simplicity and ease of installation from Agent Browser. And I primarily use Chromium browsers, so not too fussed about not having Firefox or Safari access. So, I'll use it for now and see how it goes. Also, while I've got your attention, we are so close to hitting that 100K subscriber mark. So, if you haven't already, go ahead and hit the subscribe button.

</details>
