---
title: "You Need Claude Sandboxes... 90% Faster AI Coding"
video_id: xckU9n9r8Rs
channel: "[[channels/AI LABS]]"
uploaded: 2025-09-01
processed: 2026-07-06
duration: "10:43"
url: https://www.youtube.com/watch?v=xckU9n9r8Rs
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [parallel-claude-code-development, bmad-story-splitting]
tools: [Claude Code, Cursor, Conductor, BMAD, Git, GitHub, Claude Desktop]
llms: [Claude, ChatGPT]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# You Need Claude Sandboxes... 90% Faster AI Coding

![thumbnail](https://i.ytimg.com/vi_webp/xckU9n9r8Rs/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=xckU9n9r8Rs) | 📅 Uploaded [[uploaded/2025-09-01]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A live demo of splitting BMAD-method "stories" into parallel, non-conflicting sub-stories, then running multiple Claude Code instances at once — each in its own git worktree via the Conductor IDE — to eliminate sequential wait time. A three-part task that would have taken ~40 minutes sequentially finishes in ~20 minutes (the longest single sub-task) because all three run simultaneously, then get QA-reviewed, fixed, and merged back individually.

**Watch this if:** you use the BMAD method (or any story/task-based AI coding workflow) and want to run multiple Claude Code agents in parallel on the same project without them conflicting.

## Key Takeaways
- The BMAD method turns a project brief into a PRD and architecture.md (built via BMAD's planning agents, droppable into Claude Desktop or ChatGPT), then generates "stories" — large, self-contained tasks sized to fit a single 200k-token context window.
- The core bottleneck: comprehensive BMAD stories take a long time to execute one at a time with a single Claude Code instance, even though they reduce hallucination by pre-planning commands and file locations.
- The fix: git worktrees. Ask the BMAD story-generating (Scrum Manager) agent to examine each story and split it into non-conflicting parallel sub-stories wherever possible, using a custom prompt that tells it worktrees are the parallelization mechanism and everything must merge back at the end.
- In the demo's 7-story project, stories 1 and 7 split into 3 and 2 parallel sub-stories respectively; stories 3–6 stayed single because splitting them would create conflicts.
- Conductor is used to manage the parallel Claude Code instances: each sub-story gets its own workspace/worktree (a fresh codebase copy), the BMAD dev agent is initialized per workspace, tagged to its specific story, and starts working independently.
- Real timing from the demo: sub-task 1 took ~12 minutes, sub-task 2 ~12 minutes, sub-task 3 (custom UI) ~18-20 minutes — run in parallel, total wait time is ~20 minutes instead of the ~40 minutes sequential execution would require.
- After each dev agent finishes, a BMAD QA agent reviews the story's implementation; QA caught only minor concerns in one sub-story but major issues in two others, which then went back to the dev agent for fixes before merging via PR.
- Sequential (non-split) stories still run one after another with no parallel benefit, but the split/parallel stories alone meaningfully cut total development wait time.

## 🛠 Tools & Software
- [[topics/Claude Code]] — runs each BMAD dev/QA agent inside its own git worktree, executing sub-stories in parallel.
- [[topics/Cursor]] — the codebase is also shown open in Cursor to inspect the repo state (docs vs. merged app code) alongside Conductor.
- [[topics/Conductor]] — the IDE used to create per-story workspaces (git worktrees) and run multiple Claude Code instances in parallel with a visual UI, preferred over plain terminals.
- [[topics/BMAD]] — the planning/story-generation method whose PRD → architecture → stories → dev agent → QA agent pipeline structures the whole project; a custom prompt is used to make its Scrum Manager agent generate parallel-friendly stories.
- [[topics/Git]] — git worktrees are the core mechanism enabling multiple isolated, conflict-free working copies of the same codebase.
- [[topics/GitHub]] — the repo is synced to GitHub; completed sub-stories are merged back to the main branch via pull requests.
- [[topics/Claude Desktop]] — one option (alongside ChatGPT) for running BMAD's bundled planning agents to brainstorm the PRD and architecture docs.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — powers every Claude Code instance running BMAD dev/QA agents in parallel worktrees.
- [[topics/ChatGPT]] — cited as an alternative place to drop BMAD's planning-agent bundle for brainstorming the PRD/architecture.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Before running a large BMAD story, ask the Scrum Manager agent (with a custom prompt) whether it can be split into non-conflicting parallel sub-stories built around git worktrees.
- Try Conductor to manage multiple Claude Code instances across git worktrees instead of juggling terminals or a single IDE window.
- After each parallel sub-story completes, run the BMAD QA agent before merging — don't skip review just because tasks ran in parallel.
- Merge completed sub-stories back to main one PR at a time, and only parallelize stories that are genuinely independent — leave conflicting/sequential stories as single tasks.

## 🔗 Related Videos
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: ChatGPT, Claude, Claude Code, Cursor
- [[videos/Anthropic Released A New Way To Vibe Code]] — shared: BMAD, Claude, Claude Code, Git
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Cursor, GitHub
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Claude, Git, GitHub
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, Git, GitHub
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Cursor, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Cursor, GitHub
- [[videos/The 36K-star Claude Code folder Matt Pocock just open-sourced]] — shared: BMAD, Claude Code, Cursor, GitHub

## Timeline
- `0:00` — The problem: powerful AI coding workflows create long sequential wait times.
- `0:38` — The fix: git worktrees + BMAD method for parallel development.
- `2:07` — Demo setup: BMAD's PRD and architecture.md from planning agents (Claude Desktop / ChatGPT).
- `3:00` — Stories generated by Claude Code from PRD/architecture; dev agent implements, QA agent validates.
- `4:14` — Splitting stories into parallel, non-conflicting sub-stories via a custom Scrum Manager prompt.
- `5:38` — Using Conductor to create per-story workspaces (worktrees) and initialize the dev agent per story.
- `7:38` — Real timing comparison: ~12/12/18-20 minutes per sub-task in parallel vs. ~40 minutes sequential.
- `8:49` — QA agent catches major issues in two sub-stories; dev agent fixes and re-submits.
- `9:53` — Merging completed sub-stories back to main via pull requests.

## Transcript
<details>
<summary>Full transcript</summary>

AI coding has become incredibly powerful, but it's created a new problem in my workflow: the wait time. You might think it's not significant, but that's probably because you're not using context engineering methods yet. The best framework for this is the BMAD method. It's essentially a step-by-step approach for using AI agents like Claude Code and Cursor to build real projects. It starts with structured planning, mapping out everything before implementation begins. With this planned approach, it creates stories — tasks designed to be completed in a single run using the full 200k context window. But here's the issue: when you run these stories, they're so comprehensive that they take considerable time to execute. And today, I'll show you exactly how to eliminate this waiting problem.

So, the solution I'm going to show you in this video uses GitHub worktrees at its core. If you're not familiar with them, they essentially copy your entire codebase into a sandboxed environment where you can work independently. By giving Claude these sandboxed environments and using the BMAD method in a specific way, I can enable parallel development. This means a single large task gets divided into multiple parallel tasks, allowing multiple agents to work on them simultaneously and drastically reducing my wait time.

To show you the demo, I'm just going to take this example project that I'm starting. I'm using the BMAD method in this. I won't dive into the complete workflow or setup process, but I will give a basic overview as you need that to understand the video. Otherwise, you'll be confused here — I have linked a detailed video on it in the description below. Even if you skip the video, I highly recommend checking it out on GitHub. It truly represents how AI coding will be done moving forward with these agents.

The starting point is the PRD and the architecture.md file. These are made by BMAD's team of planning agents. The agents are bundled into one file and you can drop them into Claude Desktop or ChatGPT. I brainstormed my idea with them, which initially was to build a Mac app but evolved into a simple web app. The main goal was helping people learn Mac keyboard shortcuts through an on-screen interactive keyboard. After the whole brainstorming process, I got the two documents and put them into the docs folder.

Once these two documents are complete, stories are generated based on them. Stories are essentially your project divided into big tasks that normally take developers weeks to complete. Each story contains everything required to complete a task, including the commands and where the code is supposed to be placed, since it's all pre-planned. This significantly reduces hallucination chances. These stories were generated using Claude Code, as shown here — it creates stories directly from the PRD and architecture documents. And in our case, it has been designed for parallel development, which we'll explore after covering the basic workflow. I currently have seven main stories generated by Claude Code.

After story generation, we use task-specific agents from the BMAD method. Each story is implemented by the BMAD dev agent through a slash command in Claude Code. Once implementation is complete, we use a QA agent to validate the code and ensure the dev agent correctly followed its task in the story. If tests need to be run, the QA agent handles those as well. Through this way, even if errors are made, there is a check loop that can catch and fix them.

Normally with the BMAD method, I follow a step-by-step approach by doing one task at a time. The problem with this is that a single Claude Code instance is doing the whole task, which slows down the process. This is what we'll solve with this multi-agent system. Now, here's what you're going to do: we ask the BMAD story-generating agent to examine each story and determine if it can be broken into multiple non-conflicting subtasks. If possible, split them into separate stories.

This project originally had seven tasks. The agent split the first story into three parts, the second story into three parts. Stories 3 through 6 stayed singular because dividing them would create conflicts. Story 7 became two tasks. This is how you can do parallel work with Claude Code. I'll show you exactly how much time a Claude agent took per story component. Once you see the numbers, you'll understand why this approach is essential.

The BMAD method might already have this division logic built in from a recent update — I'm not certain, but I created a custom prompt for this, which I'll share in my resources. The stories are generated by the Scrum Manager agent. My custom prompt instructs it to automatically generate stories optimized for parallel development instead of just asking it to create stories. It also ensures the agent understands we're using git worktrees as the core to prevent conflicts and that everything must merge back together at the end. I ran the SM command with this custom prompt and it generated stories made for parallel development.

Now, how do you actually use git worktrees? Worktrees aren't new — developers have used them for version-controlled software development for years. You can use them through the terminal, but there's a better way with Claude Code. I've been using Conductor. It lets you run multiple Claude Code instances in parallel using git worktrees in this IDE with this amazing UI. Even if you're not using this entire method, I recommend Conductor with Claude Code — I prefer it over terminals or using it in an IDE like Cursor. You can also manage multiple projects in Conductor. As you can see, I have two projects, Mac Shorts and a test project that I was experimenting with. I've implemented three stories here designed not to conflict with each other. I can complete story 1.1 regardless of whether story 1.2 or 1.3 are done or not — I could also start directly with story 1.3.

But before starting, you need to have a git-initialized repository which is also synced with GitHub. Currently, only the base version is in the repository — the three changes haven't been pushed yet, because I wanted to demonstrate this first. That's why the repository and Cursor still only have the docs and not the app.

Now, here's how you can use Conductor. For the multi-part stories, copy its name, go to Conductor, and create a new workspace with it. These workspaces are new worktrees that Claude will use. This creates a fresh copy of the codebase in which different Claude Code instances can work independently without conflicts. Next, initialize the dev agent using its specific command. Understanding the BMAD method is essential here — it's extensive with many commands as well. I've been using it for a while, so navigation is familiar, but there's a learning curve, and it's worth the investment. Then tag the story you're working on. This is the full command for Claude Code to work on that specific story. When initialized, it spins up the full-stack developer and begins working. I really appreciate Conductor's UI compared to the terminal — it makes using Claude Code much more pleasant. Even without the story-splitting workflow, using Conductor with Claude Code in a git project is an excellent experience.

Now I discovered something interesting while preparing this demonstration. Since these tasks are already completed, they only display the tool calls, messages, and commits. The actual time taken was only shown while they were running. So to demonstrate the timing for you, I ran the first task again — as you can see, it's been 8 minutes and we're on the sixth to-do. When I originally ran these, the first task took around 12 minutes and the second took about the same. The third task was the longest, involving custom UI implementation — that one took between 18 and 20 minutes.

Here's where the problem becomes clear. Imagine a single agent handling all of this sequentially. With the BMAD method, the setup would still be the same, but the time investment would be significantly higher. Normally the BMAD method would bundle all of this into one large story, or at best split it into two stories that would still execute one after the other. But by running them in parallel instead, I changed the entire equation. Even though the longest task still took 20 minutes, that became my total time, not the 40 minutes it would have taken running them sequentially. That's the real power of the multi-agent workflow — you're not waiting for each piece to finish before starting the next one. Everything happens simultaneously and you only wait for the longest task to complete.

Now moving on, I ran the dev agent next to start the implementation. After that, I called the QA engineer with its review-story command. QA was crucial here — it caught minor concerns in this story, but in stories 1.2 and 1.3, there were major issues requiring fixes. After the QA review, I called the dev agent again — it reviewed the QA feedback and fixed everything. That's how I completed all three stories.

Now let me explain why this initial setup took so much time and benefited from parallel processing. The first story was the foundation, initializing Next.js and installing dependencies — that was a complete task. Then the second story was the data layer — for this keyboard-focused project, we loaded all keyboard information and app data we needed. The UI components took the most time; it involved generating custom components from our pre-planning phase, and the dev agent had to follow that plan exactly. All that was just initial setup. If a single agent had handled all three parts sequentially, it would have taken significantly more time. This was why splitting tasks and using multiple agents was crucial — it maintains quality while reducing time.

After completing the story, you create a PR and ask Claude Code to merge it into the main branch. You can see the PR has been created here — it includes 104 Mac keyboard shortcuts from story 1.2's data layer. Looking at the pull request, we can merge it. Once merged, you'll notice our data folder is now in place. I'll merge story 1.2 and 1.3 one by one, then continue working on the second, third, and fourth stories through Conductor. The sequential stories from story 3 to 6 can't be parallelized since they weren't split further. However, the broken-down stories will significantly reduce development time and minimize waiting periods.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
