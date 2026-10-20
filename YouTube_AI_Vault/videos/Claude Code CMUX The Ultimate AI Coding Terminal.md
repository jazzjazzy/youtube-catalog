---
title: "Claude Code + CMUX: The Ultimate AI Coding Terminal"
video_id: 8oLP8oxqtOE
channel: "[[channels/Better Stack]]"
uploaded: 2026-03-04
processed: 2026-07-05
duration: "6:18"
url: https://www.youtube.com/watch?v=8oLP8oxqtOE
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [agent-terminal-workflow]
tools: [Cmux, Claude Code, OpenCode]
llms: [Claude, Claude Haiku]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code + CMUX: The Ultimate AI Coding Terminal

![thumbnail](https://i.ytimg.com/vi_webp/8oLP8oxqtOE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=8oLP8oxqtOE) | 📅 Uploaded [[uploaded/2026-03-04]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Cmux is a native macOS terminal built specifically for coding agents, letting them open and control a browser in a split pane, spawn multiple sub-agent instances across panes, and send custom notifications, all through a CLI and Unix socket API. The video walks through live demos with Claude Code and OpenCode showing browser control, parallel sub-agents, and notification workflows.

**Watch this if:** you run coding agents on macOS and want a terminal that gives them direct control over browsers, sub-agent panes, and notifications instead of juggling separate apps.

## Key Takeaways
- Cmux is a native Mac terminal (not related to tmux) built on libghostty and bonsplit, with tabs, splits, and a CLI/socket API agents can call.
- Agents can drive a browser inside a split pane (navigate, type, click links) with access to developer tools for debugging, similar in design to other agent-browser APIs.
- Claude Code can spawn multiple sub-agent instances in separate Cmux panes (e.g., one to understand a project, one to analyze code) and have them report back to the main instance before closing.
- Cmux notifications (including a flashing-border "trigger flash" command) let an agent alert you when a background pane finishes or needs attention.
- Because Cmux communicates purely through a CLI and Unix socket, it works with any agent harness — the video demos it with both Claude Code and OpenCode.
- Extra features not fully demoed include progress bars, custom workspace colors, agent-driven tab renaming, and reading your existing Ghostty config.
- Setup still requires manually copying in the creator's Claude/browser skills and Claude Code hooks rather than an automated installer.

## 🛠 Tools & Software
- [[topics/Cmux]] — the native macOS terminal for coding agents; demoed controlling a browser, spawning sub-agent panes, and sending notifications.
- [[topics/Claude Code]] — the primary agent harness driven through Cmux's CLI in most of the demos.
- [[topics/OpenCode]] — shown working inside a separate Cmux workspace to prove Cmux is agent-harness-agnostic.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model powering the Claude Code demos.
- [[topics/Claude Haiku]] — switched to for the demos to avoid wasting tokens on simple tasks.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Cmux and try having Claude Code open a browser split pane to navigate and test a page.
- Set up a two-instance sub-agent workflow (e.g., one analyzing code, one summarizing) that reports back to a main Claude Code session.
- Grab the creator's Claude/browser skills and Claude Code hooks to get notifications working automatically.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/Never hit Claudes Usage Limit Again]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/Opus 4.6 + Agent Teams Makes Claude Code Insane]] — shared: Claude Code, Claude Haiku, OpenCode
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Claude Haiku
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Claude Haiku

## Timeline
- `0:00` — Intro: Cmux gives coding agents browser control, sub-agent panes, and notifications via CLI/socket API.
- `0:25` — What Cmux is: a native Mac app built on libghostty, unrelated to tmux.
- `0:42` — Walkthrough of the Cmux CLI: workspaces, split panes, sidebar info, tmux-compatible commands.
- `1:33` — Claude Code uses the Cmux CLI to open a browser pane, search Google, and click a link.
- `2:27` — Claude Code spawns two sub-agent instances in split panes to analyze the project and report back.
- `3:25` — Using Cmux notifications and "trigger flash" so an agent can flag when it needs attention.
- `3:47` — OpenCode is opened in a separate workspace to show Cmux works with any agent harness.
- `5:00` — Other Cmux features mentioned: progress bars, workspace colors, tab renaming, Ghostty config support.
- `5:31` — Final thoughts: recommends the creator's Claude/browser skills and hooks, wishes setup were more automated.

## Transcript
<details>
<summary>Full transcript</summary>

This is Cmux, a terminal built for coding agents that gives them the ability to open and control a browser, create sub-agents in different panes, send you custom notifications, and much, much more through a CLI and a socket API. But, with so many other terminal agents like Warp, WezTerm, and iTerm, what makes Cmux so special? Hit subscribe and let's get into it.

Despite its name, Cmux has nothing to do with tmux. It's a native Mac app built on top of libghostty that uses a webkit browser and bonsplit for the layout, so tabs, panes, and so on. But, the real magic lies in the way the agent communicates with the app. Let me show you. So, after installing Cmux and setting it up, we should see a regular-looking terminal that supports tabs. We can do splits, either vertical or horizontal ones, and we can have tabs inside those splits if we want to as well. Now, with Cmux installed, we should also have access to the Cmux CLI, which gives us options for a bunch of things like creating a new workspace and new split panes, showing information like logs and progress in the sidebar, and even using tmux compatible commands. All this is thanks to the Cmux Unix socket, which we'll talk about later.

But, let's do something interesting. First, I'm going to clear this. I'm going to open up Claude Code, which we can see has now changed the sidebar title. We'll change the model to Haiku so that I don't waste any tokens, and then I'm going to ask Claude to use the Cmux CLI to open the browser in a new split pane, then navigate to google.com, type hello world into the input, and do a Google search. So, if I hit enter, then Claude will do his thing. And here it's learning how to use Cmux. It's opened the new tab to Google, and let's see if it does the search. Okay, it's starting to struggle, and it's done search for hello world, and it's done the search perfectly. And I can even ask it to click on links. So, let's say I want it to click on this IMDb link over here. I can say click on the hello world link from IMDb, and Claude will go ahead and do that. What's really cool is that even inside this split pane browser, I have access to the developer tools, which will help to debug pages that I'm working on. All this is done with browser commands that is similar to the API design of other agent browser tools.

So, the benefit of having this side-to-side browser terminal view is that the agent can navigate through the browser, do testing, and send back its results, which you can see as a developer in real time. Let's try something else. I'm going to close this tab, clear all this information. I'm going to ask Claude to create two instances of itself in split panes, one to understand the project, and another to analyze the code of this project. And when they're done, they should give the information back to the main Claude instance, and then close the panes. So, if we hit enter, it creates two split panes, and then it opens Claude in both of them. And now we can see it's giving them instructions, which is wild to see in real time. Now, the panes that aren't selected are a bit dark, so we can click on them to make them brighter. I'm going to fast forward this part of the video since it's going to take a while. And now that both splits are done, Claude has closed them automatically, and has got information from the first instance here, and the second instance down here, which is very cool, and you can imagine so many uses for this for checking permissions on different sub agents to make sure they don't get stuck.

But, one problem with the demo I just went through is that whenever one of them had a notification or needed my help, there was no easy way for me to know that. But luckily, Cmux makes that easy. Let's try something else. In a new Claude code session, I'm going to give it a prompt to create a new instance of Claude in a split pane using Cmux, and then in that pane, ask it to study and suggest code improvements for this project. Once it's done, write an appropriate notification using Cmux, and run trigger flash to get my attention. The trigger flash command activates a blue flashing border on the specified pane. So, while that's going, I'm going to create a new workspace, and in here, I'm going to run open code. Now, the beauty of Cmux is that because it's a CLI, it can run with any agent harness. And just as I finish opening open code, we can see we have a notification from Cmux. If I click on the bell, we can see the parallel analysis has started. So, it hasn't quite finished. But if I click on the notification, it shows me the right pane that has the information. Now, it didn't quite do what I asked it to. So, I'm going to tell it to do it again. And while that's going, let's actually go back to open code and do what I was going to do originally, which is to use the Cmux CLI to add the name of the project branch and use an appropriate icon next to the name of that branch. Now, I'm going to hit enter and let it do its thing. And we can see we have a notification from Cmux, which is the parallel analysis has started. And it looks like it started properly this time. We can even see the message inside the sidebar. So, now it's done, I'm going to ask it to close the split pane and clear the sidebar text. And we can see here it added the name of the branch with an appropriate icon.

Now, all of these examples were really simple. But I hope it gives you a glimpse into the powerful things that the Cmux terminal can do when an agent has control over it. And I didn't even go through some awesome features like being able to use a progress bar, adding a custom color to your workspace, using the agent to rename tabs, showing all the options in the command palette, and the fact that Cmux can read and apply your Ghostty configuration. Now, I used Cmux without any hooks or skills and I disabled the sandbox in Claude Code because I would have got an error. But I highly recommend you getting the Claude and browser skills for Cmux made by the creator and also setting it up with Claude Code hooks to automatically send you notifications or even writing a custom script. All this makes Cmux much more useful. But I do wish there was an easier way to set this up from scratch instead of manually having to copy and paste the skills and notifications in place. Just like with skills.sh that automatically detects what agent harness you have and applies the skill to the right directory, I wish Cmux did the same to help with setting the whole thing up, but Cmux is already an awesome tool and I'm sure a setup script can be added later on. I really like the fact that it's a native Mac app, which is good for memory and performance, and the fact that the CLI communicates with the app via JSON through Unix sockets, which helps make communication fast and simple.

</details>
