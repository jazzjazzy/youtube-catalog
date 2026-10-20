---
title: "Docker Just Fixed 90% of AI Coding By Releasing This"
video_id: ZOutBmRai2M
channel: "[[channels/AI LABS]]"
uploaded: 2025-12-02
processed: 2026-07-06
duration: "9:56"
url: https://www.youtube.com/watch?v=ZOutBmRai2M
playlist: "[[Agents skills n8n]]"
type: news
difficulty: advanced
use_case: [mcp-context-optimization]
tools: [Docker, Claude Code, GitHub, Notion]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Docker Just Fixed 90% of AI Coding By Releasing This

![thumbnail](https://i.ytimg.com/vi_webp/ZOutBmRai2M/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=ZOutBmRai2M) | 📅 Uploaded [[uploaded/2025-12-02]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Hundreds of MCP servers with thousands of tools were bloating agent context windows, so Docker built an MCP catalog plus a dynamic MCP gateway that loads only the tool definitions an agent actually needs. The host demos Docker's "code mode" — where agents write JavaScript that calls MCP tools directly inside a sandbox — to build a GitHub-repo-search tool and a GitHub-to-Notion pipeline without flooding context with raw tool results.

**Watch this if:** you're running many MCP servers with Claude Code and your context window keeps getting eaten by tool definitions and raw tool-call results.

## Key Takeaways
- MCP has scaled from 2-3 local servers per user to hundreds of servers with thousands of tools, which both Cloudflare and Anthropic have flagged as a growing context-window problem.
- Docker's MCP catalog lists verified, trusted MCP servers you connect to once (e.g. GitHub, Notion) instead of hard-coding your agent's environment server by server.
- The MCP gateway sits between your client (e.g. Claude Code) and the catalog: it knows which tools are connected and only surfaces the relevant tool definitions into context, using new `find`/`add`/`remove` meta-tools to discover and register MCP servers dynamically.
- Two things eat tokens: tool definitions sitting in context, and the raw intermediate results returned from tool calls (e.g. a GitHub search returning full descriptions, stars, and dates for every repo) — dynamic tool selection only loads the tools actually needed for a session.
- "Code mode" lets an agent write a single JavaScript tool that internally calls multiple MCP tools, running inside a Docker sandbox for security — the model only ever sees one code-mode tool instead of dozens of raw tool definitions.
- State persistence via Docker volumes means large intermediate data (e.g. a downloaded dataset) stays out of the model's context entirely; the model only receives final summaries, errors, or answers.
- Demoed live: combining repeated GitHub repo-search calls into one custom "multiarch repos" tool that writes results to a file (descriptions/links only, no stars), then a GitHub-to-Notion tool that writes filtered repo search results straight into a Notion database.
- Getting started requires updating Docker to a recent version and enabling the MCP Toolkit beta feature; the catalog and dynamic tool-selection features are then enabled by default.

## 🛠 Tools & Software
- [[topics/Docker]] — built the MCP catalog, the dynamic MCP gateway, and the sandboxed "code mode" execution environment that are the core subject of this video.
- [[topics/Claude Code]] — used as the MCP client throughout, connecting only to Docker's gateway rather than each individual MCP server.
- [[topics/GitHub]] — the GitHub MCP server is used to search repos, later turned into a custom "multiarch repos" code-mode tool.
- [[topics/Notion]] — connected as an MCP server so a code-mode tool can write filtered GitHub search results directly into a Notion database.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose context-window token usage (tool definitions + intermediate results) motivates the whole dynamic MCP approach; also referenced via Anthropic's research paper on the problem.

## 📡 Protocols & Standards
- [[topics/MCP]] — the entire video is about scaling and dynamically optimizing MCP: the catalog, the gateway, dynamic tool selection, and code-mode tool creation.

## ✅ Action Items
- Update Docker to the latest version and enable the MCP Toolkit beta feature to access the catalog and dynamic gateway.
- Connect your existing MCP servers (GitHub, Notion, etc.) through Docker's catalog instead of configuring each one directly in your agent client.
- When a workflow repeats the same handful of tool calls, ask your agent to consolidate them into a single code-mode tool to cut context usage.
- Explicitly tell your agent to write large results to a file or external database (Notion, etc.) rather than returning them inline, to keep the context window clean.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/The Best MCP Servers of 2025]] — shared: Claude, Claude Code, Docker, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, GitHub, MCP, Notion
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, GitHub, MCP, Notion
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, GitHub, MCP

## Timeline
- `0:00` — Intro: MCP scaled from a few local servers to hundreds of servers/thousands of tools, becoming a context problem Cloudflare and Anthropic both flagged.
- `1:03` — Docker's article: stop hard-coding agent environments; the token-bloat problem of loading unused tool definitions.
- `1:43` — Docker MCP catalog: verified, trusted MCP servers connected once (demoed with Notion and GitHub).
- `2:15` — MCP gateway: pre-built tools plus new `find`/`add`/`remove` commands for dynamic server discovery.
- `3:09` — GitHub MCP demo: searching repos, and noticing the model receives full raw result detail (links, stars, dates).
- `3:25` — Dynamic tool selection introduced as the article's core improvement: only load tools actually used in a session.
- `4:35` — "Code mode" introduced: agents write JavaScript that calls MCP tools directly.
- `5:26` — Sandbox security, token efficiency, and state persistence (Docker volumes) as code mode's three benefits.
- `7:35` — Demo: consolidating repeated GitHub searches into a "multiarch repos" code-mode tool that writes results to a file.
- `8:24` — Demo: building a GitHub-to-Notion code-mode tool that writes filtered search results into a Notion database.
- `9:36` — Getting started: update Docker, enable the MCP Toolkit beta feature.

## Transcript
<details>
<summary>Full transcript</summary>

One of the most important things in AI has been the MCP protocol. But 6 months later, it has become a huge problem for us. When we started, people only had two to three MCP servers running locally. But MCP has evolved into so much more. Now, people literally have hundreds of MCP servers with thousands of tools at a time, and it has become a huge problem. As you know, Cloudflare noticed this first and Claude followed along by posting a research paper about this problem. But Docker actually came up with a solution for this and solved one of the most critical problems for MCPs by coming up with an entirely new way to use them. A dynamic mode which allows you to save so many tokens, speed up your agents and make entirely new sorts of automations.

So Docker actually released an article on this in which they basically urge us to stop hard-coding our agents environment. First of all, which MCP servers do we actually trust? The second one is how do we avoid filling our context with tool definitions that we might not even use. For example, if you have a thousand tools, you might only use two or three in a single chat. The third one is how do agents discover, configure, and then use these tools efficiently and autonomously.

Now before we move further, you need to know that Docker actually set up the whole infrastructure for this way before it even became a problem. And for that you need to know about their MCP catalog in which they've listed verified MCP servers that you can actually trust. And it's really easy to connect to. You just connect them here in Docker. For example, I've connected notion here. You can see that right now I have two servers and my MCP client which most of the time is claude code only connects to docker and then docker basically manages all my MCP servers. This entirely solves the first problem about which MCP servers we actually trust.

Now, to actually enable our agents to use these MCPS dynamically, they've implemented this MCP gateway that already has pre-built tools to use the MCP servers inside the catalog and use them autonomously. So, essentially what happens is you only connect one MCP and this MCP has all the context of which tools it's connected to in the catalog. Now, for this to actually work, they added some new tools which include MCP find, add, and remove, which basically find MCP servers in the catalog by name or description, and guide you through how to add them correctly. So, for example, I'm using my GitHub MCP right here, and I'm telling it that I want to search for some interesting repos. It doesn't actually call the tool itself, but rather uses the Docker MCP server, which then calls the tool with the correct information and returns all the results. I want you to notice one thing. The LLM is returning everything about the repos — the link, the stars, the description, and even the date on which these repos were posted.

Now, moving on to dynamic tool selection. This is the most important part of the article. Again referencing the Claude article, they talk about how Claude or any AI agent actually uses more tokens: one is the tool definitions in the context window and the second is the intermediate tool results — the raw results actually returned from MCP tool calls. That's why Claude knows every small detail about the repos while I only wanted the description and the link. In my case, it only took maybe 20 tool calls before the whole context window was filled. This is one thing they've improved in the MCP gateway project where they only give the tools that are actually useful — for example, only giving me the search repo tool and not the other 40 tools that come inside the GitHub MCP, because in this session I only want to use the search repo tool.

But once you start selecting tools this way, it also opens up a new range of possibilities, and that leads us into code mode. Cloudflare basically outlined how we've been using MCP wrong, and Docker is the first one to implement this new solution. So they say that by making it possible for agents to code directly using MCP tools — meaning they take the tools and implement them in code — they can provide the agents with these code mode tools that use the tools in a completely new way. Code mode creates a JavaScript enabled tool that can call other MCP tools.

Since this is code written by an agent, it's not tested and not secure by default, so Docker has planned for this to run in a sandbox — and since they already provide Docker containers, this was a no-brainer. This approach offers three key benefits. First, it's completely secure because of sandboxing — it doesn't do any actual damage to your system. Then there's token and tool efficiency: the tools it uses don't have to be sent to the model on every request — the model just needs to know about one new code mode tool. Without code mode, if you're only using three tools repeatedly, the context of 47 other unused tools still goes alongside them. With code mode, the agent writes a custom tool using only the tools actually needed, and every time it just references that one code mode tool. Then there's state persistence: volumes manage how data is saved between tool calls and it's not actually sent to the model. A simple example: if you download a dataset, it's saved to the volume and the model only gets to know it was downloaded successfully — the model doesn't get flooded with 5 GB of data. If you then want to process the first 10,000 rows, the model reads from the volume and returns just the summary.

Now, the reason I was searching these GitHub repositories is so I can discover new open-source tools to put into my videos, running multiple calls using the find GitHub repo tool with different keywords. I presented this to Claude Code and it combined all those different tool calls into a single tool that searches repos based on whatever keywords I give it — called "multiarch repos" — and after creating the tool it used the MCP exec tool to actually run it, giving me 29 unique repos across six keywords. But the results were returned directly in the response, meaning everything was inside the context window. To fix this, I told it to write everything to a file with just the description of the repos, no stars or anything else, and it changed the tool and wrote the results to a text file in my repository.

After that, I asked it to search for the Notion MCP. Once connected, I asked if it could make a tool that outputs the GitHub search results directly into Notion instead of a text file. Using code mode, it made the GitHub-to-Notion tool that pastes results into Notion. After fixing a few little problems, I now have a database in Notion — hard-coded so whatever query I provide goes straight into the database with the different fields, including the date so I can filter easily. The model only gets the name and description of each GitHub repository at a time; the rest of the information is saved here.

Honestly, if you just go through this catalog, you'll get at least one idea of the MCPs you could chain together to make these amazing workflows, while saving tokens and preserving the performance of your own AI agent. Getting started with them is honestly pretty easy. You do need to update your Docker version, and make sure the Docker MCP toolkit beta feature is enabled. Other than that, you'll have your catalog and these new features enabled by default. All you have to do is connect your client and you can pretty much start with them.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
