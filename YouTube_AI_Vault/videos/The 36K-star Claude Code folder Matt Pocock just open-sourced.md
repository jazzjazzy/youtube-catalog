---
title: "The 36K-star Claude Code folder Matt Pocock just open-sourced"
video_id: m8U0dPfuoN8
channel: "[[channels/Indie Hacker News]]"
uploaded: 2026-04-29
processed: 2026-07-05
duration: "7:14"
url: https://www.youtube.com/watch?v=m8U0dPfuoN8
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [structured-agent-planning, claude-code-skill-management]
tools: [Matt Pocock Skills, Claude Code, Cursor, Codex, GitHub Copilot, GitHub, Linear, GSD, BMAD, Spec Kit]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The 36K-star Claude Code folder Matt Pocock just open-sourced

![thumbnail](https://i.ytimg.com/vi/m8U0dPfuoN8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=m8U0dPfuoN8) | 📅 Uploaded [[uploaded/2026-04-29]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> TypeScript educator Matt Pocock open-sourced his personal `.claude` directory — a 110KB, MIT-licensed folder of 14 plain markdown skills he uses daily, no framework or orchestrator — and it hit 36.8k GitHub stars and 2.8k forks within days. Skills like "grill me" (interrogate the plan before coding), TDD, "diagnose," and "improve codebase architecture" are pitched as small composable fixes to specific coding-agent failure modes, explicitly positioned against heavier spec-driven frameworks like GSD, BMAD, and Spec Kit.

**Watch this if:** you want a minimal, no-framework way to add planning discipline and architecture hygiene to Claude Code, Cursor, or Codex without adopting a full orchestration system.

## Key Takeaways
- The repo is just markdown: each skill is one folder with a `skill.md` file (description, when to use it, and the agent prompt) — no orchestrator, no daemon, no runtime, only ~110KB total, MIT licensed.
- Pocock explicitly names and argues against heavier process frameworks (GSD, BMAD, Spec Kit), claiming they take away control and make bugs hard to resolve; his pitch is small composable building blocks over heavier abstractions.
- The README maps four common coding-agent failure modes to specific skills: the agent didn't do what you wanted → "grill me"; the agent is too verbose → "caveman mode"; the code doesn't work → "diagnose"; you built a ball of mud → "improve codebase architecture" — each backed by a quote from The Pragmatic Programmer, Domain-Driven Design, or Kent Beck.
- "Grill me," the most-used skill, interrogates you with question after question until every branch of a plan's decision tree is resolved before any code gets written; "grill with docs" does the same but also writes discovered domain language into a `contract.md` file so the next session starts already informed.
- Other skills: strict red-green-refactor TDD; "diagnose," a structured reproduce-minimize-hypothesize-instrument-fix-regression-test debugging loop; "to PRD" (turns a conversation into a product requirements doc); "to issues" (slices a plan into independently shippable GitHub or Linear tickets); and "zoom out" (explains a piece of code in whole-system context instead of function-level).
- Install is two commands: `npx skills@latest @mattpocock/skills` to pick which skills and which agents (Claude Code, Cursor, Codex, or anything reading a `.claude`/`.agents` directory) to install onto, then a setup command configuring your issue tracker and docs location.
- The repo ships fast — a "setup" skill, a "triage" skill (moves issues through a state machine), and "caveman mode" (strips filler words for ~75% shorter agent output) all landed within the week covered, with community PRs including contributions co-authored by GitHub Copilot.
- Honest caveats: it's one engineer's opinionated best practices baked with his own TypeScript/schema/library preferences, grilling sessions can feel slow for small changes, and a few skills (like a library-specific migration helper) are narrowly tailored to Pocock's own stack.

## 🛠 Tools & Software
- [[topics/Matt Pocock Skills]] — the open-sourced `.claude` skills folder itself: 14 markdown skills for planning, TDD, debugging, and architecture hygiene, installable via `npx skills@latest`
- [[topics/Claude Code]] — one of the primary agents these markdown skills are designed to be dropped into and read via `.claude`
- [[topics/Cursor]] — named as a supported install target for the skills alongside Claude Code and Codex
- [[topics/Codex]] — named as another supported install target for the skills
- [[topics/GitHub Copilot]] — credited as co-authoring community pull requests merged into the repo this week
- [[topics/GitHub]] — hosts the repo itself and is one of the two supported issue trackers the "to issues" skill can target
- [[topics/Linear]] — the other supported issue tracker the "to issues" skill can slice a plan's tickets into
- [[topics/GSD]] — named and explicitly critiqued as a heavier process framework Pocock's approach is positioned against
- [[topics/BMAD]] — named and explicitly critiqued alongside GSD and Spec Kit as taking control away from the developer
- [[topics/Spec Kit]] — named and explicitly critiqued as one of the heavier spec-driven frameworks this minimal approach rejects

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install with `npx skills@latest @mattpocock/skills`, selecting only the skills and target agent(s) you actually want.
- Run "grill me" before any non-trivial change to force the agent to resolve ambiguity up front instead of guessing mid-build.
- Use "grill with docs" on projects with accumulated jargon so a `contract.md` file carries domain language across sessions.
- Run "improve codebase architecture" periodically (every few days) to catch a project drifting into a ball of mud.
- Expect to skip or heavily edit stack-specific skills (like Pocock's own library migration helper) that don't match your tooling.

## 🔗 Related Videos
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: BMAD, Claude Code, GSD, Spec Kit
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/The Fastest-Rising Repo on GitHub Is a Little Scary REA]] — shared: Claude Code, Codex, Cursor, GitHub
- [[videos/The HTTP Header Trick That Cuts AI Agent Costs in Half!]] — shared: Claude Code, Codex, Cursor, GitHub Copilot
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude Code, Codex, Cursor, GitHub

## Timeline
- `0:00` — The story: a TypeScript YouTuber's `.claude` config folder hits 7,400 stars in 24 hours
- `1:14` — Inside the README: naming GSD, BMAD, and Spec Kit as the wrong approach
- `2:07` — Why now: the agent ecosystem's drift toward heavier frameworks and orchestrators
- `2:51` — What's inside: grill me, TDD, diagnose, architecture, PRD, and issue-slicing skills
- `4:21` — Under the hood: one `skill.md` per folder, no runtime, no orchestrator
- `4:55` — Install: two commands via `npx skills@latest`
- `5:13` — Latest changes: setup skill, triage skill, and caveman mode shipped this week
- `5:44` — Who should care: solo builders, teams with jargon drift, TypeScript developers, and skeptics alike
- `6:28` — The verdict: opinionated but real, and worth at least reading

## Transcript
<details>
<summary>Full transcript</summary>

Here is the wildest GitHub story this week. A TypeScript YouTuber published his Claude Code config folder and it gained 7,400 stars in 24 hours. Matt Pocock runs AIHero.dev with about 60,000 newsletter subscribers, and a couple of months ago he started quietly committing his personal `.claude` directory to a public repo called "skills." It sat there for a while, then this week it caught fire — 36,800 stars total, almost 3,000 forks, all under MIT. The interesting part is what's actually inside: this is not another agent framework. No orchestrator, no planner, no spec kit. It's a folder of small markdown files Matt uses every day to ship real code.

The numbers tell the story: 36,800 stars on a repo created only in February, 2,800 forks already, and a hard-line position against vibe coding — and Pocock is the same guy who taught a generation of devs how to actually use TypeScript, so when he says vibe coding doesn't work, people listen. The README opens with a thesis people will love or hate: Pocock calls out approaches like GSD, BMAD, and Spec Kit by name and says they take away your control and make bugs hard to resolve. His pitch is that engineering is hard, and the answer isn't heavier process — it's small composable building blocks you adapt to your own brain. He lists four common failure modes working with a coding agent and names the exact skill he wrote to fix each: the agent didn't do what I want; the agent is way too verbose; the code doesn't work; we built a ball of mud. Each comes with a quote from The Pragmatic Programmer, Domain-Driven Design, or Kent Beck, then a fix that's literally just a markdown file in his Claude folder. The whole repo is tiny, 110 kilobytes, but the philosophy is very specific.

Why is this hitting now? The agent ecosystem has been moving toward heavier abstractions — spec-driven kits, BMAD workflows, multi-agent orchestrators, a new framework every week promising to own the entire process. Pocock is doing the opposite, and it's striking a nerve with engineers quietly skeptical of all of it. The repo facts are wild for something this new: 36,800 stars from a project created February 3rd, MIT licensed, written almost entirely in shell since the skills are just markdown plus tiny installer scripts, and 322 people watching for new commits — unusually high for a config dump.

The actual menu of skills: the most popular is "grill me" — tell the agent what you want to build and it interrogates you with question after question until every branch of the decision tree is resolved; Pocock calls it his most-used skill and says to run it before every single change. A sister skill, "grill with docs," does the same grilling but also writes discovered domain language into a `contract.md` file, so your second session with the agent is faster because the jargon is already documented. "TDD" forces a strict red-green-refactor loop with proper failing tests first. "Diagnose" is a structured debugging loop: reproduce, minimize, hypothesize, instrument, fix, regression test. On the architecture side, "improve codebase architecture" is run every few days and looks for places code is becoming a ball of mud, suggesting deepened modules in the John Ousterhout sense. "To PRD" turns a conversation with the agent into a proper product requirements doc for your issue tracker. "To issues" breaks any plan into independently grabbable GitHub or Linear tickets sliced vertically so each one actually ships. "Zoom out" is small but useful — it asks the agent to explain a piece of code in the context of the whole system instead of the usual function-level explanation.

The implementation is almost insultingly simple: each skill is one folder containing one `skill.md` file with a description, when to use it, and the agent prompt. A tiny installer, `npx skills@latest @mattpocock/skills`, lets you pick which skills you want and which agents to install them on — Claude Code, Cursor, Codex, anything that reads a `.claude` or `.agents` directory. No runtime, no daemon, no orchestrator — just markdown dropped into your project that the agent picks up. Installing takes two commands: the npx installer that pulls in the skills, then a setup command asking which issue tracker you use and where you save docs. After that, every skill is available as a slash command in your agent.

The repo is shipping aggressively — the latest commit landed the day before this video, adding a "setup" skill that walks through configuring all the others. Earlier in the week Pocock added a "triage" skill that moves issues through a state machine of triage roles, and a new "caveman mode" that compresses agent output by about 75% by stripping articles and filler words. Community pull requests are merging at a serious pace, including some co-authored by GitHub Copilot itself.

Who should clone this? A solo builder who already lives in Claude Code or Cursor and has felt an agent burn 20,000 tokens before realizing it built the wrong thing — the grilling skills alone are worth the install. A team whose codebase has accumulated jargon nobody can keep straight — the `contract.md` pattern is genuinely good and survives across sessions. A TypeScript developer specifically gets Matt's actual personal config, meaning his preferences for type safety, schemas, and library choices are baked in. And even an agent skeptic who thinks all of this is overcooked will find this one of the most minimal entry points available — 14 markdown files.

The honest tradeoffs: this is one engineer's personal opinions packaged as best practices, so some skills won't match your stack; grilling sessions can be slow when you just want to ship something small; and a few skills, like a migration helper tied to Matt's own libraries, are extremely specific and won't apply to most people. But for everything that's opinionated about it, the project is real — MIT licensed, almost 3,000 forks, 60,000 newsletter subscribers behind the author, shipping commits this week. If you're building with a coding agent in 2026 and you're not at least reading what someone like Pocock keeps in his `.claude` folder, you're missing the wave.

</details>
