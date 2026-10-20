---
title: "How Hermes Agent Can Save You 85% (Or More) in BG Task Token Cost"
video_id: NoF-YajElIM
channel: "[[channels/Tonbi's AI Garage]]"
uploaded: 2026-04-17
processed: 2026-07-05
duration: "18:04"
url: https://www.youtube.com/watch?v=NoF-YajElIM
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [agent-cost-optimization, llm-config-tuning]
tools: [Hermes, OpenRouter, WSL2]
llms: [Claude Opus, Kimi, Gemini, Claude Haiku, GPT-4o Mini, GPT-4o, GLM]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# How Hermes Agent Can Save You 85% (Or More) in BG Task Token Cost

![thumbnail](https://i.ytimg.com/vi/NoF-YajElIM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=NoF-YajElIM) | 📅 Uploaded [[uploaded/2026-04-17]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Hermes agent runs eight hidden "auxiliary" background tasks (compression, flush memories, web extract, vision, session search, skills hub, MCP, approval) that by default inherit your expensive main model or auto-fall-back to Gemini Flash. The video shows where these live in `config.yaml` and runs a live compression cost test — Claude Opus 4.6 at 13 cents vs. Kimi K2 at under 2 cents for the same 50K-token pass — an 85% savings that compounds to tens of dollars a month.

**Watch this if:** you run Hermes agent with a frontier model and have never touched the auxiliary/background model config.

## Key Takeaways
- Hermes silently runs 8 auxiliary tasks alongside your main chat: compression, flush memories, web extract, vision, session search, skills hub, MCP, and approval.
- Compression is the biggest cost driver — it can fire 10-20 times a day for heavy users and is where most auxiliary spend hides.
- By default these tasks inherit your main (often frontier) model, or auto-chain through OpenRouter → Vertex → Codex → Gemini Flash if left unset.
- Each task can be pointed at a different provider/model independently in `config.yaml` under the `auxiliary` block, roughly line 100.
- Live test: compressing the same 50K-token context cost $0.13 with Claude Opus 4.6 vs. $0.019 with Kimi K2 via OpenRouter — an 85% savings per pass.
- At 15 compressions/day, using Opus the whole time can run ~$60/month; switching to Kimi K2 drops it to ~$9/month, and a local model drops it to $0.
- Local models (Ollama, LM Studio, vLLM, llama.cpp) can be wired in via a `base_url` override, which takes priority over the `provider` setting, to make auxiliary tasks free.
- Watch the compression gotcha: there's a top-level compression setting AND an `auxiliary.compression` setting — the auxiliary one wins if both are set, and setting it to `auto` overrides your top-level choice back to the Gemini fallback chain.

## 🛠 Tools & Software
- [[topics/Hermes]] — the coding agent whose 8 auxiliary background models and `config.yaml` are walked through and reconfigured in this video
- [[topics/OpenRouter]] — the provider used to run the Kimi K2 compression comparison and part of the default auto-fallback chain
- [[topics/WSL2]] — the Windows environment used to navigate the filesystem to Hermes's `config.yaml`

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — used as the baseline for the live compression cost test (Opus 4.6, $0.13 per 50K-token compression)
- [[topics/Kimi]] — Kimi K2 via OpenRouter is the cheaper alternative demoed for compression, costing $0.019 for the same pass (85% savings)
- [[topics/Gemini]] — Gemini Flash is the default auto-fallback model for auxiliary tasks and a recommended pick for compression/flush memories
- [[topics/Claude Haiku]] — recommended for compression and web extract tasks
- [[topics/GPT-4o Mini]] — recommended for the flush memories task (fast, structured extraction)
- [[topics/GPT-4o]] — recommended as a solid vision-capable model for the vision auxiliary task
- [[topics/GLM]] — mentioned as a vision model the creator tried recently and liked

## 📡 Protocols & Standards
- [[topics/MCP]] — one of the 8 auxiliary tasks (MCP) dispatches MCP tool calls and can be pointed at its own model

## ✅ Action Items
- Open your Hermes `config.yaml` and find the `auxiliary` block (~line 100) to see what's currently set for each of the 8 tasks.
- Point compression and web extract at a cheaper model (Kimi K2, Claude Haiku, Gemini Flash) instead of leaving it on your frontier model.
- If you can run a local model via Ollama/LM Studio/vLLM/llama.cpp, set the auxiliary `base_url` to it to make these background tasks free.
- Double-check whether both the top-level and `auxiliary.compression` settings are configured — the auxiliary one wins, and `auto` there overrides your top-level choice.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Haiku, Claude Opus, GPT-4o Mini, Gemini
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Haiku, Claude Opus, GLM, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Haiku, Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Haiku, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Haiku, Claude Opus, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Haiku, Claude Opus, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Haiku, Claude Opus, MCP
- [[videos/Hermes The Self-Improving Agent That Gets Smarter Every Day]] — shared: GLM, Hermes, OpenRouter

## Timeline
- `0:00` — Intro: Hermes agent has 8 hidden auxiliary models running in the background
- `1:00` — Why it matters: your main model isn't the only thing being billed
- `2:15` — The 8 auxiliary tasks explained; top 4 costliest (compression, web extract, vision, flush memories)
- `4:00` — Where the config lives: navigating to `.hermes/config.yaml` in WSL
- `5:30` — How to set provider/model per task in the config file
- `7:00` — Model recommendations per task (compression, flush memories, web extract, vision)
- `9:30` — Going local: pointing auxiliary tasks at Ollama/LM Studio/vLLM/llama.cpp via base_url
- `11:15` — The compression gotcha: top-level vs. auxiliary.compression config
- `13:00` — Live demo: compressing 50K tokens with Claude Opus 4.6 ($0.13)
- `14:45` — Live demo: same compression with Kimi K2 via OpenRouter ($0.019, 85% savings)
- `16:15` — Monthly cost math: $60/month on Opus vs. $9/month on Kimi K2 vs. $0 local
- `17:30` — Wrap-up and what's coming in the May Hermes deep-dive series

## Transcript
<details>
<summary>Full transcript</summary>

So, I've been doing kind of a deep dive into Hermes agent and the different functions it has and this is one thing that I thought was pretty interesting. And I don't know, I haven't heard a lot of people talking about it, but I want to do a video on it because I thought it was a pretty nice feature. So, Hermes agent eight hidden models and you've been running them the whole time. And this is about auxiliary models. Most people ever mess with them, but it could save you a lot of money and could improve your Hermes agent performance if you take a look at it. So, today I'm going to show you what they are, which ones matter and the one config that can cut your auxiliary cost by 90%. So, if you use your Hermes agent a lot for heavy-duty software engineering coding tasks, you're probably using a frontier model Opus, Sonnet, GPT-5 something that can be quite expensive cuz you want quality, but Hermes just doesn't use your model for the chat itself and for the specific task you give it.

Hermes silently runs eight background tasks on top of your chat. Things like compressing your conversation when the context gets too big, summarizing web pages after it fetches them, analyzing images, and writing to persistent memory. On the default config, those tasks are either inherited by your main model, which can be quite expensive or it falls back to Gemini Flash through an auto detect chain. And this goes from open router to new portal and then into Codex. So, you if you have open router configured like I do, it'll automatically use Gemini Flash 3 for most of these tasks. But each task has different needs, so summarizing a page is different from analyzing an image. Compressing a long conversation is different from classifying whether a command is dangerous. So, you may want to use different models for these different tasks.

So, here are the eight tasks. The top four here are the ones that cost the most in terms of spend. Compression is for long summarizing your conversation when the context hits the threshold. Web extract is to summarize a web page after Hermes fetches it. Vision is analyzing image and browser screenshots and obviously certain models are better at that than others. Flush memories is a task that writes durable facts from your chat to your memory files when a session ends. Session search here summarizes past sessions when you search them. Skills hub matches your query to an installed skill, MCP dispatches MCP tool calls, and approval classifies risky commands if you're in smart approval mode. So, like I said, the top four here are the ones where you're going to spend the most, and this is all based on the current version of Hermes as of April 15th, 2026 — they've been updating it a lot, so double-check if you're watching this at a later date.

So, where the spend actually lives — number one by far is compression. It fires every time your context fills up to the threshold. So, for heavy users, if you're live coding or have complex automated workflows, this could fire 10 to 20 times a day and this is your biggest cost by far. Flush memories fires on every session end, so if you do /new or /end/exit this flush memories will work and it basically looks back at the context and summarizes and stores memories. It costs less than compression, but it still does add up. Web extract fires on every web page that the agent summarizes. So, if you use Hermes a lot for research, this is going to get hit constantly. And then vision fires on every image and browser screenshot that you send it. Lower frequency for some people, but it can be expensive per call because the images eat a lot of tokens, and certain models are specifically designed for vision tasks, so setting this is less about cost and more about having the right model for the task.

Okay, so where are these actually? These are in the config. I'm using this with WSL on Windows — it's going to be different on a Mac. On the bottom of your file explorer, you're going to see something called Linux, the WSL workspace. Then a folder, probably called Ubuntu (mine's Debian). Look under the home folder and your user ID, then .hermes/.hermes directory, and you'll see all of them here — this is the file you want, config.yaml. You're going to look down around line 100, depending, and see the line for auxiliary — this is where all of the auxiliary models are set: vision, web extract, compression, session search, skills hub, flush memories. You set the provider and the model — for instance, Gemini Flash, provider open router. Or say Haiku for web extract, provider Anthropic, model Claude Haiku 4.5. By default they're all set to auto right now, which walks through open router, vertex, Codex, Gemini Flash. I have open router configured and was wondering why I have all these tiny Gemini Flash charges even though I wasn't using Gemini Flash — it's because of this, they were set to auto for the auxiliary tasks.

So which model do you want to choose? This is up to you, but a few ideas: for compression, some good choices are models that have clean summaries and can handle long context — Kimi K2 is good, Claude Haiku 4.5, Gemini 2.5 Flash. For flush memories, you want something good at small, fast, structured extraction — GPT-4o Mini is quite good, and Gemini 2.5 Flash again, which is why it's kind of the default — well-balanced, fast, and comparatively cheap. Web extract — Claude Haiku 4.5 is great, and Gemini again; for this you really want factual preservation for research, so a slightly heavier model is fine. And vision — has to be a multimodal model. Gemini 2.5 Flash is good, but also GPT-4o. I used GLM 4.5 Turbo recently, which is really nice. Most frontier models do this well too, but you may want to pick a specific vision model that's cheaper than your frontier model.

One of the big benefits obviously is going local with these. If you can run a local model that's pretty good and can handle these tasks, you're taking a background task that costs money and making it cost nothing. The way you do this: base URL is your local host, whatever your local provider is pointing to — Ollama, LM Studio, vLLM, and llama.cpp are common ones. If you watch my videos you've seen me set up Ollama and llama.cpp. Just point the base URL there, choose whichever model, put a placeholder API key (not actually used), and set the timeout a bit larger since local can run slower. If you set base URL, this overrides provider — Hermes will go to your local endpoint and use your local model.

A little caveat: for compression there are actually two configs — a top-level one and an auxiliary one under the auxiliary section. If both are set, auxiliary.compression wins. And if you set the provider to auto in the auxiliary section, it overrides your top-level choice and falls back to Gemini.

[Newsletter plug: AI Garage Weekly, released every Friday, free signup in the description.]

Okay, enough talking — demo time. We're going to test compression, the costliest task. I'm going to fill a context window with the same amount of tokens and run compression once using Claude Opus via the Anthropic API, and once using Open Router with Kimi K2. If you did this local, cost would be zero — you can do the math on savings there.

First test: Claude Opus 4.6 in Hermes agent, chatting about different papers, filled up to 50,000 tokens into the context window. I haven't spent anything today on this API. Running compression now — it compressed 62 messages down to seven (or 36 down from 50, roughly), back to 1%. Cost: 13 cents. That's our baseline for comparing against the auxiliary model swap.

Now the comparison — back at 50K tokens, trying Kimi K2 from Moonshot AI, an older version released September 4th, but reasonable for this task. Configure auxiliary → compression → Open Router → Moonshot AI Kimi K2, then start a new session to pick up the config change. Filled back up to roughly 50,000 tokens, running compress — it used Kimi K2 automatically. Finished: 134 messages down to six. Cost: 0.019 cents — well, about 2 cents — still a significant savings over 13 cents with Opus. That's an 85% savings for each compression pass, and this is only 50,000 tokens — hour-long sessions will fill a lot more of the context window.

One compression pass doesn't sound like much — 13 cents vs. 2 cents — but compression fires constantly. On a real work day with multiple hour sessions, research tasks, browser activity, and coding tasks, you can easily hit compression 10, 15, 20 times a day. Using Opus every time via API can easily hit $60/month at 15 compressions a day. Using a cheaper model like Kimi K2 bumps that down to $9/month — at least $50 saved. And going local would save the total amount. This was just the compression demo — using local or cheaper models on the other auxiliary tasks stacks the savings even more.

So to wrap up: Hermes has eight auxiliary tasks you can configure independently. Focus on the top four — compression, flush memories, web extract, and vision. Match the model to the task, especially for vision if you have a model you like that's cheaper than your frontier model. And local models work here too — point your local model at Hermes for these background tasks even if it can't handle your main project work. That's a great way to get savings. Thanks for watching — subscribe if you want more Hermes-focused videos, and stay tuned for a deep-dive Hermes master class starting in May with a couple videos each week.

</details>
