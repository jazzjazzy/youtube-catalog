---
title: "Convert Any MCP Server to Code Execution (Template)"
video_id: Fg8VHXr-WVM
channel: "[[channels/Arseny Shatokhin]]"
uploaded: 2025-11-12
processed: 2026-07-06
duration: "11:28"
url: https://www.youtube.com/watch?v=Fg8VHXr-WVM
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [mcp-token-optimization, mcp-code-execution-pattern]
tools: [Cursor, Claude Code, Codex, Notion, Google Drive, GitHub, Agency Swarm, Agencii]
llms: []
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Convert Any MCP Server to Code Execution (Template)

![thumbnail](https://i.ytimg.com/vi_webp/Fg8VHXr-WVM/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=Fg8VHXr-WVM) | 📅 Uploaded [[uploaded/2025-11-12]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A build-along implementing Anthropic's "MCP code execution" pattern: instead of loading every MCP tool's full description into the agent's context, each tool gets written out as code the agent discovers and reads on demand via a Python/shell sandbox — cutting token usage dramatically. The demo builds a sales-ops agent (Google Drive MCP + Notion MCP) two ways — direct MCP and code-execution — deploys both, and compares real token costs: 32k tokens for direct MCP vs. 12k for code execution, dropping to just 4k once the agent saves and reuses a self-generated "skill."

**Watch this if:** you're burning excessive tokens on MCP tool definitions and want a concrete, reusable template for converting any MCP server to Anthropic's code-execution pattern.

## Key Takeaways
- The core problem: directly wiring MCP servers into an agent loads every tool's full schema/description into context up front, even for tools never used in a given task.
- The code-execution pattern instead has the agent write/discover tool code in a code execution tool (IPython interpreter + persistent shell) that reads one tool file only when needed — so the agent's context only ever holds the tool it's actually using.
- Using a starter template with special commands ("MCP code execution," "add MCP," "write instructions"), the coding agent (Cursor in the demo) scaffolds a server directory with per-tool code files for each linked MCP server (15 tools generated for Notion MCP, 4 for Google Drive MCP) instead of passing raw tool descriptions into context.
- Provide MCP server credentials up front — the demo hit a Google Drive auth failure mid-build because credentials weren't set before testing.
- Writing agent instructions matters as much as the architecture: the agent is prompted to always check a persistent "mount skills" folder first, use an existing skill if one matches the task, otherwise read only the one tool file it needs, then propose a new reusable skill afterward.
- Live comparison on the same task (copy a meeting transcript from Google Drive into a Notion page): the direct-MCP agent manually retyped the entire transcript into its context, burning ~32,000 tokens; the code-execution agent completed the same task using a fetch-tool call for ~12,000 tokens.
- The agent can self-improve: after completing the task, it proposed and saved a new reusable "skill" to the persistent mount directory; re-running the same prompt in a fresh chat then reused that skill and dropped token consumption to just ~4,000 tokens (~10x less than the first run).
- Verdict: the pattern is production-ready but reliability-sensitive — models aren't trained on this pattern yet, so prompting must explicitly describe the workflow, or the agent will over-call tools, read unnecessary files, and run code more times than needed. Best reserved for sophisticated agents (analytics, research, operations) rather than simple ones like customer support, where the added complexity isn't worth it.

## 🛠 Tools & Software
- [[topics/Cursor]] — the IDE used to build both agents via the starter template's special commands (create agent, MCP code execution, add MCP, write instructions).
- [[topics/Claude Code]] — mentioned as an alternative coding agent to Cursor for building the same template (just tag the relevant workflow/command files in the prompt).
- [[topics/Codex]] — mentioned alongside Claude Code as another alternative coding agent that can be used instead of Cursor.
- [[topics/Notion]] — the CRM in the demo; wired in as an MCP server (15 generated tool files) that both agent variants read from/write meeting transcripts to.
- [[topics/Google Drive]] — the source of meeting transcripts; wired in as an MCP server (4 generated tool files) for both agent variants.
- [[topics/GitHub]] — hosts the starter template and the resulting agent repo, which is pushed and then deployed from.
- [[topics/Agency Swarm]] — the multi-agent framework/starter template used to scaffold both the direct-MCP and code-execution sales-ops agents.
- [[topics/Agencii]] — the deployment platform used to host and run both agent variants for the live token-cost comparison, including built-in tracing/dashboards.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — the video's entire subject: converting standard/direct MCP server integration into Anthropic's token-efficient "code execution" pattern, compared side-by-side on token cost.

## ✅ Action Items
- Before wiring up an MCP server this way, gather all required credentials/auth up front rather than mid-build.
- Use a "write instructions" step that explicitly tells the agent to check a persistent skills folder first, use a matching skill if found, otherwise read only the one tool file needed, and propose new skills afterward.
- Compare token costs directly (via your framework's tracing/dashboard) between a direct-MCP agent and a code-execution agent on the same task before committing to the pattern.
- Reserve the code-execution pattern for sophisticated, multi-step agents (analytics, research, ops) rather than simple ones like customer support, where the added complexity isn't worth it.
- Let the agent save self-generated skills to persistent storage and re-test the same task in a fresh session to confirm token savings compound over repeated runs.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor, GitHub, MCP
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/The Fastest-Rising Repo on GitHub Is a Little Scary REA]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, GitHub, MCP, Notion
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude Code, GitHub, MCP, Notion
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude Code, GitHub, MCP, Notion
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Cursor, GitHub, MCP

## Timeline
- `0:00` — Recap: MCP code execution reduces token consumption ~98% vs. direct MCP.
- `0:45` — Demo setup: a sales-ops agent (Google Drive MCP + Notion-as-CRM MCP) built from a starter template.
- `1:35` — Creating the base agent with code-execution tools (IPython interpreter, persistent shell) via Cursor.
- `2:17` — Using the "MCP code execution" command to convert linked MCP servers into per-tool code files.
- `3:40` — Cursor generates 15 Notion tool files and 4 Google Drive tool files; Google Drive auth issue surfaces.
- `4:07` — Writing agent instructions: check skills folder first, read only needed tool files, propose new skills.
- `5:30` — Testing the code-execution agent locally against a Notion page.
- `6:03` — Deploying both agent variants (direct MCP vs. code execution) to Agencii.
- `6:33` — Live task: copy a transcript from Google Drive into Notion; agent saves a new reusable skill afterward.
- `8:00` — Testing the direct-MCP agent on the same task — it manually retypes the full transcript.
- `8:36` — Token-cost comparison via tracing dashboard: 32k (direct MCP) vs. 12k (code execution) vs. 4k (with saved skill).
- `9:35` — Conclusion: production-ready with careful prompting; best for sophisticated agents, not simple ones.

## Transcript
<details>
<summary>Full transcript</summary>

In my last video, I showed a new method proposed by Anthropic called MCP code execution. This technique is the future of building AI agents because it reduces token consumption 98% while giving your agents way more autonomy and flexibility to evolve their own skills. In this video, I'll build this live with you step by step. I'll compare this new approach with the old direct MCP method and give you the final repo plus a template to convert any MCP server to this new pattern. At the end, I'll also share whether this is actually ready for production or not. Before you watch this video, make sure you watch the previous one to fully understand all the theory behind this new method. Let's dive right in.

So the agent that we will build today is the sales operations agent from Anthropic's blog post that can read meeting transcripts and then attach them into your CRM without actually reading the contents of the file. The architecture for this agent is pretty simple — it's just one agent with this code execution tool that connects to Google Drive MCP and Notion MCP, because our CRM is in Notion.

So in order to get started, you need to copy our starter template, which will now contain a new special command to use this new pattern. Make sure to set visibility to private, and then open this repo in Cursor. I'll be building this in Cursor, but you can also use Claude Code, Codex, or any other AI coding agent that you prefer. The only thing you need to do if you're not using Cursor is to simply tag this workflow file and the command files that we'll be using in the prompt.

So I'm going to start simple and just tell Cursor to create a sales ops agent with two built-in tools: an IPython interpreter and a persistent shell tool. The reason we need these two tools is because the agent must be able to actually discover local files and then run them in Python in order to use this new approach. Both of these tools are already available in our framework. Let's hit send and wait until the agent is built. Now I'm also going to tell it to add another "sales ops direct MCP" agent for comparison later. By the way, if you're building a more sophisticated MVP, there is also a new PRD command which you can use to have more control over your agent structure.

Okay, now here's where the magic happens. I added a new special command called "MCP code execution," which you can use to add MCP servers to an agent using this new pattern. So all you need to do in order to use this is simply tag this command and then tell Cursor which MCP servers to use. I recommend finding the exact MCP servers you need on GitHub or elsewhere and then adding links back into Cursor. Now simply hit send again.

This command already describes to Cursor pretty much everything it needs to know about this new pattern, and even links the blog post and all the other resources it might need. This way Cursor can reliably add it using the same structure proposed in the blog post. You can see how Cursor created the server directory with the code for our servers, and then proceeds to creating the code for individual tools. You might also need to authenticate the server if it's using OAuth. Now it proceeds to creating files for individual tools — this server is made here directly in code instead of passing this description and the arguments directly into the agent's context window. Cursor saves this description in code, so then whenever our agent needs to use this tool, it will simply read this file and then see the whole description and arguments in order to use this tool. This way, again, we don't load all the tools — we only load one tool that Cursor actually needs to use.

Okay, so in total Cursor created 15 tools for the Notion MCP server and 4 tools for Google Drive. It has also already tested the Notion MCP server; however, it wasn't able to test Google Drive because of missing credentials. So make sure you provide all the credentials up front — do not repeat my mistake. Typically you can find instructions on how to get the credentials inside the README of your MCP server. Then you can simply tell Cursor to retest the server, and you'll also be required to authenticate.

Okay, now the next step is to write instructions. For writing instructions, I also recommend you use this "write instructions" command and then simply tag the agent you want to create the instructions for. Then Cursor is going to ask you a few questions to properly define the context for your agent — make sure you answer these carefully, and the most important one is the process and workflow. Prompting is key with this technique, and in order for this agent to use it effectively, it must clearly understand the process.

So basically the first step is to always check available skills in the mount skills folder — I'll explain why the mount folder later — then it should use the skill if such a skill is found for a specific task; if no skills are found, it should only read one tool that it needs to use, and after that it should combine all such tools in order to complete a task successfully, and finally provide suggestions for new skills to be added. You can play around with this workflow — this is just a general process from the blog post, but I think there are a lot of innovations just from prompting the agent. Let's hit send.

In the meantime, I also want to add MCPs using the direct MCP approach to the other "sales ops direct MCP" agent. For this we also have a command, it's simply "add MCP," and I'm also just going to link the two MCP servers that we added to the previous agent.

Okay, now we are ready to test this agency. Let's open it in terminal and just run `python agency.py`. Now let's perform a simple test — let me ask it what's on this Notion page. So first the agent listed the mount skills directory, then it read the fetch tool file to understand all the parameters, and it seems like it ran into some issues with the imports. However, then at the end I was still able to read this page by performing this fetch tool request, and it provided me with a preview of this file.

Okay, now the next step is to deploy this agent and then we'll compare it with the direct MCP approach. So let's push our changes to GitHub, and now let's go to Agencii — hit create new agency, and then find this new agent repo. Then provide your keys from the .env file, and now let's wait until our agency is deployed.

Okay, so now our agency is deployed, so let's actually test it. Let me put it in a custom GPT — let's select both agents and let's deploy it. Now let me send this task from Anthropic's blog post: to copy the transcript from Google Drive and paste it into a page in Notion. Let's see if it's actually going to be able to do it.

Seems like it did read way too many files — for example, it even read this server file, which it definitely doesn't need. And now finally it tells me that it was in fact able to do this — let's check the Notion page. And yes, indeed, we now get this transcript from our Q&A call exactly like it was on Google Drive. And also at the end, it proposed to create this new skill for itself. So let me tell it to save the skill — you can see that the agent told me that it saved the skills in the mount skills directory.

So the reason you need to use this mount directory is because we now have persistent storage on our platform, and without this feature it would not be possible to allow your agents to evolve and build their own skills over time. So in this mount directory, essentially, your agents can now save files like this and reference them across different chats. So now if I start a new chat and then send the same prompt again, the agent should take a lot less time and just use the skill in order to do this task quickly. You can see how now it found the skill and read the file, and the agent was able to still perform the same task.

Okay, now let's quickly test another agent that uses the direct MCP approach. So now you can see how this agent is reading this whole transcript with the G Drive read-file tool, which hopefully is not going to cost me too much, and it also read the Notion page, and now it's trying to add this transcript to this Notion page. But as you can see, it has to manually type this whole thing, which is definitely going to cost me too much now. So you can see how it's literally spending like probably tens of thousands of tokens for no reason, simply because it had to do one simple copy-paste operation. Finally, it's finished.

So now let's take a look at the traces and analyze the costs. Tracing is enabled by default in our framework, and in order to see the traces, all you need to do is go to the dashboard and simply find the name of your agency. Okay, so let's see this "sales ops direct MCP" agent — in total this agent consumed 32,000 tokens. This is just insane, and most of these tokens aren't even input tokens — it's also a lot of output tokens, which are extremely expensive. And with this new approach, the amount of tokens is only 12,000, which is a lot less, although it's still quite a bit. I think the reason this still consumes so many tokens is because this agent, as you can see, just performs way too many unnecessary tool calls. But I do think it's completely possible to optimize it with more prompting. And when the agent used one of the existing skills, it only consumed 4,000 tokens to perform the same task, which is now around 10 times less.

So in conclusion, I believe this approach is extremely powerful, but as they say, with great power comes great responsibility. While I was definitely able to reduce the token consumption from the intermediate tool outputs, the agent still consumed more tokens than it should have when calling the tools — it executed code way too many times, it read way too many unnecessary files, and it just took too long to perform a simple task on the first attempt. However, the agent was still able to save a lot more tokens compared to the old direct MCP approach. Additionally, it was even able to self-improve by creating a new skill, which cut down the number of code executions in subsequent runs.

So my final verdict is: yes, this approach is ready for production, but it requires proper prompting — prompting here is key. While the LLMs aren't trained for this new method yet, you have to carefully describe how to use this new pattern, otherwise they're going to make a lot of mistakes. But if you do it right, and I'm sure many of you will, with this repo, the benefits far outweigh the costs. You get way more autonomy and flexibility with only a minor drop in reliability. So yes, this is the new paradigm — just let your agents run the code. We no longer have to create these abstractions on top of other abstractions, because agents can just generate the code to do whatever they need by themselves.

However, don't use it for simple agents like customer support — save it for more sophisticated general agents like analytics, research, or operations. For simple agents, it still doesn't make sense. And when you're ready to deploy this, check out our platform, because infrastructure overhead is actually the biggest downside of this approach, and we're the only platform on the market that supports everything you need to run this out of the box. More advanced AI agent templates are coming on this channel soon.

</details>
