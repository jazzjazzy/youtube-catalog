---
title: "The Last Claude Code Tutorial You'll Ever Need"
video_id: EHDzlot7LKU
channel: "[[channels/AI LABS]]"
uploaded: 2026-01-04
processed: 2026-07-06
duration: "8:43"
url: https://www.youtube.com/watch?v=EHDzlot7LKU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [context-engineering]
tools: [Claude Code, Git, Jira, Figma]
llms: [Claude Sonnet, Gemini]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# The Last Claude Code Tutorial You'll Ever Need

![thumbnail](https://i.ytimg.com/vi_webp/EHDzlot7LKU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=EHDzlot7LKU) | 📅 Uploaded [[uploaded/2026-01-04]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Instead of adopting a pre-made framework like BMAD or SpecKit, this video breaks down the underlying context-engineering principles every good Claude Code workflow actually relies on: progressive disclosure, structured external note-taking, managing the "attention budget" as context fills up, isolating work in sub-agents, choosing the right file format per task, using Git as a progress log, and reaching for slash commands and MCP only where they genuinely help.

**Watch this if:** you keep copying other people's AI-coding frameworks and they don't quite fit your project.

## Key Takeaways
- Pre-made frameworks (BMAD, SpecKit, etc.) often fail because they weren't built around your specific project — better to learn the underlying principles and build your own workflow.
- Context windows are smaller than they look in practice: Anthropic models have 200K tokens, Gemini models 1M, but past messages, memory files, tool definitions, and MCP calls all eat into that budget alongside your actual prompt.
- Progressive disclosure is the most important principle — reveal only what the model needs right now; Claude Code Skills are described as the embodiment of this (frontmatter tells the model when to use a skill without loading its full content).
- Use MCP only when external data access is genuinely required; use Skills for everything else — a common mistake is reaching for MCP servers for tasks that don't need them.
- Structured external note-taking (files the agent writes decisions, issues, and technical debt into) preserves critical context across compaction/context resets better than relying on the built-in compaction summary alone.
- "Attention budget": once context passes roughly 70% of the limit, models hallucinate more and start ignoring tools — manage this proactively via manual compaction, Claude's built-in rewind, or starting a fresh context per task, rather than letting auto-compact trigger at 90%.
- Sub-agents run in their own isolated context window and only return their output to the main agent, keeping tool-call/search noise out of the primary context — useful for research-style side tasks.
- File-format choice affects token efficiency: YAML (most efficient, good for schemas/configs) > Markdown (good for docs like CLAUDE.md) > XML (Claude-specific, good for tagged sections) > JSON (least efficient, use sparingly).
- Git commit history can double as a progress log for the agent across a project or task, and Git worktrees enable parallel sub-agent work; slash commands standardize repeated instructions (e.g. commit format, a "catch-up" command pointing the agent at external memory files).

## 🛠 Tools & Software
- [[topics/Claude Code]] — the primary tool used throughout to illustrate every principle: Skills, sub-agents, compaction, rewind, and slash commands.
- [[topics/Git]] — discussed as both version control (reverting problematic changes) and a context-engineering tool: commit history as a progress log, and worktrees for parallel sub-agent work.
- [[topics/Jira]] — cited as a use case for MCP: pulling ticket data directly so Claude Code can start implementing changes from a ticket.
- [[topics/Figma]] — cited as a use case for MCP: feeding Claude Code an app's style guide from Figma to drive design tasks the model's built-in capabilities can't handle alone.

## 🤖 LLMs Mentioned
- [[topics/Claude Sonnet]] — Sonnet 4.5 is cited for its built-in context-editing feature that tries to filter noise from the context window on its own using grep-style commands.
- [[topics/Gemini]] — cited for comparison, noting Gemini models have a 1 million token context window versus Anthropic's 200K.

## 📡 Protocols & Standards
- [[topics/MCP]] — discussed at length as the mechanism for pulling in external data (Jira tickets, Figma style guides); the video stresses using MCP only when external data is truly needed, not as a default.

## ✅ Action Items
- Build your own lightweight workflow around your project instead of adopting a framework wholesale — pull principles, not the whole package.
- Give agents explicit, narrow instructions (e.g. "check endpoints one by one") instead of vague broad ones that pollute context.
- Set up an external notes file for decisions/issues/technical debt so context survives compaction and resets.
- Watch your context percentage and manually compact or rewind before hitting ~70-90%, rather than waiting for auto-compact.
- Offload research-style side tasks to sub-agents so their tool calls don't bloat your main context window.
- Match file format to task: YAML for schemas/configs, Markdown for docs, XML for Claude-specific tagged sections, JSON sparingly.
- Set up slash commands for repeated instructions (commit format, "catch-up" context loading) and attach MCP servers only to the commands that genuinely need external data.

## 🔗 Related Videos
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Sonnet, Git, MCP
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Sonnet, Gemini, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Sonnet, MCP
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Sonnet, Git
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Sonnet, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Sonnet, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Sonnet, MCP
- [[videos/Claude Code (New Lazy-MCP Loading) They FINALLY FIXED the BIGGEST ISSUE of CLAUDE CODE]] — shared: Claude Code, Claude Sonnet, MCP

## Timeline
- `0:00` — Why pre-made frameworks (BMAD, SpecKit) often don't fit your project, and why you should learn the underlying principles instead.
- `0:39` — Context window basics: 200K (Anthropic) vs 1M (Gemini) tokens, and what actually fills that budget.
- `1:39` — Progressive disclosure as the core principle; Claude Code Skills as its embodiment; MCP vs Skills guidance.
- `2:47` — Structured external note-taking to preserve context across compaction and resets.
- `3:29` — The agents.md/CLAUDE.md pattern for guiding agents on how external files are structured.
- `3:43` — Attention budget: context over ~70% causes hallucinations and ignored tools; managing compaction proactively.
- `4:41` — Sub-agents running in isolated context windows for research-style side tasks.
- `5:29` — File-format token efficiency: YAML, Markdown, XML, JSON compared.
- `6:22` — Git as both version control and a context-engineering tool: commit history as progress log, worktrees for parallelism.
- `7:07` — Slash commands for standardizing repeated instructions (commits, docs, "catch-up" context loading).
- `7:58` — MCP use cases: Jira for tickets, Figma for style guides, attached directly to slash commands.

## Transcript
<details>
<summary>Full transcript</summary>

You already know about these AI coding frameworks like BMAD, SpecKit, and others. But these are not the only ones. There are hundreds of people experimenting and launching their own workflows. But when you try them out, you'll notice that they often fail to deliver on their promise. It's not because their methods are bad — it's because they don't fit your specific use case. When we build apps, the majority of the time we create our own workflows instead of relying on pre-made ones. This is because workflows should be built around your specific use case and only work if they align with the project you're trying to build. So how do you build a workflow for your own process? For that you need to know certain principles — these are the principles that every framework uses in one way or another.

Before discussing the main principles, it is essential for you to know what's inside the context window of these AI tools. It's really important, as managing context is basically what these frameworks do. The context window is basically the amount of information the model can remember at once. Anything that goes out of the model's context window goes out of its working memory and it has no way to recall it. Models have a limited context window — for example, Anthropic models have a 200K token context window and Gemini models have 1 million. Even though these might look like really big numbers in terms of the messages you send, they actually are not that huge, because in these AI tools, the context window does not only consist of your system prompt and user messages, but also includes a lot of other things like your past messages, memory files, tools, MCP calls, and so on. You need to learn how to make the most out of this limited working space so that when you build your workflows, the model does exactly what you want it to do. I will be using Claude Code as my primary coding tool throughout the video, but you can build your workflow with any platform as they all have the tools needed for these principles.

The most important principle and the key to any workflow design is progressive disclosure. That means revealing to the LLM only what matters and keeping the model's attention focused on what is actually needed right now, rather than filling the context window with everything it might need in the future. Now, more advanced models like Sonnet 4.5 have a context-editing feature built right in, where they can understand what's noise and try to filter it out on their own, and they use grep commands to narrow down what you want. But that alone is not enough — when we give vague instructions, even these newer models load a lot of things that are not needed and pollute the window. Instead of asking Claude to fix the error in your backend, it is better to ask it to check the endpoints one by one rather than asking it to fix everything at once.

The Skills feature in Claude is now open source and all tools can use it. Skills are pretty much the embodiment of progressive disclosure — their description provides just enough information for your AI coding platform to know when each skill should be used without loading everything into the context. A huge mistake people make is using MCPs for everything. You should only use MCPs when external data is required, and use Skills for everything else.

The second, equally important, principle is that information not needed right now should not belong in the context window. To achieve this, the tools use structured note-taking, and we can use this to our advantage by providing your AI tool with external files that it can use to document any decisions, issues, or technical debt. This approach allows your agent to maintain critical context that might otherwise be lost when building something really complex. These tools also have a compaction feature to manage the context window, and when the context resets, you don't have to rely solely on the compaction summary. For example, your agent can use these notes to gain context on what has already been done and what still needs to be done. This approach is particularly helpful for long-horizon tasks, which are inherently complex. You might be familiar with the agents.md — it's a standard context file that all agents read before starting the session. Some agents don't follow this and have their own, such as the CLAUDE.md, and I use them to guide the agent on how the external files are structured and what to write in each one of them.

Sometimes these agents randomly pause in the middle of a long-running task. A lot of the time this happens because the context has gone above 70% of its limit. This is where the concept of attention budget comes in. Your context window is what the model pays attention to while generating output. When it goes over 70%, the model has to focus more and there's a higher chance of hallucinations. In terms of AI agents, it stops them from using their tools effectively, and oftentimes they just choose to ignore them. To solve this, there are several built-in tools you can use. As you already know, compaction allows the model to start afresh with a proper summary of what has happened as the starting prompt and a reduced context window. So, instead of letting it fill up to 90% and triggering the autocompact feature, try to keep an eye on the context window and do it yourself. If you're experimenting, use Claude's built-in rewind so that you can delete the unnecessary parts instead of continuing them and asking Claude for changes. You should also clear or start a new context window for any new task so that the previous context doesn't slow down the model.

Another thing that stems from the principle of progressive disclosure is the ability of these agents to run tasks in the background without polluting the main context window. Sub-agents work in their own isolated context window and only report the output back to the main agent. This is particularly helpful when working on tasks that are isolated from each other, because your main context window is protected from being bloated with the tool calls and searches that the sub-agent makes, ensuring the information remains in its dedicated working zone. Since these agents run in the background, you can continue interacting with your main agent and let it work on something that actually requires your attention. Whenever I want something researched, such as the rules of a new framework that I'm working with, I just use these sub-agents. This way their tool calls and searches are isolated and they just return the answer to the main agent.

If you understand the principle of note-taking, you should also know which file format to use for which task. Since these files have different formats, they affect the token count and hence the efficiency of your workflow. YAML is the most token efficient, so I mainly use it for database schemas, security configs, and API details — its indentation helps models structure information properly. Markdown is better for documentation like your CLAUDE.md, because the heading levels make it easy for the model to navigate between sections. XML is specifically optimized for Claude models — Anthropic states that their models are fine-tuned to recognize these tags as containers and separators, which is useful when you have distinct sections like constraints, summaries, or visual details. Other models generally prefer Markdown and YAML over XML. And lastly, JSON — it's the least token efficient because of all the extra braces and quotes, so I only use it for small things like task states and don't really recommend using it for the most part.

Git is one of the most basic things you're taught when starting programming. We've seen another trend with these context workflows in which people actually use the git commit history as a reminder to the model of the progress that's been made, whether across the whole project or on a single task. Even if you don't want to use it to store progress, you should generally use these context-engineering workflows in a git-initialized repository. Having a context-engineering workflow means that you don't allow the model to do everything at once, but instead act on planned steps one by one. If at any stage you encounter a problem, Git lets you control which version to revert to and helps in evaluating which change is causing problems. People have also implemented parallelism with Git worktrees — I've also shown plenty of workflows where sub-agents work in dedicated worktrees for parallel work.

Whatever workflow you end up making, there are always going to be cases where you end up repeating instructions for common procedures. A good example is how you ask the AI tools to do git commits or update your documentation. In almost all of these AI tools, there are ways to reuse your most repeated prompts. I often use custom slash commands in my own projects because they basically give Claude a reusable guide. For example, I often use a "catch-up" command that contains instructions on how I structure memory outside the context window, so Claude knows how to catch up with the project instead of reading every file. They are also good at enforcing structure — for my commits and documentation to follow a defined format, I use a "commit" command that follows a specific structure for how it should write commit messages and what pre-commit checks it should make before committing. This way, the slash commands keep everything standardized and I don't have to instruct Claude again and again to perform tasks the way I prefer.

As you know, MCPs should be used whenever external data is required. Jira is the most widely used team-management software — if you want to get information from tickets, you can use the Jira MCP, so it can access tickets directly and start implementing changes. Similarly, I use the Figma MCP to provide Claude Code with the app's style guide, which it then uses to construct the design for tasks where the model's built-in capabilities fall short. MCPs are essential for interacting with external sources efficiently. You can include these MCPs directly in your slash commands so that they become part of your whole workflow.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching, and I'll see you in the next one.

</details>
