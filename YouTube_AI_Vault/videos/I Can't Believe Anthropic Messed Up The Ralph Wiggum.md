---
title: "I Can't Believe Anthropic Messed Up The Ralph Wiggum"
video_id: XVAhQ-EcrWA
channel: "[[channels/Better Stack]]"
uploaded: 2026-01-21
processed: 2026-07-06
duration: "8:20"
url: https://www.youtube.com/watch?v=XVAhQ-EcrWA
playlist: "[[Agents skills n8n]]"
type: review
difficulty: advanced
use_case: [context-window-optimization]
tools: [Claude Code, Ralph Loop, Ralphie, Loom, Agent Browser, GitHub]
llms: [Claude Sonnet, Claude Opus, GPT-5]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# I Can't Believe Anthropic Messed Up The Ralph Wiggum

![thumbnail](https://i.ytimg.com/vi_webp/XVAhQ-EcrWA/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=XVAhQ-EcrWA) | 📅 Uploaded [[uploaded/2026-01-21]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Better Stack breaks down the original Ralph Wiggum loop (a bash while-loop that re-prompts an agent from scratch each iteration) and argues most popular implementations — including Anthropic's own Claude Code plugin — get it wrong by compacting context between iterations instead of fully resetting it. The video explains why keeping context in the model's "smart zone" is the whole point of Ralph, then scores real implementations from Anthropic, Ryan Carson, Razmik, and Matt Pocock against that canonical design.

**Watch this if:** you're running (or building) a Ralph-style autonomous coding loop and want to know why your agent gets dumber the longer it runs.

## Key Takeaways
- LLMs perform best in a "smart zone" — roughly the first 30-60% of the context window — and measurably degrade as context fills past 60-90%, because autoregressive models have to sift through everything already written to predict the next token.
- Before you write a single prompt, the system prompt, built-in tools, skills, MCP tools, and any agent.md file already consume part of that budget (roughly 10% on a typical Claude model just for system prompt + tools) — keep all of these as small as possible.
- The canonical Ralph loop, created by Geoff Huntley, is just a bash while-loop that cats a plan.md into a brand-new Claude invocation each iteration — no memory carries over, so every task starts with a full, clean context window.
- Compaction — summarizing prior context instead of resetting it — is the core flaw the video calls out: the model guesses what's "important" to keep and can silently drop critical details.
- Anthropic's official Ralph Wiggum plugin compacts context between iterations and caps runs with max iterations plus a completion promise, which the video argues undermines Ralph's main advantage of a truly fresh context each loop.
- Other implementations vary in legitimate ways: Ryan Carson's version appends to agent.md every loop (which bloats context over time), Razmik's Ralphie adds parallel Ralph runs and browser testing, and Matt Pocock drives the loop from GitHub issues.

## 🛠 Tools & Software
- [[topics/Claude Code]] — Anthropic's official Ralph Wiggum plugin runs the loop as a slash command inside Claude Code, with max iterations and a completion promise.
- [[topics/Ralph Loop]] — the video's central subject: a bash while-loop, created by Geoff Huntley, that re-prompts an agent from a fresh context window each iteration.
- [[topics/Ralphie]] — Razmik's script built on the Ralph pattern, notably adding the ability to run parallel Ralphs.
- [[topics/Loom]] — Geoff Huntley's follow-on project, aiming to build software autonomously and correctly.
- [[topics/Agent Browser]] — the Vercel browser-testing tool Razmik's Ralphie wires in to run automated browser checks.
- [[topics/GitHub]] — in Matt Pocock's version of Ralph, tasks are tracked as GitHub issues that the loop works through one at a time.

## 🤖 LLMs Mentioned
- [[topics/Claude Sonnet]] — used as the reference model, alongside Opus, for the ~200K-token context window and "smart zone" math.
- [[topics/Claude Opus]] — grouped with Sonnet in the same context-window/degradation discussion.
- [[topics/GPT-5]] — used only as a token-counting reference point (the full Star Wars: A New Hope script measures ~54K tokens in GPT-5).

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Audit your agent's context budget: minimize system tools, skills, MCP tools, and agent.md length before your task prompt is even added.
- If you build a Ralph-style loop, fully reset context between iterations instead of compacting/summarizing it — compaction can silently drop information the model needed.
- Drive your loop's task list from an external, human-editable source (a plan.md or GitHub issues) rather than letting the agent accumulate its own notes inside agent.md.

## 🔗 Related Videos
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/Claude Code TASKS (New Upgrade) RIP Ralph Loops Anthropic UPGRADED Claude Code with this FEATURE]] — shared: Claude Code, Claude Opus, Ralph Loop, Ralphie
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude Code, Claude Opus, Claude Sonnet, Ralph Loop
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude Code, Claude Opus, GitHub, Ralph Loop
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Claude Sonnet, GitHub
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, GitHub

## Timeline
- `0:00` — Ralph Wiggum's rise across Twitter/YouTube; is everyone actually doing it wrong?
- `0:30` — Recap: the canonical Ralph loop, created by Geoff Huntley.
- `0:51` — Why context degrades: the "smart zone" vs. the "dumb zone," and why autoregressive models struggle with long context.
- `1:31` — What already eats into context before your first prompt: system prompt, tools, skills, MCP tools, agent.md.
- `3:00` — Why Ralph is genius: one goal per full context window, driven by a plan.md.
- `5:00` — The problem with compaction: the model guesses what's important and can lose critical details.
- `5:33` — Why Anthropic's official Ralph Wiggum plugin gets it wrong (compaction between iterations, max-iteration caps).
- `6:22` — Why Ryan Carson's approach drifts from canonical (appending to agent.md on every loop).
- `6:52` — Valid tweaks: Razmik's parallel Ralphie + Agent Browser testing, Matt Pocock's GitHub-issue-driven Ralph.
- `7:35` — The future of Ralph: Geoff Huntley's Loom project.

## Transcript
<details>
<summary>Full transcript</summary>

Ralph Wiggum is absolutely blowing up. We made a video about it last year, and since then, it's all anyone is talking about on Twitter. Matt Pocock has made loads of videos on it. Ryan Carson has written a very popular article on it. And Razmik has built on it with his Ralphie script. But, is everyone doing it wrong? The creator has already said that some implementations are incorrect. So, what's the correct way to do it? And why is Ralph currently the best way to build software with AI? Hit subscribe, and let's get into it. The Ralph loop was created by Geoff Huntley and written about way back in June last year. It is essentially a bash loop that gives an AI agent the exact same prompt over and over again. But, it's genius on so many levels because it lets the AI agent work in its smartest mode, which is the mode where it has as little context as possible. Take a look at this. So, let's imagine this is the total context window for an agent. From 0 to about 30% is what we'll call the smart zone, which is where the agent performs the best. From about 30 to 60%, it still performs really well. And from 60% onwards, so 60, 70, 80, 90, that's when it starts to degrade. We'll call it the dumb zone. Now, these numbers aren't set in stone and could be different per model. So, the smart zone for a certain

model could be 40, 50%, but usually over 80% context window, that's when the dumbness starts to begin. So, for Claude Sonnet or Opus, the typical tokens for a context window is 200,000. So, you can say the first 60K is the smart zone. The next 60K is still okay, but not as good as the first 60K tokens. And then the last 80K, it doesn't seem to perform as well. Now, this is my personal experience with this model. You might have had other experiences. And so, the reason for this is because the model itself is what we call autoregressive, meaning it has to look at the previous tokens to predict the next one. And if you have loads and loads of tokens, it has to go through a lot of them to find out the important bits that are relevant to the next task at hand. Now, let's focus on the first 30%. Even before you write your first prompt, there's some things that get added to the context window automatically. First is the system prompt, and then the system tools. These on a typical Claude model take 8.3% and 1.4% of the context. So, almost 10% of this 30. And then if you have skills, that can get added. And also if you have custom MCP tools. Finally, if you have an agent.md file, that gets added too. And the larger, of course, for any of these things, so the larger the MD file, the more tokens it will take up. And this is all even before you've added your own prompt. So, in general, it's best to keep this

section as small as possible. So, have less tools, have less skills, and have less in your agent.md file so that the model is working at its most optimum context. And to get an idea of exactly how much 60K is, if we were to get the whole script of Star Wars: A New Hope, that is about 54,000 tokens in GPT-5. So, roughly this amount. Now, you may be wondering, what about compaction? Can that help with this whole process? And we'll talk about that a bit later. But now, let's move on to exactly how Ralph can help with this. So, the benefit of Ralph is that you focus on one goal per context window. So, the whole 200K context window, you can dedicate that to one goal or one task. And the way we do that is we write a prompt that will first say inspect the plan.md file. This contains the tasks to be done. So, something like create the front end, create the back end, do the database, and so on. That is a very high-level example. Of course, you go way more detailed if you were doing Ralph and more granular, but we'll stick with that example for now. So, this prompt will tell the agents to pick the most important task, then make those changes. After making those changes, run and even push and commit those changes, as well as doing a test. And once you're done with those, once the tests have passed, then tick the task as done in the plan.md file, and do that again. So, the agent will keep looking for the most important task to do until it's

completed all the tasks. Now, actually, let me take that back because you could keep having the Ralph loop go over and over again even if it has completed all the tasks. And the benefits of that is that it may even find things to fix or find features to add that don't exist in the plan.md file. But, if it is going off the rails, the benefits of having Ralph is that you can stop the whole process whenever you want, adjust the prompt.md file, and then run the whole process again. And Ralph makes this so simple because this whole process is executed in one single bash while loop. So, here it just cats the prompt.md file, so prints it to the agent, and then runs Claude in YOLO mode. Of course, the flag isn't YOLO, it's dangerously skip permissions, but for the sake of space, I've kept it short. And what makes Ralph special is that it's outside of the model's control. So, the model can't control when to stop Ralph. It will just keep going. And that way, you can ensure that when a new task runs or when a new prompt is triggered, the context, so here, is pretty much where it is when you first open the agent. So, this is fresh. It doesn't have any compaction. It doesn't have anything added. So, each new task gets the most amount of context and uses the model in its most smart or most optimal context window state. Basically, compaction is where the agent will look at all the tokens that have been written

in the context window and pick out the most important bits for the next prompt. So, it will pick what it thinks is most important, but it doesn't know what is actually most important. Therefore, compaction might lose some critical information and make your project not work as expected. Anyway, now that we've seen the canonical Ralph loop implementation from the creator, this helps us see why other implementations are different. Let's take a look at the Anthropic implementation, which uses a slash command to run Ralph inside of Claude Code, has max iterations and a completion promise. So, the problem with this specific Ralph Wiggum plugin is the fact that it compacts the information when it's moving onto the next task. So, if it finishes one task and reruns the prompt, instead of completely resetting the context window, it compacts what was previously done. Therefore, could lose some vital information. There's also the slight issue of having max iterations and a completion promise because sometimes it's nice to just let Ralph keep going. It can find very interesting things to fix that you wouldn't have thought of before. And if you watch it, so be a human on the loop, you may see patterns, good or bad, from a specific model that you can tweak and enhance in your original prompt. If we take a look

at Ryan Carson's approach to the Ralph loop, we can see here that it's not quite canonical simply because on each loop, it has the possibility of adjusting or adding to the agent.md file. Now, depending on the system prompt or any user prompts you've added to the model, in my experience, by default, models can be very wordy. And so, if on each iteration, you're adding to the agent.md file, which gets added to the context at the beginning of each user prompt, then you're just adding more tokens into the context window, pushing the model into a place where it could potentially give you dumb results. But, the fact that people are making their own scripts from the basic Ralph loop bash script is a testament to how simple and easy it is to understand. And although there is a canonical way of doing Ralph, I think it's okay for developers, teams, and companies to tweak it to their specific use case. For example, I love the fact that in Razmik's Ralphie script, there's a way to run parallel Ralphs. And also the fact that you can use the Agent Browser tool from Vercel to do browser testing. I also love the fact that in Matt Pocock's version of Ralph, he adds tasks or things to do as GitHub issues, and the Ralph loop will pick the most important one, work on it, and mark it as done when it's complete before working on the next one, which I think is really clever. I think the power and

simplicity of Ralph means that it's going to stick around for a very long time. And you also may see a lot of iterations and improvements from it. I really like the way Geoff Huntley is taking this with his Loom project where he wants to create a way to make software autonomously and correctly. But, with all these Ralphs autonomously creating new software, you need a way to search for errors and make sure they get fixed. This is where BetterStack comes in because not only can it ingest logs and filter out errors from them, but it can also handle error tracking on the front end. So, with this MCP server, you can ask an agent to specifically pick out errors from the front end or back end instead of reading through the whole log, which in turn reduces the context window. So, go and check out BetterStack, and let me know what you think in the comments.

</details>
