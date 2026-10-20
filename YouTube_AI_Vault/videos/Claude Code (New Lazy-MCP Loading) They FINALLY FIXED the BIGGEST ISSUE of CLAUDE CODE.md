---
title: "Claude Code (New Lazy-MCP Loading): They FINALLY FIXED the BIGGEST ISSUE of CLAUDE CODE!"
video_id: qBE4OVS6Nho
channel: "[[channels/AICodeKing]]"
uploaded: 2026-01-16
processed: 2026-07-06
duration: "10:04"
url: https://www.youtube.com/watch?v=qBE4OVS6Nho
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [mcp-context-management]
tools: [Claude Code, Verdant, Codex, Vertex AI, Amazon Bedrock]
llms: [Claude Opus, Claude Sonnet]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code (New Lazy-MCP Loading): They FINALLY FIXED the BIGGEST ISSUE of CLAUDE CODE!

![thumbnail](https://i.ytimg.com/vi/qBE4OVS6Nho/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=qBE4OVS6Nho) | 📅 Uploaded [[uploaded/2026-01-16]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> AICodeKing explains Anthropic's new MCP Tool Search feature, which fixes the long-standing problem of MCP servers eating up huge chunks of Claude Code's context window before any work even starts. Instead of loading every tool definition upfront, Claude now searches a tool catalog on demand (via regex or BM25) and loads only the tools it needs — cutting token usage by ~85% and significantly improving tool-selection accuracy (Opus 4.5 up to 88.1%).

**Watch this if:** you run Claude Code with several MCP servers and have hit context-window exhaustion or degraded tool selection because too many tool definitions were loaded at once.

## Key Takeaways
- With multiple MCP servers connected, all tool definitions previously loaded into context upfront — some users reported 67,000+ tokens consumed before sending a single prompt, out of a ~200K token window.
- Tool-selection accuracy also degrades once more than 30–50 tools are available simultaneously, according to research Anthropic cited.
- MCP Tool Search kicks in automatically once tool descriptions would exceed ~10% of context, switching Claude to a search-based approach that discovers and loads only relevant tools for the current task.
- Anthropic's benchmarks: tool search preserves ~191,300 tokens of context vs. ~122,800 with the traditional upfront-loading approach — an ~85% reduction in token usage for tool definitions.
- Accuracy gains: Opus 4 went from 49% to 74% on MCP evaluations with large tool libraries; Opus 4.5 went from 79.5% to 88.1%.
- Under the hood it's a client-side similarity-search tool that Claude can call repeatedly (refining keywords, running searches in parallel) — two variants exist: regex-pattern search and BM25 natural-language search.
- Tools can be marked `defer loading: true` so they aren't loaded into context until Claude actually searches for and needs them; Anthropic recommends keeping your 3–5 most-used tools non-deferred for best performance.
- The feature works with prompt caching (discovered tools can be reused across multi-turn conversations) and is currently in public beta, available via a beta header for Opus 4.5 and Sonnet 4.5 on the Claude API, Google Cloud Vertex AI, and Amazon Bedrock; Claude Code enables it automatically with no configuration needed.
- The host notes this removes his old workaround of running separate coding-agent setups per MCP server (e.g. splitting front-end/back-end tool sets across different Claude Code/Codex sub-agent instances inside Verdant) just to avoid overflowing one agent's context.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI that automatically detects excessive MCP tool-definition size and switches to the new search-based tool loading, with no user configuration required.
- [[topics/Verdant]] — the graphical coding tool the host uses to run multiple coding agents at once, previously requiring manual per-agent MCP/context splitting.
- [[topics/Codex]] — mentioned as one of the CLI sub-agents (alongside Claude Code) the host used to run separately to manage context per task before this update.
- [[topics/Vertex AI]] — one of the platforms (alongside the main Claude API) where the new MCP Tool Search beta is available.
- [[topics/Amazon Bedrock]] — the other cloud platform where the MCP Tool Search beta is available.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — benchmarked before/after the update: Opus 4 improved from 49% to 74% and Opus 4.5 from 79.5% to 88.1% on MCP tool-selection accuracy evaluations.
- [[topics/Claude Sonnet]] — Sonnet 4.5 is one of the two models (with Opus 4.5) supporting the new MCP Tool Search beta.

## 📡 Protocols & Standards
- [[topics/MCP]] — the Model Context Protocol whose multi-server tool-loading problem this entire feature addresses; explained at a basic level (connecting Claude to databases, APIs, file systems, etc.).

## ✅ Action Items
- If you use Claude Code with several MCP servers, check whether MCP Tool Search has kicked in automatically (it triggers once tool descriptions would exceed ~10% of context) — no setup should be required.
- If building directly against the Claude API with many tools, opt into the MCP Tool Search public beta via the beta header on Opus 4.5/Sonnet 4.5.
- Mark your 3–5 most frequently used tools as non-deferred and defer the rest (`defer loading: true`) for the best balance of speed and context savings.
- Reconsider any workaround setups that split MCP servers/tools across multiple separate agent instances just to avoid context overflow — this feature may make that unnecessary.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Opus, Claude Sonnet, Codex
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Claude Sonnet, Codex
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP

## Timeline
- `0:00` — Intro: the biggest problem with using multiple MCP servers in Claude Code — context window exhaustion.
- `0:25` — What MCP is: connecting Claude to databases, APIs, file systems, and other external tools.
- `0:49` — The problem in numbers: 67,000+ tokens consumed before a single prompt with 7+ MCP servers.
- `1:42` — Tool-selection accuracy also degrades past 30–50 simultaneously available tools.
- `2:08` — Introducing MCP Tool Search: dynamic, on-demand tool discovery instead of upfront loading.
- `3:25` — The numbers: ~191,300 tokens preserved vs. ~122,800 (an 85% reduction), plus accuracy gains for Opus 4 and Opus 4.5.
- `4:38` — How it works under the hood: a client-side similarity-search tool, regex vs. BM25 variants.
- `6:00` — `defer loading: true` and the recommendation to keep 3–5 frequent tools non-deferred.
- `6:37` — Works with prompt caching across multi-turn conversations; currently in public beta.
- `7:16` — Availability: Opus 4.5/Sonnet 4.5 on the main API, Vertex AI, and Amazon Bedrock; automatic in Claude Code.
- `7:51` — Context: most-requested GitHub feature, part of Claude Code's broader growth (~115K weekly developers).
- `9:09` — Host's own workflow: previously split MCP/agent setups across tools like Verdant to manage context, now less necessary.

## Transcript
<details>
<summary>Full transcript</summary>

Hi, welcome to another video. So, if you have been using Claude Code with MCP servers, you probably know about one of the biggest issues with it: the more MCP servers you add, the more your context window gets eaten up before you even start doing any work. If you don't know what MCP is, it stands for Model Context Protocol, and it's basically a way to connect Claude to external tools and data sources — things like databases, APIs, file systems, and a whole bunch of other stuff. It's like giving Claude superpowers to interact with the outside world.

But here's the problem: every time you add an MCP server, all the tool definitions from that server get loaded into Claude's context window. I've seen people report setups with seven or more MCP servers where their context was already at 67,000 tokens before they even sent a single prompt — that's literally insane. Your context just evaporates before any actual work begins, and it becomes a huge pain to manage. Think about it — you have a context window of around 200,000 tokens, and before you even ask Claude to do anything, a third of it is already gone just because of a bunch of MCP tools being installed. That's not ideal at all.

And it's not just about token usage — when Claude has access to too many tools at once, it actually becomes worse at selecting the right tool for the job. There's research showing Claude's ability to correctly select tools degrades significantly once you have more than 30 to 50 tools available at the same time. So you're not just wasting tokens, you're also making Claude worse at its job.

But Anthropic has now fixed this issue with a new feature called MCP Tool Search, and honestly, this is pretty amazing. Basically, instead of loading all your MCP tools into the context window up front, Claude Code now dynamically discovers and loads tools on demand. It detects when your MCP tool descriptions would use more than 10% of your context, and when that happens, it switches to a search-based approach. What this means is Claude only sees the tools it actually needs for the current task — it searches through your tool catalog using keywords and then loads only the relevant tools into context. So if you have hundreds or even thousands of tools, Claude won't be overwhelmed by them anymore. This is a big deal because previously, having around 50 tools would consume like 10 to 20,000 tokens just for the tool definitions alone — a huge chunk of your context window wasted just listing out the tools.

Now let's talk about the actual numbers, because they're quite impressive. According to Anthropic, the tool search feature preserves around 191,300 tokens of context compared to 122,800 with the traditional approach — an 85% reduction in token usage while still maintaining access to your full tool library. And the accuracy improvements are also significant: in their internal testing, Opus 4 went from 49% to 74% accuracy on MCP evaluations when working with large tool libraries, and Opus 4.5 improved from 79.5% to 88.1%. So not only does it save tokens, it also makes Claude better at selecting the right tools — a double win. Pretty cool, right?

Now, let me tell you how this actually works under the hood. The feature uses a similarity-search tool that operates client-side — basically a regular tool that takes in a keyword and does a similarity search to return a list of tool names. Because it functions as a standard tool within Claude's agent loop, the model can issue multiple searches, refine keywords, and make parallel calls to find the right tools. So let's say you ask Claude to get the weather in San Francisco — instead of having all 500 of your tools loaded in context, it will first search for tools related to weather and only load those specific tools, then use the weather tool to get the information you need. It's much more efficient this way.

There are two variants of the tool search: one uses regex patterns, where Claude constructs patterns to search for tools (for example, searching for "weather" or "get data" to find matching tools), and the other uses BM25, which allows Claude to use natural-language queries to search for tools. So you can pick whichever works better for your use case. You can also mark tools with "defer loading" set to true, meaning those tools won't be loaded into Claude's context initially — Claude will only discover them when it actually needs them through the search tool. They recommend keeping your three to five most frequently used tools as non-deferred for optimal performance, and the rest can be deferred; this way Claude always has quick access to your most common tools while still being able to discover the rest when needed.

Another thing that's pretty cool is that this feature works with prompt caching as well — so if you're having multi-turn conversations, Claude can reuse discovered tools in subsequent turns without having to re-search for them, making the whole experience much smoother. This feature is currently in public beta, so you'll need to use the beta header in your API requests. It works with Claude Opus 4.5 and Claude Sonnet 4.5 on the main API, and also on Google Cloud's Vertex AI and Amazon Bedrock. For Claude Code specifically, it will automatically detect when you have too many MCP tools and switch to this search-based approach — you don't really need to do anything special, it just works. Claude Code handles all of this behind the scenes, which is nice.

This is honestly one of the biggest improvements to MCP and Claude Code — it was actually the most requested feature on their GitHub, and they finally implemented it. People have been asking for lazy loading on MCP servers for a long time, and this is essentially what this feature provides. If you've been avoiding using multiple MCP servers because of context issues, now you can go ahead and use as many as you want — this changes things quite a bit. You can now connect Claude to all your databases and services without worrying about running out of context.

I think this is a really good step by Anthropic — they're actually listening to the community and fixing the pain points. The MCP ecosystem is getting much better with updates like this, and with Claude Code reportedly being used by around 115,000 developers weekly and reaching a billion-dollar annualized run rate, it makes sense that they're putting a lot of effort into making it better. If you're building something with the Claude API and using a lot of tools, I'd definitely recommend checking this feature out — it can really help you scale your tool library without running into context issues.

Previously, I used to have different coding-agent setups for different tasks with different MCPs, just to make sure I didn't overflow one agent with too much context. For example, I mainly use Verdant for all my coding — it's graphical, and I can fire up a lot of agents at once and work with it. What I used to do was give it the context of how to run sub-agents like Claude Code and Codex via CLI and keep a tab on them for things like front-end and back-end. I guess that's not needed now, as Claude Code can handle it in itself — so that's great, and I hope all the other tools get this too. Overall, it's pretty cool. Anyway, share your thoughts below and subscribe to the channel — you can also donate via the Super Thanks option or join the channel for some perks. I'll see you in the next video. Bye.

</details>
