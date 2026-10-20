---
title: "Claude Cluster is Insane… Upgrade Your Claude Code Workflow"
video_id: V-xBaFveTvA
channel: "[[channels/AI LABS]]"
uploaded: 2025-12-19
processed: 2026-07-06
duration: "7:15"
url: https://www.youtube.com/watch?v=V-xBaFveTvA
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [parallel-ai-coding-workflows, claude-code-background-agents]
tools: [Claude Code, Git]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Cluster is Insane… Upgrade Your Claude Code Workflow

![thumbnail](https://i.ytimg.com/vi_webp/V-xBaFveTvA/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=V-xBaFveTvA) | 📅 Uploaded [[uploaded/2025-12-19]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Claude Code quietly shipped async background agents in its changelog (not its blog), letting sub-agents run full autonomous tasks in a separate process while you keep working in the main thread. The video explains how to push agents to the background, when they save real time (research, parallel refactors, multi-angle code review), and shows a git-worktree-based workflow for running several agents on isolated branches at once — plus quick coverage of instant auto-compact, prompt suggestions, agent flags, and session forking.

**Watch this if:** you use Claude Code and want to parallelize research, reviews, or multi-branch experiments without opening multiple terminals or Claude instances.

## Key Takeaways
- Claude Code added async background agents, announced only in the GitHub changelog: sub-agents and bash commands can now run asynchronously and message the main agent when they wake up.
- Workflow: ask Claude to hand a task to a sub-agent, push it to the background with Ctrl+B, keep working in the main thread, and the sub-agent reports results back when done; check running agents with the `tasks` command.
- This replaces the old workaround of opening multiple terminals with separate Claude instances to get parallel work done — Claude Code now manages and coordinates background agents internally.
- Best uses: long research tasks that would otherwise bloat your main context window, parallel updates across many files/pages (e.g. migrating all components to a new library), and running several independent review agents at once (security, performance, refactoring, dead-code) while the main agent works on a different feature.
- The most powerful angle: pairing background agents with git worktrees, so each agent works in its own directory/branch, committing changes in isolation without constant branch switching — e.g. spawning three agents to implement three different UI themes in parallel, then merging only the one you like.
- Other shipped features: instant auto-compact (down from ~2-3 minutes, likely from maintaining per-project history in the `.claude` folder), a prompt-suggestion feature (press Enter to accept), an agent flag to launch Claude directly as a specific project agent, and session forking (press Escape twice) usable with the resume flag.
- Don't background any task that needs your input or approval mid-run — it will block and can get lost if the main agent is busy elsewhere; also avoid assigning agents tasks that depend on each other, since that creates conflicts.
- Best practices: watch token usage (each background agent consumes real tokens and can add up on your bill), keep tasks isolated, and give each spawned agent a descriptive name so you can track what it's doing.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the subject of the video: its new async background agents, sub-agent workflow, instant auto-compact, prompt suggestions, agent flag, and session forking/resuming.
- [[topics/Git]] — git worktrees are used to let each background agent work on an isolated branch/directory, avoiding branch-switching conflicts and enabling parallel experiments (e.g. multiple UI theme variants).

## 🤖 LLMs Mentioned
- [[topics/Claude]] — described as the model now handling background-agent coordination and result-integration itself, replacing manual multi-terminal setups.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try pushing a long research task to a Claude Code background agent (Ctrl+B) while continuing other work in the main thread, then check progress with `tasks`.
- Set up a custom slash command (in `.claude/commands`) that spawns a background agent inside a dedicated git worktree for isolated feature/branch work.
- Launch several review agents in parallel (security, performance, refactor, dead-code) on a codebase instead of running them one at a time.
- Give every background agent a descriptive name so multiple concurrent agents stay easy to track.
- Avoid backgrounding any task that needs your approval or input mid-run, and avoid assigning agents interdependent tasks.

## 🔗 Related Videos
- [[videos/Anthropic Released A New Way To Vibe Code]] — shared: Claude, Claude Code, Git
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, Git
- [[videos/You Need Claude Sandboxes 90 Faster AI Coding]] — shared: Claude, Claude Code, Git
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Git
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Claude Code
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude, Claude Code

## Timeline
- `0:00` — Claude Code quietly ships async background agents, announced only in the GitHub changelog.
- `0:47` — Basic workflow: create a sub-agent, push it to the background with Ctrl+B, check with `tasks`.
- `1:16` — Under the hood: background agents run as a separate process handling full multi-step tasks autonomously.
- `1:47` — Ideal use cases per Anthropic: research while coding, review workflows, parallel tasks, keeping the main context clean.
- `2:38` — Practical use: offloading long research tasks to the background to avoid bloating the main context window.
- `3:13` — Parallelizing updates across multiple files/pages simultaneously (e.g. library migration).
- `3:32` — Running multiple review agents in parallel (security, performance, refactoring, dead code).
- `3:50` — The "unexpected angle": combining background agents with git worktrees for isolated branch work.
- `4:28` — Custom slash command setup for spawning worktree-based background agents.
- `4:37` — Example: three agents implementing three UI themes in parallel, merging only the winner.
- `5:14` — Other new features: instant auto-compact, prompt suggestions, agent flag, session forking.
- `5:58` — When NOT to use background agents: tasks needing input/approval, or interdependent tasks.
- `6:37` — Best practices: token usage awareness, task isolation, descriptive agent naming.

## Transcript
<details>
<summary>Full transcript</summary>

The developers of Claude Code just silently announced massive updates that almost no one is talking about. The biggest of which is the release of Async background agents. What's strange is that you won't find these features mentioned anywhere on Anthropic's main site or even their blog. Now, you might be wondering if these are actually useful, and honestly, I wasn't sure at first either, but I found an unexpected angle that's completely changed how I use them. So, in this video, I'm going to break down exactly what that is, why it makes a lot of existing AI coding frameworks basically unnecessary, and then walk through several other Claude features.

They announced these new features in the change logs on Claude Code's GitHub repo. They mentioned that these agents and bash commands can run asynchronously and send messages to wake up the main agent. The idea here is to achieve true parallel working. It is quite simple to use them. We first ask Claude to handle a task that benefits from a sub agent, and then the main agent creates a sub agent for the task. When the agent has started running, we push it to the background using Ctrl+B and continue working with the main agent on other tasks. When the sub agent has completed the task, it wakes up the main agent with the results. We can also check our running agents using the tasks command.

Under the hood, the background agent works as a separate process that is able to execute complex multi-step tasks autonomously, meaning it can independently handle full-scale tasks on its own. They allow you to continue interacting with Claude Code's main thread without blocking their execution, so you can use your time effectively instead of waiting. When they're done executing, they report the results back to the main agent. Previously, you had to open multiple terminals with separate Claude instances for this purpose. Now, Claude does this itself, managing background agents internally, coordinating multiple agents and integrating the results on its own without the manual setup we were using earlier. They say background agents are ideal for researching while coding, reviewing workflows, performing parallel tasks, and handling any task that shouldn't pollute your main context window.

Before we discuss whether these agents actually save us time, let's take a quick break to talk about Automata. After teaching millions of people how to build with AI, we started implementing these workflows ourselves. We discovered we could build better products faster than ever before. We help bring your ideas to life, whether it's apps or websites. Maybe you've watched our videos thinking, "I have a great idea, but I don't have a tech team to build it." That's exactly where we come in. Think of us as your technical co-pilot. We apply the same workflows we've taught millions directly to your project, turning concepts into real working solutions without the headaches of hiring or managing a dev team. Ready to accelerate your idea into reality? Reach out at hello@automator.dev.

So, I tried out what they were suggesting and from the time I've spent with them so far, I really like what I'm seeing. I think these agents have a lot of potential. These background agents can handle any research task that takes a lot of time or might bloat your context window. You can simply move that research to the background and assign a separate task to the main agent. This allows the main agent to work on something completely different while remaining totally isolated from the research task. These agents make it much easier to implement changes on separate pages at the same time by parallelizing tasks. Instead of waiting for one agent to handle everything sequentially, you can update them simultaneously. For example, if you're switching all your components to a new library, you can use background agents to update them all at once.

Other than that, you're often left with tasks like reviews that take up a lot of time. You can use async agents to launch several of them simultaneously. One for a security review, one to identify performance bottlenecks, one for refactoring code, and another to check for duplications or unused code. You can run all of these tasks in the background while your main agent stays focused on a completely different feature update. This way, each agent works separately and handles its own task independently from the others.

Now, here's the unexpected angle I mentioned earlier. You can even equip background agents with the ability to manage their work in a git worktree, allowing them to commit and push changes in isolation. Some of you might have already thought about this, but for those who don't know, git worktrees are an extremely underutilized feature that lets you work on multiple branches in separate directories. This means you can avoid constant branch switching in a single workspace and simply spawn as many agents for as many features as you like.

To use this workflow, I set up a custom slash command that creates a background agent to work on tasks in separate worktrees. All the instructions for this command live right in the commands folder, which you can find inside the .claude folder. Let's say I'm working on an app, but I'm not happy with the theme. I have three different theme ideas and I want to implement all of them to see which one looks best. Without worktrees, I would have had to clone the repo separately, create three different branches, or open separate Claude instances just to keep the tasks apart. But with background agents, all of that changes. The three agents worked in parallel to implement those themes separately, all while leaving my main design completely unaffected. This allows me to simply merge the theme I like into the main project and discard the others. This setup made the implementation process significantly faster because all the changes are isolated. I can choose the theme I like best from the different options. It gives me the freedom to experiment and execute without worrying about breaking the main design or having to revert unwanted changes.

In the change logs, they announced some other really cool features, and one that I personally am really thankful for is instant auto-compact. Compacting used to take a good 2 to 3 minutes, but now it happens significantly faster because it's likely maintaining histories for each project right in the .claude folder. Claude Code also added a prompt suggestion feature where you can simply press Enter to accept a suggestion or just type a new prompt in its place. You can use the agent flag while starting Claude to run it as the specific agent you have in your project, allowing you to delegate tasks to it directly. Claude Code now allows you to fork sessions and choose between them when you launch Claude with the resume flag. All you have to do is press the Escape key twice and your current session will be forked.

Now, even though background agents are great, there are certain areas where you shouldn't use them, as they will hinder your workflow instead of making it better. For example, you don't want to background any task that requires your input, because that would cause the agent to get blocked and unable to proceed. You also don't want to background any task that requires your approval while it's running. It would just get blocked in the background and you could actually lose track of it if the main agent is busy with another task. It is also highly recommended not to assign tasks that depend on each other, as this can create conflicts in your agents' work. Instead, it's much better to assign isolated tasks to each agent.

There are a few best practices you need to keep in mind to get the most out of this workflow. While using background agents, you need to keep token usage in mind. Even though they speed up your work, each agent consumes a significant number of tokens, so it's important to track this if you want to avoid high bills. Since agents return their output to the main agent, you have to make sure your tasks are isolated. Also, when you're spawning an agent, give it a descriptive name. That way, if you're managing multiple agents at once, you'll know exactly what each one is doing.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
