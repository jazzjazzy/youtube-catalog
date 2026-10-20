---
title: "Claude Code Skills Just Got Even Better"
video_id: RAZVk5NPNtE
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-03-05
processed: 2026-07-05
duration: "16:15"
url: https://www.youtube.com/watch?v=RAZVk5NPNtE
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [skill-authoring-and-testing]
tools: [Claude Code, Skill Creator, VS Code]
llms: [Claude, Claude Opus, ChatGPT]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Skills Just Got Even Better

![thumbnail](https://i.ytimg.com/vi/RAZVk5NPNtE/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=RAZVk5NPNtE) | 📅 Uploaded [[uploaded/2026-03-05]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Anthropic updated its official Skill Creator skill so Claude Code can build, evaluate, benchmark, and trigger-tune skills much more reliably. The video explains the difference between capability-uplift and encoded-preference skills, walks through evals/benchmarks/trigger tuning, then live-builds a "YouTube weekly roundup" reporting skill from a one-shot prompt, iterating twice based on feedback.

**Watch this if:** you build or maintain Claude Code skills and want a repeatable way to test, benchmark, and improve them instead of guessing whether they still work.

## Key Takeaways
- A skill is just a plain-text "recipe" (instructions) that Claude reads to perform a task consistently — readable by anyone, not code.
- There are two skill types: capability-uplift skills (teach Claude to do something it's weak at, like front-end design) which can go stale as base models improve, and encoded-preference skills (sequential, workflow-like, personal to you) which stay durable since future models won't be trained on your specific process.
- Anthropic's official Skill Creator skill packages best practices for creating, modifying, and measuring skills, replacing the need to manually read Anthropic's lengthy skill-authoring PDF.
- Evals let you feed example outputs you want, then have the agent test prompts against your skill and optimize it — useful both to catch regressions (skill gets worse as models change) and to spot growth (skill becomes unnecessary as models improve).
- Benchmarks report pass rate, time, and token usage with vs. without a skill loaded, giving concrete evidence of the uplift a skill provides.
- Trigger tuning analyzes a skill's description against various natural-language prompts and rewrites it so Claude calls the right skill more reliably, reducing false triggers and misfires.
- The live demo shows a one-shot, intentionally vague prompt producing a working skill + PDF report on the first try, then two rounds of feedback (data accuracy, deeper research) tightening the output using the project's existing scripts and agents.
- Anthropic's stated direction is that eventually a plain natural-language description of what a skill should do may be enough for the model to figure out the rest — reducing the need to spell out steps, rules, and format.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent used throughout to install the Skill Creator plugin and build/run the new YouTube weekly roundup skill.
- [[topics/Skill Creator]] — Anthropic's official skill for creating, evaluating, benchmarking, and trigger-tuning other skills; installed via `/plugins` and used to drive the entire demo.
- [[topics/VS Code]] — the editor the presenter is working in while running Claude Code for the demo.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying Claude Code and all the skill-building/evaluation throughout.
- [[topics/Claude Opus]] — discussed specifically (as Opus 4.6, with hypothetical Opus 5) to illustrate why capability-uplift skills can become obsolete as the base model improves.
- [[topics/ChatGPT]] — appears as a topic inside the generated report's key takeaways ("fill the ChatGPT to Claude migration" content gap).

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install the official Skill Creator plugin via `/plugins` in Claude Code and ask it to explain what skills you already have.
- Classify your existing skills as capability-uplift vs. encoded-preference to know which ones need periodic re-evaluation as models change.
- Run an eval/benchmark on a skill you rely on to see its pass rate, time, and token usage with vs. without it loaded.
- Use trigger tuning if you have many skills and notice Claude misfiring or failing to call the right one from natural language.
- Try building a new skill with a deliberately vague one-shot prompt, then refine it with two rounds of specific feedback like the video demonstrates.

## 🔗 Related Videos
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, Claude Code, Claude Opus
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, Claude Opus, VS Code
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude, Claude Code, Claude Opus, VS Code
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, Claude Opus, VS Code
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Claude Opus, VS Code
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude, Claude Code, VS Code

## Timeline
- `0:00` — What is a skill: a plain-text recipe Claude reads to perform tasks consistently.
- `0:52` — Two types of skills: capability-uplift vs. encoded-preference, with examples and why they age differently.
- `3:27` — Anthropic's official Skill Creator skill: what it does (create, modify, measure, optimize skills).
- `4:23` — Evals explained: testing a skill against example outputs to catch regressions and spot growth.
- `6:15` — Trigger tuning: analyzing and rewriting a skill's description so it's called more reliably.
- `7:47` — Installing the Skill Creator skill via `/plugins` in Claude Code and verifying it's active.
- `8:44` — Building a new "YouTube weekly roundup" skill from a deliberately vague one-shot prompt.
- `12:24` — First result reviewed and critiqued (design good, data inaccurate); second iteration requested with deeper research.
- `14:18` — Final output: a much more accurate, in-depth weekly roundup PDF report built in about 20 minutes total.

## Transcript
<details>
<summary>Full transcript</summary>

Claude skills just got 10 times easier to build and stronger to use. So in today's video, I'm going to explain exactly why that is and then I'm going to live build a completely new skill right here in front of you guys.

So real quick, what is a skill? It's basically just a recipe. So that when you ask your agent to make you for example a LinkedIn post, it will read the recipe and it will get it right every single time. And when I say recipes, I literally just mean text. It's just text instructions, it's like a prompt.

So what did Anthropic actually do that made all these skills better? They updated their skill creator skill, which is literally a skill that teaches Claude how to build, test, measure, refine, just make all the skills better and better and better. First, there are two different types of skills. We have a capability uplift skill, which basically is a prompt — it teaches Claude how to do something better, for example design websites with a front-end design skill or run Excel formulas. And then we also have encoded preference skills, which means Claude already understands each of these pieces, but it needs to follow them in a specific order — these are more like actual workflows.

Capability uplift skills might fade over time because, for example, right now we're on Opus 4.6 — what if Opus 5 drops and default Opus 5 is better at front-end design than Opus 4.6 with the front-end skill? At that point you might just need to retire that skill completely. But with an encoded preference skill, these will probably stay pretty durable and accurate because the process is very specific usually to you, which future models won't be trained on.

Now, with this new skill creator skill, which is an official Anthropic skill, we can actually evaluate them. It creates new skills, it can modify and improve existing skills, it can measure skill performance. Anthropic has done things before like dropping a 33-page PDF walking through fundamentals, planning and design, testing and iteration, distribution and sharing, patterns and troubleshooting — pretty thorough. So you could either take time and learn this, or just give your agent the skill creator skill, and all that information's already in there.

Evals let your agent actually evaluate the quality of your skill and then make improvements. Give your agent tons of examples of really good outputs you want, and it will look at your skill, test out some prompts, compare it to the outputs, and optimize your skill for you. There are two reasons we need evals: to catch regressions (as the model evolves it might use the skill worse, an early signal you need to evolve your skill) and to spot growth (a model might do a better job without a skill at all, at which point you can archive it). We can also run benchmarks — when a model updates or you iterate on a skill, run the evals and get a pass rate, time, and token usage, side by side with and without the skill loaded.

The final piece is skill trigger tuning. Once you've got a project filled with 10 or more skills, you might get false triggers or misfires — you wanted it to use a skill and it used the wrong one, or didn't use any at all. Using trigger tuning, the skill creator analyzes your skill, tests different prompts you might use to trigger it, and edits the description so that skill gets called more accurately.

And what I think is really cool, and how I want to end this section before the live demo: Anthropic themselves say, "Over time, a natural language description of what the skill should do may be enough, with the model figuring out the rest." I really think that word "may" should actually be "will." Today, when we're telling our agent to build skills or giving it an SOP, we're giving it steps, rules, and format. But in the future we're going to be able to just tell it in high-level natural language what we want, and it's going to figure out the rest and get there with a spec.

All right, so I am in my Herk 2 project, which is kind of just my personal assistant in Claude Code, and I'm going to show you guys how we can actually get the skill installed. Whether you're in VS Code, which is where I am, or in the terminal, or desktop app, you just need to do /plugins. Click on manage plugins, search for skill-creator, and there's the official one. Click install — you can install for just you, for your project, or locally. I'm going to install it for the whole project, then restart Claude Code. I verify it by asking, "Hey, do you have the skill creator skill? What does it do?" and it confirms.

So I'm going to switch on to plan mode and see if it can build us a new skill. I said: "I need you to create a skill called YouTube weekly roundup, where at the end of every week, you will look at the videos that I made that week, analyze the comments, analyze the views, engagement, and give me a PDF report on all of the insights, the strengths, weaknesses, threats, opportunities." I kept this pretty vague intentionally to see what it comes back with, since most people using skills right now are executives and operators, not engineers — they're good at explaining what they want but not the technical nitty-gritty.

It came back and asked some clarifying questions — a rolling 7-day window, report sections, and to use the brand assets in my folder for the PDF style. It came back with a plan, and I accepted a one-shot prompt to see what the skill could do. In its to-do list, the last step was to run the test and iterate with the skill creator eval process. It created everything, rendered an HTML template as an actual PDF, and I found the file in my projects folder — logo, weekly roundup, three videos published, some view/like/comment stats, an executive summary. But glancing at it, the data didn't look correct, and the SWOT analysis and competitor context sections were empty.

So I cleared the context (it had used 62%), went back into plan mode, and gave honest feedback: aesthetically it looked great, but the data was all wrong — I needed it to actually look at how it's scraping YouTube channel data, comments, and competitor videos so real data goes into the report. It sent back some raw JSON data it had found from my channel, but it wasn't in-depth enough — exactly what we'd talked about earlier: right now it's our job to explain clearly that we want granular comment analysis, what's working for others in the space, and trending videos, then use that to figure out strengths, weaknesses, opportunities, and threats.

While that ran, I looked at what it had actually built — in .claude/skills, the YouTube weekly roundup skill.md has YAML up top (name, description, disable model invocation false, argument hint), context, channel benchmarks, an optional focus, and step-by-step instructions calling a "fetch YouTube data" script. In my scripts folder there's prepare data, render report, and it reused a script I already had in the project instead of creating a new one — a great example of why using a project and a skill more makes both stronger.

It came back with another detailed plan ending in an audit with the skill creator, and I fired it off. It refreshed channel data, used three agents in parallel, prepared the report, populated the data, and rendered the PDF. The result: quick hits like top competitor move and biggest opportunity, seven videos published with more accurate stats, an executive summary with real takeaways (doubling down on certain title styles, a dedicated tutorial idea, filling the ChatGPT-to-Claude migration content gap), per-video breakdown including a video published an hour earlier, a two-page SWOT analysis, top comments and audience signals, competitor context across several channels, and what's trending in AI that week. All of this was built in about 20 minutes, and from here the plan is to keep running it and giving feedback so the skill creator keeps improving it.

</details>
