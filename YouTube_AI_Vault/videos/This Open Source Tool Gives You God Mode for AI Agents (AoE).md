---
title: "This Open Source Tool Gives You God Mode for AI Agents (AoE)"
video_id: fPz9OB3Bau8
channel: "[[channels/Better Stack]]"
uploaded: 2026-05-06
processed: 2026-07-05
duration: "5:55"
url: https://www.youtube.com/watch?v=fPz9OB3Bau8
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [multi-agent-orchestration, terminal-workflow-management]
tools: [Agent of Empires, Claude Code, Codex, Docker, Git, tmux, Agent Deck]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This Open Source Tool Gives You God Mode for AI Agents (AoE)

![thumbnail](https://i.ytimg.com/vi/fPz9OB3Bau8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=fPz9OB3Bau8) | 📅 Uploaded [[uploaded/2026-05-06]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Agent of Empires (AoE) is a free, open-source terminal dashboard that sits above your existing coding agents (Claude Code, Codex, etc.) to run and monitor many of them at once, using git worktrees for branch isolation and optional Docker sandboxes for safety. A single `brew install aoe` and `aoe launch` replaces terminal-juggling and status-guessing with one TUI showing every agent's running/waiting/idle/error state.

**Watch this if:** you're running two or more CLI coding agents at once and losing time to terminal chaos, branch collisions, or not knowing which agent is stuck.

## Key Takeaways
- AoE doesn't replace coding agents like Claude Code or Codex — it's an orchestration layer that sits above whatever you're already running.
- Install is one command (`brew install aoe`, then `aoe launch`); pressing the N key spins up a new named agent instance directly in the TUI.
- It solves four concrete problems: terminal chaos (one view instead of many tmux sessions), status blindness (running/waiting/idle/error shown without attaching), branch conflicts (git worktrees give each agent its own branch, same repo), and safety (optional Docker sandboxes contain agent access).
- Sessions survive restarts and can reportedly be checked from a phone via a mobile dashboard; per-project profiles and a built-in diff viewer are also included.
- Compared to tmux, AoE adds awareness and automation on top of raw persistence; compared to Agent Deck, AoE leans further into structure — worktrees, Docker, and parallel workflows built for scale.
- Real user feedback cited: status-at-a-glance and worktrees+Docker together are the most praised features; rough edges remain in the still-evolving web dashboard and there have been tmux-integration bugs (fixed quickly).
- Verdict: worth it if you're running two-plus CLI agents; if you only run a single agent, it won't change much for you, though it's free and quick to try.

## 🛠 Tools & Software
- [[topics/Agent of Empires]] — the open-source TUI "mission control" dashboard reviewed in this video; orchestrates multiple coding agents from one screen
- [[topics/Claude Code]] — one of the coding agents AoE sits above and was demoed spinning up as a managed agent instance
- [[topics/Codex]] — named as another coding agent AoE orchestrates rather than replaces
- [[topics/Docker]] — used for optional sandboxes so agents run contained instead of with full system access
- [[topics/Git]] — git worktrees give each parallel agent its own branch in the same repo, eliminating collisions
- [[topics/tmux]] — the baseline terminal multiplexer workflow AoE is directly compared against and built on top of
- [[topics/Agent Deck]] — a similar orchestration tool named as AoE's closest comparison, with AoE going further on structure/scale

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install AoE with `brew install aoe` and run `aoe launch` to try the TUI dashboard on your existing agents.
- If running multiple CLI agents, switch to git worktrees per agent to eliminate branch collisions.
- Turn on Docker sandboxing before letting agents run with broad file/system access.
- Skip it if you only run one agent at a time — the value only shows up at two-plus concurrent agents.

## 🔗 Related Videos
- [[videos/I Open-Sourced My Own AFK Software Factory]] — shared: Claude Code, Codex, Docker
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Claude Code, Docker, Git
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Git
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Codex
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, Codex
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Codex
- [[videos/Agent memory resolved]] — shared: Claude Code, Codex
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Git

## Timeline
- `0:00` — AI agent chaos: tabs, tmux sessions, and stuck agents becoming unmanageable at scale
- `0:31` — What Agent of Empires is: a mission-control dashboard that sits above your existing agents
- `1:00` — Live demo: installing AoE with `brew install aoe` and running `aoe launch`
- `1:12` — Spinning up two Claude-based agents side by side using the N key
- `1:45` — How AoE fixes terminal chaos with one unified view
- `2:32` — Git worktrees give each parallel agent its own branch, same repo, zero collisions
- `2:56` — Docker sandboxes contain agent access for safer parallel workflows
- `3:31` — AoE vs tmux and Agent Deck: awareness/automation and heavier structure for scale
- `5:01` — Real user feedback: status-at-a-glance and worktrees+Docker praised most
- `5:26` — Weaknesses (evolving web dashboard, past tmux bugs) and final verdict

## Transcript
<details>
<summary>Full transcript</summary>

Running one AI coding agent, it's easy. We do it all the time. Running five or 10 at once, it turns into a mess real quick. Tabs everywhere, tmux sessions you can't track, one agent stuck, another wrecking your branch, and you have no idea which is which. This is Agent of Empires, the mission control dashboard that lets you command all your AI agents from one screen. In the next 60 seconds, I'll show you why this is picking up traction.

All right. Now, quick reset here. Agent of Empires is not another coding agent, okay? No. It doesn't replace Claude, Codex, or anything else. It just sits above them. It runs everything you're already using in your workflow. And this matters now because things changed. 1-2 years ago, we ran one agent. Now, we're running multiple agents, 5, 10, 20, whatever the number is. And the real problem isn't AI quality, it's how we manage these agents while working together. You don't know what's running. You don't know what's still stuck. Your terminals are multiplying. Branches collide, and sometimes, or more often than not, things are breaking quietly. Agent of Empires fixes that. Let me show you.

If you enjoy coding tools to speed up your workflow, be sure to subscribe. We have videos coming out all the time. All right. Now, to install this, it's one command. I'm on a Mac, so I brew install AOE, then I can run AOE launch. And this is where it really comes together. This screen, the TUI, this is your entire agent system, okay? So, now let's make this real. Let's just spin up two agents here using Claude. One working on auth, one refactoring this API. I can press the N key here to generate this. Now, normally, this is multiple terminals, multiple branches, and lots of switching. Here, it's already organized for us.

Now, watch this. After pressing N key, I give it a name. This one's running, right? I can generate a new one. This one's waiting. I didn't attach anything. I didn't guess. I can go into the first one. I can prompt it. I can switch to the other one. I can run the prompt. And I can monitor the two as they're going through making their changes. I can jump in. I can jump out. I can switch between them instantly. And they are building everything out together where I can come back here and monitor everything. I can even group agents into folders. I can create more. And here's the part most people don't expect. This is the simple part.

Now, let's break down why this matters. I mean, this was insane, right? A really good UI for this. So, that's why it matters. Because this either saves you time or it doesn't. Now, the first problem we have is this terminal chaos. We're running too many sessions, so we're switching too much. Our brain is doing the routing internally. AOE replaces that with one view we can now switch between with everything visible. Our next problem is the status blindness. You don't know what your agents are doing. So, we have to keep checking, right? You end up keep checking again and again. That is just costing you more time, right? And it breaks your flow. AOE shows you running, waiting, idle, error without actually attaching anything. So, we go from guessing to actually knowing what's happening.

Then we have branch conflicts, agents stepping on each other, overriding work, and creating just a big mess. AOE uses Git worktrees where each agent gets its own branch, same repo with zero collisions. The last problem here this solves is the safety. Giving agents full access can be risky. AOE adds optional Docker sandboxes. Agents can now stay contained. Your system stays safe. Plus, session survive restarts. You could check from your phone if you wanted to, which is honestly kind of cool. Profiles per project and diffs built in.

Now, again, this is awesome. It does not replace your tools. It just doesn't. All it does, remember, is it sits above them. Tmux gives you persistence. AOE gives you more awareness and automation. Agent Deck is similar, but AOE leans heavier into structure, worktrees, Docker, parallel workflows, built for actual scale. Then, yes, IDE agents are great for single files. AOE is for running multiple agents across a full repo.

All right. Now, here's what people actually like. Status at a glance changed everything, right? This is great. That comes up a lot. We can visually see everything here. I can check agents from my phone. I didn't actually try this, okay? So, don't take my word on that, but this has the power to do that. It's pretty cool. It's bigger than it sounds. Worktrees plus Docker finally made it safe. That's good. And a lot of people say the same thing. It feels like there is a lot more control over what's actually happening cuz we have all this right here in our terminal that I can alternate between.

But no, it's not perfect. There's a learning curve. Honestly, not much. It was super easy to set up. If you don't like terminals, well, this is a terminal interface. Sorry. The web dashboard is still evolving. There are still rough edges, and there have been bugs like Tmux issues, but they got fixed really fast. And oh, guys, honestly, if you're running one agent, you don't need this, okay? This is for controlling multiple agents, and that is where this is really going to shine. So, is it worth it? Well, yeah. If you're running two or more CLI agents, absolutely yes. Check it out. Install it today. It's open source. It's free. It's going to save you a boatload of time. It reduces your mental load. All this really good stuff. It just really just keeps you in the flow. If you're running a single agent, this isn't going to change anything, okay? But it takes a minute to try, so you can still try it. That's a big upside there. If you enjoy coding tools and tips to speed up your workflow, be sure to subscribe to the Better Stack channel. We'll see you in another video.

</details>
