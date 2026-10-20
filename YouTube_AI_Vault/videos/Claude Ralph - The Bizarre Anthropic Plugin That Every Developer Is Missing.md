---
title: "Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing"
video_id: ny_BAA3eYaI
channel: "[[channels/Better Stack]]"
uploaded: 2025-12-30
processed: 2026-07-06
duration: "4:24"
url: https://www.youtube.com/watch?v=ny_BAA3eYaI
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [autonomous-coding-loop, long-running-agent-tasks]
tools: [Claude Code, Ralph Loop, Amp, Python, TypeScript, Bun, Beads]
llms: [Claude, Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing

![thumbnail](https://i.ytimg.com/vi_webp/ny_BAA3eYaI/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=ny_BAA3eYaI) | 📅 Uploaded [[uploaded/2025-12-30]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Anthropic turned Geoffrey Huntley's "Ralph" technique — repeatedly re-feeding an agent the same prompt until it signals completion — into an official Claude Code plugin built on the stop hook instead of a raw bash loop. The video explains the technique's origins, shows how Anthropic's version works (completion promise, max iterations, state file), and demos converting a Python script to TypeScript with passing tests.

**Watch this if:** you want to let Claude Code grind autonomously on a well-defined coding task (e.g. a rewrite, a TDD loop) without babysitting it, and want to understand the safety knobs (completion criteria, max iterations) before turning it loose.

## Key Takeaways
- The "Ralph" technique, named after Ralph Wiggum, was created by Geoffrey Huntley as a simple bash while-loop: give an agent a prompt, wait for its response, then feed it the exact same prompt again.
- Real-world results cited: an MVP delivered for under $300 in agent costs versus an estimated $50,000 for a contractor; six repos shipped overnight during a YC hackathon (including a full Python-to-TypeScript rewrite of browser-use); a new programming language built from scratch in under three months.
- Anthropic's official Claude Code plugin reimplements Ralph properly: instead of an external bash loop, it uses Claude's stop hook, which fires when Claude finishes a turn, checks a state file for an active loop, and — if the configured completion promise (e.g. "done" or "complete") hasn't been produced — re-triggers the same prompt.
- You invoke it with a slash command, supplying your prompt, a completion promise, and an optional max-iterations limit to cap runaway cost.
- Demo: converting a Python audio-delay script to TypeScript, with a prompt.md instructing Claude to write passing tests; Claude iterated until the rewritten script ran correctly and generated bun-based tests.
- Best practices: use clear, unambiguous completion criteria (not "make it good"), break complex tasks into incremental steps, and avoid using it for tasks requiring human judgment.
- The presenter suggests pairing Ralph with a tool like Beads to supply incremental steps and keep the loop on track.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI where the official Ralph plugin runs, invoked via a slash command with a prompt file, completion promise, and max-iterations flag.
- [[topics/Ralph Loop]] — the video's central subject: Anthropic's stop-hook-based implementation of Geoffrey Huntley's original bash while-loop technique for re-prompting an agent until a completion signal appears.
- [[topics/Amp]] — shown briefly as another agent CLI the original bash-loop version of Ralph was demonstrated with, alongside Claude Code.
- [[topics/Python]] — the source language of the demo script (a mic audio-delay tool) being rewritten.
- [[topics/TypeScript]] — the target language Claude rewrites the demo Python script into.
- [[topics/Bun]] — Claude generates tests for the rewritten script using Bun's test module.
- [[topics/Beads]] — mentioned as a tool the presenter would like to pair with Ralph to supply incremental steps and keep it on track.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — runs inside Claude Code for the Ralph demo (rewriting the Python script and writing tests).
- [[topics/Claude Opus]] — cited as an example of an expensive model where uncapped Ralph iterations could produce a large bill, motivating the max-iterations flag.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try the Ralph plugin in Claude Code on a well-defined task (e.g. a language rewrite) with an explicit completion promise like "done".
- Set a max-iterations limit before running Ralph with expensive models like Opus to avoid runaway cost.
- Write clear, incremental completion criteria rather than vague goals, and avoid using Ralph for tasks needing human judgment.

## 🔗 Related Videos
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, Claude Opus, Ralph Loop
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, Claude Opus, Ralph Loop
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, Claude Opus
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, Claude Opus, Ralph Loop
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus

## Timeline
- `0:02` — Intro: Ralph Wiggum-inspired Claude Code plugin that re-runs a prompt until the task is done.
- `0:33` — Origin story: Geoffrey Huntley's original bash while-loop technique.
- `1:15` — Real-world results: $300 MVP vs. $50K contractor quote, six repos shipped overnight at a YC hackathon, a new programming language built in under 3 months.
- `1:56` — How Anthropic changed Ralph: built on Claude Code's stop hook instead of a bash loop, using a state file and completion promise.
- `2:41` — Demo: converting a Python audio-delay script to TypeScript with passing tests via Ralph.
- `3:25` — Max-iterations flag explained as a cost-control safety mechanism.
- `3:49` — Best practices: clear completion criteria, incremental steps, avoid tasks needing human judgment; idea to pair Ralph with Beads.

## Transcript
<details>
<summary>Full transcript</summary>

This is Ralph Wigum, arguably the dumbest character in the Simpsons that has become the inspiration for a clever Claude's code plug-in designed to run Claude through the same prompt over and over again until it's actually done, even if it keeps failing. Naive and relentless persistence. Perfect for lazy models that give up too early and don't complete the task. But why did Anthropic even create this? And won't this cost a lot of money since it's running the same prompt again and again? Let's find out. And before we do, don't forget to hit subscribe.

Now, before I get into using Ralph with Claude code, you need to understand where the idea came from because it's pretty weird. Goat farmer Jeffrey Huntley, who I don't think is an actual goat farmer, but that's beside the point, came up with a technique earlier this year he called Ralph, which is essentially an infinite bash while loop that takes a prompt, gives it to an agent, then waits for the response, and gives the agent back the exact same prompt again. So, this is what it looks like to run a prompt with AMP, and this is what it looks like to use with clawed code. It's simple, but very powerful because if you give the agent a clear completion criteria and a completion signal, you can essentially leave it running overnight and wake up to a completed task.

Jeff spoke about this technique at a talk and an engineer used it with lots of agents to deliver, review, and test an MVP for under $300, whereas it would have cost him $50,000 to hire a contractor. And during a YC hackathon, the repo mirror team used it to ship six different repos overnight, one of which was a complete rewrite of browser use from Python to TypeScript, which made the founder smile. It was also used to create a brand new programming language from scratch in under 3 months, which let's just say is not a language I plan to use anytime soon.

But if you think the Anthropic team wrote a oneline bash script and turned that into a plug-in, you'd be very wrong because the team have done a lot of work to properly integrate it into claude code. The way it works is you type the Ralph slash command, give it your prompt at the completion promise, which can be complete or done, and you can also add a max iteration, which we'll talk more about later, and it uses this information to create a state file when it starts running. But instead of relying on a bash loop, it uses the clawed stop hook, which you can learn all about in this video. But essentially, the stop hook usually runs when clawed code has finished a task, and in this case checks for any active loops by passing the state file, reads the latest output, and if it can't find the completion promise, it triggers Claude to run the same prompt again. So Claude will go back, look at the code it's produced, and improved it based on the prompt if it's missed anything out.

Let's go through a quick demo. This is a Python script I use to delay audio from my mic when I'm recording. And if I wanted to convert this Python script to TypeScript, I can use Ralph with my prompt and D file and give it a completion promise of done. I'll hit enter to let it go to work. And usually if I run this in a coding agent without Ralph, the agent will complete the task and will generate some code for me, but part of the code won't work. But luckily, inside my prompt MD file, I've told it to write passing tests. So hopefully it will write tests and run those tests on the script until they pass. Let's fast forward this process. And now if we run the script, we can see it's running correctly detecting my audio devices. And everything is written in TypeScript just like I asked it. It's even generated some tests using the bun test module.

Now this is all good if you're on a super expensive clawed plan or have deep pockets if you're using API based pricing. But if you want to use an expensive model like Opus and don't want to wake up to a huge bill, then this is where the max iterations flag comes in useful. This prevents infinite loops by stopping iterations at a number set by you. So each time the stop hook triggers Claude to rerun the prompt, it increments the max iterations number and will stop when it hits the number specified.

But this isn't the only thing to consider when using the Ralph plug-in. You also have to use it with clear completion criteria. So don't say make it good or make it pretty. If you have a complex task, break things down into incremental steps and also don't use it for tasks that require human judgment. Personally, I think it would be great to pair Ralph with something like beads, which will give it incremental steps and will make sure it stays on the right path. But you may have also noticed we're less than 10K away from hitting 100K subscribers, which is absolutely amazing. So, if you haven't done so already, go ahead and hit that subscribe button.

</details>
