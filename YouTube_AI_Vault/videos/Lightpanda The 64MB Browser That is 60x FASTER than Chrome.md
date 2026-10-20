---
title: "Lightpanda: The 64MB Browser That is 60x FASTER than Chrome"
video_id: yFWYK3wN88w
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-28
processed: 2026-07-05
duration: "5:35"
url: https://www.youtube.com/watch?v=yFWYK3wN88w
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [web-scraping, browser-automation]
tools: [Lightpanda, Chrome, Puppeteer, Claude Agent SDK]
llms: [Claude]
protocols: [CDP]
transcript: true
tags: [youtube, ai-automation]
---

# Lightpanda: The 64MB Browser That is 60x FASTER than Chrome

![thumbnail](https://i.ytimg.com/vi_webp/yFWYK3wN88w/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=yFWYK3wN88w) | 📅 Uploaded [[uploaded/2026-04-28]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Lightpanda is a headless browser built from scratch in Zig (no WebKit, no Chromium) that exposes the Chrome DevTools Protocol so Puppeteer and Playwright can drive it as a drop-in replacement for headless Chrome. The video builds a Claude-SDK agent with a custom web-fetch tool, benchmarks Lightpanda against headless Chrome for both raw scraping and agent-driven fetches, and shows where Lightpanda wins big and where it completely fails.

**Watch this if:** you're running headless browsers inside an AI agent's tool loop and want to know whether swapping Chrome for something faster and lighter is actually safe.

## Key Takeaways
- Lightpanda is written from the ground up in Zig with no WebKit or Chromium underneath, making it dramatically smaller and faster than headless Chrome, but it renders no pixels and doesn't support service workers, IndexedDB, or CORS.
- It exposes the Chrome DevTools Protocol, so existing Puppeteer or Playwright code can point at a Lightpanda server instead of Chrome with no rewrite.
- On a single-page Wikipedia scrape the gap was small (344ms vs 392ms), but scraping 100 pages took Lightpanda 18 seconds versus 30-60 seconds for Chrome — the advantage compounds with scale.
- Inside an actual Claude-SDK agent with a custom web-fetch tool, Lightpanda's browser memory footprint was 66MB versus Chrome's 829MB (roughly 12x smaller) with faster per-fetch times and the same overall wall time.
- Lightpanda fails on single-page applications: fetching Airbnb listings worked fine in Chrome but returned nothing in Lightpanda, because its V8 engine only handles language-level JavaScript execution (async/await, closures, promises), not full SPA rendering.
- Verdict: for straightforward content fetching and scraping inside an agent's tool loop, Lightpanda is the better default; for JS-heavy single-page apps, headless Chrome is still necessary.
- Lightpanda also ships its own MCP server and a hosted cloud service, though the video deliberately runs everything locally to keep the comparison fair.

## 🛠 Tools & Software
- [[topics/Lightpanda]] — the headless browser under test: built in Zig, benchmarked against Chrome for both raw scraping speed and memory use inside an agent
- [[topics/Chrome]] — used as the headless baseline browser, run via the Chrome DevTools Protocol for the same benchmark scripts and agent tool calls
- [[topics/Puppeteer]] — connects to both the Lightpanda server and headless Chrome over CDP to drive the fetch scripts and benchmarks
- [[topics/Claude Agent SDK]] — used to build the demo agent with a custom web-fetch tool that calls out to Lightpanda or Chrome depending on the test

## 🤖 LLMs Mentioned
- [[topics/Claude]] — powers the demo agent that answers questions (e.g. summarizing JS array methods) using content fetched by the web-fetch tool

## 📡 Protocols & Standards
- [[topics/CDP]] — the Chrome DevTools Protocol that Lightpanda exposes, letting Puppeteer/Playwright connect to it exactly as they would to headless Chrome

## ✅ Action Items
- Swap headless Chrome for Lightpanda in scraping-heavy agent tool loops and measure the memory/speed difference for your own workload.
- Keep a Chrome fallback path for any target site that's a JS-heavy single-page application, since Lightpanda can't render those.
- If exploring further, check Lightpanda's own MCP server and hosted cloud option instead of self-hosting.

## 🔗 Related Videos
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude, Puppeteer
- [[videos/This Browser Agent Can Do Anything (or They Buy You A Mac Mini)]] — shared: CDP, Chrome, Claude
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Chrome, Claude
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Puppeteer
- [[videos/Anthropic Released A New Way To Vibe Code]] — shared: Claude, Puppeteer
- [[videos/CloakBrowser made Claude agents undetectable (15k stars on GitHub)]] — shared: CDP, Claude
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Chrome, Claude

## Timeline
- `0:00` — Intro: Lightpanda is a Zig-built headless browser, 9x faster and 16x less memory than Chrome
- `0:31` — Origin story: released 2024, pivoted from scraping tool to AI-agent focus
- `1:00` — Plan: build a Claude SDK agent with a custom web-fetch tool to compare Lightpanda vs Chrome
- `1:22` — Basic example: scraping one Wikipedia page's reference links
- `1:53` — Single-page result: Lightpanda 344ms vs Chrome 392ms
- `2:03` — Scaling to 100 pages: Lightpanda 18s vs Chrome 30-60s
- `2:32` — Building the actual agent with a web-fetch tool and metrics tracking
- `3:47` — Side-by-side agent results: fetch time and memory (66MB vs 829MB)
- `4:28` — Where Chrome wins: Airbnb SPA fetch fails on Lightpanda
- `5:07` — Verdict and pointer to a Chrome MCP remote-debugging video

## Transcript
<details>
<summary>Full transcript</summary>

This is Light Panda, a headless browser designed for AI agents written from the ground up in Zig, so no WebKit or Chromium, which makes it up to nine times faster and uses 16 times less memory than headless Chrome. It even exposes the Chrome developer protocol, so it can be used with Puppeteer or Playwright, but it doesn't render any pixels or support common web APIs like service workers, IndexedDB, and CORS. So why is it even used in Open Claw and Vercel's agent browser? Light Panda was released around 2024 by Pierre, Francis, and Kate, long before Claude's code was even a thing and around the time ChatGPT started to get popular. It started out as a web scraping and automation tool, but soon after agents blew up in popularity, they pivoted to AI agents and managed to get a round of funding out of it. But was this just a quick rebrand because of the popularity of AI or is it actually good for agents? We're going to test this out by building our own agent using the Claude SDK with a custom web fetch tool, using Chrome and Light Panda as the web browsing engines and comparing the differences to see which one is better and why. Although Light Panda does have an MCP server and has its own cloud service, we'll try and do things as locally as possible, and we'll go through a basic example before expanding into making the web fetch tool.

Here is a script that essentially fetches a bunch of links from Wikipedia. It will first create a Light Panda server, then connect to that server using Puppeteer, go to Wikipedia, go through all the links in the references section, and print them out. Light Panda found all the links in 344 milliseconds. Trying the same thing with Chrome takes 392 milliseconds — not that much of a difference. But things change dramatically with multiple pages. A similar script instead gets links from 100 pages fetching from the web browser to HTTPS, JavaScript, Python, and more. With Light Panda, the whole thing is done in 18 seconds; with Chrome, it takes about 30 and in some cases 60 seconds.

Now let's see how the performance differs running through an agent. Here's a very basic agent using the Claude SDK with a web fetch tool that runs a prompt summarizing the difference between array, map, filter, and reduce in JavaScript by going to specific MDN links. Below is the agentic loop, and the web fetch function runs whenever there's a tool call. Below that, some metrics and a function to calculate browser memory. This project uses Light Panda and Chrome via the Chrome DevTools protocol, running each on a port that Puppeteer connects to before running the agent. Starting the server with Light Panda serve and running the agent fetches the three MDN URLs, gives the information to Claude, and returns the difference between map, filter, and reduce plus the metrics. Running the same thing with Chrome, after clearing its default caching so the comparison is fair, also fetches the URLs and gives an answer from Claude — but here's where things are drastically different.

Putting the results side by side: both do three fetches, but the fetch time for Light Panda was almost twice as fast as Chrome. Wall time is the same, but the browser memory for Light Panda is only 66 megabytes versus Chrome's 829 — more than 10 times smaller. Agent memory is a bit smaller for Light Panda too, though the browser engine wouldn't change that value much. Honestly, you should never use Chrome for headless browsing again — Light Panda is up to 21 times smaller than Chrome, faster, and uses way less memory.

But there is one scenario where you'd want Chrome instead: changing the prompt to fetch five properties from Airbnb in Tokyo works fine with Chrome but Light Panda can't get the listings, because Airbnb is a single-page application. Light Panda does have a V8 engine to execute JavaScript, but that's just for language-level execution — async/await, closures, promises — not for rendering something as complex as a full SPA. So apart from not being able to render SPAs correctly, which might change in the future, Light Panda is a great tool to add to a custom agent that needs to do web search or web fetching. And while on the topic of web browsing with an agent, if you've ever wanted Claude Code to control your actual running Chrome session safely, with your logged-in details and everything, check out the video on remote debugging using the Chrome MCP server.

</details>
