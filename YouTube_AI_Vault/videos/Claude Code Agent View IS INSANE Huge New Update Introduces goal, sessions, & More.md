---
title: "Claude Code Agent View IS INSANE! Huge New Update Introduces /goal, sessions, & More!"
video_id: -jINRoST0mk
channel: "[[channels/WorldofAI]]"
uploaded: 2026-05-12
processed: 2026-07-05
duration: "10:49"
url: https://www.youtube.com/watch?v=-jINRoST0mk
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [ai-agent-session-management, autonomous-coding-workflows]
tools: [Claude Code, Codex]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Agent View IS INSANE! Huge New Update Introduces /goal, sessions, & More!

![thumbnail](https://i.ytimg.com/vi_webp/-jINRoST0mk/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=-jINRoST0mk) | 📅 Uploaded [[uploaded/2026-05-12]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Anthropic shipped a major Claude Code update: Agent View, a centralized dashboard for managing multiple concurrent Claude Code sessions; a new `/goal` command (modeled on OpenAI Codex's own goal feature) for persistent, outcome-based autonomous execution; plus background sessions via `/bg`, a `/radio` lo-fi coding station, and quieter, smarter prompt compaction.

**Watch this if:** you run multiple Claude Code sessions at once and want a single dashboard to track, peek into, and reply to them, or you want autonomous "run until done" execution instead of step-by-step prompting.

## Key Takeaways
- Agent View (research preview) gives one unified dashboard showing every active Claude Code session, whether it needs input, and whether it's completed — accessed via the left arrow from any active session.
- You can peek into a session's latest turn and reply inline without leaving your current workflow, or press enter to jump fully back into the transcript.
- `/bg` moves an existing session to a background/autonomous run, or `Claude bg <task>` launches a brand-new background session directly, skipping the foreground entirely.
- Suggested use cases: dispatching multiple coding tasks in parallel and returning to completed PRs, long-running "PR babysitter" or dashboard-updater agents, and rapid peek-mode switching between active sessions — though the presenter is skeptical this meshes with Claude Code's existing usage limits.
- `/goal` introduces persistent, outcome-based execution: you define a completion condition and Claude keeps working across turns autonomously until it's met, working in interactive sessions, plan mode, remote control, and even Claude Code Mobile (so you can kick off an overnight task from your phone).
- Anthropic distinguishes how different modes decide when to stop: `/goal` waits for a specific outcome, loop-based runs use time intervals, stop hooks wait on external scripts/conditions, and normal chat waits for user input each turn.
- Prompt compaction is now silent (no more explicit "context trimmed" alerts) and improved to better preserve sensitive instructions and user intent during long sessions, reducing context drift.
- The presenter's closing take: he likes Agent View but remains frustrated with Claude Code's usage/rate limits, which he says is pushing him and others toward OpenAI Codex.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI coding agent receiving all of these updates: Agent View, `/goal`, `/bg` background sessions, `/radio`, and improved prompt compaction
- [[topics/Codex]] — OpenAI's coding agent, referenced as the direct inspiration for Claude Code's new `/goal` feature and named as where the presenter (and others) are shifting due to Claude Code's rate limits

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Try Agent View's left-arrow session list to monitor multiple concurrent Claude Code sessions from one place.
- Use `/bg` or `Claude bg <task>` to kick off long-running autonomous work (e.g., a PR babysitter) without tying up a foreground terminal.
- Define a clear completion condition and try `/goal` for tasks you'd rather not micromanage turn-by-turn, including from Claude Code Mobile for overnight runs.
- Note that Agent View and `/goal` are research-preview features currently limited to Pro, Max, Team, Enterprise, and Claude API plans.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Codex
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, Codex
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Codex
- [[videos/Agent memory resolved]] — shared: Claude Code, Codex
- [[videos/Claude Code (New Lazy-MCP Loading) They FINALLY FIXED the BIGGEST ISSUE of CLAUDE CODE]] — shared: Claude Code, Codex
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Codex
- [[videos/I Open-Sourced My Own AFK Software Factory]] — shared: Claude Code, Codex

## Timeline
- `0:00` — Introduction: a massive wave of new Claude Code features
- `0:49` — Agent View: a centralized dashboard for managing every Claude Code session
- `3:38` — How Agent View works: left-arrow session list, inline peek/reply, background sessions via `/bg`
- `5:15` — Use cases: parallel PR dispatch, PR babysitters, dashboard updaters, peek-mode switching
- `6:59` — `/goal`: persistent outcome-based execution, including Claude Code Mobile support
- `8:46` — `/radio`: Claude FM, the built-in lo-fi coding radio station
- `9:10` — Prompt compaction: now silent, better preserves sensitive context and user intent
- `10:01` — Wrap-up: praise for Agent View, frustration with rate limits, shift toward Codex

## Transcript
<details>
<summary>Full transcript</summary>

It's been quite some time since we last covered Anthropic's Claude Code, and they have recently dropped a massive wave of new features. From Agent View, which gives you a centralized place to manage all of your Claude Code sessions, to a new slash goal feature that works almost like OpenAI's Codex slash goal system. Now, you also have an improved compaction prompt system that helps preserve sensitive context and reduces loss of user intent during long-running sessions. There's a lot more to unpack here, and honestly, some of these updates push Claude Code even further into the fully agentic development space. So, let's dive into it all. To start things off, let's take a look at the new Agent View feature inside Claude Code, which was just launched today. This is one of the biggest workflow updates that they have added so far because it basically turns Claude Code into a centralized agent management system, instead of just a terminal-based coding assistant. Right now, it's launching as a research preview, but the idea is actually pretty powerful. You now have one unified dashboard that is showing every active Claude Code session in real time. And with Claude agents, you can dispatch multiple coding sessions simultaneously without each one taking over an individual terminal tab. Each agent keeps running independently in the background while you manage everything in a single interface. And honestly, this starts pushing Claude Code closer to becoming a full agent orchestration environment rather than just becoming a coding CLI tool. You can instantly see which agents are actively working, which ones are waiting for user input, and which tasks are fully completed. You can also jump in and out of sessions without losing context, reply inline to unblock an agent, and manage multiple long-running workflows at the same time. For developers that are running complex agentic coding tools, this is a massive quality of life upgrade to Cloud Code, and it is super helpful.

So, how this works is actually pretty interesting. Agent View is essentially going to improve how you visualize and interact with Cloud Code sessions within the CLI, and it first starts off by having it see everything at once. This is by pressing the left arrow from any active session or running Claude agents in your terminal as a command. You can then view all of the different agents. This gives you a unified list of all the different running Claude sessions, showing you whether the agent actually needs your input, and if it does, you can essentially just right-click onto it or click enter, and you can then provide the latest response to it. And that way, it will also display all of your last interactive sessions as well, and then it will be able to let you interact with other agents within this list. Next, you also have the ability to peek into sessions and reply without leaving your current workflow. This is by selecting a session preview on the latest turn, and if the agent is waiting on a decision, you can answer inline and immediately continue execution. And if you want to fully jump back into a workflow, you can press enter and it attaches you directly into the full transcript. And finally, what you also have is having Claude support fully background sessions. This is with any existing workflows that could be moved into agent view using the slash bg feature, or you can skip the foreground entirely with Claude bg and then add in your task, and this is to instantly launch a fresh, autonomous session running in parallel.

Now, you may ask, how can you actually use this feature? Well, early users that Claude have reported are using it to scale multiple concurrent Claude code sessions at once. This is by dispatching different ideas and workflows in parallel while returning later to fully completed pull requests ready for review. Now, I kind of doubt that cuz you all know Claude code limits are atrocious, and I don't know how this is going to help with that cuz you have multiple agents now running simultaneously that are going to eat up so many tokens. So, I don't know how truthful this is, but regardless, if you do have the ability to pay for your own API and pay for tokens as you go, it is something that could be used for long-running autonomous agents like PR babysitters. Or, you can have it for dashboard updaters. You can even use this new feature for looping background jobs with upcoming runtimes visible directly in the interface that we had showcased. And since you can quickly jump between sessions using simple and arrow navigations, you can also use the peek mode. And that is where you could rapidly switch between coding tasks, quick code-based questions, and then active workflows without losing context, while also tracking which session successfully shipped the PR. And just remember, this is a research preview feature and it's only available for pro, max, team, enterprise, and Claude API plans. Now, if you are to go into Claude code and you are to use the Claude agents manned within Claude code, it is going to list out an agent preview of all the live sessions right now. So, in this case, I don't have anything, so it's not going to be able to showcase all of them, but it would be able to list out all of them directly within your session.

Next up is one of the biggest additions to Claude code in this recent update, which is the slash goal feature, which similarly copies what Codex is doing with its own slash goal feature. This basically introduces persistent outcome-based execution directly inside Claude code. So, instead of manually prompting the model every single step of the way, you can now define a completion condition, and Claude continues working across multiple turns autonomously until that goal is fully achieved. And what's really interesting is that it works everywhere, including interactive sessions with the plan mode, and even remote control. This is with all of these different workflows where you can set the slash goal feature. So, the agent is no longer just waiting for constant user interactions after every single step. It is something that will be functioning across all of these different approaches. Now, what's also great is that Anthropic has also allowed it to actually be accessible through Claude Code mobile. This means that you can actually start a long-running autonomous task from your phone, give Claude an objective, and then you can leave it overnight, and then come back to see whether the agent was successful and if it was able to complete that workflow. Now, Anthropic has also explained that there is workflow process for Claude Code that can determine when it should continue execution versus when to actually stop. This new goal feature is going to wait for the specific outcome to be achieved, and then the loop feature can run based on the time intervals. Stop hooks wait for the external scripts or conditions, while normal chat modes will be able to wait for the direct user input after each response. Overall, this is a great new feature, and it's something that you should definitely take a look at.

Now, next is a fun new update that they have released called slash radio, which opens up Claude FM. This is Anthropic's built-in low-fi coding radio station that is directly accessible within Claude Code, and it is something that will make using Claude Code more engaging cuz you get to listen to the FM radio of Claude. Lastly, this isn't a massive feature, but Claude Code also updated how system prompt compaction works. This is with prompt trimming, which is now silent, meaning Claude no longer shows explicit alerts when context gets complicated or shortened during your long session. They also improved the compaction prompt itself so the model properly prioritizes preserving sensitive instructions and important user intent during trimming, which helps overall reduce context drift in long-running agent workflows.

But that was a nice wave of new updates from Anthropic, and I definitely love this new agent view feature. It's going to make session management a lot easier with Claude Code, but I still wish that they improve on the Claude Code limits. I hope that they can improve and increase rate limits for it, cuz right now it is unusable, and which is why many people are shifting over to Codex, including myself.

</details>
