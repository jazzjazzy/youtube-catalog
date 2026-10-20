---
title: "Katelyn Lesse – Evolving Claude APIs for Agents, Anthropic"
video_id: aqW68Is_Kj4
channel: "[[channels/AI Engineer]]"
uploaded: 2025-12-04
processed: 2026-07-06
duration: "13:24"
url: https://www.youtube.com/watch?v=aqW68Is_Kj4
playlist: "[[Agents skills n8n]]"
type: news
difficulty: advanced
use_case: [agent-context-window-management]
tools: [Claude Code, Claude Skills, GitHub, Sentry]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Katelyn Lesse – Evolving Claude APIs for Agents, Anthropic

![thumbnail](https://i.ytimg.com/vi_webp/aqW68Is_Kj4/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=aqW68Is_Kj4) | 📅 Uploaded [[uploaded/2025-12-04]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Katelyn Lesse, who leads Anthropic's Claude Developer Platform team, explains how the Claude API is evolving along three axes: harnessing Claude's growing capabilities (extended thinking, tool use), managing Claude's context window (MCP, a memory tool, context editing), and giving Claude a computer to work autonomously in (the code execution tool and Agent Skills), all illustrated through Claude Code.

**Watch this if:** you're building agentic systems on the Claude API and want to understand the platform primitives (thinking budgets, memory, context editing, code execution, skills) Anthropic sees as the path to better long-running agent performance.

## Key Takeaways
- The platform helps developers in three ways: harnessing Claude's capabilities, managing Claude's context window, and giving Claude a computer to act autonomously with — all framed around real examples from Claude Code.
- Extended thinking is exposed as a tunable API feature with a token budget, letting you choose between a quick answer and longer reasoning depending on task complexity (e.g. Claude Code deciding when to "think longer" while debugging).
- Tool use lets Claude reliably call both Anthropic's built-in tools (e.g. web search) and custom tools defined with just a name, description, and input schema — Claude Code relies on this constantly for reading/writing/searching files and running tests.
- MCP (introduced a year prior) lets agents pull in context and tools from external systems (e.g. GitHub, Sentry) that live outside the immediate conversation window.
- A memory tool, first shipped as a client-side file system, lets Claude decide what's worth storing outside the context window (e.g. codebase patterns, git workflow preferences) and pull it back in only when relevant.
- Context editing's first iteration clears out old tool results, since past tool call outputs consume a lot of window space but aren't necessarily useful later — combining memory + context editing produced a 39% performance bump on Anthropic's internal evals, on top of expanding some models to a 1M-token context window.
- The code execution tool lets Claude write and run code inside a secure, sandboxed environment that Anthropic's infrastructure manages (containers, security) — this was the key primitive behind launching Claude Code on web and mobile, which required solving container orchestration and session persistence for sessions you can walk away from.
- Agent Skills (folders of scripts, instructions, and resources) combine with the code execution tool and MCP: MCP supplies tools/context, skills supply the domain expertise for using them well — e.g. Claude Code pulling in a web design skill to follow a project's design system when building a landing page.

## 🛠 Tools & Software
- [[topics/Claude Code]] — used throughout as the running example for every platform feature discussed (extended thinking, tool use, MCP, memory, context editing, code execution, skills).
- [[topics/Claude Skills]] — Agent Skills are described as folders of scripts/instructions/resources Claude pulls into its sandbox, combined with MCP and the code execution tool, exemplified by a web design skill for landing pages.
- [[topics/GitHub]] — given as an example external system Claude Code connects to via MCP for additional context and tools.
- [[topics/Sentry]] — given as another example external system accessible via MCP alongside GitHub.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose capabilities (thinking, tool use), context management (memory, context editing), and autonomous computer use (code execution, skills) the entire talk is about.

## 📡 Protocols & Standards
- [[topics/MCP]] — introduced a year before this talk as the standardized way for agents to reach external systems/context/tools; discussed as complementary to the memory tool, context editing, and Agent Skills.

## ✅ Action Items
- If building on the Claude API, use the extended-thinking token budget to trade off speed vs. reasoning depth per task rather than always maxing it out.
- Define custom tools with a clear name, description, and input schema so Claude can reliably choose and call them.
- Connect MCP servers for any external systems (issue trackers, error monitoring, etc.) your agent needs context from, rather than stuffing that context into the prompt.
- Use the memory tool to store reusable context (codebase patterns, workflow preferences) outside the window instead of repeating it every session.
- Enable context editing to clear stale tool results and combine it with memory for meaningfully better eval performance.
- Look at the code execution tool plus Agent Skills together when you want Claude to work autonomously in a sandboxed environment with domain-specific expertise.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, GitHub, MCP, Sentry
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, MCP, Sentry
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Sentry
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, GitHub, MCP, Sentry

## Timeline
- `0:33` — Speaker intro: Katelyn leads the Claude Developer Platform team at Anthropic.
- `1:31` — Framing: three ways the platform helps developers get the best out of Claude, illustrated via Claude Code.
- `1:52` — Harnessing capabilities: extended thinking as a tunable, budgeted API feature.
- `3:10` — Tool use: built-in and custom tools, and how Claude Code relies on many of them constantly.
- `5:19` — Managing Claude's context window: introducing MCP for external systems like GitHub and Sentry.
- `6:39` — Memory tool: a client-side file system for storing and recalling context outside the window.
- `7:44` — Context editing: clearing stale tool results; 39% eval performance bump combining memory + context editing.
- `8:23` — Giving Claude a computer: the philosophy behind letting Claude act autonomously.
- `9:15` — Claude Code on web/mobile: solving sandboxing, container orchestration, and session persistence.
- `10:19` — The code execution tool: secure sandboxed code execution as infrastructure Anthropic manages.
- `11:12` — Agent Skills combined with MCP and code execution, e.g. a web design skill for landing pages.
- `12:44` — Closing: platform roadmap recap and Anthropic hiring pitch.

## Transcript
<details>
<summary>Full transcript</summary>

Good morning. So first let's give a huge thank you to Swix and the whole AI Engineer organizing team for bringing us together. I'm Katelyn and I lead the Claude Developer Platform team at Anthropic. So let's start with a show of hands — who here has integrated against an LLM API to build agents? Okay, I'm talking to the right people. So today I want to share how we're evolving our platform to help you build really powerful agentic systems using Claude.

We love working with developers who do what we call raising the ceiling of intelligence — always trying to be on the frontier, always trying to get the best out of our models and build the most high performing systems. I want to walk you through how we're building a platform that helps you get the best out of Claude, using a product you hopefully all know — Claude Code.

So when we think about maximizing performance from our models, we think about building a platform that helps you do three things. First, the platform helps you harness Claude's capabilities — we're training Claude to get good at a lot of stuff and we need to give you the tools in our API to use the things Claude is actually getting good at. Next, we help you manage Claude's context window — keeping the right context in the window at any given time is really critical to getting the best outcomes from Claude. And third, we're really excited about this lately: we think you should just give Claude a computer and let it do its thing.

Starting with harnessing Claude's capabilities. Here's a first example, relatively basic: Claude's performance on various tasks scales with the amount of time you give it to reason through those problems. We expose this to you as an API feature — do you want Claude to think longer for something more complex, or do you want a quick answer? We also expose this with a budget — you can tell Claude how many tokens to spend on thinking. For Claude Code, you're often debugging pretty complex systems, or sometimes you just want a quick answer, and Claude Code takes advantage of this feature to decide whether or not to have Claude think longer.

Another basic example is tool use. Claude has gotten really good at reliably calling tools. We expose this in our API with both our own built-in tools, like our web search tool, as well as the ability to create your own custom tools — you just define a name, a description, and an input schema, and Claude is pretty good at reliably knowing when to go call those tools and pass the right arguments. This is relevant for Claude Code — it has many, many tools and is calling them all the time to do things like read files, search for files, write to files, and rerun tests.

So the next way we're evolving the platform to help you maximize intelligence from Claude is helping you manage Claude's context window. Getting the right context at the right time in the window is one of the most important things you can do to maximize performance, but context management is really complex to get right, especially for a coding agent like Claude Code — you've got technical designs, your entire codebase, instructions, tool calls, all potentially in the window at any given time.

Let's start with MCP, model context protocol. We introduced this a year ago, and it's been really cool to see the community swarm around adopting it as a standardized way for agents to interact with external systems. For Claude Code, you might imagine GitHub or Sentry — plenty of places outside the agent's context where there might be additional information or tools you want your agent to interact with. This will obviously get you much better performance than an agent that only sees the things in its window as a result of your prompting.

The next thing is memory. If you can use tools like MCP to get context into your window, we introduced a memory tool to help you keep context outside the window that Claude knows how to pull back in only when it actually needs it. We introduced the first iteration of our memory tool as essentially a client-side file system — you control your data, but Claude is good at knowing "this is a good thing I should store away for later," and it knows when to pull that context back in. For Claude Code, you could imagine your patterns for your codebase, or your preferences for git workflows — things Claude can store away in memory and pull back in only when relevant.

The third thing is context editing. If memory helps you keep stuff outside the window and pull it back in when it makes sense, context editing helps you clear stuff out that's not relevant right now. Our first iteration of context editing is just clearing out old tool results — tool results can be really large and take up a lot of space in the window, and we found that tool results from past calls aren't necessarily super relevant to help Claude get good responses later in a session. For Claude Code, it's calling hundreds of tools, and all those files it read are taking up space in the window, so it takes advantage of context management to clear those things out. We found that combining our memory tool with context editing gave a 39% bump in performance over our own internal evals — really huge. And we're expanding on this by giving you larger context windows — for some models, up to a million tokens. Combining a larger window with tools to edit what's in it maximizes performance, and over time we're teaching Claude to better understand how much room it has left and respond accordingly.

So here's the third thing: we think you should give Claude a computer and just let it do its thing. There's a lot of discourse right now around agent harnesses — how much scaffolding, how opinionated, how heavy or light. At the end of the day, if Claude has access to writing code, and access to running that same code, it can accomplish anything — you can get really great professional outputs just by giving Claude runway to go do that. But the challenge is the infrastructure and expertise needed to give Claude access to things that get you better results when it's using a computer.

A fun story: we recently launched Claude Code on web and mobile. This was a fun project because we had a lot of problems to solve. When you're running Claude Code locally, it's using your machine as its computer, but if you start a session on web or mobile and walk away, where is Claude Code running? We needed a secure environment for Claude to write and run code that's not necessarily approved by you, we needed container orchestration at scale, and we needed session persistence because many of you started sessions and walked away, and we had to make sure everything was ready when you came back to see the results.

One key primitive here is our code execution tool — we released this in the API, allowing Claude to write code and run that code in a secure, sandboxed environment. Our platform handles containers and security so you don't have to think about these things. For Claude Code, there's plenty of examples — like "make an animation more sparkly" — where you want Claude to actually run that code. We really think the future of agents is letting the model work pretty autonomously within a sandbox environment, and we're giving you the infrastructure to do that.

This gets really powerful once you think about giving the model actual domain expertise in what you're trying to do. We recently released Agent Skills, which you can use in combination with our code execution tool. Skills are basically folders of scripts, instructions, and resources that Claude has access to and can decide to run within its sandbox environment, based on the request you gave it and the description of a skill. You can combine skills with tools like MCP — MCP gives you access to tools and context, and skills give you the expertise to make use of those tools and that context. For Claude Code, a good example is web design: whenever you launch a new landing page, you want it to follow your design system and patterns, and Claude will know this is a good time to pull in the web design skill. Tomorrow, colleagues from our team are giving a talk on skills — I definitely recommend checking that out.

So these are the ways we're evolving our platform to help you take advantage of everything Claude can do: harnessing Claude's capabilities, managing Claude's context, and giving Claude a computer and letting it do its thing. We're going to keep evolving the API as Claude gets better and gets more capabilities. As memory and context evolve, we're going to up the ante on the tools we give you to let Claude decide what to pull in, store away, and clean out. And we're going to keep leaning into agent infrastructure — orchestration, secure environments, sandboxing — to make sure those are ready for you to take advantage of. And we're hiring at Anthropic, growing our team across product, design, DevRel, and more. Please reach out to us, and thank you.

</details>
