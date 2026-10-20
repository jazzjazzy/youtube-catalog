---
title: "7 new open source AI tools you need right now…"
video_id: Xn-gtHDsaPY
channel: "[[channels/Fireship]]"
uploaded: 2026-03-12
processed: 2026-07-05
duration: "6:14"
url: https://www.youtube.com/watch?v=Xn-gtHDsaPY
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [ai-agent-tooling-roundup, open-source-ai-tools]
tools: [Claude Code, Agency, PromptFoo, MicroFish, Impeccable, Open Viking, NanoChat, Heretic]
llms: [Claude, GPT-5, Gemini, Gemma]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# 7 new open source AI tools you need right now…

![thumbnail](https://i.ytimg.com/vi_webp/Xn-gtHDsaPY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=Xn-gtHDsaPY) | 📅 Uploaded [[uploaded/2026-03-12]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Fireship's rapid-fire tour of 7 open-source projects for the AI-agent-heavy dev workflow: Agency (role-based agent templates), PromptFoo (prompt/model testing and red-teaming, recently acquired by OpenAI), MicroFish (multi-agent prediction engine simulating reactions to real-world data), Impeccable (a 17-command front-end design skill), Open Viking (a file-system-based memory/context database for agents with tiered loading), Heretic (automated removal of model safety guardrails via "abliteration"), and NanoChat (build/train your own small LLM end-to-end for ~$100 in GPU time).

**Watch this if:** you want a fast-scan list of lesser-known open-source tools for agent orchestration, prompt testing, front-end polish, agent memory, and small-model training.

## Key Takeaways
- Agency provides free, open-source agent templates for nearly every startup job role (front-end dev, back-end dev, security engineer, growth hacker, etc.) that can be combined together inside Claude Code to go from zero to product without personally implementing every role.
- PromptFoo (recently acquired by OpenAI) works like a unit-testing framework for prompts: test different prompt/model combinations to find what performs best, plus run automated red-team attacks to check for vulnerabilities like prompt injection.
- MicroFish is a multi-agent AI prediction engine: it extracts real-world data (breaking news, financial trends), builds a digital world, and has multiple independently-personality'd agents react to and discuss that data — like a miniature evolving synthetic social network used for trend/strategy prediction.
- Impeccable is an open-source front-end-design skill with 17 commands to fix generic "vibe-coded" UI — e.g. `distill` to simplify an overly complex UI, `colorize` to apply brand colors, `animate`/`delight` to add unique polish.
- Open Viking is a database purpose-built for AI agent context: instead of jamming everything into a vector database, it organizes an agent's memory, resources, and skills into the file system with a tiered loading system that cuts token consumption, auto-compresses content, and refines long-term memory over time.
- Heretic automates removal of a model's safety guardrails via a technique called "abliteration" — fully automatic, no expensive post-training required; run it from the command line against a censored model (e.g. Google's Gemma) to get an uncensored version.
- NanoChat implements an entire LLM pipeline end-to-end (tokenization, pre-training, chat fine-tuning, evaluation, and a web UI) — you can train your own small language model for roughly $100 in GPU time; it won't rival Claude, GPT-5, or Gemini, but gives full control over a model you own.

## 🛠 Tools & Software
- [[topics/Claude Code]] — cited as where Agency's role-based agent templates get combined together to build a product.
- [[topics/Agency]] — open-source agent templates for common startup roles, meant to be composed together inside a coding agent.
- [[topics/PromptFoo]] — prompt/model testing framework with automated red-teaming for vulnerabilities like prompt injection; recently acquired by OpenAI.
- [[topics/MicroFish]] — multi-agent prediction engine that simulates independent agents reacting to real-world data to forecast trends/strategies.
- [[topics/Impeccable]] — a 17-command open-source front-end-design skill (distill, colorize, animate, delight) for improving generic AI-generated UI.
- [[topics/Open Viking]] — file-system-based, tiered-loading memory/context database purpose-built for AI agents, as an alternative to jamming everything into a vector database.
- [[topics/Heretic]] — automated model-guardrail removal tool using the "abliteration" technique, run from the command line against models like Gemma.
- [[topics/NanoChat]] — end-to-end open-source LLM training pipeline (tokenization through chat fine-tuning and web UI) for building your own small model cheaply.

## 🤖 LLMs Mentioned
- [[topics/Gemma]] — used as the example censored model that Heretic's abliteration technique is run against.
- [[topics/Claude]] — cited as a benchmark a NanoChat-trained model won't match.
- [[topics/GPT-5]] — cited as a benchmark a NanoChat-trained model won't match.
- [[topics/Gemini]] — cited as a benchmark a NanoChat-trained model won't match.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try combining Agency's role-based agent templates inside Claude Code for a small project instead of hand-implementing every dev role yourself.
- Run PromptFoo's red-team tests against any app that lets end users interact with your AI to check for prompt-injection vulnerabilities.
- If your AI-generated UI looks generic, try Impeccable's `distill` command first, then `colorize` and `animate`/`delight`.
- If you're managing a lot of agent context, look at Open Viking's file-system + tiered-loading approach as an alternative to a vector database.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Gemini, Gemma
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Claude, Claude Code, Gemini
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Claude, GPT-5, Gemini
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: Claude, Claude Code, Gemini
- [[videos/The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing]] — shared: Claude, GPT-5, Gemini
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude, Claude Code, Gemini
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code

## Timeline
- `0:00` — Intro: the state of AI-assisted coding in 2026, framing for the 7-tool roundup.
- `1:20` — Agency: role-based agent templates combinable inside Claude Code.
- `1:50` — PromptFoo: prompt/model testing and automated red-teaming.
- `2:29` — MicroFish: multi-agent prediction engine for trend/strategy forecasting.
- `3:14` — Impeccable: 17-command front-end design skill for fixing generic UI.
- `3:43` — Open Viking: file-system-based, tiered-loading agent memory database.
- `4:22` — Heretic: automated guardrail removal via abliteration.
- `4:57` — NanoChat: train your own small LLM end-to-end for ~$100.
- `5:26` — Sponsor segment: Recall AI unified meeting-bot API.

## Transcript
<details>
<summary>Full transcript</summary>

Every developer in 2026 has the same problem. You open your editor, you write one line of code, and suddenly a dozen different AI agents are arguing in your terminal about how to do it better. And if you're one of those weirdos like me who actually enjoys the craft of writing code, congratulations, you're officially living in the dark ages of Slop Overflow. Instead of grinding for hours and earning those sweet dopamine hits line by line, you now just tell the AI what you want and watch it hallucinate an entire code base. Writing code isn't fun anymore, layoffs are intensifying, and even the CEO of Replit said that nowadays knowing how to code is actually a disadvantage. "Not having a coding experience is becoming an advantage." "The building a product is more efficient than ever, unless you're a stupid programmer who cares about stupid things like architecture and security." "Coders get lost in the details." But he's absolutely right. The hard truth is that we're not going back to the good old days of hand-crafted code, and the only way forward is to embrace the chaos and learn how to enslave the machines. In today's video, we'll look at seven different open-source projects you've never heard of that will help you whip your AI agents into shape and build highly effective Slop pipelines. It is March 12th, 2026, and you're watching the Code Report.

In the past, if you were an indie full-stack developer, it meant you had to have skills on the front end, back end. You had to understand DevOps, security, UI/UX design, and a bunch of other BS. But nowadays, you don't need to learn all that stuff. You just need to hire the right agents. And a tool that can help you do that quickly is the Agency, which is a free and open-source project that provides agent templates for basically every job role you would find at a startup, like a front-end developer, back-end developer, security engineer, a growth hacker, Twitter engager, and many others. You can easily combine all these agents together in Claude Code, which can more efficiently help you go from zero to an actual product without needing to directly implement every personality and skill.

That's cool, but when you put these agents to work, how do you know your prompts are any good? Well, that's where Prompt Foo comes in, another open-source tool that was just recently acquired by OpenAI that you can think of like a unit testing framework for your prompts. If you're using AI to build an app that lets the end user interact with AI also, half the battle is figuring out if you're using the best model with the best prompt. A prompt foo lets you test different prompts with different models that to optimize what's going to actually work best in your application. On top of that, it can also do automated red team attacks to find out if your app is vulnerable to things like prompt injection, which is important because if your chatbot can be tricked into revealing your API keys by a 14-year-old on Discord, your app is probably going to fail.

If failing sucks, but it's a lot easier to not fail when you can predict the future. And Miro fish can help you do that. It's a multi-agent AI prediction engine that starts by extracting a bunch of data from the internet, like breaking news and financial trends. It then uses that data to create a digital world where multiple agents with independent personalities then react to and discuss the data, almost like a miniature evolving artificial social network. Yeah, it might be in Chinese, but if you don't know how to speak Chinese yet, all I can say to you is need law whole law. You're falling behind. Like for example, if you want an app idea that's guaranteed to make you a billion dollars, you can spin up micro fish to analyze trends at the macro and micro level and then predict a strategy that's guaranteed to make you rich. It's really that easy, but here's the problem. You go to build that app and the UI has these dumb purple gradients like every single other vibe coded app.

Well, to fix that, you need impeccable, an open-source project optimized for front-end design. It's a skill that comes with 17 different commands that can help your UI not suck so much. Like one thing that drives me crazy is that many AI chatbots create UIs that are way too complex. Well, with impeccable, we can use the distill command to simplify everything in one go. And then we can use commands like colorize to add our brand colors, then slowly add in commands like animate and delight to make the UI look more unique and special.

But perhaps the single most important skill of the modern vibe engineer is managing context. If the context is garbage, the output is garbage. An open-source project trying to your context better is Open Viking, a database designed specifically for AI agents. Instead of jamming everything into a vector database, Open Viking organizes an agent's memory, resources, and skills into the file system. Not only is that a sane way to unify your contacts, but it also uses a tiered loading system, which can dramatically reduce token consumption and save you a bunch of money. And it automatically compresses content and refines long-term memory, which will make your agent smarter the more you use it.

But depending on your project, you may not need an agent that's more smarter. You may need that's more based, and that's where Heretic comes in. Virtually all models out there have guardrails that prevent you from doing fun things like cooking meth in your shed or building high-yield thermonuclear warheads. Heretic allows you to remove this draconian woke censorship using a technique called obliteration. This approach allows the tool to be completely automatic and doesn't require any expensive post-training. All you have to do is take a smart yet highly censored model like Google's Gemma, run this tool from the command line, and now you have a model without the bubble wrap that will obey any command.

But maybe that's not even enough to satisfy your unhinged ambitions. In that case, you may want to just build your own LLM from scratch, and believe it or not, you can actually do that with NanoChat, which implements the entire LLM pipeline, including tokenization, pre-training, fine-tuning for chat, evaluation, and a web UI so you can actually talk to it. What's crazy though is that you can use it to train your own small language model for about $100 in GPU time. It's not going to be Claude, GPT-5, or Gemini, but at least it gives you a model that you have absolute control over.

But the only thing that's a bigger waste of time than writing code by hand is going to meetings, and that's why you need to know about Recall AI, the sponsor of today's video. If you've ever tried building AI meeting tools from scratch, you know it's a nightmare trying to maintain separate integrations for Zoom, Google Meet, Microsoft Teams, and all the others. Recall solves this problem by giving you one unified API that works across every meeting platform. You set up a meeting bot or desktop recording with a few lines of code like I'm doing here and it'll capture transcripts, recordings, and metadata in real-time. The thousands of companies like HubSpot and ClickUp use it to handle all their meeting infrastructure and most teams are able to ship recording and note-taking features to production in a few hours instead of months. So check out recall.ai/fireship to get $100 in free credits to try it out for yourself.

This has been the Code Report. Thanks for watching and I will see you in the next one.

</details>
