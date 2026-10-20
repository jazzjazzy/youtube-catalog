---
title: "This Browser Agent Can Do Anything (or They Buy You A Mac Mini)"
video_id: YDqqRqqlnJU
channel: "[[channels/Eric Michaud]]"
uploaded: 2026-04-21
processed: 2026-07-05
duration: "6:32"
url: https://www.youtube.com/watch?v=YDqqRqqlnJU
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [browser-automation, web-scraping]
tools: [Browser Harness, Chrome, Excalidraw, Python]
llms: [Claude]
protocols: [CDP]
transcript: true
tags: [youtube, ai-automation]
---

# This Browser Agent Can Do Anything (or They Buy You A Mac Mini)

![thumbnail](https://i.ytimg.com/vi_webp/YDqqRqqlnJU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=YDqqRqqlnJU) | 📅 Uploaded [[uploaded/2026-04-21]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Browser Harness is a new open-source repo from the Browser-Use team that gives an LLM direct, full control of Chrome via CDP — so confident it can handle any task that the founders offered a free Mac Mini to anyone who finds a task it fails on. The video walks through what makes it different (a self-annealing `helpers.py` file the agent extends itself, plus a library of pre-built domain skills), sets it up locally, and uses it to automate clicking through a lead-gen directory to reveal and collect emails/phone numbers.

**Watch this if:** you want a browser agent that controls Chrome directly instead of going through a scraping framework, and want to see a real lead-generation automation built with it.

## Key Takeaways
- Browser Harness plugs directly into Chrome via the Chrome DevTools Protocol (CDP), locally or in the cloud, giving the LLM effectively a mouse and keyboard rather than a scripted API layer.
- Its standout feature is `helpers.py`, a self-annealing capabilities file: when the agent needs a capability it doesn't have yet (like uploading a file), it writes the missing code into `helpers.py` itself, so the harness permanently gains that skill for future runs.
- It ships with a library of pre-built domain skill files (TikTok, Facebook, eBay, Etsy, Craigslist, Steam, Zillow, and more) plus a documented set of interaction primitives (tabs, uploads, downloads, drag-and-drop, iframes).
- Setup is a simple clone-and-run-setup-prompt flow; Chrome opens locally with remote debugging enabled, or you can use the free cloud option (3 concurrent remote browsers, no card required).
- The demo automates a real lead-gen workflow: clicking "reveal phone/email" buttons behind a directory site's UI, first proven out by the AI itself, then converted into a deterministic Python script that runs unattended and only wakes the AI (or pings the human via SMS/Telegram) when something breaks.
- This turns the AI into "a manager rather than a micro-manager" — a Python script does the repetitive clicking and CSV export, and the AI is only invoked for exceptions.
- Browser Harness's own promotional examples (seen on the founder's Twitter) include generating and scheduling TikTok videos and an agent drawing a heart in Excalidraw, illustrating how general the mouse/keyboard-level control is.

## 🛠 Tools & Software
- [[topics/Browser Harness]] — the open-source repo under review: gives an LLM direct CDP-level control of Chrome, with a self-extending `helpers.py` and pre-built site skill files
- [[topics/Chrome]] — the browser Browser Harness controls directly via remote debugging, run locally for the demo
- [[topics/Excalidraw]] — shown in a founder's example screenshot as a browser agent drawing a heart, illustrating mouse/keyboard-level control
- [[topics/Python]] — used to turn the proven-out AI workflow into a deterministic script that runs the lead-gen automation unattended

## 🤖 LLMs Mentioned
- [[topics/Claude]] — shown in a founder's example controlling the browser to draw in Excalidraw, demonstrating general-purpose mouse/keyboard control

## 📡 Protocols & Standards
- [[topics/CDP]] — Browser Harness is built directly on the Chrome DevTools Protocol, which is how it gets full control of the browser instead of going through a higher-level automation library

## ✅ Action Items
- Clone Browser Harness and run its setup prompt locally to see the self-annealing `helpers.py` behavior firsthand.
- Start with a real repetitive browser task (like lead-gen directory scraping) to prove out an AI workflow, then convert it into a deterministic script for unattended runs.
- Check the pre-built skill files (TikTok, Zillow, Facebook, etc.) before writing new interaction code from scratch.

## 🔗 Related Videos
- [[videos/Lightpanda The 64MB Browser That is 60x FASTER than Chrome]] — shared: CDP, Chrome, Claude
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Chrome, Claude
- [[videos/Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing]] — shared: Claude, Python
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude
- [[videos/CloakBrowser made Claude agents undetectable (15k stars on GitHub)]] — shared: CDP, Claude
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Chrome, Claude
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude, Excalidraw

## Timeline
- `0:00` — Intro: Browser Harness and the "find a broken task, get a Mac Mini" challenge
- `0:23` — What Browser Harness is: direct Chrome CDP control
- `0:54` — Founder's Twitter examples: TikTok scheduling, self-modifying harness, Excalidraw drawing
- `1:39` — Local setup: clone, run setup prompt, allow remote debugging
- `2:12` — helpers.py and the self-annealing capability model explained
- `2:48` — Pre-built domain skills: TikTok, Zillow, Facebook, and more
- `3:22` — Applying it to local web scraping and anti-bot-prone lead directories
- `4:12` — Building the AI manager: proving the workflow, then scripting it deterministically in Python
- `5:43` — Wider possibilities: social media automation, free local tools, and a nod to the Hermes agent

## Transcript
<details>
<summary>Full transcript</summary>

In this video, we're going to talk about Browser Harness, a new repo put out by the folks at Browser-Use, and why it's easily the best browser agent I've ever used. I've been playing with it a little bit this afternoon and I'm already convinced. We're going to talk about some practical use cases, some cool stuff it can do, and how to get started. The very first thing that got me was a post by Browser-Use saying "first person to find a task that doesn't work gets a fresh Mac Mini." The second post was about the repo they just put out called Browser Harness — the idea is to give full browser control to an LLM, built directly on the CDP, plugging directly into your Chrome browser either locally or on the cloud.

Looking through the founder's Twitter, there's a screenshot of his Browser Harness agent generating a video, uploading and scheduling it on the TikTok studio, then analyzing the best hooks based on views. He says it modifies its own harness, so no task is impossible, and it shares domain-specific skills between agents. Then there's a screenshot of Claude drawing in Excalidraw — literally drawing a heart. That's the browser agent. It really seems like they've given the LLM a mouse and keyboard.

It's a public repo, so you can clone it, and it's as easy as running the setup prompt. When Chrome opens in your environment, you allow remote debugging and it runs locally, no problem. It also runs on the cloud for remote browsers — they offer free remote browser use, three concurrent browsers, no card, where you set up an API key, but let's focus on local for now. The unique thing about this isn't just the browser agent approach but this helpers.py file — it's self-annealing, the agent can update it on its own. For example, if the agent wants to upload a file and helpers.py doesn't have the capability, the agent writes the line of code needed into the helpers file, and now it's able to do that task forever because it's baked into the harness.

They've also got a bunch of these already built out — an MD file for TikTok, one for Facebook, Etsy, eBay, Craigslist, Steam, Zillow for real estate listings. Quite a lot of domain skills already mapped out. The interaction skills list explains exactly how the LLM interacts with Chrome — tabs, uploads, downloads, drag and drop, iframes, everything.

The number one thing I use browser agents for is web scraping — getting information from a directory, finding leads. We always run into anti-bot stuff or obfuscation, emails hidden behind separate button clicks, and it's hard to wire that into something like a Playwright agent. So I gave Browser Harness a shot on a directory where you click "reveal phone" or "reveal email" to collect publicly available information — totally safe, not black hat, but normally you have to be at the desk clicking those buttons. I wanted to automate that.

What was exciting: we had the AI running that to begin with, and since we had the SOP proven out by the AI first, we were then able to write a deterministic Python script to do it automatically. The AI isn't babysitting anything, but it's still woken up if there are any errors. That's the crazy use case here — I've turned the AI into more of a manager rather than a micro-manager doing all the different tasks. The Python script runs in the background getting the emails, and if there's any lag or blank page, the AI addresses the issue and continues, or escalates to me via SMS or Telegram so I can fix the problem. The script goes through each page clicking the reveal-email button and outputs into CSV format. Because it's publicly available information you could collect yourself, it's ethical — no strain on servers, no nefarious methods.

I see a lot of practical use cases beyond lead generation — social media platforms that are hard to connect to, like Instagram, Facebook, LinkedIn, could get automations completed from the browser side. This runs for free locally with your Claude Code instance or whatever you're using. I want to check out how people are using this with things like the Hermes agent moving forward, but that's a different video.

</details>
