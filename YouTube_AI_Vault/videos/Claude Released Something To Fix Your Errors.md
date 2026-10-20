---
title: "Claude Released Something To Fix Your Errors"
video_id: NuKrtiJqW3Y
channel: "[[channels/AI LABS]]"
uploaded: 2025-12-26
processed: 2026-07-06
duration: "7:48"
url: https://www.youtube.com/watch?v=NuKrtiJqW3Y
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [automated-browser-testing, ai-visual-testing]
tools: [Claude Code, Claude Browser Extension, Playwright, Puppeteer, Chrome, Google Docs, Google Sheets]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Released Something To Fix Your Errors

![thumbnail](https://i.ytimg.com/vi_webp/NuKrtiJqW3Y/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=NuKrtiJqW3Y) | 📅 Uploaded [[uploaded/2025-12-26]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Claude Code's new native Chrome extension (an integrated MCP) replaces flaky Playwright/Puppeteer-based browser automation for testing. The video walks through fixing the extension's out-of-the-box problems — bloated context from section-by-section screenshots, oversized HTML extraction, and wasted time on cookie pop-ups — with custom scripts, CLAUDE.md instructions, and a structured slash-command testing workflow.

**Watch this if:** you use Claude Code for visual/browser testing and are burning tokens or context window on repetitive screenshot loops, pop-up dismissal, or oversized page extraction.

## Key Takeaways
- Claude Code's native Chrome extension (shipped as an integrated MCP) is presented as a major upgrade over Playwright or Puppeteer MCP, which had bloated context windows, cluttered project folders with screenshots, and often failed to complete actions.
- Problem 1 — inefficient screenshots: by default Claude scrolls and screenshots each section of a page separately, then stitches them together; a custom script for full-page screenshots (wired up via a custom slash command) gets the same accuracy much faster and cheaper on tokens.
- Problem 2 — context bloat: MCP browser tools often load all HTML inside the `<main>` tag instead of specific divs; CLAUDE.md instructions constrain extraction to only what's needed.
- Problem 3 — cookie pop-ups: instead of letting Claude burn tokens screenshotting/scrolling to dismiss them, a script matching common "accept" button selectors auto-dismisses cookie banners before Claude proceeds, triggered via CLAUDE.md instructions.
- Security limitation: Claude is deliberately blocked from completing CAPTCHAs or authentication — you must pre-authenticate any login-gated site before assigning Claude a task there.
- Advantage over Puppeteer/Playwright MCP: being a native tool built by the Claude Code team, it can interact with your already-signed-in browser sessions (e.g. Google Docs, Google Sheets) rather than running in an isolated, session-less environment.
- Known limitations: browser integration is compute/context-intensive (watch for auto-compaction), Chrome-only (no other Chromium browsers), buggy with multiple Chrome profiles, and subject to Manifest V3's limit on how long an extension can run — long end-to-end test sessions can get blocked mid-task.
- Workflow fix for the Manifest V3 timeout: instead of one long end-to-end test run, split testing into multiple test files with priority levels, preconditions, and expected results, plus a CLAUDE.md-driven habit of writing a test report after each file so progress survives context compaction.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent using the new Chrome extension/MCP to run automated browser testing workflows.
- [[topics/Claude Browser Extension]] — the video's central subject: Claude Code's new native Chrome integration (an MCP) for browser automation and visual testing, with fixes for its default screenshot, context, and pop-up handling behavior.
- [[topics/Playwright]] — named as one of the older MCP-based browser automation approaches this new extension is compared against and improves on.
- [[topics/Puppeteer]] — named as the other MCP-based browser automation approach (e.g. "Claude Code vs Cursor's Puppeteer MCP") that the native Chrome extension is positioned to replace.
- [[topics/Chrome]] — the browser the extension is built for; noted as Chrome-only, not other Chromium browsers, with bugs around multiple profiles.
- [[topics/Google Docs]] — cited as an example service Claude can interact with using retained signed-in session state via the Chrome extension.
- [[topics/Google Sheets]] — cited alongside Google Docs as another signed-in service Claude can interact with via the extension.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model running in Claude Code that drives the browser extension-based testing workflow throughout.

## 📡 Protocols & Standards
- [[topics/MCP]] — the new Chrome extension is described as shipping as "an integrated MCP" giving Claude Code custom browser tools, contrasted with the older Playwright/Puppeteer MCP servers.

## ✅ Action Items
- Replace section-by-section screenshot testing with a custom full-page screenshot script wired into a slash command.
- Add CLAUDE.md instructions to limit HTML extraction scope and avoid context bloat during browser testing.
- Write (or borrow) a script that auto-dismisses common cookie/consent pop-ups before Claude proceeds with a page.
- Pre-authenticate any login- or CAPTCHA-gated site before handing Claude a browser testing task.
- Split long end-to-end test plans into multiple smaller test files with a documented testing guide, to survive Manifest V3 timeouts and context compaction.

## 🔗 Related Videos
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, MCP, Puppeteer
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Chrome, Claude Code, MCP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Chrome, Claude, Claude Code, MCP
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, MCP, Playwright

## Timeline
- `0:00` — Intro: Claude Code's new Chrome extension framed as a major upgrade over Playwright/Puppeteer MCP for testing.
- `1:31` — Problem 1: inefficient section-by-section screenshots; fix with a full-page screenshot script and slash command.
- `2:17` — Problem 2: MCP tools loading excessive HTML content; fix via CLAUDE.md context-management instructions.
- `2:50` — Problem 3: wasted tokens dismissing cookie pop-ups; fix with an auto-dismiss selector script.
- `3:41` — Security limitation: Claude can't complete CAPTCHAs or authentication on your behalf.
- `4:15` — Why the native Chrome integration beats Puppeteer/Playwright: retained sessions, access to signed-in services like Google Docs/Sheets.
- `4:46` — Known limitations: high context/compute cost, Chrome-only, multi-profile bugs.
- `5:17` — Manifest V3 long-run limitation causing mid-task session blocks; fix via split test files and per-file test reports.
- `6:43` — Structured testing workflow: guided slash command that tests, documents, and monitors context automatically.

## Transcript
<details>
<summary>Full transcript</summary>

The way our team builds our apps has been significantly improved. The reason? Claude code recently launched its Chrome extension. You might think this was already possible with the Playwright or Puppeteer MCP, but those tools had serious problems like an unnecessarily bloated context window, a messed up project folder filled with random screenshots, and most of the time they couldn't even complete the actions on the app. This is why I was never a huge advocate of automated testing using AI, but this is also why I was really excited about this new Claude extension. If you've been keeping up with the channel, you might know that we actually made a video on it some time ago. The funny thing is that it wasn't meant for Claude code, but we clearly said that this extension has way more potential if it was. And here we are. Now it's finally out as an integrated MCP, and it gives Claude code all the custom tools it needs. Now, right out of the box, it has some huge problems that we should fix, but before we dive into those, let's take a quick break to talk about Autometa.

Coming back to the problems, the biggest one I faced was that it took too many sequential steps to just test something really simple. You might have noticed that when you ask Claude to visually test a website's landing page, it performs a scroll operation for each section and captures a screenshot at every step. It then stitches all the screenshots together to analyze the UI section by section. You might think this is a good approach, but it's not. Instead of this, we can make it take full-page screenshot and save all those tokens. To solve this, I used a script that leverages different web tools to take the full shots. I also added instructions to use that script in a custom slash command in my project. Now, when I use that command to test the landing page, it recognizes that this is a full-page test based on the instructions I've included and uses the script directly instead of the usual section by section method. Because of this, the test happens significantly faster and it has the same accuracy.

The second problem I encountered was when these MCP tools tried to load a huge amount of content all at once for a simple task. Instead of loading specific divs, it often loads all the HTML within the main tag, which contains a huge amount of tokens even when it's not necessary. This ends up consuming a large chunk of the context window, and even your simplest tasks can bloat it significantly. To solve this, I added instructions in the cloud.md file on how to properly manage context when using the Claude Chrome extension. This way, any extraction is precisely limited and it doesn't bloat the context with unnecessary information.

Another problem is that Claude wastes a lot of time when it encounters websites that contain unwanted pop-ups such as cookie notices and similar prompts. To get rid of them, it uses the same screenshot and scroll sequences, but this is wrong. Instead of letting Claude consume unnecessary tokens and time, we can use other workarounds to handle these pop-ups. As an alternative, I created a script that includes the most common accept button selectors and patterns for dismissing cookie banners. It finds those selectors in the code and executes functions to dismiss the pop-ups automatically. I also added instructions in the cloud.md file so it runs this script first before proceeding with the main content. Now, whenever I ask Claude to go to a website, it first follows the instructions in cloud.md and executes this JavaScript. This automatically dismisses the cookie banners, allowing Claude to continue with the main content without wasting any tokens or performing unnecessary steps.

For security reasons, Claude has been limited from performing captures or completing authentication on your behalf. So, if you come across a website that contains them, Claude can't complete this process for you. This is something you have to handle on your own. Whenever you work on a website that requires login or capture verification, make sure you've already authenticated before giving Claude the task. This way, it won't get blocked and waste any time.

So, these were the main problems I could solve. But to properly use it for testing, you actually need a proper workflow to test out any application. But before we get to that, I want to talk a little more about why I prefer the Claude Chrome integration over Puppeteer. This is mainly because it's a native tool built by the developers of Claude code themselves, and it offers much better integration with improved control and features. These MCPs are focused on testing in a dedicated separate environment that maintains no sessions. They're often troublesome to install and clutter your project folder with all the screenshots. On the other hand, with this new Chrome integration, Claude has the ability to interact with your signed-in accounts. It can interact with services like Google Docs and Google Sheets. It can even retain all session information and use it to perform tasks even better.

Before we get to the workflow, I want to mention that browser integrations do use a lot of context because they're just more compute-intensive than regular tool calls. They've even mentioned it in one of their blogs. So, you do need to keep an eye on the auto compaction while working with Claude code. Also, since this is the Chrome integration, it only works with Chrome. I expected it would work with any Chromium browser, but it doesn't, and we can't really solve that. And for those of us that use multiple Chrome profiles, it'll be a little more frustrating because it continuously opens up the wrong profiles. And I do hope they solve this bug pretty soon.

With all the fixes I mentioned earlier and the integration of Claude with Chrome, my development workflow has improved significantly. However, Chrome extensions have a limitation in manifest V3. They can be blocked if they run for too long. Many people are asking the developers of Claude code to fix this on their repo as well. If you're doing end-to-end testing of your web application from start to finish, this can cause the session to be blocked by Chrome, and Claude will stop unexpectedly. You'd then have to re-prompt it to restart execution. This can be particularly troublesome if you assign a long-running task to Claude and step away from your computer only to return and find the task only partially completed.

For this exact reason, instead of end-to-end testing, I created multiple test files covering all different aspects of the application, detailed information on priority levels, preconditions, testing steps, and expected results. There's also a testing guide on how to conduct these tests along with a readme for the test documentation. As you know, Claude has a limited context window, and when that limit is reached, instructions and progress can be lost. For this reason, I added instructions in the cloud.md file that tell Claude to create a comprehensive test report document after testing each file. This way, even if you have to compact because the browser tools consume a lot of context, Claude can retain awareness of what's been tested and what still needs testing by referring to these progress files.

Now, before progressing with any test, the best practice is to run a compact because testing your application using Chrome is going to consume a lot of your context window. To streamline my testing process, I created another custom slash command. What this command does is test in a guided manner and create documentation in a proper structure after testing following the cloud.md instructions. I also added instructions to monitor the context before starting any task so that when testing begins, it doesn't lose context midway and compact while it's working. This way, when you start the testing process, you just use the slash command and provide the file you want to begin testing with, and Claude starts testing by following the exact instructions. It identifies issues on its own and uses the browser and all the necessary tools for testing. It interacts with elements automatically and is able to find errors that are not usually visible, but can be detected by reading the console output. It also documents the testing at the end as instructed. In this way, the entire testing process is significantly improved because Claude has access to console logs and can perform automated testing in the browser more effectively than ever before.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the Super Thanks button below. As always, thank you for watching, and I'll see you in the next one.

</details>
