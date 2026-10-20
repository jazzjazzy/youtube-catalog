---
title: "Introducing /visual-plan - rich plans for Claude Code + Codex"
video_id: NE0aBuQF0HA
channel: "[[channels/Steve (Builder.io)]]"
uploaded: 2026-06-16
processed: 2026-07-05
duration: "4:26"
url: https://www.youtube.com/watch?v=NE0aBuQF0HA
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [agent-plan-review, pr-review-automation]
tools: [Claude Code, Codex, GitHub]
llms: []
protocols: [MDX, HTML, Markdown]
transcript: true
tags: [youtube, ai-automation]
---

# Introducing /visual-plan - rich plans for Claude Code + Codex

![thumbnail](https://i.ytimg.com/vi/NE0aBuQF0HA/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=NE0aBuQF0HA) | 📅 Uploaded [[uploaded/2026-06-16]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Steve (Builder.io) introduces /visual-plan, a Claude Code + Codex skill that turns plan-mode's wall of markdown into interactive MDX — diagrams, wireframes, interactive API specs, and annotated code you can review and comment on before the agent builds — plus a companion /visual-recap skill for reviewing what an agent (or a PR) actually did.

**Watch this if:** you skim past Claude Code's plan-mode markdown and keep missing details until after implementation.

## Key Takeaways
- Claude Code's plan mode outputs a huge markdown essay that's easy to skim past, causing small but important details to get missed until after implementation.
- /visual-plan generates plans as MDX with interactive components: diagrams, interactive API specs, schema/diff views, annotated code, and pan-and-zoomable wireframes you can comment on and iterate on before the agent starts working.
- A companion skill, /visual-recap, produces the same kind of interactive visual summary after an agent finishes work — or for reviewing someone else's pull request — instead of a terse summary or a granular line-by-line diff.
- The underlying bet is that engineering is moving to a "plan level" of abstraction, similar to how developers stopped reasoning in assembly once they trusted C compilers — as agents get more reliable at implementing a clear plan, humans can reason and collaborate at the plan/spec level instead of the code level.
- MDX (not raw HTML or plain markdown) was chosen as the output format because it supports reusable, customizable components, stays consistent across different agents/models, and checks into a repo more cleanly than generated HTML "slop."
- Both skills and the MDX-generating application are open source on GitHub and installable via a CLI, along with a GitHub Action that posts an interactive visual-plan snapshot directly in pull request comments.

## 🛠 Tools & Software
- [[topics/Claude Code]] — one of the two agents /visual-plan and /visual-recap are built for; used in plan mode
- [[topics/Codex]] — the other target agent for these skills, alongside Claude Code
- [[topics/GitHub]] — hosts the open-sourced skills/app; also where the companion GitHub Action posts visual-plan snapshots on pull requests

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MDX]] — the chosen output format for visual plans/recaps, replacing markdown and HTML for reusable, consistent, interactive components
- [[topics/HTML]] — rejected as a plan format: slow/verbose to write and doesn't look good checked into a repo
- [[topics/Markdown]] — the current default plan-mode output; the format /visual-plan is trying to move past

## ✅ Action Items
- Install the visual-plan skill (BuilderIO/skills on GitHub) and try it in Claude Code or Codex plan mode instead of reading raw markdown plans.
- Use /visual-recap after an agent finishes work, or on a teammate's PR, instead of relying on a text summary or line-by-line diff.
- Set up the accompanying GitHub Action to post an interactive visual-plan snapshot in PR comments automatically.
- Fork the MDX-generating app to add your own custom components if the defaults don't fit your stack.

## 🔗 Related Videos
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, GitHub
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Codex, GitHub
- [[videos/I Open-Sourced My Own AFK Software Factory]] — shared: Claude Code, Codex, GitHub
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Codex, GitHub
- [[videos/OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)]] — shared: Claude Code, Codex, GitHub
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: Claude Code, Codex, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Codex, GitHub
- [[videos/The 36K-star Claude Code folder Matt Pocock just open-sourced]] — shared: Claude Code, Codex, GitHub

## Timeline
- `0:00` — The problem: plan mode's wall of markdown text and missed details
- `0:14` — Building /visual-plan: MDX instead of markdown or HTML
- `0:29` — What it generates: diagrams, interactive API specs, wireframes
- `0:52` — Reasoning at the "plan level," like trusting a C compiler
- `1:18` — The reverse skill: /visual-recap for reviewing agent work
- `2:19` — Catching mismatches early with wireframes and visual recaps
- `2:39` — Why MDX over HTML: reusable components, cross-agent consistency
- `2:58` — Open-sourced skills and CLI available on GitHub
- `3:58` — GitHub Action: visual-plan snapshots posted on every pull request

## Transcript
<details>
<summary>Full transcript</summary>

Plan mode in Claude Code is incredible, but I always find my eyes glazing over this huge markdown essay in my terminal. And I've realized after I implement things that I totally miss some important small details that were not clear to me at first because it was just too much stuff to read, honestly. I've been experimenting with this new skill I made called visual plan. It's somewhat inspired by that post about how HTML is better than markdown, but HTML can be slow and verbose to write, it doesn't look good checked into a repo, and I found I can make much better visual plans with reusable components. So I made a skill called visual plan. It generates plans as MDX with super visual components, diagrams, API specs that are interactive, schema design changes, annotated code, and even pan and zoomable wireframes. Every UI lets you look at a wireframe first, comment on it, iterate, answer open questions visually and interactively, and then have the agent work. I found this to be a much more intuitive interface for me to reason about what the agent's doing.

It's really made me feel like humans and engineering is entering a new abstraction phase where we reason about things at the plan level. As long as the plan's what we want, agents are getting more and more reliable executing on that — almost to the degree to which we trust a C compiler to compile to assembly reliably. As long as the plan is good, and we make the plan clear, consumable, easy to understand, easy for people to reason about, share, comment, etc., more and more we can trust the agents to implement it as expected.

I also made a skill for the reverse of this. I call it visual recap. What it can do is after the agent works, give you a recap of everything it did — the same idea: wireframes, interactive API specs and diffs, schemas, annotated code, etc. So now when you're reviewing what the agent has done for you, or looking at a pull request for somebody else's code, rather than looking at a small summary or a super granular line-by-line mess, you can see a visual recap — interactive, easy, intuitive. You can even share these with others to comment, and then pass the comments and feedback to the agent to improve. This has let me catch stuff way sooner, before the agent does something I didn't realize, because maybe the text sounded fine, but the wireframe makes me realize, "Oh wait, no, that's not what I had in mind." Or in a more clear and visual way, I see what types of APIs I want to create and I'd like them shaped differently. I'm able to catch stuff earlier as well as afterwards in recaps of my work or someone else's work — matching things that maybe aren't as obvious just looking at React and Tailwind code, confirming they're actually what I wanted before it goes out to production.

It's tedious to hand-test every single thing every time. Having a snapshot at a glance that's clear, and that I can interactively drill into, has been a game-changer compared to just static markdown. And all of this is customizable — you can add your own components, customize the components. It's MDX, a better format for checking in. It can do way more, and there's consistency too — it's not just random HTML every time. This move to MDX from HTML, from previously markdown, is the full circle I needed. I'd much rather see MDX raw files in code versus HTML, and there's so much more you can do with reusable components than generating HTML "slop" every time, different every time. It also means when you change agents or models, you get consistency as well.

I open-sourced all of this — the skills, and the application that generates MDX, which you can fork and customize with your own components. You can check it out on GitHub, install and try it out with the CLI I made. I'd love to know your feedback — not just whether you like the plans or recaps, or whether it's handy (including the fact that you can install a GitHub Action with the CLI), but also whether this new idea of how we reason as engineers makes sense.

I really believe the plan level is the real reasoning level we're going to be thinking in, talking in, and working in, and I want to make it clear and beautiful and a good experience. As we trust agents more to implement correctly, and other agents check the work against the plan and the implementation spec, we can work faster and get our minds out of the details — like how people don't look at assembly much anymore; they reason at the level of C, and that opened up new abstractions and the ability to move fast, but safely. I think this opens up new ways of collaborating — you can share the same plan with product managers, designers, etc., so everyone reasons about the areas they care about, like design/wireframes for some and behavior for a PM.

One more thing I think is cool: there's also a GitHub Action I made that can run this automatically on every pull request and show you a snapshot of a visual plan right there in the comments every time — you can click in and interact with it, making it easier and more consumable to review pull requests. So again, it's not just a choice between a short description and a long, granular line-by-line diff — you actually see visuals, diagrams, interactive API specs, more consumable code, and even annotated code. Anyway, it's all free and open source, you can find it on my GitHub. Let me know what you think.

</details>
