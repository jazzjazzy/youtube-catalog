---
title: "Progressive Disclosure in Claude Code"
video_id: DQHFow2NoQc
channel: "[[channels/Developers Digest]]"
uploaded: 2026-01-12
processed: 2026-07-06
duration: "13:59"
url: https://www.youtube.com/watch?v=DQHFow2NoQc
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [context-management]
tools: [Claude Code, Cursor, Cloudflare]
llms: [Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Progressive Disclosure in Claude Code

![thumbnail](https://i.ytimg.com/vi/DQHFow2NoQc/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=DQHFow2NoQc) | 📅 Uploaded [[uploaded/2026-01-12]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Cloudflare, Anthropic, and Cursor have independently converged on the same fix for MCP context bloat: stop loading every tool definition up front and instead let agents discover tools on demand via file systems, bash, and code execution. The video walks through each company's data (Anthropic's tool-search-tool cut context from 77k to 8.7k tokens and boosted Opus 4 MCP accuracy from 49% to 74%) and shows how Claude Code Skills implement the same progressive-disclosure pattern.

**Watch this if:** your Claude Code or MCP-based agent is burning huge amounts of context on tool definitions it rarely uses.

## Key Takeaways
- Cloudflare's "Code Mode" blog post argued MCP tools should be converted to a TypeScript API in a sandbox rather than loaded directly as tool schemas — models are better at writing code than at picking from long tool lists, and this cut token usage by 98.7%.
- Anthropic's "advanced tool use" release added a tool-search-tool that discovers tools on demand: context dropped from 77,000 to 8,700 tokens (85% reduction), and MCP-evaluation accuracy rose from 49% to 74% on Opus 4 and 79.5% to 88.1% on Opus 4.5.
- Cursor independently confirmed the same pattern, reporting a 46.9% reduction in total agent tokens from on-demand tool discovery.
- The shared industry direction: give agents a file system and bash, and let discovery happen through grep/glob/search rather than dumping everything into context up front.
- Claude Code Skills are a concrete implementation — only the skill's frontmatter (a handful of tokens) loads by default; the full skill body and any referenced files load only when actually invoked.
- Anthropic's memory tool is just plain markdown files (no embeddings, no vector search) — agentic file search felt better and worked better than embedding-based retrieval in practice.
- An experimental Claude Code CLI flag exposes the same tool-search capability directly, potentially replacing loading full MCP server schemas into context (still a work in progress at time of recording).
- Net effect: agents are no longer capped at 5-20 MCP servers before performance degrades — you can scale to thousands of skills/tools via hierarchical, on-demand lookup.

## 🛠 Tools & Software
- [[topics/Claude Code]] — main subject: Skills, the experimental MCP-CLI tool-search flag, and file/bash-based agent design are all demonstrated as the practical implementation of progressive disclosure.
- [[topics/Cursor]] — cited as independently confirming the same token-efficiency gains from on-demand tool discovery (46.9% reduction in agent tokens).
- [[topics/Cloudflare]] — its "Code Mode" blog post is presented as the originating insight: convert MCP tools into a TypeScript API executed in a sandbox instead of loading tool schemas directly.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4 and Opus 4.5 benchmark numbers are cited to show accuracy gains (49%→74% and 79.5%→88.1%) from the tool-search-tool approach.

## 📡 Protocols & Standards
- [[topics/MCP]] — the entire video is framed around fixing how MCP tools are loaded into context; discussed at length as both a good protocol and a source of token bloat when used naively.

## ✅ Action Items
- Set up a Claude Code Skills directory and move rarely-used tool logic/instructions into skill files instead of the main system prompt.
- Try the experimental MCP-CLI tool-search flag in Claude Code to see context savings on your own MCP server list.
- Audit your current agent's context window for MCP tool definitions that are loaded but rarely invoked, and consider converting them to on-demand lookups.
- Structure skills hierarchically (subskills with references) rather than as one flat directory once you have more than a handful.

## 🔗 Related Videos
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Claude Opus, Cursor, MCP
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Cursor, MCP
- [[videos/The Best MCP Servers of 2025]] — shared: Claude Code, Cloudflare, Cursor, MCP
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Opus, MCP
- [[videos/9 NEW Claude Mods that can truly change how you work]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude Code, Claude Opus, MCP

## Timeline
- `0:00` — Intro: AI infrastructure companies are independently converging on the same agent-building pattern.
- `0:38` — Cloudflare's "Code Mode" blog post: MCP tools converted to a TypeScript API, 98.7% token reduction.
- `1:20` — Anthropic's advanced tool use: tool-search-tool cuts context from 77k to 8.7k tokens; Opus 4/4.5 accuracy gains.
- `2:57` — The shift to file systems and bash as the new industry focus, replacing "everything in context up front."
- `4:24` — Implementing progressive disclosure in Claude Code via Skills frontmatter and on-demand loading.
- `6:34` — Programmatic tool calling and the memory tool: plain markdown files, no embeddings.
- `7:19` — Experimental MCP CLI flag for tool-search directly inside Claude Code.
- `8:49` — Scaling to thousands of skills/MCPs via hierarchical, on-demand discovery.
- `11:41` — Claude automatically clearing old tool results as context limits approach.
- `13:31` — Conclusion: tools as files, loaded on demand, bash is all you need.

## Transcript
<details>
<summary>Full transcript</summary>

In this video, I'm going to be going over progressive disclosure within Claude Code. Now, one of the interesting trends that I've noticed over the past several months is a lot of AI infrastructure companies from Cloudflare, Anthropic, Vercel, Cursor, from products to model companies across the board are all arriving at the same conclusion independently, and that's in and around how to build AI agents. And honestly, it's not probably what we would have expected 6 months ago. In this video, I'm going to be touching on progressive disclosure, but I'm also going to be touching on bash and file systems generally. Now, this is going to be applicable to how you can use Claude Code, but you can also use this within other systems as well as how you can develop agents.

Right off the bat, I want to touch on this blog post that came out in September from Cloudflare, "Code Mode, the better way to use MCP." In this article, they basically describe that the way that we've been using MCP is completely wrong. And one of the ideas with this is when we load up the MCP directly as tools to the LLM, there are a number of different issues with that that actually come up. You might have those MCPs within context and then never actually use them. And one of the interesting things with this approach was actually converting MCPs to TypeScript. And the realization was effectively models are really good at writing code. They're not necessarily great at leveraging MCP. And essentially what this boils down to is what if we just had the model write the code, find the MCPs that it needs rather than having that all within the context.

And just a couple months later, Anthropic basically confirmed the same conclusion. They released some product features. This was something that really didn't get a lot of attention when it originally came out. Basically, the idea is instead of loading all of the tool definitions up front, the tool search tool discovers tools on demand. Claude only sees the tools that it actually needs for the current task. You can see the context window at the top here of the previous way using 77,000 tokens of context. And then below with the tool search tool, it only has 8,700 tokens. This represented an 85% reduction in token usage while maintaining access to your full tool library. And internal testing showed significant accuracy improvements on MCP evaluations when working with large tool libraries. Opus 4 improved from 49% to 74% and Opus 4.5 improved from 79.5% to 88.1%. The idea with this is if you only have the tools that you actually need or are using at the current time, that context window is going to work much more effectively.

And what was interesting with this is just last week Cursor also confirmed the same thing. Effectively, here's the exact same chart that I just showed you and they explain the efficiency gains that they do by doing this, but has reduced the total agent tokens by 46.9%. And the other thing that's really great with this is when you're putting those MCP tools within the context and you're not necessarily using them all the time, you're going to be spending an awful lot of money just sending in those requests for just if they happen to need them.

I think this paradigm basically been confirmed by enough heavy hitters within the industry that this is a good pattern to follow. And the interesting things with this is we went from the focus being in and around GPUs and now we're moving to an interesting area where I think sandboxes and file systems, at least the time of inference and when we're using these AI applications, is going to become increasingly the focus and effectively they all arrived at the same conclusion. Progressively disclose only what you need to the model when you need it. The industry trend in terms of how this is done is give agents a file system as well as bash and let them leverage those methods like being able to grep and glob and find all the different files that it needs and load them up only when it needs that.

Now in terms of MCP, now a lot of people have given it flak over time. I don't think it's going anywhere but in terms of the way that we're actually leveraging it, just like Cloudflare mentioned, that's going to be the biggest change. Instead of burning tokens and having all of these different servers within the agent context, whether it's within Claude Code, Cursor, or the agentic products that we're building, we're going to have a more effective way of how we're going to be managing MCPs. And honestly, in my opinion, it's a great protocol. A lot of people have adopted it. There's easy ways to deal with authentication and things like that depending on the services. There's a lot that's been ironed out. I don't think that's going away anytime soon. But I think the big trend that we're going to see is instead of having that tool schema sit within context, we're going to have a lot of those tools that would have otherwise live within context progressively disclose because there's going to be a lot of tools that you might only use one in 10 times for each turn of the conversation. For instance, maybe even less than that.

Now, in terms of the approaches for this, what's great with this is it's actually really easy to set up. Skills are the most obvious way to use this within Claude Code. You can set up a skill file. The front matter is going to be disclosed to the model. You're going to be able to have the description when the model actually invokes different things and you can move from really just 10, 20, 30, 100 tokens within the front matter and then have these skills where it will load the first file and then it can have references within that skill and progressively disclose within each skill and then also it can go and look through all of the different other skills that it has and similar thing, progressively disclose and only read those and load them up as prompts within context when needed.

The insight and the shift is really instead of just loading everything, burning all the tokens, having less room for actual work and degrading results of what the model is actually capable of doing — because say if the context is at 100,000 tokens of context, the results that you'll get where if it had maybe just 10,000, it's going to be much less. And we're moving to a way where we're going to be discovering things on demand, loading only what's needed. And the other great thing with this is we're going to have massive token savings, which means faster applications, cheaper applications, and overall better results. Agents, they need file systems and bash, and you can effectively get out of the way.

Now, the thing with this is it's really a different new architecture. I was actually uneasy with this type of idea initially, but the thing with it, I think that's really at the essence that makes this really nice is it's actually really intuitive, right? You can have these different files. They can progressively disclose. They can be within directories. They can encode this knowledge and that's the interesting thing with this pattern is you don't need to equip an agent with the knowledge of how to use a Postgres database or how to use this or that — every single agent out there knows how to use bash and once you know how to use bash you can update files, you can read files, you can use all of these different methods like skills which is effectively progressive disclosure, which is the same type of idea with all of this.

The insight that Cloudflare had was instead of generating JSON tool calls, generate TypeScript code that runs in a sandbox — the MCP server becomes a TypeScript API in isolated sandboxes. And the result that they found with this is a 98.7% reduction in token usage.

Back to the blog post with Anthropic. Now within advanced tool use, there were a few different things that they put out and they all sort of correlate to one another. They had the tool search tool, the programmatic tool calling as well as the memory tool. With programmatic tool calling, for instance, the way that this works, similar to what Cloudflare discovered, it will invoke the tools in a code execution environment. Then in terms of memory, these are file-based, simple markdown files. It was a similar idea within Claude Code. Something that Boris Cherny I've heard him mention where instead of having all of the embeddings and vector, just have that agentic search. It just felt better. It just works well. And I think if you've leveraged Claude Code, seeing how it reads different files, reads sections of files at times, that feels like a much better approach than all of the mechanics that go into a lot of these embeddings type of systems.

Next up, this is a little piece of alpha. Right now, there's an experimental MCP CLI. There are a couple ways this is changing at time of recording when I put this out. This might have actually changed to another flag. It could potentially be removed as they're working on it. This is something that they're actively trying out is how to get that tool search capability directly within Claude Code. Now, what you can do with this is instead of having all of that MCP within the context window of Claude Code, if you set this flag, you're going to be able to have the same tool search capability and instead of loading all of those tokens within context, you'll be able to have that same capability. Now, is it perfect? Is it right? I found it work quite well, but does it work quite as well as having the MCPs directly within context? I'm not entirely sure. So, this is still actively a work in progress, but if you want to try it out, it's a really simple flag within Claude Code that you can use if you want to try this out.

And the really wild thing with this direction is if you had a number of different MCP servers, that could easily add up into tens of thousands of tokens of context that was being directly passed to the model every single time. And this effectively brings it down to almost zero. Now, there will be a little bit within the system prompt in terms of how they actually make this work and those mechanics, but it really is orders of magnitude less context that you're going to be using from something like that.

And I think the big and exciting thing with this is all of a sudden we can be a lot more ambitious. We don't need to be bound by only being able to have 5, 10, 20 MCP servers and then all of a sudden the performance degrades within our application or within Claude Code. Now we can have thousands, tens of thousands, maybe even hundreds of thousands of skills or MCPs or whatever that is within a directory or within a system that's easily able to look up and find what it needs at time of when it needs it. And additionally, we can have hierarchical structures similar to skills — you can have a flat directory of all of the different skills, but you can also break it up into subskills. It can read different pieces and discover, okay, I need this reference that's within this skill file and go down the lineage and find what it needs.

There's a few different ways in terms of the architecture of this, but all in all, I think this is the paradigm shift that we're going through right now, like literally over the coming weeks and months where all of a sudden we're going to have applications that are going to have access to a ton more capabilities and work quite effectively through some of these strategies. And I think what's interesting with this — whether it's Anthropic within their web app they use sandboxes, now their sandbox products from Vercel, Cloudflare, Daytona, Lovable uses a form of sandboxes — all of these different sandboxes. What it allows us to do is to have these sort of ephemeral file systems where we can read and write to spin up little applications and then shut them down as needed.

I think this is going to be much more of the paradigm in 2026 for agentic development and how you can also leverage Claude Code. If you're leveraging Claude Code within the cloud, similar idea here, they're spinning up a sandbox. But what's interesting with Anthropic is within even Claude, the consumer-facing web app, you'll notice that it will also write to a file system for a lot of different operations. It will also write scripts as well for a lot of different features like if you're working with a spreadsheet or whatever it might be.

All in all, if we boil it down, MCP, file system, and code execution — that might be the answer, at least as it stands right now. Just to run through the pattern quickly on how you could use this within Claude Code. You have access to the file systems. It can read, write, search files. We've all seen it leverage that within the core methods. It has bash as well. Execute commands, run scripts, push things to git, whatever it might be. And then now what we can do is we can have code execution to call the MCP servers.

The idea and the mindset to think about is give the agent a file system and get out of the way. Tools become files, discovery becomes search, execution becomes code, and context remains small.

Next up, another interesting insight that Anthropic had was that Claude can automatically clear old tool results as you approach your limits. So, this is another interesting idea that instead of having and adding those all to context is you can progressively remove those from context as they might become less and less relevant.

Now, in terms of memory, I think the way to think about this is it's just files. This can be your claude.md. This can be different markdown files. This can be different scripts. This can be skills. It's nothing too complicated. There's no embeddings. There's no complex retrieval. Just keep it simple. We can read it. We can edit it. We can search it. Keep it simple. If it's simple for us, it's going to be simple for agents.

Now, how do we actually leverage this? So, I think it's with skills and progressive disclosure. So, within Claude Code, you can create a skills directory and you can put different skills that you have. It might be a web research skill. It could be a code review skill. Within that skill file, you can chain different references to different scripts, different markdown files. And that's going to be how you can have these different files where it will read and load up only at time of when it needs it. Effectively how it works, the agent will see the front matter of the skill and that's going to be what gets loaded within the static context. Say it's a web research skill, you could say okay within this skill I have Firecrawl or what have you within that skill and then the agent will only search and read that skill folder and load up all of the context that it needs when it actually needs it. So the idea with this is you're going to be able to scale to many more skills without that additional context bloat.

Okay. So all in all, I think you can now be more ambitious without context burn worries. Agents can tackle bigger tasks. Before we had to keep tasks a little bit small. We had to minimize tool use, watch for context limits, worry about it resetting, and now we can have things that can run for multiple hours, use potentially dozens or hundreds or maybe even thousands of different tool integrations. We can have these complex workflows without complex orchestration. If the system knows how to effectively look up for tools as well as skills, all of a sudden these systems become much more powerful and much more ambitious in terms of what we can build. We can build systems that potentially run for hours, run autonomously all of a sudden as a result of some of these new patterns.

Context potentially is no longer the bottleneck. If we can just offload context to memory to these different files, we can leverage the tool search capabilities. We can leverage the skill and progressive lookup capabilities. All of this combined is a really effective way to manage context. We can have a system that sort of has memory and working memory, can write helper scripts, can update skills. There's a ton that we can do by leveraging the file system and bash that I think is pretty exciting.

All in all, I think the trend is pretty clear. I think Cloudflare had a lot of really interesting ideas. Then Anthropic came out, Cursor, and now I think everyone is converging on, hey, this is actually a pretty good idea and pattern. It's a little counterintuitive, but it does work. And the industry is really converging in and around the same answer right now. Tools as files, loaded on demand, skills, progressive disclosure, bash is all you need. That's pretty much it for this video. If you found this video useful, please comment, share, and subscribe. Otherwise, until next one.

</details>
