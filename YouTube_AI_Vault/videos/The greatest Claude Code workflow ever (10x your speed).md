---
title: "The greatest Claude Code workflow ever (10x your speed)"
video_id: WdD6uD_kupY
channel: "[[channels/Alex Finn]]"
uploaded: 2026-01-13
processed: 2026-07-06
duration: "17:13"
url: https://www.youtube.com/watch?v=WdD6uD_kupY
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [claude-code-multitasking-workflow]
tools: [Ghostty, Claude Code, VS Code, Cursor, GitHub, Antigravity]
llms: [Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The greatest Claude Code workflow ever (10x your speed)

![thumbnail](https://i.ytimg.com/vi_webp/WdD6uD_kupY/sddefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=WdD6uD_kupY) | 📅 Uploaded [[uploaded/2026-01-13]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Alex Finn argues that running Claude Code inside the Ghostty terminal — instead of the VS Code/Cursor extension or desktop app — is the fastest, most efficient workflow because it avoids the heavy memory usage that slows a computer down when multiple editor windows are open, and it gets new Claude Code features (like plan mode) first. He then builds a full AI-driven habit-tracking app live, demonstrating plan mode, running multiple Claude Code instances/terminal splits side by side for multitasking, and using Git branches/worktrees to safely run several agents on the same project at once.

**Watch this if:** you use Claude Code across multiple projects at once and your computer bogs down running several VS Code/Cursor windows simultaneously.

## Key Takeaways
- Running Claude Code's CLI in a lightweight terminal (Ghostty) instead of inside VS Code or Cursor avoids the heavy memory/CPU overhead of running multiple full editor windows — you can have "hundreds" of terminals open without slowing the computer down.
- Claude Code's CLI/terminal version reportedly gets new features (e.g. plan mode) before the VS Code extension or desktop app.
- Ghostty is a free, highly customizable terminal (thousands of themes) that supports easy window/pane splitting (`split right`) and multiple tabs, letting you run a dev server right next to Claude Code in one window.
- Plan mode (`shift+tab` twice) works best in the terminal version — asking Claude Code to "feel free to ask me questions" at the end of a prompt encourages more clarifying questions, and the host says the more Claude interviews you before building, the better the resulting app turns out.
- Core multitasking pattern: open a second (or third) Ghostty window/tab running its own Claude Code instance to work on a different project (or a different role — e.g. "you're a project manager for this app, review it and suggest improvements") while the first one builds, instead of getting distracted on social media while waiting.
- To safely run Claude Code on the same project in multiple windows at once, explicitly ask it to create a new branch and work tree for the second task — this is standard Git/GitHub functionality that keeps concurrent agents from overwriting each other's changes (requires the project already be pushed to GitHub).
- Split a terminal (`file > split right`) to run `npm run dev` in one pane while working in Claude Code in the other, so you can copy server error logs straight into the Claude Code conversation without switching apps.
- The host notes that with a strong-enough model (Opus 4.5 in this workflow), you rarely need to manually inspect or edit code — but when you do, opening a file directly (which happened to launch Antigravity as his default editor) and closing it afterward keeps memory usage low.

## 🛠 Tools & Software
- [[topics/Ghostty]] — the customizable, lightweight terminal the entire workflow is built around, used to run Claude Code, split panes for dev servers, and multiple simultaneous Claude Code windows.
- [[topics/Claude Code]] — run via CLI inside Ghostty, using plan mode to interview the host before building a habit-tracking app, and run in multiple parallel instances for different tasks.
- [[topics/VS Code]] — named as one of the slower alternatives (extension/CLI) the host moved away from due to memory consumption when running multiple windows.
- [[topics/Cursor]] — named alongside VS Code as a heavy, memory-intensive alternative that slows down when running several instances for multitasking.
- [[topics/GitHub]] — branch and work-tree creation (requested directly through Claude Code) is used to let multiple Claude Code windows safely work on the same project without conflicting.
- [[topics/Antigravity]] — mentioned as the editor that happened to open by default when the host needed to manually edit a file/environment variable.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4.5 is credited as reliable enough that the host says he rarely needs to review the code it writes.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install Ghostty (ghostty.org) and run Claude Code inside it instead of a VS Code/Cursor extension if multitasking across projects is slowing your machine down.
- Use plan mode (`shift+tab` twice) and end prompts with "feel free to ask me questions" to get Claude Code to interview you for better-specified apps before it starts building.
- Split your terminal to run your dev server in one pane and Claude Code in the other so you can paste error logs straight across without alt-tabbing.
- When running Claude Code on the same project in more than one window, explicitly ask it to create a new branch and work tree for each task to avoid agents overwriting each other's work.

## 🔗 Related Videos
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Cursor, GitHub
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor, GitHub, VS Code
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Claude Opus, Cursor, GitHub
- [[videos/Planning In Claude Code Just Got a Huge Upgrade]] — shared: Claude Code, Claude Opus, GitHub, VS Code
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Cursor, GitHub
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, GitHub
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Antigravity, Claude Code, Claude Opus

## Timeline
- `0:00` — Intro: after testing 15 ways to use Claude Code, this is the fastest/most efficient.
- `0:22` — Why the terminal (Ghostty) beats VS Code/Cursor extensions and the desktop app: memory usage and getting new features first.
- `2:41` — Ghostty introduction: free, customizable, pane splitting, multiple tabs, simple setup.
- `5:16` — Building the app: plan mode, the habit-tracker prompt, and Claude Code's clarifying questions.
- `8:02` — Multitasking demo: opening a second Ghostty window to brainstorm features for another app while the first app builds.
- `10:21` — Running the same project in multiple windows safely via Git branches/work trees.
- `12:32` — Reviewing the finished habit-tracker app, splitting the terminal to run `npm run dev` alongside Claude Code, and debugging via copy-pasted server logs.
- `14:07` — Running a third Claude Code window as a "project manager" role feeding suggestions to the main "developer" window.
- `15:26` — Wrap-up: editing files directly when needed, and why this is the host's favorite workflow right now.

## Transcript
<details>
<summary>Full transcript</summary>

I have figured out the best workflow ever for Claude Code. After testing all 15 possible ways you can be using Claude Code, the way I'm about to show you is the fastest, best, and most efficient. Whether you're brand new to Claude Code or a seasoned vet, if you stick with me until the end, you will be building faster with Claude Code than you ever have before. Let's get into it.

So, this is Ghostty. What you're looking at here might not look like much, but this is by far the best way to be using Claude Code. We've covered this in a prior video, but there are a few popular ways to use Claude Code — the extension inside Cursor or VS Code, the desktop app, or the CLI in VS Code. Up until now, the CLI in Visual Studio Code was the best — it gave a really nice interface to see code while working with Claude Code. But there's one major issue that made using VS Code or Cursor with Claude Code intolerable: speed. If you have more than one VS Code or Cursor open at a time, it slows your computer down to a halt. If you've been using Claude Code, this is probably how you use it: VS Code open, either the extension or the CLI open, and if you want to work on two or three projects (which the creator of Claude Code recommended doing in a previous video), you'd have to open two or three of these VS Codes or Cursors. The memory consumption on these apps is unbelievably high — open a second or third one and your computer basically turns boiling hot and slows to a crawl.

That's where the Claude Code CLI in the terminal comes in, specifically Ghostty. This is the reason it's the best: you can have hundreds of these terminals open and your computer will still run fine. So it's by far the best on speed, and also the best on features and functionality — something figured out over the last month or so is that Claude Code in the terminal gets all the updates and features first. It got the latest plan mode before all the others, before the extension, before the desktop app. Using it in the terminal, you get the best features and functionality, and it lets you multitask because you can open up so many terminals without slowing your computer down — you can work with as many Claude Codes as you want at the same time. The CLI in the terminal, specifically Ghostty, destroys the CLI in VS Code, the desktop app, the extension, any other way you use it.

Setting it up: go to ghostty.org (two Ts), hit download, it's completely free. Ghostty is a customizable terminal with more features and functionality — exactly like the terminal on your PC or Mac, except much easier to use. You can customize it with thousands of built-in themes and colorways, easily split the terminal (one click, "split right" gives a second terminal in the same window, so you can run servers right next to Claude Code), and use multiple efficient, easy-to-switch tabs. It's just more usable, quick, and efficient than VS Code, Cursor, or your regular terminal. Setup is simple: if you've never used Claude Code before, take the install command (in the description), paste it into Ghostty, sign up for a subscription on Claude's site, and you're set. Once Claude Code is installed, just type `claude` inside Ghostty and you'll see it open up.

Now let me show you my workflow: building a full application with Claude Code inside Ghostty — how I multitask, run servers, edit code files, my full workflow beginning to end, and why it's the absolute best. First, after opening Claude Code inside Ghostty, go into plan mode (shift+tab, then shift+tab again) — you'll see "plan mode on." Plan mode inside Claude Code in the terminal is the best plan mode out of them all (I've tested them all) — the desktop app only just got plan mode, and the extension's plan mode used to be "nerfed" in that it wouldn't ask you questions. The terminal's plan mode has the latest features and is by far the most powerful.

Here's the prompt (pause and grab it from the description): "I want to build out a habit tracking app. I want it to be beautiful but simply themed. I want it to track my habits, streaks, and excellent animations and visuals that make the app satisfying, and allow me to track my mood. I'd also like advanced AI functionality. Feel free to ask me questions to come up with more ideas." Claude's plan mode already asks clarifying questions by default, but explicitly inviting more questions encourages it to ask even more — the more Claude Code interviews the host, the better the app turns out, so he always adds that line.

After hitting enter, Claude starts asking a ton of questions, which he loves: "We're going to make this a web app. What kind of AI features are you envisioning?" — he picks an AI habit coach that actually coaches which habits to do. "What visual style appeals to you most?" — dark and elegant. "How do you want to visualize your progress?" — all visualization types, just to see what fits. He finds this question flow much smoother in the terminal than in the extension. It continues: "How should habits be organized and tracked?" — simple checkboxes; "What AI provider" — Claude's API; "How should data be stored?" — local browser storage; mood-tracking granularity — kept simple. He likes that plan mode surfaces details he hadn't considered (like mood-tracking design) purely by asking about them.

While the app builds, he opens a second Ghostty window to work on another project (Creator Buddy) — a common mistake is getting distracted (social media) while an agent works, and the fix is multitasking instead. This kind of parallel work was painfully slow in VS Code/Cursor due to memory overhead, but trivial in Ghostty. He asks the second Claude Code instance, in plan mode, "Take a look at our app — which other features should we add to increase engagement?" so now two Claude Code instances are working: one building the habit tracker, one brainstorming Creator Buddy features. Referencing a prior video about Boris (Claude Code's creator), who reportedly runs five Claude Code windows at once, the host prefers just two for focus, though the same approach scales further.

On working on the same project across multiple windows: yes, this is possible — just ask Claude Code to create a new branch in a new work tree, standard Git/GitHub functionality that keeps each window's code changes separate so agents don't overwrite each other. This requires the project already be on GitHub. (He offers a dedicated video on this multi-window-per-project workflow if there's interest.) A major advantage of the Ghostty approach is that these terminal windows take up very little screen space compared to VS Code/Cursor's code-heavy interface — you only see what Claude Code is doing, not the code itself, and with a model as capable as Opus 4.5, you rarely need to check the code it writes.

Once the habit tracker finishes building, he demonstrates debugging: `file > split right` splits the terminal, runs `npm run dev` on the right (serving on localhost:3003) while continuing to work with Claude Code on the left and watching server logs on the right. The finished app: a dark, elegant habit tracker with streaks, an "Add Habit" flow (icon + color picker), mood tracking, a confetti effect on completion, Apple-Watch-style progress rings, and an Insights tab. When a couple of errors show up in the server logs, he copies them straight into Claude Code for a fix — all without leaving the one screen, which he credits for both speed and memory efficiency.

He then opens a third terminal/window, launches a third Claude Code instance in the same habit-tracker project, and assigns it a different role: "You're a project manager for this app — take a look at the app and give me a rundown for improvements." Good suggestions from this "project manager" Claude get copy-pasted into the "developer" Claude on the left — true multitasking that wasn't feasible with VS Code/Cursor's slowness. If he wants a fourth window as a "marketer" writing tweets, that's equally possible.

For manual file edits (e.g. environment variables): just open a Finder window, navigate to the file, and open it — in his case, this happened to launch Antigravity as the default editor; he makes the change and closes it again to conserve memory. Because Opus is capable enough, this kind of manual intervention is rare. One more tip: to make changes to the same project in a second window without conflicts, explicitly tell Claude Code to "create a new branch for a second feature we are building and put it in a new work tree" — this keeps the two sets of changes from stepping on each other, provided the project is already pushed to GitHub (again, offering a dedicated video on this if requested).

Having tried every Claude Code workflow out there as of this posting, this is his favorite — fastest and most efficient for keeping the computer responsive while multitasking easily. He acknowledges this space moves fast and next week's "best workflow" might look different, but for now, this is it. If you learned something, like the video, subscribe, and check out Vibe Coding Academy (linked in the description) for a community of vibe coders with weekly calls. See you in the next video.

</details>
