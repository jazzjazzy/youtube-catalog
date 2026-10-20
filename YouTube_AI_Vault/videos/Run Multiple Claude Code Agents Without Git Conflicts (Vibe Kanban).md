---
title: "Run Multiple Claude Code Agents Without Git Conflicts (Vibe Kanban)"
video_id: W45XJWZiwPM
channel: "[[channels/Zen van Riel]]"
uploaded: 2026-01-07
processed: 2026-07-06
duration: "9:27"
url: https://www.youtube.com/watch?v=W45XJWZiwPM
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [parallel-agent-coding]
tools: [Vibe Kanban, Claude Code, Git, VS Code]
llms: [Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Run Multiple Claude Code Agents Without Git Conflicts (Vibe Kanban)

![thumbnail](https://i.ytimg.com/vi/W45XJWZiwPM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=W45XJWZiwPM) | 📅 Uploaded [[uploaded/2026-01-07]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Running many Claude Code instances at once usually causes merge conflicts and unreviewed code. This video demos Vibe Kanban, an open-source Kanban board that runs each agent task in its own isolated git worktree/branch, so you can build a Plants vs. Zombies clone with three parallel Claude Code agents, review diffs and leave inline comments, then safely rebase, resolve conflicts, and merge each branch into main.

**Watch this if:** you want to run several Claude Code agents in parallel on the same repo without stepping on each other's changes.

## Key Takeaways
- Running many Claude Code instances at once on a shared branch causes two problems: merge conflicts from overlapping file edits, and unreviewed code that can hide production bugs.
- Vibe Kanban organizes agent work as Kanban tasks; each task, when started, spins up an isolated git worktree/branch for that agent so parallel agents don't collide by default.
- Tasks are written like spec-driven development prompts (a to-do card with a detailed description) — Claude Code (Opus, the default model shown) picks the task up and works in its own branch.
- Even with isolated worktrees, conflicts can still occur where logic overlaps (e.g. a shared "plant registry" file both new features need to edit) — Vibe Kanban surfaces this at merge/rebase time.
- The workflow keeps a human-in-the-loop: a task moves to "in review" when the agent session finishes, and you inspect the diff, test the branch, and only then merge to main.
- You can leave inline code-review comments on specific lines and send them back to the agent, which resumes using the full conversation history for that task/branch to make the requested change.
- When a merge conflict does appear, you can either resolve it manually or ask Claude Code itself to resolve it — the video shows Claude Code fixing a plant-registry conflict automatically.
- Every agent session is saved and browsable in the Kanban board, unlike raw terminal sessions which are hard to recover if a terminal or machine is lost.

## 🛠 Tools & Software
- [[topics/Vibe Kanban]] — the open-source orchestration tool at the center of the video: creates tasks, runs isolated git worktrees per agent, tracks review status, and handles rebase/merge into main.
- [[topics/Claude Code]] — the agent used for all three parallel coding tasks (new plant features, debug panel), running under the Opus model by default.
- [[topics/Git]] — git worktrees and branches are the isolation mechanism Vibe Kanban relies on; rebasing and merging are demonstrated directly.
- [[topics/VS Code]] — opened via Vibe Kanban's "open in IDE" action to inspect and run the code in a task's specific branch.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — named as Vibe Kanban's default model driving the Claude Code agent sessions shown in the demo.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Vibe Kanban and point it at a repo to try running 2-3 Claude Code tasks in parallel on isolated branches.
- Write task descriptions like spec-driven prompts (clear, detailed) so the agent has enough context to work independently in its own worktree.
- Review each task's diff and leave inline comments before merging, rather than merging agent branches directly to main.
- When a merge conflict appears after rebasing, try asking Claude Code to resolve it before resolving manually.

## 🔗 Related Videos
- [[videos/Planning In Claude Code Just Got a Huge Upgrade]] — shared: Claude Code, Claude Opus, Git, VS Code
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, Git
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, Git
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, Claude Opus, Git
- [[videos/Claude Code Skills Just Got Even Better]] — shared: Claude Code, Claude Opus, VS Code
- [[videos/Claude Code Task System ANTI-HYPE Agentic Coding (Advanced)]] — shared: Claude Code, Claude Opus, Git
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude Code, Claude Opus, VS Code
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude Code, Claude Opus, Git

## Timeline
- `0:00` — Why running many parallel Claude Code instances usually fails: merge conflicts and unreviewed code.
- `0:58` — Vibe Kanban overview; demo project is a Plants vs. Zombies clone built to showcase parallel work.
- `1:28` — Creating the first task (cherry bomb plant) as a spec-driven description card, using Claude Opus by default.
- `2:19` — Creating a second task (squash plant) and starting it while the first is already running.
- `3:12` — Starting a third task (debug panel) — three Claude Code agents now working simultaneously.
- `3:41` — Explaining git worktrees: each agent works on its own branch off main, visible in VS Code.
- `4:37` — Human-in-the-loop merge process: tasks move to "in review" when the agent session finishes.
- `5:19` — Reviewing diffs, leaving inline code comments, and sending revision requests back to the agent.
- `6:29` — Opening a task's branch in VS Code and testing the cherry plant in the running game.
- `7:15` — Merge conflict appears between two plant features sharing a registry file; resolved by asking Claude Code to fix it.
- `8:23` — Rebasing and merging the debug panel and squash plant branches, then testing the finished features in-game.

## Transcript
<details>
<summary>Full transcript</summary>

Many people are trying to run 10 Claude Code instances at once to speed up their AI coding. But everyone who does this will run into two issues. First of all, Claude Code is going to cause massive merge conflicts because all of these different agents will try to change the same files. And secondly, you don't even understand the code these agents are writing, which is going to lead to massive production bugs. But today I'm showing you Vibe Kanban, which is a really great open-source project that you can use today to organize all of these agents and to check up on the code to make sure that you can speed up your AI coding while still keeping control of what you're actually doing.

Today's demo app is going to be a clone of the very popular game Plants vs. Zombies, and it's just a bit of a fun game to showcase what it means to do a lot of parallel work. Because with this kind of game development, you will see that you can actually parallelize a lot of the things that are needed to make the game work properly. For example, this is a game where you're supposed to create plants that can defend against zombies, right? We're going to be using Vibe Kanban to actually orchestrate my agents. And I'm going to pull it up right here, and it's all hosted locally. So I can just go into my PVZ clone, which is the repository, and you can see that I already finished quite a lot of tasks. And these tasks were all done through Vibe Kanban and created this first proof of concept. It's not very beautiful, but of course I'm not creating any assets here — it's all just created with AI code.

What we're going to do now is we're going to create two tasks to create new plants to try and defeat the zombies faster. So first I'm going to click here on a plus in to-do and I'm going to write the task: add a cherry bomb plant to the game. And this is just going to be very similar to your spec-driven development — here you need to describe in detail what you're trying to build. So in this case I have a little bit of an explanation already that I'm just going to copy paste here to explain that this is an instant-use explosive plant that will explode in a 3x3 area. And this is already enough for Claude Code to then pick up on these changes in my main branch, using the default model which is Claude Opus at the moment. So I can just go ahead and create the task. I can decide to not start it yet and then it will just be added to my Kanban board, just like with a regular scrum/agile process, and then I can move it into "in progress" and now I can manually say that I want a Claude agent to start working on this in the base branch. So we're going to go ahead and start it, and then you'll be able to see the code changes come in.

But before we do that, we're just going to go ahead and create a new task specifically to create the squash plant, and this one can just squash zombies that are right in front of the plant. So I'm just going to go ahead and paste the same kind of description here. So we're going to go ahead and create that task like so. And in this case we can just go check out the other task here, and you can see that it's already working — it's reading all of the files to understand how to create a plant. And the great part about this is that the logic for these two different plants can live in different files, so you're not going to get a merge conflict. However, there are some places in this kind of game where these two plants will overlap in terms of the code that has to be changed — for example, the top bar here that determines all the plants available for you to use. So I'm expecting a merge conflict to come up.

But while these two tasks are running, let's create one more task. I'm still kind of developing this clone, and it would be nice to have a bit of a debug menu for me to give myself more sun power, or just spawn in some zombies to test if specific plants are working properly. So I'm going to go and create a new task for that. We're going to go ahead and type "debug panel features," and I'm just going to prompt it with some of the things that I want, like that zombie spawner and the plant cooldown toggle. So I'm just going to paste that in here, and we can go ahead and start creating that immediately.

Now while Claude Code is thinking in three different agents, I wanted to let you know that you can check out my free newsletter in the description down below so you can keep up to date with these kinds of AI projects and advance your career with real AI coding.

I want to share with you why this is so effective. If you check out Visual Studio Code, you'll be able to see that we don't just have our main branch — we actually have these specific subtrees that these agents are working in on their own. So they're not all working on the main branch; they have their own branch based on main that they are now editing. So you can, for example, already see the cherry plant has a branch here where the properties of the plant are being determined already, and all of this is just being done in its own branch. And you'll see the changes for the squash plant and the debug panel show up in here as well.

And so the idea with this is that you can very easily create a lot of parallel work and then carefully merge it into your branch. And this is where the human loop comes in — you're going to be the person pressing the button to merge all of this work into main. The great part is before you merge, you can test out the specific branch. You can just have code reviews that I'll show you later. And only then, when you know the code actually works, will you be pushing it into the main branch.

So we can already see that the cherry one is in review. And what does it mean when a task is in review? Well, it means that Claude Code has finished the session, and as a human I can actually check out the code and see if everything works as intended. When I open this, you can see that I can check out the entire Claude Code session, which is properly saved into memory. And that's really nice because if you know anything about Claude Code terminal sessions, if you close all of them, it's very difficult to get a visualization of what happened — if your computer crashes, you have a pretty big problem. You can go back into the history of previous chats, but it's not as nice an interface as just being able to see all of the sessions in this Kanban-style board.

I can even go back into those first tasks and check out how exactly this was implemented. So if you want to check out how the cherry plant was implemented, we can go ahead and click this button here to see the diff — basically just see all the code changes that were made. The great part about this too is that you can have some comments on a specific line of code — write the comment like so: "I want you to double check this code." And then if I extend this window just a little bit, you can see here that you have both that commenting capability as well as the capability to just send over your review comments to the AI agent in order to just revise some code.

So for example, one thing that I can do is I can clear my review comments and I can ask it to change the cost to just 100. Of course this is a small change, I could have done that myself, but I just want to show how this really works. So now I'm asking Claude Code to change the cost to just 100, which it will be able to do — because even though LLMs are stateless, it's able to pick up on the work by reading the entire conversation history of this specific task, as well as working in that feature branch. So now, very quickly in just a couple of seconds, it was able to start a new Claude Code session and change the cost from 150 to 100 sun. Very cool stuff.

Now to check out what this code does, I can go ahead and go to the triple dots here and open it in the IDE. This will just open Visual Studio Code in the correct branch folder. And now I can just go ahead and run "npm run dev" to just restart my dev server. And you can see that the plant is in there right now. And just in time here, we're going to try and see if the cherry plant works. And there you go, it successfully seems to work.

Now I want to make sure that this piece of code is actually going to be in my main branch. All I need to do is just click on the merge button here, and that's it — now the code is merged. And you can even see here that that task is automatically moved into the done section.

Now let's see if the squash plant works as well. So I'm going to go ahead and open a diff here. You can see that I actually will not be able to merge it properly because it's also one commit behind. So I'm just going to rebase this to make sure that we can merge it safely. And now you can see — whoops, we have a conflict, because we were adding two plants, and even though the plant logic lives in different files, the actual registry of all the plants is in the same file. And you can see here that these two parallel agents were already in conflict with each other trying to edit the same file.

Now the great part about this is that I can solve it myself, or I can ask Claude Code to resolve this specific conflict. Because it's a small change, I know that Claude Code can do this successfully, and I'm just going to ask it to do that safely. And you can already see here that with my very small-scale app, even though I was running just three parallel agents, I already have a merge conflict. But because I'm now using something like Vibe Kanban, I'm able to just take care of this. And indeed, you can now see that the merge conflict is solved simply by adding those two plants next to each other, which is totally fine.

And while it's doing that, let's go ahead and exit out, because we can probably merge the debug panel without any issues, simply because I'm pretty sure all of that code lives in different places. So if I try to merge, you will see that it's not going to happen because the base branch has moved forward. I need to first rebase this branch to make sure it has all the latest changes for main, and then I can merge it successfully. So indeed, we got it merged, and now in the new version of the app we actually have the debug panel, and I'm able to just give myself extra sun or just spawn a bunch of zombies just so I can test everything out. There you go, they're coming along now, and the cherry plant will take care of them.

So, coming back to the squash plants, we're just going to rebase one more time now that the merge conflicts are solved. We're going to merge the branch. And now, if I just double check, we can indeed see we've got a nice little plant. So I can just go ahead and test it out by waiting for a zombie. And then if I spawn it in here, you can see that it squashes it. And there you go, it disappears.

Now, this game is obviously a toy example — I'm not going to rebuild a game that's already existed for over 15 years. The video here was really more about the workflow, understanding how to properly analyze and understand which parts of your software can be parallelized, and then using something like Vibe Kanban to do that in a very structured way. If you want to keep track of AI coding trends in 2026, make sure to sign up for my newsletter in the description down below. And then I'll see you next time.

</details>
