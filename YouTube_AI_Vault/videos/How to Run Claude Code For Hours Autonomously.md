---
title: "How to Run Claude Code For Hours Autonomously"
video_id: o-pMCoVPN_k
channel: "[[channels/Developers Digest]]"
uploaded: 2025-12-29
processed: 2026-07-06
duration: "13:35"
url: https://www.youtube.com/watch?v=o-pMCoVPN_k
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [autonomous-long-running-agents, stop-hook-automation]
tools: [Claude Code, Ralph Loop, GitHub, Git, Playwright, Claude Browser Extension]
llms: [Claude, Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# How to Run Claude Code For Hours Autonomously

![thumbnail](https://i.ytimg.com/vi_webp/o-pMCoVPN_k/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=o-pMCoVPN_k) | 📅 Uploaded [[uploaded/2025-12-29]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> METR's latest benchmark shows Claude Opus 4.5 can work independently for nearly 5 hours at a 50% completion rate, up from ~5 minutes for GPT-4 era models. This video shows how to actually get that persistence in practice: configuring Claude Code's stop hook (via the official Ralph Wiggum plugin) so tests re-run and failures get fed back automatically, quoting Claude Code creator Boris Cherny on running it for minutes, hours, and days at a time.

**Watch this if:** you want Claude Code to grind through a to-do list or long refactor unattended for hours instead of stopping and waiting for you after every step.

## Key Takeaways
- METR's benchmark shows Claude Opus 4.5 can operate autonomously for 4 hours 49 minutes at a 50% completion rate (dropping notably at an 80% bar); GPT-4-era models topped out around 5 minutes, illustrating the trajectory of improvement.
- Claude Code won't run unattended out of the box — the agent harness needs configuring for persistence; the presenter compares trusting it to trusting a self-driving car's autopilot: get comfortable with its behavior and guardrails first.
- Hooks are shell commands that fire at specific points in Claude Code's workflow (like git hooks, but for the agent loop); the stop hook specifically fires when Claude finishes and would otherwise ask a question or stop.
- The stop hook makes long runs deterministic: when Claude finishes, tests can run automatically, and failures get fed back into Claude to keep iterating until they pass — closing a loop that pure prompting can't reliably achieve.
- Boris Cherny (Claude Code's creator) tweeted that in the last 30 days he personally landed 259 PRs, 457 commits, 40,000 lines added and 38,000 removed, all written by Claude Code and Opus 4.5, running for minutes/hours/days via stop hooks.
- The official Ralph Wiggum plugin implements this: running the "Ralph loop" creates a state file, and each time Claude tries to stop, the stop hook re-feeds the prompt until a max-iteration limit or a completion promise is met.
- Practical pattern demoed: point Claude at a to-do.md file with unchecked tasks; each stop-hook iteration picks up the next unchecked item, implements it, runs unit/integration tests (or tools like Playwright or the Claude browser extension for front-end checks), fixes failures, and marks the item complete before continuing.
- Critical safety note: always set both a max-iterations limit and a completion promise, or the Ralph loop will run infinitely and burn tokens with no exit condition.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI/agent harness being configured with hooks to run autonomously for extended periods.
- [[topics/Ralph Loop]] — the official Anthropic "Ralph Wiggum" plugin demoed: a stop-hook-driven loop that re-feeds a prompt until a max-iteration count or completion promise is reached, used here to work through a to-do list.
- [[topics/GitHub]] — hosts the official Ralph Wiggum plugin repo linked in the video and referenced for Claude's PR/commit activity.
- [[topics/Git]] — mentioned as one of the risky actions (commit, push, delete) Claude Code can take unattended, motivating the need for guardrails.
- [[topics/Playwright]] — cited as a tool to validate front-end work as part of the test-and-fix loop between iterations.
- [[topics/Claude Browser Extension]] — cited alongside Playwright as a way to validate front-end changes ("leveraging Claude within Chrome") during autonomous runs.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model running inside Claude Code throughout the autonomous stop-hook setup and demo.
- [[topics/Claude Opus]] — specifically Claude Opus 4.5, cited in METR's benchmark (nearly 5-hour autonomous runs) and by Boris Cherny as the model behind his large volume of autonomously-produced PRs/commits.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install the official Ralph Wiggum plugin and try the Ralph-loop slash command on a to-do.md-driven task.
- Always set a max-iterations limit and a completion promise before starting a long autonomous run.
- Add a validation step (unit/integration tests, Playwright, or the Claude browser extension) after every iteration so failures get caught and fixed before moving on.
- Get familiar with Claude Code's permission prompts and guardrails before turning on fully autonomous stop-hook runs, the same way you'd learn a car's autopilot before trusting it.

## 🔗 Related Videos
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Browser Extension, Claude Code, Claude Opus, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, Git, GitHub
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, Git, Playwright
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, Claude Opus, Git, Ralph Loop
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, Playwright
- [[videos/Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing]] — shared: Claude, Claude Code, Claude Opus, Ralph Loop
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Browser Extension, Claude Code, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, Playwright

## Timeline
- `0:00` — Intro: goal is running Claude Code autonomously for hours.
- `0:09` — METR benchmark: Claude Opus 4.5 runs autonomously for ~4h49m at 50% completion, vs. ~5 minutes for GPT-4-era models.
- `0:52` — Claude Code needs harness configuration for persistence; self-driving-car analogy for trust and guardrails.
- `2:39` — Hooks explained: shell commands firing at workflow points; focus on the stop hook.
- `4:47` — Boris Cherny's tweet on real-world usage: 259 PRs, 457 commits, 40K+ lines via stop hooks over 30 days.
- `6:48` — Implementing the Ralph loop: state file, re-feeding the prompt until max iterations or completion promise.
- `10:48` — Practical demo of the stop hook triggering and re-feeding the prompt through a synthetic to-do list.
- `13:28` — Conclusion: always set max iterations and a completion promise to avoid infinite loops.

## Transcript
<details>
<summary>Full transcript</summary>

In this video, I'm going to be showing you how to set up Claude Code to be able to run autonomously for hours. Now, just recently, Meter came out with the latest benchmark of Claude Opus 4.5 that showed that this model can perform independently and autonomously for 4 hours and 49 minutes. Now, this is at a 50% completion rate. If we go down to 80%, this number does drop down quite a bit. But the main thing with this is as we take a look at the trajectory of how the models have improved over time. If we go back to when GPD4 was a huge deal at the time, just to give you an idea in terms of how long this model could run for, this was only able to run for 5 minutes. But now we're entering a new era where these models can run for quite a long time and they're getting increasingly accurate at actually being able to have successful runs.

Now, in terms of actually setting this up, you aren't going to be able to just set it up within cloud code. you aren't just going to be able to type claude within your CLI and be able to walk away for minutes or even hours. You do have to configure the agent harness a little bit just to give it a little bit more persistence. Now, the nice thing with this actually is it actually isn't that difficult. And I'm going to be showing you one of the official ways in terms of how Anthropic actually sets this up and how some of the members on that team leverage this method to have this actually run for a particularly long time.

If you've used Cloud Code before, the first time that you run it, it will actually ask you permission for everything that you're doing. And one of the things with Cloud Code is it's very similar to a self-driving car. Now, the first time that I got in a car that had an autopilot feature, one of the first things that they said to me is actually don't turn this on by default. Actually get comfortable with being able to leverage it, know how to turn it on and off, and then as soon as you actually trust the system, then you'll be a lot more comfortable with actually turning it on. It's a very similar thing within Claude Code. You do want to generally get an idea in terms of what it will do or what it's capable of doing because it can run a lot of different commands on your machine. It can commit to git. It can push things. It can delete things. If you're not careful, it can do things that you don't want it to do. But once you know the capabilities, you'll get familiar with some of the guardrails that you might want to have in place.

Now, when you go and you run cloud code for the first time, you'll see that it will go through this process and it will ask you these different questions. But one of the issues is oftent times when you want it to run tests or if there's something that fails, if you're trying to just have it go off for a particularly long time, if you try and do that with just prompting, you'll know that it will often get lazy. Part of the solution with this is actually making it a little bit more deterministic. In the case of tests, for instance, what you can do is you can actually have tests run automatically once Claude finishes. Now, if they fail, you can actually feed that input back into Claude code. And what this will do is it will create this loop where claude code has this non-deterministic LLM pattern. But when you equip it with something called hooks and the stop hook in particular, that's going to allow it to persist much much longer.

There are a number of different hooks within cloud code. Effectively, what hooks are is they're shell commands that are going to fire at particular points within the cloud workflow. So you can sort of think of it like git hooks, but effectively for AI and cloud coding. One of the things with these is you see there's a number of different hooks in terms of where you can actually leverage this. Now there are a number of different hooks within cloud codes. What this will allow you to do is you can actually block it from running particular commands if you don't want it to run things. You can actually check before it actually invokes those different tool calls which could potentially be detrimental. You might just want to block it from not leveraging git or whatever it might be. Now what you can also do is you can have this after the tool use is complete. And additionally what you can do is you can actually call these events after the tool use is done.

But what I'm going to focus on within this video is the stop hook. And what this is helpful for is when Claude actually finishes the process, but it might ultimately come back and ask you a question. Even if you ask it to go and focus on something for a particularly long time, you might get creative and try and just prompt your way to have it run for a long time. But what the stop hook or any hook will do is it will actually allow you to have something more deterministic within this agentic flow. You will be able to bank on whenever that stop hook calls. You can actually have a process to run through.

Now, the power of the stop hooks is if you just think about it, as soon as Claude finishes the work, what the hook will do is it will fire automatically and you can configure this for a number of different things. If you want it to actually run different unit tests or integration tests or whatever it is, you can have those set up to run as soon as the process is finished. And then if those tests fail, Claude will be able to see that output and it will be able to feed that in and start the process and repeat until it's done. And one of the key insights with this is if you just ran your tests is Claude wouldn't know if the tests pass unless you actually ran it within the process. But what stop hooks allow you to do is you can actually pass that in at arguably one of the best times because it's going to be able to show you okay after all of the edits and things that it did. It can actually verify whether it works or not. And this can be used in a number of different ways.

Now in terms of some of the real world use cases for this. So the creator of Cloud Code, Boris Journey, I'll just read through this tweet quickly. He said, "When I created Claude Code as a side project back in September 2024, I had no idea it would grow to what it is today. It is humbling to see that Claude Code has become a core dev tool for so many engineers, how enthusiastic the community is, and how people are using it for all sorts of things from coding to DevOps to research to non-technical use cases. This technology is alien and magical, and it makes it so much easier for people to build and create. Increasingly, code is no longer the bottleneck. A year ago, Claude struggled to generate bash commands without escaping issues. It worked for seconds or minutes at a time. We saw early signs that it may become broadly useful for coding one day. Fast forward to today, the last 30 days, I landed 259 PRs, 457 commits, and 40,000 lines added, and 38,000 lines removed. Every single line was written by Claude Code and Opus 4.5. Claude consistently runs for minutes, hours, and days at a time using stop hooks. Software engineering is changing, and we are entering a new period in coding history. And we're still just getting started." And then within here, you can see all of the different usage and the number of tokens that he had leveraged. Just to give you an idea, now mind you, this is the creator of Claude Code. This is someone who arguably knows the system better than anyone else. But just to show you actually what this can perform and I don't actually think that this is just marketing or anything like this he is definitely a very genuine person and if you've leveraged claude code in particular with Opus 4.5 you will probably know exactly what he's talking about.

Now in terms of one of the things that I noticed within this tweet that I did want to pull up is there was a question from Simon Willis and he asked okay Claude consistently runs for minutes, hours and days at a time using stop hooks and then he asked him to expand on this. In his response, Boris mentioned when Claude stops, you can use a stop hook to poke at it, tell it to keep going. And then he gave an example within one of their official repositories to what they call Ralph Wiggum. Now, if you know Ralph Wigum, he's from the Simpsons. And one of the things with Ralph is he's determined to get it done. So, he'll just keep trying until it actually works, which is sort of a funny analogy in terms of how you can actually get Claude to work.

Now, effectively, how this works is you're going to be able to run the quote unquote Ralph loop. You'll be able to pass in your task. Once you pass in your task, it's going to create a state file within your Claude folder. Once that's set up, as soon as Claude works through what you're trying to do and tries to exit, the stop hook will block it from exiting and it will refeed what it's trying to do within the prompt. And then this process will repeat until the max iterations or the promise is actually met. Where this is useful, it could be useful within a test-driven development workflow, but also where this can be helpful is if you have particularly long to-do lists. Let's say you scaffold out an initial plan for how you want to have your feature or application or whatever sort of level that you actually want to plan out. If you want to have cloud code go through that list without actually stopping, what you can do is you can actually point it at the to-do list and then it will have those tasks that it will loop through and it won't actually finish until it actually meets the criteria.

This can also be helpful in a number of other scenarios. Think things like large refactors or migrations. Within the to-do example, what you can do is you can set up something like a to-do MD file. And what you can do is you can instruct Claude to go through these tasks and actually mark them complete as you go. For instance, let's imagine you have a task.md file. What you can do within here is you can use the raph loop to complete all these tasks in the to-do.md. Then what you can also do in addition to this is you can also include tests after each iteration. And this can be particularly helpful because oftent times if you don't include a validation step while it's actually running through, it might go through a particularly long to-do list, but then get to the end and realize there might have been some catastrophic failures that sort of built on top of. So being able to actually iteratively go through and have the system build on top of what it's done, it can be a good way in terms of actually leveraging these systems and if you can try and validate the work as much as you can. So this can be with unit test integration test leveraging playright for things on the front end or leveraging claude within Chrome and all of those types of things.

If you haven't used to-do list within claude code now there is a to-do feature built right in where it will just decide to leverage that when it needs to. But additionally you can also do this yourself if you want to have a little bit more control over it. You can instruct Claude to go through a markdown file. You can put just like you see on the slide here all of the different things that you want it to do including all of the different validation steps along the way. And then with each iteration, you will see the cloud will go through and it will pick up all of the unchecked items. It will implement the feature or fix or whatever you have within that actual line item. It will run the unit test and integration test depending on what you have within the list. And then if the test fails, it will go ahead and it will fix that before it goes and continues on and marks it complete. What this allows you to do is you can sort of just walk away and then hopefully come back to a finished list working feature or working application depending on the scope of what you actually put within your to-do list.

Now, the other thing that's cool with this is you do have the option where you can stack multiple hooks together. And the other thing with this is when you leverage hooks is you can leverage these interchangeably and you don't necessarily need to just use one. For instance, within my cloud environment, I have a number of different hooks that are set up that invoke different actions at different times. Thanks for logging, thanks for notifying me, all of these types of things are particularly helpful.

Now, as you can imagine, by leveraging these more deterministic patterns combined with the non-deterministic agentic harness that is cla code and the model, because often times you just can't predict what it will ultimately do. You can have maybe a high degree of confidence if you know what you're passing within context, but oftent times for these long running tasks, there is the potential where it can go off course. And having things that can actually check it and run these more deterministic triggers and scripts at at particular times can be very very helpful. This can keep your code clean. This can prevent dangerous operations and like I've mentioned a couple times already, ensure that tests pass before actually stopping.

Now, to get this set up, one of the fastest way to get going with this is if we go to the Ralph Wiggum plugin. And what you'll notice within here is what plugins are is actually being able to configure a number of different things within Cloud Code at once. You can have sub aents, you can have skills, and in this case, you can actually leverage hooks. Now, the core piece of this is if we take a look at the hooks, what we'll notice within here is we have the stop hook trigger. This is going to be how we actually invoke the different hooks that we have on this stop event. If I go back here and we take a look at this stop hook, this is an example in terms of what a hook looks like in terms of what you can actually invoke every time that it stops. And you can have a number of different scripts that invoke whenever Claude actually stops. Within here, you can see we have a formatter, iteration, max iteration, as well as the completion promise.

Once you have it all installed, what you're going to be able to do is have this slash command for Ralph loop. So within the Ralph loop, what you're going to be able to do is put in your prompt, the number of max iterations as well as the completion promise. So what actually validates that that step is complete. Within here, what I can do is I can specify go through my to-do list step by step and mark down every step that is complete once it's actually done. I'll go ahead and I'll kick this off. What we see on the lefth hand side here is I have a number of different steps just to demonstrate this. We'll create a text file. But what you'll notice is in between each of these is I'm synthetically trying to trigger that stop process within Claude. And this is just to demonstrate what that hook will look like when it is triggered within Claude. We can see it went ahead. It completed the first task here. And now for our second task. What you'll notice within here is we have this stop hook error where it says go through my to-do list step by step and mark down every step that is complete once it's actually done. And now what this looks like and how it can persist is instead of actually returning a message to you, it will call this trigger and it will pass this back into Claude and have it just continue to go through the process within here. Within here, if I just scroll down, I see that number three is done. Once it gets to four, again, we have that hook being triggered as if there was a stop and returning a message back to us. And instead of stopping, we're just passing that back into context to have it to continue to go through the list.

Now the one thing that I do want to mention with Ralph loops or this type of process is just make sure that you do set the max number of iterations as well as your promise. Otherwise this will run through. You see that my task list is complete. But if you don't specify that you have a completion promise or a max iteration it will just continue to go through and the loop will run infinitely. So, just make sure that you do actually specify both of these cuz otherwise you don't want to get in a scenario where you're just burning all of these tokens by effectively having an infinite loop.

Otherwise, that's pretty much it for this video. I'll put the link to the GitHub repository within the description of the video. But otherwise, if you found this video useful, please like, comment, share, and subscribe. Otherwise, until the next one.

</details>
