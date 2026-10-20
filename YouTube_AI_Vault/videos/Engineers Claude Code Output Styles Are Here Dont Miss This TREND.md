---
title: "Engineers… Claude Code Output Styles Are Here. Don't Miss This TREND"
video_id: mJhsWrEv-Go
channel: "[[channels/IndyDevDan]]"
uploaded: 2025-08-18
processed: 2026-07-06
duration: "31:49"
url: https://www.youtube.com/watch?v=mJhsWrEv-Go
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [generative-ui-agent-output, multi-agent-status-tracking]
tools: [Claude Code, Cursor, ElevenLabs, Ollama, Firecrawl, uv, Aider]
llms: [Claude Opus, Claude Sonnet, GPT-OSS-20B]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Engineers… Claude Code Output Styles Are Here. Don't Miss This TREND

![thumbnail](https://i.ytimg.com/vi/mJhsWrEv-Go/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=mJhsWrEv-Go) | 📅 Uploaded [[uploaded/2025-08-18]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> IndyDevDan initially dismissed Claude Code's new Output Styles feature as useless, then discovered it enables real generative UI: an agent-generated HTML output style produces a working, styled HTML guide on every response instead of plain text. He pairs this with custom status lines (built on hooks and simple JSON session state) to track multiple parallel Claude Code instances, then argues that two other new features — Opus-plans/Sonnet-builds mode and background bash commands — push Claude Code away from being an unopinionated engineering primitive.

**Watch this if:** you run multiple Claude Code instances in parallel and want a concrete look at output styles (including generative UI) and custom status lines for tracking agent state.

## Key Takeaways
- Output styles change Claude Code's system prompt to control response format — six built-in styles include default, table, YAML, ultra-concise, text-to-speech summary, and HTML/generative UI.
- The ultra-concise style noticeably reduces input/output token consumption; the YAML style imposes a highly structured response that the presenter found often outperforms other formats.
- The HTML output style is framed as "the one output format to rule them all": Claude Code generates a real, styled HTML file on the fly and opens it — the first genuinely useful application of generative UI, not a gimmick.
- A custom "genui" output style (built on the HTML style) was demoed generating on-the-fly HTML guides, TypeScript interfaces, and Pydantic classes across multiple parallel Claude Code instances running different models (Sonnet, Opus) and different prompts, including a Firecrawl-powered Hacker News sentiment-analysis research task.
- Output styles only change the prompt — one of the three fundamental levers of any agentic system (context, model, prompt) — which is why the presenter frames this as a core principle of AI coding, not a one-off trick.
- Custom status lines (paired with Claude Code hooks and a simple JSON-based session-state system) show the current model, last prompt(s), and an agent-generated name — making it far easier to track what's happening across several concurrently running Claude Code instances.
- One status-line variant used a local Ollama model (GPT-OSS-20B) running on the presenter's MacBook purely to generate a one-word name for each agent session, with a 5-second timeout fallback.
- The presenter criticizes two newer Claude Code features — Opus-plans/Sonnet-builds mode and background bash command management — as a "slight overreach," comparing the plan/build split to Aider's older architect mode, and argues Claude Code should stay an unopinionated primitive rather than prescribe how models and background tasks are managed.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the video's subject: output styles (table, YAML, ultra-concise, text-to-speech, HTML/generative UI) and custom status lines are demoed across multiple parallel instances.
- [[topics/Cursor]] — used briefly to edit the status-line configuration files/settings.
- [[topics/ElevenLabs]] — the text-to-speech engine an output style triggers to summarize an agent's completed work as audio.
- [[topics/Ollama]] — runs a local GPT-OSS-20B model on the presenter's MacBook to generate short agent names for the status line.
- [[topics/Firecrawl]] — used inside a demoed agent prompt to research and summarize the top 5 Hacker News posts.
- [[topics/uv]] — cited as part of the demo codebase's technical stack ("Astral uv").
- [[topics/Aider]] — referenced as the original AI coding tool that pioneered a plan/architect + build two-model prompt chain, used as a comparison point for Claude Code's new Opus-plan mode.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — used for planning in the new Opus-plan mode and demoed generating YAML-formatted, generative-UI responses.
- [[topics/Claude Sonnet]] — used for the "build" step in Opus-plan mode and shown generating HTML output alongside Opus.
- [[topics/GPT-OSS-20B]] — run locally via Ollama to generate short one-word agent names for the custom status line.

## 📡 Protocols & Standards
- [[topics/MCP]] — referenced when a generated TypeScript interface is based on MCP server definitions already present in the agent's system prompt/context.

## ✅ Action Items
- Try switching Claude Code's output style to HTML/generative UI (`/output-style`) and compare the resulting on-the-fly HTML guide against a default text response for the same prompt.
- Build a custom "genui" output style layered on the HTML structure for your own recurring tasks (docs, guides, breakdowns).
- Set up a custom status line (via a `user-prompt-submit` hook and simple JSON session state) that tracks the current model, last prompt, and an agent-generated name across multiple parallel Claude Code instances.
- If running many Claude Code instances at once, use the ultra-concise or YAML output styles to cut token usage or improve structured-response quality.
- Consider whether prescriptive features like Opus-plan/Sonnet-build mode fit your workflow, or whether you'd rather manage model selection and background tasks yourself.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Aider, Claude Code, Claude Opus, Claude Sonnet
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Code, Claude Opus, Claude Sonnet, GPT-OSS-20B
- [[videos/Elite Context Engineering with Claude Code]] — shared: Claude Code, Claude Opus, Firecrawl, MCP
- [[videos/I Tried the Open Source ElevenLabs Alternative (Voicebox)]] — shared: Claude Code, Cursor, ElevenLabs, MCP
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Claude Sonnet, Cursor
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP

## Timeline
- `0:00` — Intro: six Claude Code output styles run against the same prompt across six instances.
- `1:48` — Walkthrough of default, table, YAML, ultra-concise, and text-to-speech output styles.
- `4:26` — The HTML output style explained as "the one format to rule them all" — real generative UI.
- `5:22` — Building a custom "genui" output style via `/output-style` on top of the HTML structure.
- `7:32` — Parallel multi-agent demo: Firecrawl Hacker News research, TypeScript interface generation, Pydantic class generation across Sonnet/Opus instances.
- `14:15` — Status line feature introduced — tracking model, working directory, and git state.
- `16:03` — Status lines combined with hooks and JSON session state to show last prompt and generated agent name; local Ollama/GPT-OSS-20B used for naming.
- `23:18` — Controversial features: Opus-plan/Sonnet-build mode and background bash commands, compared to Aider's architect mode.
- `26:45` — Feature breakdown: how output styles (system prompt) and status lines (hooks + JSON state) actually work under the hood.

## Transcript
<details>
<summary>Full transcript</summary>

Engineers. Here we have six Claude Code instances. In each instance we have six unique output styles: default, table format, YAML format, ultra concise format, text-to-speech summary, and most importantly, HTML format. For every agent with every style, we have one prompt.

Honestly, when I first saw the output styles feature drop, my first thought was, "This is useless." But I never let my initial reaction prevent me from doing the real work and understanding the feature. After a quick dev session, I learned just how useful these output styles are. Never bet on your first initial reaction without doing the work.

"Dan, I've explained how to add new hooks to your Claude Code setup with examples and configuration steps." So, you can hear our text-to-speech format summarize the exact work that was completed. We can see our results starting to flow in here. We're going to break down every one of these output formats. Believe it or not, this feature release marks the beginning of viable generative UI. The Claude Code team is on a generational hot streak, shipping valuable features back to back to back. But there are two features I'm not a fan of because they could take the tool in the complete wrong direction. We'll talk about that in this video. Right next to the output styles drop, we also have the status line feature that lets you customize your Claude Code interface. And I can guarantee you, you're not using this feature to its full potential yet.

Default, table, YAML, ultra concise, text-to-speech, HTML. New features are only valuable in relation to existing features. In our first Claude Code instance, you can see the default response for the following prompt. We asked `/quest`, how can I add a new hook? If we look at this response format, you can see it's the default Claude Code response format, but now we have full control over the output style of Claude Code. If we switch to our table output format, you can see something very different. We have clean formatted tables helping us speed up the flow of information between us and our agents. You can see this is a valuable format for organizing information.

Now we get to my second favorite output format, YAML. At first, this format might seem kind of weird and kind of out of place, but the YAML output format actually has a really interesting way of organizing information in a highly structured way. I found that this specific Claude Code instance typically outperforms the rest. Why might that be? The YAML format provides a highly structured, informational way to get responses out of your Claude Code instances.

So, next up, we have the ultra concise format. This format is the most similar to the default Claude Code response, but it's going to be concise and just give you enough information. I've also found that the ultra concise response format reduces the number of input and output tokens that Claude Code consumes.

Next, the text-to-speech format. In the beginning, you heard after our agent completed its work, it communicated exactly what it's done. Okay, so you know in the system prompt it has the instructions: whatever command you just ran, summarize it. So I asked it to run that audio summary again. It ran it and then it ran an audio summary on the audio summary.

Okay, so that's fantastic. But there is one output format that is more important than all of them. We have the HTML format. This is the most important output format of them all. Let me explain why. This is the one output format to rule them all. At first, you might be thinking, "Dan, this is stupid. This is super hard to read. There's no way I'm going to actually get information by reading HTML." You know, we're talking 10 to hundreds of responses per day as we're doing real engineering work with Claude Code, with agent coding tools. Let's slow down and really think about what's happening here. We have dynamic, accurate HTML generation our agent is generating on the fly. What you're looking at here is the first useful application of generative UI. With a few tweaks to this prompt, we can create a new output style that enhances the information rate between us and our agent.

Let me show you exactly what I mean. Let's fire up a brand new Claude Code instance, `/output-style` to update the style, and then we're going to hit "genui." What you just saw was format eight — this our HTML structure. This prompt builds on top of the HTML layer. Let's fire this off and let's run that exact same prompt that we ran before. `/quest`, how can I add a new hook? And what you're going to see here is nothing short of extraordinary. With output styles, with Claude Code, our agent can build UI on the fly. Now, I'll create a comprehensive HTML guide explaining how to add a new hook to Claude Code. On every response, our agent is going to generate UI and respond to us in this rich way.

Okay, check this out. How to add a new Claude Code hook. Okay, let's see exactly what happened there. It wrote to a temporary file. It opened it at the end of the response and it generated an HTML guide for us. This is generative UI. This is not a gimmick. This is yet another powerful agent-coding tool, a powerful agent-coding pattern you now have in your toolbox. With every request, we can now have our agent generate UI for us. This is generative UI. And you can see here we got a great breakdown on exactly how to add this. It's got consistent, simple themes and styles. This is insane, right? And then we have project structure, right? It's really breaking down how we can add a Claude Code hook. We even have some next steps. We have files referenced. Here we have UI that was generated on the fly for us. This is HTML — it's the language of UI, and of course Sonnet and Opus can generate this for us with no problem. Okay, it does take a little more time to generate the response, but you can see how powerful this can be.

Let's run some more of these. Output style genui, output style genui. Here we're going to generate a TypeScript interface. Here we're going to do some research with Firecrawl — we want to see the top five Hacker News posts, break down the sentiment. I'm going to update the model here, switch to Opus, and this is going to be in that YAML format. Create a Pydantic class for the Claude Code hook output structure. All right, so we're going to run that. Now we have multiple agents running on our behalf getting work done for us.

All right, check this out. Here's our Hacker News sentiment analysis. We can quickly validate this: "the future of large files in git is git." If we just search this, you can see there's that 453 points — that looks right. This is quite fascinating. There's a new paradigm to operate in. You can see the points on the side there. We are getting the top five posts on Hacker News right now of this date. We have a temp file getting generated for us on the fly. Here's another one — we have that TypeScript interface get generated. Here's a summary of the work done, task completed, overview. It created this new types file for us based on the JSON structure in this file. Clean, simple write-up, right, detailing exactly what was done. Preconfigured variables. You can see here's the interface hierarchy, just giving us a breakdown of what this looks like. We can of course open up this codebase, just search for types — there it is. If we look at the MCP JSON sample, this exact type right here. And it looks like it typed it out nicely for us here based on the other MCP servers it has in its system prompt.

And here's our last request here, wrapping up: CC generate Claude Code hook models. So based on all the output types from our hooks, look at this incredible UI, right? Every time it runs, it's generating UI for us. You can imagine pushing this further, adding a layer on top of this where we can interact back and forth. You can imagine a layer where Claude Code itself, the terminal interface, is actually presenting us with generated terminal user interfaces and letting us interact with that. There are really no limits to this capability. We have truly the first useful application of generative UI — us interacting with our agents, our agents giving us specific responses. This is all based on our output style system prompt.

Okay, this feature is ultra powerful. I'm almost embarrassed to say that I thought this was not useful. This is ultra powerful, and I think that probably even the Claude Code engineers haven't really realized this capability, or where this could go — they have now because they're watching this video. What's up, Anthropic engineers, Claude Code engineers — thank you, you guys are doing incredible work here, but this is really extraordinary, right? This is the power of the primitive that is Claude Code. This is the power of stacking up the right feature set, putting together the right tools, and most importantly, understanding the fundamentals of AI coding and what's actually happening under the hood of the agent. All this does is it updates the prompt. The output style — they say it here, right? I'm really happy that they're being really clear about the fundamental unit that this is updating. The output styles update the system prompt.

As viewers of the channel know, there are only three key elements of every agentic system: context, model, prompt. If you master these, if you understand these, you can move from tool to tool to tool, to idea to idea to idea, at light speed, because everything is built on this. This is a principle of AI coding, a principle of the generative AI age. When you combine this with some tools, you get some really extraordinary things.

Okay, so before we move on to how output styles work, let's talk about status lines. As you can see here, I have a pretty bare-minimum status line. A lot of the status lines you've probably seen so far are like vibe coding — it's the lowest hanging fruit. When you combine hooks and a simple state management system, your status lines can become tremendously more valuable. Let me show you exactly what I mean.

Here we have a simple minimal status line: model, current working directory, git branch plus the changes uncommitted, or Claude Code version. This is simple, mostly static information. Let's update our status line to use a new format. I'll open up Cursor, go to my settings here, we'll search for status line. If we open up our folder structure here, I have a dedicated status-lines directory with four versions giving us different status-line outputs. Let's update to v2 and let's see exactly what this looks like. Now we have model and no recent prompt. So you can see exactly where this is going, right? I'll say "hi." We now have our most recent prompt in the status line.

So who cares, why is this important? If you follow this channel, you probably are running more than one Claude Code instance at any time. Just like AI coding is not enough, one agent is not enough. As soon as you start using powerful agent coding tools like Claude Code, there are only two directions to go: better agents or more agents. Output formats help us with better agents; status lines help us with more agents.

Open up a new terminal window, fire up Claude Code, let's go YOLO mode in Opus. Let's update our output style just for fun — we'll use text-to-speech summary. This is a great format when you have multiple agents and you're working in parallel doing a lot of work, long-running tasks. You can put on text-to-speech and when your agent finishes, it'll respond back to you. Here's the kicker: this says "hi." I can say "who's investing the most in AI data centers" — just any prompt. And you can see here we have a brand new last-executed prompt. Now, on its own, not very useful, but when you're switching instances all the time, this becomes very useful. If you're really pushing this tool, you've likely opened up three, five, ten instances of it and you're prompting all the time. So it becomes very helpful to have this last-prompt status line to remind you what is going on.

When you combine just a little bit of state with Claude Code hooks with the status line, you get a really powerful capability here that builds on your agent coding tool. We have emojis based on whether we're asking a question or creating new code. "Claude, create a compressed README based on this README" — we have the create keyword there, an information-dense keyword, and now our recent prompt shows a light bulb because it's creating or updating something new. "I've analyzed your Claude Code hooks mastery codebase. It's an advanced toolkit for extending Claude Code with hooks, sub-agents, and custom behaviors." We got that text-to-speech response — useful for interacting with multiple agents. This kind of replaces our stop-hook text-to-speech response that we've been using in previous videos. Now with output styles, we can have our agent run a tool every time it finishes; in this case, the tool happens to be ElevenLabs text-to-speech.

Output styles in combination with status lines increase the information rate between ourselves and our agents. And when you push this further with something like a compressed README that cuts 650 lines down to 150 while keeping all essential information, you get generative UI. Here's another generative UI response for that question I asked about data center investments — Claude Code did some research and created a breakdown for us. Clear winner here for AI data center: OpenAI Stargate, 500 billion over four years. A great breakdown — again, generative UI, my agent just put this together for me, with a little timeline.

Now, I have these four windows open, doing a lot of work in parallel. I can cycle through these and know exactly what was going on. Let's go to status line v3, and I'll leave v4 for you to experiment with. Let's fire up Claude once again, run Opus with permissions. The new flow here is: set my output format, let's set a YAML structured format, and search for that new compressed README — what does this codebase do, read only this file. Our status line updated with a name for our agent. Opus is a little bit better at formatting YAML. We have a great YAML-based response: overview, core functionality, eight life cycles for controlling Claude Code, sub-agents, meta agent, custom features — status line, output formats, technical stack (Astral uv), use cases, key innovations. And our status line has the last prompt and an agent name — another tool to scale your agents.

In this status line v3, we now have trailing prompts — historic trailing prompts, the most up-to-date, and the second-to-last prompt we ran. As we're interacting with agents more and more as engineers, the key value proposition is increasing the information rate between you and your agent, between you and the work you're trying to do.

I did mention there are a couple features I'm not as happy about coming out of the Claude Code team. Let's quickly talk about those. `/model` Opus plan mode. When you submit a prompt, Claude Code is going to plan with Opus and then build with Sonnet. If you've been with the channel a while, this feature might make you think of Aider, the original AI coding tool. Aider was one of the first AI coding tools to really leverage language models — this is traditional AI coding, not agent coding, there are no tool calls happening in Aider. Aider was one of the first tools to build out an architect mode; this was innovative because they used a prompt chain, two prompts with two models. Aider separated thinking and building — we had already talked about prompt chaining on the channel around this time.

Why do I have an issue with this? Why is plan/build, architect/builder, something I have beef with? The power of Claude Code lies in its flexibility, control, and simplicity. As the creator Boris said, Claude Code is a primitive — an engineering primitive. This feature feels like a slight overreach to me, along with the bash background commands. To me, it feels like the beginning of loss of directional focus. They should let the engineer decide on the models, how they're used, the planning, the building, and things like background task management, bash controls.

I can simplify what I'm trying to say further: don't tell me how to use the models, don't tell me how to manage my bash commands in my background processes. This is something I always watch out for with every tool, especially the leading tool. I have a guiding question that helps me determine if a new feature is valuable or if it should even exist: in the generative AI age, we always have to keep track of the context, model, and prompt every step of the way. The leading question is, do I know exactly what the context, model, and prompt are at every step of the process in whatever tool I'm using? Any feature that obscures this, or inserts an opinion about how you or I should manage the big three, throws up a huge yellow, orange, red flag to me.

To be clear, both of these features are useful — Opus-plan/Sonnet-build is quite a useful feature, I'm not saying it's not valuable, but you can build a great feature that is directionally incorrect for your product, for your mission, for your stated engineering philosophy. Maybe this is just me — let me know what you think about this. Do you think that Opus plan mode and background commands are a slight overreach from Claude Code, from the team? Is this the right set of features they should be building out? I think this is the first sign of things going a little off course, but maybe I'm overanalyzing, being too detail-oriented. Let me know in the comments if you like this direction from Claude Code, separate from the individual features themselves. Again, I'm not saying background bash commands and Opus plan aren't valuable features.

So with that aside, you can see here that output styles and the status line increase the information rate between you and your agent. So let's quickly understand how this works. These are very simple features which I absolutely love — the Claude Code team is keeping it simple. If we open up Claude, open up output styles, you can see we have all of these output styles detailed here: bullet points format, HTML structure, markdown, and of course the genUI. This codebase is going to be available to you, link in the description.

So that's genUI. You can see how this works and tweak it to make it your own. You can see we have that key workflow step for these agentic workflows where we want our agent to take actions back to back to back. This is a great place to get a high-level breakdown of what the prompt does exactly. So that's that HTML structure and TTS, it's all there.

If we close that, we can focus on our status lines. I've created a dedicated folder for this — output styles is an Anthropic-specific directory, status lines is something I created just for organizational purposes, just like the data directory here. You can see in the status-line directory, the only thing you need to focus on is main — we read in the line, we generate whatever status line you want using whatever data you want, but most importantly, we're just printing it. That's it, that's how status lines work. And to run this specific status line, all you need to do is add this to your `.claude` settings file.

If we open up v3, you can see something really cool in combination with our Claude Code hook. If we look for user prompt, and open up these files side by side, we are managing session data. So every Claude Code prompt makes a contribution to our agent-specific data — we have this new `.claude` data directory, and if we open up one of the sessions, you can see we have information about that particular session that we can update, write to, and read from: session ID, agent name, prompts. This is how we're populating our agent name and our prompt history, and we can keep prompting. This is all because we have a simple state management system — again, just JSON objects, super readable, very understandable. In the user-prompt-submit hook, we're combining these two features to get more value out of them. Prompts append; if we don't have an agent name, we're doing something really awesome. If you remember from our GPT-5 nano agents video, we were running GPT-OSS 20 billion — here we're doing that exact same thing. If we open up `ollama.py`, we're having a powerful on-device model right on my MacBook generate unique names for our agent. This is a super simple, great use case for these agents — generating a one-word name. This is prompt engineering 101, that's it. The agent has 5 seconds to generate this or it falls back, and this is how we update state for our status lines.

What you're seeing here, all these features you've seen in this video, are essential ideas of what you can do with output styles. You can take this further and combine, merge, and add conditional branches directly in your output-style system prompt to direct which output type your agent uses based on the prompt at hand. This is what makes Claude Code so great — it's a new primitive of engineering, the engineer's agent that's increasingly customizable and so far, so good, very unopinionated. This is key: it's not a dedicated solution, this is what we as engineers need to solve any problem we face. And this is why again I feel like the plan mode and the bash command is starting to look like a slight overreach of this principle of being an unopinionated, simple engineering primitive. Tell me what you think about that, drop a comment down below. This codebase is available to you, link in the description. No matter what, stay focused and keep building.

</details>
