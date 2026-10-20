---
title: "How to Enable the TUI in the Dashboard: Session Recovery Tips & Prompts"
video_id: J9tyn8b6dqM
channel: "[[channels/Clearmud]]"
uploaded: 2026-05-24
processed: 2026-07-05
duration: "6:18"
url: https://www.youtube.com/watch?v=J9tyn8b6dqM
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [session-recovery, agent-dashboard-setup]
tools: [Hermes, Tailscale, WSL2]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# How to Enable the TUI in the Dashboard: Session Recovery Tips & Prompts

![thumbnail](https://i.ytimg.com/vi_webp/J9tyn8b6dqM/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=J9tyn8b6dqM) | 📅 Uploaded [[uploaded/2026-05-24]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A walkthrough of enabling the built-in TUI chat inside the Hermes agent dashboard, plus the session-recovery trick (find session → play → ask for state → continue) and a set of copy-pasteable prompts for resuming, checkpointing, naming, and validating sessions.

**Watch this if:** your AI agent workflow breaks whenever a chat interface clears, refreshes, or resets and you don't know how to get your context back.

## Key Takeaways
- The Hermes dashboard's TUI chat isn't enabled by default — the easiest path is to prompt your own agent to install and enable it (with auto-start on host reboot) rather than doing it manually.
- The core insight: the chat surface is not the session — closing a tab, hard-refreshing, or clearing the terminal doesn't destroy the underlying session or its context.
- Recovery trick: go to the sessions tab, find the most recent session, hit the play button, and it restores full context even after a hard refresh.
- A "resume" prompt ("continue from where we left off, first summarize the current state in five bullets") gives a fast TL;DR of a long-running session.
- A "checkpoint" prompt (current task, last verified state, next action, approvals needed) is useful for handing off unfinished work between sessions or days.
- A "wrong session check" prompt has the agent confirm what it was working on before proceeding, and stop if the context doesn't match — a safeguard against acting in the wrong session.
- Operational rules: never expose port-forwarded dashboards without a security layer like Tailscale, and Windows users currently need WSL2 for the TUI chat to work (a native one-click Windows install is in beta).

## 🛠 Tools & Software
- [[topics/Hermes]] — the agent dashboard whose built-in TUI chat is enabled and demoed, including session recovery via the sessions tab
- [[topics/Tailscale]] — recommended security layer for anyone port-forwarding the dashboard
- [[topics/WSL2]] — currently required on Windows for the Hermes TUI chat to function

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Prompt your agent to install and enable the Hermes TUI chat, and set it to auto-start when the host PC restarts.
- Bookmark the sessions tab and use the play button as your standard recovery path after any refresh or crash.
- Save the resume, checkpoint, session-naming, and wrong-session-check prompts from clearmud.ai/resources for reuse.
- If port-forwarding the dashboard, put Tailscale (or an equivalent) in front of it before exposing it.

## 🔗 Related Videos
- [[videos/How Hermes Agent Can Save You 85 (Or More) in BG Task Token Cost]] — shared: Hermes, WSL2

## Timeline
- `0:00` — Intro: enabling the built-in TUI chat feature in the Hermes agent dashboard
- `0:39` — Goal for the video: enable TUI chat, which is off by default
- `1:02` — Recommends prompting your own agent to install/enable it rather than doing it manually
- `1:57` — The trick: find a session, hit play, ask for state, then continue
- `2:41` — Live demo: a hard refresh to simulate losing a session
- `3:10` — Session restores with full context after hitting play
- `3:25` — Resume prompt: "continue from where we left off, summarize in five bullets"
- `3:41` — Checkpoint prompt for handing off unfinished work
- `4:08` — Session-naming prompt for easier lookup later
- `4:19` — Wrong-session check prompt to confirm context before continuing
- `4:32` — Operational rules: use Tailscale for port forwarding, WSL2 required on Windows
- `5:46` — Final thoughts

## Transcript
<details>
<summary>Full transcript</summary>

Today, I'm going to show you how to enable the built-in chat feature in the Hermes agent dashboard. It's an awesome nifty way to use your TUI chat within the dashboard. I'm going to give you some tips and tricks, as well as some copy-pasteable prompts that you can use to make your life easier. So, without further ado, let's build. All right. So, as you can see here on the screen, I had my executive assistants, Sneo and Muddy, prep this visual prop for us. To follow along, and you know, if you want to check this out, go to clearmud.ai/resources. This is completely free to access, and you can copy-paste any of these prompts to make your lives easier.

So, you know, what we're going to do today is we're going to enable the TUI chat feature within your Hermes dashboard. It doesn't come pre-configured or enabled by default. We have to do that manually. So, there's one of two ways to accomplish that, right? You can do it manually, which usually requires installing some prerequisites. Although, I will admit, my agent does this for me. So, I have tested running this Hermes dashboard TUI command, and it works. But, I highly recommend just prompt your agent to do it for you. All you got to do is come to this resource tab, copy-paste this text here, or say something along the lines of I'd like to enable the built-in TUI chat for my Hermes dashboard. Please install it and enable it by running that command. Make sure it's always on in the background, so even if our host PC restarts, the dashboard comes back online, and the TUI chat is always enabled. I'm going to give you a visual on what that looks like here.

So, as you can see here along the left, we have this really cool chat feature, right? And look, it's that TUI chat that you would normally access in the terminal, right? Don't just stop there. Right? You can see the chat tab, as I showed you there. It survives a close and reopen. Sessions are visible. Now, here's a little trick that I didn't know by default. I actually had somebody in the community share this with me, but you can actually find the session, click play, ask for state, then continue. The play button is that recovery path. So, if you do close your tab, if you do do a hard refresh by accident, and you think you lost your session, or you have to start from scratch, that's not the case. You can actually go into your dashboard, go into the sessions tab here, and then you'll see your most recent sessions, and all you got to do is hit this play button right here, and it will take you back into that TUI chat session. Right? So, and let me give you just a quick visual of what that looks like.

So, I'm going to do a hard refresh here. How you doing today? All right, I'm not giving it any complex tasks right now. We're in the middle of a demo. Great. Now, let's say I hard refresh this, and I lose that session. Let's say I did a whole bunch of work in that session, and I don't want to have to re-explain myself, right? Well, all you have to do is go over to the sessions tab, and you'll see that most recent session here. All you got to do is hit this play button, and voila, it restores that session with all of the context. Here are some copy-paste of prompts, more so for checking the state and getting a summarization.

Let's say you have a long-standing session, you did a whole bunch of work, you don't even remember everything that you did. Well, here's a very useful resume prompt. So, once you go into sessions, hit play, and restore the session, you can say continue from where we left off, first summarize the current state in five bullets. Right? So, you get that TLDR of what that session's about. Alternatively, you could write a checkpoint prompt, where we say, "Before you continue, write a short checkpoint, current task, last verified state, next action, and anything I need to do to approve before you proceed." So, let's say you were working on something all day the day before, and you didn't finish. Well, this is a great way to kind of figure out where you left off, and figure out what is the next task, and what do you need from me, right? Another thing is the session naming prompt. Nifty feature, right? You can just prompt in there saying, "Hey, name this session," whatever you want to name it, so it's easier to find in the sessions tab. And then, you can also do a wrong session check. Before doing any new work, tell me what task this session was handling, the last useful result, and the next action. If the context does not match, stop. Right? And some small operational rules. This should go without saying, please please do not do any port forwarding without proper security harnesses in place, right? Namely, Tailscale, which is one of the most popular solutions. Windows users do need WSL 2, at least at the time of recording this. This may very well change, as I know that the Hermes agent team is working on a beta solution for a kind of a one-click install EXE file on Windows. As of now, that does not work. But, you do need WSL 2 installed for this chat to work.

And then, use sessions as that operating aboard, right? Don't feel like anything ever gets lost. Don't feel like once you close the session, right? It's gone forever. No, all you got to do is just go find it, hit play, and alternatively, you can start a fresh session, give it enough context, and say, "Hey, find the session where we did X, Y, and Z." It will take some time, but it will find it. And then, a reopen chat tab starts fresh unless you resume, as you saw throughout this demo. I did a few hard refreshes, and you saw real time what happens, right? And yeah, I hope you found some value in today's video. Now, I'm not an AI expert. I'm building in public and sharing what actually works. If you'd like to see me make a particular video around a specific topic, drop a comment below. Let me know who you are, what you do, who your target audience is, and what your question is, and I will add a video to my queue custom tailored just for you. Thank you so much for tuning in to today's video. My name is Marcelo. This is Clear Mod, and clarity matters.

</details>
