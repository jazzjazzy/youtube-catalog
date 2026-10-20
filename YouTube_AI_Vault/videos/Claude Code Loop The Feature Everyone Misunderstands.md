---
title: "Claude Code Loop: The Feature Everyone Misunderstands"
video_id: Xxqu-kz00gw
channel: "[[channels/Better Stack]]"
uploaded: 2026-03-10
processed: 2026-07-05
duration: "5:45"
url: https://www.youtube.com/watch?v=Xxqu-kz00gw
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [recurring-task-scheduling]
tools: [Claude Code, Claude Desktop, Claude Cowork]
llms: [Claude, Claude Sonnet, Claude Haiku, GPT-5.4]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Loop: The Feature Everyone Misunderstands

![thumbnail](https://i.ytimg.com/vi_webp/Xxqu-kz00gw/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=Xxqu-kz00gw) | 📅 Uploaded [[uploaded/2026-03-10]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Anthropic's new loop skill for Claude Code schedules prompts to rerun at set intervals, and many people are misusing it as an OpenClaw replacement for persistent bot messaging. The video explains why that breaks down (3-day task expiry, session-only storage) and shows the actual intended use cases plus better options for truly persistent scheduling.

**Watch this if:** you want to understand what Claude Code's loop/cron feature is actually good for before wiring it up to a chat bot.

## Key Takeaways
- The loop skill schedules prompts on an interval (minutes/hours/days) or at a specific time using the local machine's timezone, backed by a cron create/list/delete skill.
- Loop prompts can invoke skills, read files, and call MCP tools — anything a normal Claude Code prompt can do.
- Cron jobs get a random jitter (0-6 min per hour) so scheduled jobs don't all hit the Anthropic API at once.
- Two dealbreakers for using loop as an always-on assistant: tasks auto-expire after 3 days, and they're stored in session memory only, so closing the terminal session wipes them.
- Loop is best suited for session-scoped, rerun-manually-style tasks: tailing a log file, checking a job queue, or watching for new issues.
- For tasks that need to run forever, use Claude Desktop's built-in Scheduled Tasks sidebar feature (runs on your local machine as long as the app is open) instead.
- Claude Cowork also has a Scheduled option, but it executes inside a sandboxed environment rather than your local file system — important to know before you pick where to put a persistent task.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the loop skill/cron create/list/delete tools are demoed directly in the terminal.
- [[topics/Claude Desktop]] — its Scheduled Tasks sidebar is shown as the way to run a task forever on the local machine.
- [[topics/Claude Cowork]] — its Scheduled option is compared against Claude Desktop's, noting it runs sandboxed rather than locally.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the general model family running Claude Code throughout the demo.
- [[topics/Claude Sonnet]] — the default model in the Claude Code session shown.
- [[topics/Claude Haiku]] — switched to for the simple demo prompts since they don't need a more sophisticated model.
- [[topics/GPT-5.4]] — mentioned as a just-released OpenAI model, pointing viewers to another video for details.

## 📡 Protocols & Standards
- [[topics/MCP]] — loop prompts can call MCP tools as part of a scheduled task.

## ✅ Action Items
- Try scheduling a loop prompt in Claude Code to tail a log file or check a job queue on an interval instead of a persistent bot use case.
- Set up a forever-running task in Claude Desktop's Scheduled Tasks sidebar if you need true persistence.
- If you prefer a terminal-only workflow, look into Kenneth's plugin for persistent Claude Code scheduling.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Haiku, Claude Sonnet
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Haiku, Claude Sonnet
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Cowork, Claude Sonnet
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku, Claude Sonnet
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Sonnet, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Haiku, Claude Sonnet, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Sonnet, MCP
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude, Claude Code, Claude Desktop, MCP

## Timeline
- `0:00` — Anthropic's loop skill is released; people are misusing it as an OpenClaw replacement.
- `0:29` — Discussion of hype vs. actual usefulness of new Claude Code features.
- `0:56` — Demo: creating a loop task with an interval, switching to Haiku for simple prompts.
- `1:45` — Loop capabilities: skills, file reads, MCP tools, cron list/delete.
- `2:24` — Issue #1: cron tasks auto-expire after 3 days.
- `3:07` — Issue #2: cron tasks live in session memory only, not written to disk.
- `3:39` — The actual intended use case: rerunning a task manually in the same session (logs, job queues, issue checks).
- `4:06` — Running tasks forever via Claude Desktop's Scheduled Tasks sidebar.
- `4:39` — Claude Cowork's Scheduled option runs sandboxed vs. Claude Code's local file system.
- `5:22` — Mention of Kenneth's terminal scheduling plugin and OpenAI's GPT-5.4 release.

## Transcript
<details>
<summary>Full transcript</summary>

The Anthropic team have released a loop skill for Claude code to run prompts at set intervals and people on the internet are going crazy hooking it up to Discord or Telegram to communicate with their agent just like they would with open Claude, and some are even using it for Ralph loops. But, they're using it all wrong because the loop skill was not designed for that purpose. I mean, there is a reason they didn't call it schedule and call it loop. Hit subscribe and let's find out why.

It's no secret that Claude is being used to write 100% of Claude code because the team have been shipping features like crazy. But, usually the hype level matches the usefulness of the feature. So, Claude remote control, lots of hype because it's very useful. Async hooks, less hype because they're less useful. But, this is the first feature that has more hype around it than the usefulness of the actual feature. Before you get angry, let me explain. So, here is the latest version of Claude code running Sonnets, which I'm going to change to Haiku since the prompts I'm going to use don't require such a sophisticated model. So, here I just have the loop, which takes an interval in minutes, hours, or days. Note the minimum granularity is a minute. So, even though you can't write seconds, Claude doesn't support them yet. And then, it also takes a prompt. So, I'm going to write say "Hello." And if I hit enter, it uses the cron create skill to create a scheduled task.

You can also set a specific time. So, I could do loop and here it said "Hello." Very quickly, I'll write a prompt of say "Hello again." at 6:30 p.m. And here, Claude uses the local time for the machine you've installed Claude code on and not UTC. So, keep that in mind. I'll set this to a daily recurring task, and that's pretty much it. The prompt can contain anything you want. So, skills, like I could use this tweet skill to write me a tweet along the lines of Claude has an awesome new loop skill, and I'll set that to run every 3 minutes. The prompt can also read a file, run MCP tools, basically anything you can do with Claude code, you can add to your prompt. And I can list the current cron jobs running with this prompt, which uses the cron list tool to list out the jobs, and I could delete a job by saying what the job does or by using the ID. There's also a jitter on the time of cron jobs to prevent multiple jobs at the same time hitting the Anthropic API, which means an hourly job can fire anywhere between 0 and 6 minutes on the hour.

Now, yes, this is a really cool feature, and people are saying it has replaced open Claude for them because you can set it on an interval to pull messages from WhatsApp or Telegram and respond to them like a real AI assistant, which is what people were using open Claude for doing. But, there are two major issues with the loop feature that prevent it from being an open Claude killer. First of all, the cron tasks auto expire after 3 days to prevent you from having long-running tasks that you might have forgotten about. This could, of course, be really annoying if you've hooked the loop up to listen for Telegram messages and go to it on the fourth day to find out it doesn't work. Now, there is a way to run jobs forever inside Claude code without a plugin, but we'll talk about that later on in the video.

The second issue is that cron tasks are stored in session memory and are not written to disk. So, if I close this Claude code session, I'm going to clear my terminal and create a new one, then if I ask it to list my scheduled tasks, you'll see that nothing has been scheduled even though I scheduled two tasks in the previous session. This means if you wanted to close the session to update Claude, or if you wanted to use the loop feature for a Ralph loop, it isn't really a good idea since you can't properly reset the session and have to rely on compaction to continue long-running tasks.

So, what should you be using this feature for? Well, whenever you have to rerun a task manually in the same session because something has changed, then you should be using a loop for that. For example, if you're checking the last 50 lines of a continuously updating log file for errors, seeing how many items are left in a job queue, or checking if you have any new issues in your project. Now, I'm sure the team will add more options to loop in the future, like setting a specific model for a task or changing the expiry time.

But, if you want a task to run forever in Claude code, you can kind of already technically do that without any plugins. You can do that in Claude for desktop by opening the sidebar if it isn't already and clicking on scheduled in the menu. Now, if you don't see the schedules option, you may have to update Claude for desktop. And here, we can create a task giving it a name, description, and prompt. We can even change the model, set permissions, and set frequency down here. This is exactly the same as if we were to write schedule inside the prompt section of Claude code desktop.

But, what's really interesting is that inside co-work, there is also a scheduled option. Now, this is different from the scheduled option in Claude code, not only because the model looks different and we have to click on more options to change the default model, but also because Claude co-work runs inside a sandboxed environment, whereas Claude code runs on your local machine. So, if you schedule a task in Claude code, that's going to use your local file system, whereas for Claude co-work, it's going to do it in a sandboxed environment, which is important so you know where to put your scheduled tasks.

Now, the benefit of adding a scheduled task inside Claude desktop is, of course, the task will run forever as long as the computer is switched on and the Claude desktop app is opened. But, if you're like me and would rather use Claude code in the terminal to schedule tasks, then you can use this plugin by Kenneth, which does look promising and I may try it out in the future if there's enough interest. Speaking of other promising things I haven't yet tried out, OpenAI released GPT-5.4 last week and people seem to be excited about it. If you want to know more, check out this video from James, who goes through all the details.

</details>
