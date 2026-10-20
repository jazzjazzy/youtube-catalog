---
title: "Master Local AI in 29 minutes (LM studio + AnythingLLM)"
video_id: unPhOGyduWo
channel: "[[channels/Keith AI]]"
uploaded: 2025-11-18
processed: 2026-07-05
duration: "29:11"
url: https://www.youtube.com/watch?v=unPhOGyduWo
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [local-ai-assistant-setup]
tools: [LM Studio, AnythingLLM, DuckDuckGo, Google Custom Search API]
llms: [Qwen, DeepSeek, Kimi, Grok, GPT-5, ChatGPT, Claude, Gemini]
protocols: [RAG, MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Master Local AI in 29 minutes (LM studio + AnythingLLM)

![thumbnail](https://i.ytimg.com/vi_webp/unPhOGyduWo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=unPhOGyduWo) | 📅 Uploaded [[uploaded/2025-11-18]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A beginner-friendly, end-to-end walkthrough of running AI entirely on your own computer using LM Studio (model hosting, vision, web search, presets) paired with AnythingLLM (RAG, agent skills, drag-and-drop agent flows). Demos include extracting numbers from a receipt photo, scheduling a Google Calendar event, scraping Reddit/LinkedIn/Hacker News/X for content ideas, and networking a gaming PC's LM Studio server to a less powerful Mac.

**Watch this if:** you want a completely free, private, offline-capable AI setup that can still search the web, read images, and run autonomous agents.

## Key Takeaways
- Local AI keeps data on your own machine, works where public AIs are blocked, costs nothing beyond electricity, and (per artificialanalysis.ai benchmarks) now covers roughly 80% of what public models can do.
- In LM Studio, model size (parameter count and download size) determines how complex a task the model can handle and whether it fits your RAM/disk — smaller models like Qwen 4B are a safe starting point.
- Model cards flag vision (image understanding), tool use (agentic actions), and reasoning (visible thinking) capabilities — pick based on what the task needs.
- LM Studio can extract structured data straight from a photo (a receipt) using a vision-capable Qwen model, and can browse the live web via a DuckDuckGo integration to get past its training cutoff.
- AnythingLLM adds what LM Studio alone can't: RAG over your own documents/scraped pages, plus AI agents that use built-in and community skills (web search, calendar events, scraping) or fully custom drag-and-drop agent flows.
- AnythingLLM's agent flows can log into gated sites like LinkedIn or X via its browser tool, then scrape and summarize content (e.g., an "AI news" flow or a Hacker News headline extractor).
- LM Studio's server mode lets a more powerful machine (e.g., a gaming PC running Qwen 30B) host models that a weaker machine (a Mac limited to Qwen 4B) can call over the same Wi-Fi network via AnythingLLM.
- Swapping LM Studio's built-in DuckDuckGo search for Google's Custom Search API (100 free queries/day) gives noticeably better web-search results for agents.

## 🛠 Tools & Software
- [[topics/LM Studio]] — used to download/run local LLMs, tune chat settings, extract data from a receipt image, enable web search, and host a server other machines can call.
- [[topics/AnythingLLM]] — used to add RAG (scraping and embedding web pages), AI agent skills (calendar events), and custom drag-and-drop agent flows (scraping Hacker News/X/LinkedIn).
- [[topics/DuckDuckGo]] — enabled as LM Studio's built-in web-search integration so the local model can answer questions past its training cutoff.
- [[topics/Google Custom Search API]] — configured as a higher-quality alternative to DuckDuckGo for AnythingLLM's web search, using a free 100-query/day API key.

## 🤖 LLMs Mentioned
- [[topics/Qwen]] — the primary model demoed throughout (4B on a Mac, 30B on a gaming PC), used for chat, vision (receipt OCR), and agent tool use.
- [[topics/DeepSeek]] — cited via benchmarks as the strongest open-source model for coding tasks.
- [[topics/Kimi]] — cited via benchmarks as the top open-source model for general intelligence, tied with GPT-5 on agentic tasks, though too large (32GB) to run on the presenter's machine.
- [[topics/Grok]] — cited via benchmarks as the best-performing model for coding and as beaten by Kimi on general intelligence.
- [[topics/GPT-5]] — cited via benchmarks as tied with Kimi for the top agentic-AI model.
- [[topics/ChatGPT]] — referenced as a public/cloud AI example when contrasting local vs. public AI.
- [[topics/Claude]] — referenced as a public/cloud AI example when contrasting local vs. public AI.
- [[topics/Gemini]] — referenced as a public/cloud AI example when contrasting local vs. public AI.

## 📡 Protocols & Standards
- [[topics/RAG]] — explicitly explained and demoed: scraping a webpage (Arsenal's results page) into AnythingLLM's workspace so the model can answer questions using it.
- [[topics/MCP]] — mentioned as part of LM Studio's plugin/integration ecosystem (DuckDuckGo and other MCP-style integrations you can install).

## ✅ Action Items
- Install LM Studio, download a small vision+tool-use model (e.g., Qwen 4B), and try extracting data from a receipt photo.
- Enable the DuckDuckGo integration in LM Studio so your local model can answer questions about current events.
- Install AnythingLLM, point it at LM Studio's server, and try the built-in Calendar Event agent skill.
- Build a simple agent flow in AnythingLLM (e.g., scrape a news site and summarize the top links) and save frequent prompts as presets.
- If you have a spare powerful machine, run LM Studio's server on it and connect to it from a weaker laptop via AnythingLLM over your local network.

## 🔗 Related Videos
- [[videos/Someone open-sourced a hedge fund (53k stars on GitHub)]] — shared: Claude, DeepSeek, Gemini, Grok
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: ChatGPT, Claude, Gemini, Grok
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Gemini, MCP, Qwen
- [[videos/The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing]] — shared: ChatGPT, Claude, GPT-5, Gemini
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, GPT-5, Gemini
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, MCP
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Claude, Gemini
- [[videos/Google's New Universal Commerce Protocol]] — shared: ChatGPT, Gemini, MCP

## Timeline
- `0:00` — Introduction: what the video covers (scraping, calendar scheduling, receipt OCR, web search) using free local AI tools.
- `0:16` — Why use local AI: privacy, access in restricted countries, zero cost, and a closing capability gap with public models.
- `1:17` — Setting up LM Studio: download, first model pick, and an overview of what LM Studio and AnythingLLM each bring to the setup.
- `3:28` — Downloading and choosing LLM models: parameter counts, download size vs. RAM, vision/tool-use/reasoning tags, and artificialanalysis.ai benchmark rankings.
- `8:37` — Using LM Studio features: extracting numbers from a receipt photo, enabling DuckDuckGo web search, and saving reusable prompts as presets.
- `12:34` — Integrating AnythingLLM as a client to LM Studio's server, then a first RAG demo scraping a webpage into a workspace.
- `17:54` — Advanced AnythingLLM features: agent skills (Calendar Event), custom skills vs. drag-and-drop agent flows, and scraping Hacker News/X/LinkedIn (with browser login for gated sites).
- `26:43` — Connecting LM Studio (running on a gaming PC) with AnythingLLM (running on a Mac) across the local network, plus swapping in Google's Custom Search API.
- `28:57` — Conclusion and recap of what local AI can now do.

## Transcript
<details>
<summary>Full transcript</summary>

So, in this video, I'm going to show you how you can scrape websites to give you ideas for content, set up a calendar event for meetings, extract numbers from photos of receipts, and search the internet, and summarize key findings using local AI tools, all for free. So, let's get started. I'm going to give you the ultimate breakdown on how to use local AI. There are four reasons why you should consider using a local AI. I've taught over 400 people how to use AI. And the most common question I get is that the company doesn't allow them to use public AI because of privacy reasons. As we all know, anything you can send to the AI is not private. So, if you don't want your data to be sent to an external company, you can use local AI and it runs only on your computer. The second is that there's a lot of countries where you can't even access some of the public AIs and running locally is a good alternative. Number three, its cost. Running a local AI is essentially free except for electricity costs. So if you want to save some money, you should definitely consider using a local AI. And number four, 6 months ago, there was a huge gap between open-source local AI models and what's available with public AIs. But in the latest benchmarks, that gap is closing. And I really think you can achieve 80% of what you can do with public AIs using a local model.

So let's get into it. We're going to use two AI tools. Number one, LM Studio. And I'm going to teach you how to set it up, install an LLM, tune your model settings, your chat settings, teach you how to use plugins and MCP, and then finally setting up a server so other computers can also access it. And then I'm going to teach you AnythingLLM, which gives it additional power. In particular, it gives you the power of using AI agents to automate a lot of tasks that you do all the time. So, I'm going to teach you how to set it up, how to use AI agents, how to build custom skills and slash commands, and they work on top of another. Ultimately, you can do something really cool where I have a gaming laptop that has high performing hardware, and then I can access that through my Wi-Fi network from my Mac. So, I can run my LLM model using my gaming machine and then use it on my Mac. And I'll show you how you can do that as well.

Before we start, I have to clarify what is a public AI and a local AI. With a public AI such as ChatGPT, Claude, Gemini, you're sending your data through the internet to be processed and then sent the data back to you. With a local AI, you basically use your computer's CPU and GPU hardware and you process your request on your local computer without it ever leaving your computer.

Okay. The first thing you need to do is go to lmstudio.ai and download LM Studio. Once you've downloaded LM Studio, the first thing you need to do is to download a large language model. Come to the left, click on discover, and you'll see a bunch of LLM models here. The good thing is that they have a best match and they have what's called a staff pick. Some basics about large language models: you'll see a whole bunch of different models — 4B, 8B, 20B — and the larger the number means more parameters, meaning it can deal with more complicated tasks. You have to check the LLM's parameters and its download size, plus how much RAM you have, to know if you can run it. The second thing that I love about LM Studio is that it's got capabilities highlighted: vision (image processing), tool use (agentic actions), and reasoning (visible thinking). If you're really hardcore, you can go to artificial analysis, an independent site that evaluates all the LLMs out there. Right now, in terms of open-source models, Kimi is performing the best, even beating out Grok 4 and Claude on general intelligence. For coding, Grok 4 is the best. And for agentic AI, GPT-5 is number one, tied with Kimi. But Kimi's model size is 32 gigabytes and likely too large to run on my computer.

Now that you have your basic local AI running, I'm going to show you three features: processing images, connecting to integrations, and using presets. First example: extracting numbers from a receipt. Download an LLM with vision capability, start a new chat, attach the receipt image, and ask it to extract numbers. It reads through all the numbers on the receipt and gives me the total, each dish ordered, and the date and time.

Now, the power of integrations. Let's ask who's the mayor of New York — it answers based on its 2024 training cutoff, missing the actual new mayor. So let me turn on DuckDuckGo, a search engine, and ask again — now it does a web search and correctly finds the new mayor. To add DuckDuckGo, search for "duckduckgo LM Studio," click "run in LM Studio," and it installs. There's a ton of other MCPs and integrations you can add, but DuckDuckGo is one of the more useful ones.

The final LM Studio feature: presets. If you have prompts you use all the time, save them as a preset so you don't have to retype them — a great way to build a prompt library.

Now, AnythingLLM. LM Studio alone can't let models interact with outside tools beyond simple search — for Google, Reddit, LinkedIn, and more, you need AI agents, which is what AnythingLLM provides. To set it up, first turn on LM Studio's server in developer settings, then download AnythingLLM and point its LLM settings at LM Studio so it uses the same downloaded models as a client calling that server.

Another cool AnythingLLM feature: uploading your own documents to create a custom RAG — Retrieval Augmented Generation, meaning you give the AI more context it wouldn't otherwise have. Demo: asking about Arsenal's recent football scores, the model has no real-time access. So I scrape Arsenal's results page into AnythingLLM (fetch website, move to workspace, save and embed), and now asking the same question returns the correct recent scores. That's how you build your own RAG — useful for meeting notes, emails, and communication history.

Now the most useful AnythingLLM feature: agents. Go to settings, agent skills, and you'll see built-in skills like web search, generate charts, save files, scrape websites, view/summarize documents, and RAG long-term memory. You can also add custom skills and agent flows via the community hub — chat with Slack, calendar events, an SEO advisor, MidJourney prompts, and agent flows like a Hacker News flow. Demo: import the Calendar Event skill, turn it on, then in a new thread use "@agent" and ask it to create a calendar event for a basketball game at 9pm — the agent generates calendar links for Google/Outlook, ready to save.

Custom skills require programming; agent flows are a no-code, drag-and-drop alternative for building your own automations — API calls, web scraping, reading/writing files, and chaining steps together with LLM processing in between. Demo: a Hacker News headline flow that extracts links on topics you care about, and an AI news flow that scrapes X.com for viral AI content and reports back a summary (e.g., "Google launches deep research notebook"). Before scraping login-gated sites like Twitter/X or LinkedIn, use the browser tool's "open browser" to log in first, after which AnythingLLM can access that data. This is very similar to n8n and make.com, but 100% local — nothing leaves your own computer.

If agent flows feel like too much work, use presets in AnythingLLM the same way as in LM Studio — e.g., a saved LinkedIn post prompt that checks your feed for relevant AI material.

One more tip: LM Studio only offers DuckDuckGo for web search, but its results aren't always great. In AnythingLLM's web search settings you can instead choose Google, which gives 100 free queries per day — just grab a search engine ID and API key from Google and paste them in for much better results.

Finally, the bonus: running LM Studio on a more powerful gaming Windows PC (with the larger Qwen 30B model) as a server, and calling it from a less powerful Mac (limited to Qwen 4B) via AnythingLLM's LLM settings using the Windows machine's local IP address plus "/v1". As long as both machines are on the same Wi-Fi network, this works — great for an office where IT can host one powerful server that colleagues' weaker machines all call into.

</details>
