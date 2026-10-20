---
title: "Supercharge OpenCode With 1300+ Free Skills in One Command Makes It 100x  Powerful"
video_id: baGKgnbQUq8
channel: "[[channels/AI Stack Engineer]]"
uploaded: 2026-03-29
processed: 2026-07-05
duration: "9:53"
url: https://www.youtube.com/watch?v=baGKgnbQUq8
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [agent-skill-installation, opencode-workflow-scaffolding]
tools: [OpenCode, Antigravity Awesome Skills, GitHub]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Supercharge OpenCode With 1300+ Free Skills in One Command Makes It 100x  Powerful

![thumbnail](https://i.ytimg.com/vi/baGKgnbQUq8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=baGKgnbQUq8) | 📅 Uploaded [[uploaded/2026-03-29]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A one-command install wires the free, open-source "antigravity-awesome-skills" repository (1,300+ expert-level skill.md files, 28,000+ GitHub stars) into OpenCode, giving it on-demand, domain-specific instructions instead of generic output. The video installs it, explains OpenCode's on-demand skill-loading mechanism, tours the skill categories and trust levels, and builds a real project-management dashboard live using brainstorming, front-end design, React patterns, and API security skills in sequence.

**Watch this if:** you use OpenCode and want senior-developer-quality, structured output instead of generic scaffolding on real features.

## Key Takeaways
- OpenCode out of the box relies on general knowledge and produces generic output for anything requiring real structure (proper component architecture, security-aware APIs, TDD workflows) — skill.md files close that gap by giving it structured, domain-specific instructions it loads only when referenced, avoiding wasted context.
- The antigravity-awesome-skills repo (v9.1a, 28,000+ stars, 4,000+ forks) works natively across OpenCode, Claude Code, Gemini CLI, Codex CLI, Cursor, Kiro, and GitHub Copilot, but this video's setup focuses specifically on OpenCode.
- Install via an NPX command with a `--path` flag pointing at the project root (for per-project skills) or the global agents path (for skills available across all projects) — OpenCode auto-discovers skills from both project and global folders, plus any `.opencode/skills` folder found walking up to the Git root.
- Verify installation with `/skills` inside OpenCode to list everything that loaded; also run `/init` to generate an `agents.md` file describing your codebase's structure and conventions, and commit it to Git.
- Skills are listed by name and short description in OpenCode's native skill tool so the agent knows what's available before you ask — referencing one in a prompt loads its full skill.md content on demand rather than dumping everything into context upfront.
- Categories span Architecture (system design, C4 diagrams, ADRs), Business (copywriting, pricing, SEO), Data & AI (RAG pipelines, agent orchestration, prompt engineering), Development (language/framework expertise), General (brainstorming, doc co-authoring), Infrastructure (Docker, AWS serverless, CI/CD), Security (API security, SQL injection testing, compliance), Testing (TDD, QA automation), and Workflow (async job orchestration).
- Each skill carries a trust level — "official" skills come directly from vendors like Anthropic, Google, Vercel, Microsoft, and Supabase, while "safe" skills are community-built and non-destructive; curated role-based bundles (Web Wizard, Hacker Pack, Product Pack, Essentials) act as a reading list for picking the 5-6 skills relevant to a given task.
- Live demo: using plan mode, the brainstorming skill asks clarifying questions (standalone page vs. larger app, mocked vs. real API data, mobile responsiveness) before producing a full planning document (component hierarchy, state management approach, folder structure, naming conventions) — the kind of document that normally takes a developer 30-45 minutes to write.
- Switching to build mode and invoking front-end-design and React-patterns skills against that plan produces a properly typed, componentized dashboard (isolated sidebar, stat cards, task list with correctly-scoped filter state, activity feed) that wouldn't need refactoring before shipping — the difference described as coming from the instructions, not the underlying model.
- Running an API-security-best-practices skill against planned backend endpoints (before any backend code exists) flags issues like missing input sanitization, unguarded routes, and token handling problems in a short report — effectively a code review that happens before the code is written.
- The "skill creator" skill lets you turn team-specific conventions (naming patterns, deployment processes) into your own custom skill.md files, walking you through the required structure so OpenCode becomes progressively more aligned with how your team actually works.

## 🛠 Tools & Software
- [[topics/OpenCode]] — the terminal-based coding agent the entire video is built around, demonstrated using plan mode, build mode, `/skills`, and `/init` alongside the installed skill library
- [[topics/Antigravity Awesome Skills]] — the free, open-source, MIT-licensed repository of 1,300+ skill.md files installed and toured in depth, including its categories, trust levels, and curated bundles
- [[topics/GitHub]] — the skills repo itself (28,000+ stars) is hosted there, and the generated `agents.md` file is recommended to be committed to Git

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install antigravity-awesome-skills into OpenCode via the NPX command with `--path` set to your project root or global agents path.
- Run `/skills` to confirm the install worked, then `/init` to generate and commit an `agents.md` file.
- Before building a new feature, switch to plan mode and invoke the brainstorming skill to get clarifying questions and a full planning document first.
- Chain skills in sequence (e.g. brainstorming → front-end design → React patterns) rather than relying on one general-purpose prompt.
- Run an API-security-best-practices skill against planned backend endpoints before writing backend code.
- Use the skill-creator skill to turn your own team's conventions into a reusable custom skill.md file.

## 🔗 Related Videos
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: GitHub, OpenCode
- [[videos/Multica The Open Source Tool That Makes Claude Code 10x Better]] — shared: GitHub, OpenCode
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: GitHub, OpenCode

## Timeline
- `0:00` — Why OpenCode's default output is generic and what skills add
- `1:12` — The antigravity-awesome-skills repo: scale and cross-tool compatibility
- `2:20` — How OpenCode's native skill tool loads skills on demand
- `3:00` — Installing via NPX with the `--path` flag, project vs. global install
- `3:50` — Verifying with `/skills` and generating `agents.md` via `/init`
- `4:40` — Tour of skill categories: architecture, business, data/AI, dev, infra, security, testing, workflow
- `6:00` — Trust levels (official vs. safe) and curated role-based bundles
- `6:40` — Live demo: brainstorming skill plans a project dashboard
- `7:40` — Build mode: front-end-design and React-patterns skills implement the plan
- `8:40` — API-security skill reviews planned backend endpoints
- `9:10` — Skill creator: building your own custom skills

## Transcript
<details>
<summary>Full transcript</summary>

OpenCode is already capable on its own — terminal-based, connects to any LLM provider, has plan mode, build mode, undo/redo, and handles real codebases with little setup — but the default install is just the base. A free, open-source repository plugs directly into it and adds over 1,300 expert-level skill files covering everything from architecture planning and React patterns to API security auditing and infrastructure setup. The repo, antigravity-awesome-skills, sits at version 9.1a with 28,000+ GitHub stars and 4,000+ forks, and despite the name works natively with OpenCode, Claude Code, Gemini CLI, Codex CLI, Cursor, Kiro, and GitHub Copilot — this video focuses specifically on the OpenCode setup. Without extra context, OpenCode uses general knowledge to figure out what to build, which is fine for simple things but produces generic output for anything needing real structure — proper component architecture, security-aware APIs, test-driven workflows. Skills close that gap: each is a skill.md file giving OpenCode structured, domain-specific instructions, loaded on demand only when referenced (via OpenCode's native skill tool), so no context is wasted on skills you don't need for the current task. To install,

OpenCode looks for skill files in a few locations — the repo's install uses an NPX command with a `--path` flag defining exactly where OpenCode should look (this path convention can vary by tool). Running it from your project root drops skills into a project-level folder; pointing it at the global agents path instead makes skills available across every project without copying them each time. OpenCode auto-discovers skills from both the project-level and global folders, and also checks a `.opencode/skills` folder if present, walking up from the current working directory to the Git root. After installing, verify it worked by running `/skills` inside OpenCode to see everything available. From there, run `/init` (if you haven't already) to have OpenCode analyze your project and generate an `agents.md` file describing your codebase's structure and conventions — commit that file to Git. Internally, OpenCode lists all available skills (name plus short description) in its native skill tool description so the agent knows what exists before you ask; referencing a skill in a prompt makes OpenCode call that tool, load the full skill.md content, and apply it — a deliberate choice to load a skill when relevant rather than dumping everything into context upfront. Touring what's actually inside:

Architecture covers system design, C4 diagrams, architecture decision records, and scalable component patterns — the starting point for new projects or major structural decisions. Business covers copywriting, pricing strategy, and SEO audits, more relevant to product-building than pure coding. Data & AI covers RAG pipelines, LLM app design, agent orchestration, and prompt engineering, useful if OpenCode sits inside an AI product stack. Development covers language and framework expertise (TypeScript, Python, React patterns, and more). General covers planning and documentation skills like brainstorming and doc co-authoring. Infrastructure handles Docker, AWS serverless, Vercel deployments, and CI/CD pipeline setup. Security is a particularly strong category — API security, SQL injection testing, vulnerability scanning, compliance checks, and hack tricks. Testing covers TDD workflows, test design, and QA automation. Workflow covers orchestration tools for async jobs

and background processing. Every skill also carries a trust-level classification: "official" skills come directly from vendors like Anthropic, Google, Vercel, Microsoft, and Supabase; "safe" skills are community-built and non-destructive — worth checking before running anything unfamiliar. Curated "bundles" group skills by role: Web Wizard (React, Tailwind, front-end design), Hacker Pack (penetration testing, vulnerability scanning), Product Pack (planning, SEO, strategy), and Essentials (clean code, planning, validation basics applicable to almost any project) — install everything once, then use a bundle as a reading list to identify the five or six skills relevant to the current task. A live demo builds a project-management dashboard using three skills in sequence: brainstorming, then front-end design, then React patterns. After opening OpenCode in the project directory and switching to plan mode (a key OpenCode habit — always review the plan before building), the prompt asks the brainstorming skill to plan a dashboard with a sidebar, stats overview, filterable task list, and activity feed, on a React/TypeScript/Tailwind stack. Rather than jumping straight to code, the

brainstorming skill asks clarifying questions first — standalone page or part of a larger app, mocked or real API data, mobile responsiveness required — then produces a full planning document covering component hierarchy, state management approach, folder structure, naming conventions, and which external libraries to use, the kind of document that would normally take a developer 30-45 minutes to write by hand. Switching back to build mode and invoking front-end-design and React-patterns skills against that plan produces a properly structured result: a sidebar component with typed navigation props, individual stat card components with separate label/value/trend props, task-list filter state managed at the correct level in the component tree, an isolated activity-feed component, full TypeScript typing throughout, and a folder structure matching the brainstorming document — output a senior developer wouldn't need to refactor before shipping, with the difference attributed to the instructions being followed, not the underlying model. Running an API-security-best-practices skill against the planned backend endpoints, even before any backend code exists, flags issues like missing input sanitization, unguarded routes, and token handling problems in a short report — a code review happening before the code is even written. One more notable skill is "skill creator," which helps you build your own custom skills from scratch: if your team has internal conventions (a naming pattern, a deployment process) the model doesn't know about, skill creator walks you through the required skill.md structure and produces a file you can drop straight into your skills folder — over time making OpenCode progressively more aligned with how your team specifically works. Documentation pointers: a getting-started guide, a usage guide with OpenCode-specific prompt examples, and a Windows truncation-recovery guide are all in the repo's docs folder; the whole thing is MIT licensed, actively maintained, and every skill file is readable so you know exactly what you're running.

</details>
