---
title: "Give Me 13mins, I Will Show You The Right Agent Setup"
video_id: ywIhw15za9Y
channel: "[[channels/AI LABS]]"
uploaded: 2026-04-10
processed: 2026-07-05
duration: "13:12"
url: https://www.youtube.com/watch?v=ywIhw15za9Y
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-project-setup, spec-driven-testing]
tools: [Claude Code, Supabase, shadcn ui, Playwright, GitHub, Trello, Notion, k6]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Give Me 13mins, I Will Show You The Right Agent Setup

![thumbnail](https://i.ytimg.com/vi_webp/ywIhw15za9Y/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=ywIhw15za9Y) | 📅 Uploaded [[uploaded/2026-04-10]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A complete pre-build checklist for Claude Code projects: a dedicated planner agent to produce a product-focused PRD, a hand-written (not `/init`-generated) CLAUDE.md, MCPs/agents/skills configured before coding starts, explicit negative constraints, progress and learnings documents, spec-first testing, upfront issue tracking, and load testing before calling anything production-ready.

**Watch this if:** you keep hitting the same agent mistakes across projects and want a repeatable setup checklist to run before writing your first prompt.

## Key Takeaways
- Use a dedicated planner agent (not Claude Code's built-in plan mode, which is too technical/not product-focused) to interactively question you until requirements are clear, then generate a PRD document saved to the project.
- Write CLAUDE.md by hand instead of relying on `/init` — it should only contain what the agent doesn't already know (conventions, style, project-specific rules), not things it can discover itself from the file structure, and it should link out to the PRD rather than duplicating it.
- Connect MCPs (e.g., Supabase for backend, Playwright for browser testing) and configure dedicated agents (planner, commit agent, refactoring agent, verification agent) and skills (e.g., a front-end skill) before starting to build, not mid-project.
- Distinguish agents from skills: use skills for repeatable workflows needing consistent guidance/references (e.g., a front-end skill); use agents for tasks that need their own dedicated context window.
- Add explicit negative constraints (a separate doc linked from CLAUDE.md) — positive instructions leave an implicit gap agents will fill by improvising, so state what the agent should NOT do (e.g., don't default to purple/blue UI themes).
- Maintain a progress file (what's done/left) and a learnings file (errors, causes, fixes) that the agent actively updates, so it doesn't re-derive state from the codebase or repeat past mistakes.
- Write tests from the PRD's requirements before implementation, not after — tests derived from what was actually built will miss features that were specified but implemented incorrectly or not at all.
- Track issues from day one via GitHub (technical teams) or a connected Trello/Notion MCP (non-technical collaborators), and use Git worktrees to test experimental changes in isolation.
- Stress-test for expected concurrent load (e.g., with k6) before calling an app production-ready, since AI-generated code isn't inherently built for multi-user scale.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent being configured end-to-end: planner agent, CLAUDE.md, skills/agents/MCPs, negative constraints, progress/learnings files, and spec-first testing.
- [[topics/Supabase]] — connected via MCP as the backend for the example project.
- [[topics/shadcn ui]] — the UI component library connected prior to building, alongside Playwright for testing.
- [[topics/Playwright]] — connected via MCP for browser testing and used by a dedicated verification agent to check UI and user flows.
- [[topics/GitHub]] — recommended for issue tracking and structured commit messages, with worktrees for isolated experimentation.
- [[topics/Trello]] — suggested as a project-management alternative to GitHub issue tracking for non-technical team members.
- [[topics/Notion]] — connected via MCP so the agent can log and track bugs/issues for non-technical collaborators.
- [[topics/k6]] — the load-testing tool used to stress-test a Next.js app for expected concurrent user load.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — referenced throughout as the model powering the planning, implementation, and plan-mode scalability analysis described in the setup.

## 📡 Protocols & Standards
- [[topics/MCP]] — used to connect Supabase, Playwright, and Notion to the agent's project so it can access these external services/tools directly.

## ✅ Action Items
- Build a dedicated planner agent with a PRD template instead of relying on Claude Code's default plan mode.
- Write your own CLAUDE.md by hand, keeping it limited to non-obvious conventions and linking to your PRD instead of duplicating it.
- Add a negative-constraints doc listing explicit "don'ts" for your project's UI/behavior.
- Create progress.md and learnings.md files and instruct the agent (via CLAUDE.md) to keep them updated during implementation.
- Write tests from your PRD's requirements before implementation begins, not after.
- Set up issue tracking (GitHub, or Notion/Trello via MCP) before development starts, not after issues pile up.
- Run a load test (e.g., with k6) against your expected concurrent user count before treating the app as production-ready.

## 🔗 Related Videos
- [[videos/The Best MCP Servers of 2025]] — shared: Claude, Claude Code, MCP, Notion
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/ShadCN is Way too Powerful Now]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, MCP, Supabase
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP

## Timeline
- `0:00` — Intro: why 60 years of software process still matter, now for enabling agents rather than humans
- `0:36` — Plan requirements with a dedicated planner agent instead of Claude Code's technical plan mode
- `2:05` — Writing a proper CLAUDE.md by hand instead of using `/init`
- `3:36` — Setting up skills, agents, and MCPs (Supabase, shadcn/ui, Playwright) before building
- `5:55` — Why negative constraints are needed to close the gap left by positive instructions
- `7:32` — Progress and learnings documents to prevent the agent losing track or repeating mistakes
- `8:57` — Writing tests from the PRD's specs before implementation, not after
- `10:14` — Issue tracking via GitHub, or Notion/Trello for non-technical collaborators
- `11:37` — Preparing for production scale with load testing (k6) and Claude's plan mode

## Transcript
<details>
<summary>Full transcript</summary>

The truth is that AI will never revolutionize the software building process, at least not in the way that you think. It sure makes everything faster, and it also makes it easier to recover when things go wrong. But the processes that have been set over 60 years of product building are still as important today, just for different reasons. Before they were implemented to make sure that humans had a structured way to develop these products, but now that has shifted to enabling AI agents to work the way humans did. So, in order to make AI agents work properly, you need to set up their environment the right way so that they actually follow the process. And we are going to go through all of the steps you need to take before you even start building.

Planning your requirements properly is the most important thing you do before writing a single prompt. This is the part where no matter how good models get, you would need to spend time. Now, there are multiple ways of planning. You can plan your app using Claude Code in planning mode, but its planning is very technical focused, not product focused. As we mentioned in the previous video that with the way agents are progressing, the planning mode doesn't need to be as detailed or technical and should instead focus heavily on the product aspect because the new models are powerful and planning has to be different than as it used to be with the early models being not much capable. So, instead of Claude's planning mode, you can create another agent to help plan out your app. It contains the instructions for helping build a proper PRD with a template as well to guide Claude on what exactly the requirements are. Once you have set up the agent, you can give Claude a prompt to use it and plan out the app you want to build. It actually loads the planner agent and keeps asking questions until it understands all of the requirements. It keeps on asking questions until you're satisfied with the planning. Now, to understand the MVP, the agent is designed to ask many questions, and at the end it will ask you if there is anything else that you need in your app. If you do, you can add the things that you want the agent to implement. If you are satisfied with all of the questions and think that the agent has understood the plan, you can just tell it that's it. After the questioning and answering session, it creates a PRD document and saves it to the project folder. This document contains details on all the requirements you discussed. The implementation is divided into phases and it contains all the key design decisions and everything that is needed for the app.

Now that you have refined what app you want to build, the next step is to properly define a Claude.md file. This file is important because it contains all of the instructions that you want your agent to follow. You link the PRD document so that it can access all of the app requirements directly from there and you don't have to repeat anything here. This file should contain only the things that the agent does not know, instead of mentioning the things that it already knows. It references the rules that you want the project to follow. You can add in your project conventions and all of the instructions that you want Claude to specifically follow while implementing the app. The ideal approach is that you do not create the Claude.md file from the init command and instead create it on your own because this command just generates the file based on what the existing codebase is like, not what it actually needs to know. But this file is not a write once file that you set and forget. You have to keep adding things to it so that it can incrementally improve the process of building apps while you work. Now, as we talked about in our previous video, this file is loaded once and stays in the context forever, acting as a guideline while it's working. So, make sure that this file does not contain things that are actually not needed or are specific to one area of implementation. The things that you need to add to this file are the best practices your project will follow, your coding conventions, your writing style and conventions, and other similar things, but not the things that it can figure out on its own, like how the project is structured. For that, it can read the file structure and understand it by itself. So, take your time when you're writing this file and ensure that it is properly tailored to your needs and your project before actually implementing the app.

The next thing you set up is your skills, agents, and any MCP you want to use in your project, all prior to actually building it. MCPs are easier to connect. You can just connect whichever external service you want the agent to access and have them installed by running their installation commands. For example, we wanted our backend built on Supabase, so we connected the Supabase MCP to our agent in the project. We are using shadcn/ui for UI components and Playwright for browser testing, you need to have them all connected prior to building the app so that agents can access these tools while building. But those were just for connecting to external services, and you also need to configure agents. You can configure as many agents as needed. You already have a dedicated planner agent for planning. You can also create a commit agent which is responsible for committing, running pre-checks, and following conventional commit messages, a refactoring agent that refactors the code and improves performance overall, and a verification agent that uses the tools of the Playwright MCP so that it can verify if the UI and user flow are working as intended, and it contains all the instructions on how to do that.

Now, aside from the agents, you also need to configure skills. You can create as many skills as you need, and you can easily create them using the skill creator, which is available on the open-source GitHub repo. You can add as many references as you want and also include scripts so that it can run the script directly and use its output. For the distinction between when to use agents and when to use skills, implement all those workflows that are repeatable and need guidance and references as skills. For example, you can create a front-end skill because it's a repeatable workflow and needs to follow dedicated guidelines consistently throughout the app. Implement agents for tasks that need a dedicated context window. You can also use the front-end skill that's open-source and is actively used by the Claude Code's creator himself. You also need to add path-specific rules for particular aspects of your app. These rules define the path to which they apply and include all the instructions needed for implementing that specific part. You can configure as many of these as you like and also link them in your Claude.md so that the agent knows it has to follow these instructions. As we mentioned earlier, Claude.md is for broad principles, so that's why you have path-specific rules tailored to specific parts so the agent knows what it needs to do for specific implementation.

But even with all of these positive instructions, there is still a gap. Agents are biased toward action and may implement things beyond what your positive constraints specify. Therefore, you need to explicitly tell the agent what it should not do. You can create this file in your docs folder and link it in Claude.md so the agent knows these constraints exist. It should contain all instructions tailored to the project specifying each and every thing you don't want the agent to create. Negative constraints are important because positive specs leave an implied gap and negative constraints close that gap, removing ambiguity and preventing the agent from experimenting where it shouldn't. They give a clearer goal for what the output shouldn't look like. For example, if you don't want the AI to follow the default purple or blue and white combination it usually uses, explicitly state that you don't want that instead of just implying it.

Now, this is one thing that most AI frameworks use in one form or another, which is using multiple documents for different purposes. But the core behind all of those documents is the progress and learning document. The progress file is critical because when you are working on a large-scale app with multiple features, the agent loses track of which features it has already implemented and which it has yet to work on. Without this file, the agent has to go back, read the implementation, and compare it against the docs to figure out what's been done. That creates overhead and wastes both time and tokens. So, create a progress file where the agent can just look at one place and know exactly where things stand. But tracking progress alone is not enough because the agent also needs to know what went wrong. Therefore, you also need a learnings file where the agent records its errors, what caused them, and how it fixed them. This way, when it encounters a similar situation later, it doesn't make the same mistake twice. Now, since both of these files are meant to be actively updated while the agent is implementing the app, you need to explicitly instruct the agent in the Claude.md so that it keeps adding to these files, improving its knowledge base during the build. Now, these two files are the most essential ones that every setup needs.

Another common mistake is implementing tests only at the end of development. This is problematic because if you ask an agent to write and implement tests after the features are built, the tests won't be as effective as they would be if written beforehand. When writing tests, you should have the agent refer to the PRD you created and based on that, deduce how the functionality should work. The agent should then write tests from these deduced requirements, essentially reverse engineering the functionality and things where the app might go wrong from the PRD. Once the tests are ready, you can run them at the end to cross-verify if the implementation meets the requirements. The reason for writing tests first is that if you implement them afterward, the agent only knows what was actually implemented, tests for the features as they exist, not for the functionality as required in the specifications. This can cause you to miss testing features that were specified but not implemented correctly. Because the agent optimizes toward the implemented approach, it may slack on thorough testing, missing edge cases that could have been caught if the tests were derived directly from the specs. You shouldn't give the agent open-ended instructions like test the application because this way Claude just optimizes for the implementation. Instead, implement proper tests guided by the specs so the agent knows exactly what to optimize for.

Another problem many people encounter during app development is the lack of upfront issue tracking. Without it, issues pile up with no record of what caused them or when they started. And as the app scales up, it gets harder to track. Therefore, maintaining proper logs during testing is crucial. Many people use GitHub for this, and GitHub is an excellent platform for tracking and managing issues. Combining it with well-structured Git commit messages provides guidance to Claude on what was done in each commit and allows it to track its progress. One of the best features of Git is that if a change breaks the codebase, you can revert commits. And if you want to test something experimental, you can use the work tree to do it in isolation. You can configure your setup so that the agent commits after every implementation using detailed messages to maintain clarity. But GitHub works well for technical users, and non-technical team members may struggle to submit issues. Therefore, for them, connecting the agent to a project management tool like Trello or Notion is ideal. This allows logging issues, tracking progress, and collaborating on fixes. You should connect the MCP of the respective tool so the agent can access it, track issues, move them across boards, and manage reporting efficiently. You also need to add an instruction in Claude.md specifying that the agent should use the Notion MCP for tracking bugs and issues properly. Setting this up at the start is invaluable as the project scales and multiple people start developing together, ensuring that everything can be logged and tracked efficiently.

But even if your app works perfectly in testing, AI-generated code is not inherently built to handle multiple users simultaneously. This is why many people find AI implementations underperforming in production. Therefore, you need to prepare for that as well. If you have an estimate, you can tell your agent the expected number of users and that multiple users will be using the app at the same time. The agent should then write the test cases for stress testing the load based on this information. There are multiple testing tools you can use, and you can choose whichever matches your requirements. We used k6 for a Next.js app because it's easy to implement and matched our requirements. You can also use Claude's plan mode here to map out multiple approaches for the app because here we need a detailed technical plan. Claude plans based on the PRD and the approximate number of users you expect to be using it simultaneously. Claude asks multiple questions from different perspectives and clarifies potential issues that could arise in production. This helps the app fail gracefully even if problems occur and ensures the user experience is optimized. Using this mode, you can clarify your intent and have the agents plan for scalability as well. This plan becomes the final piece in taking your app from an idea to production-ready.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the Super Thanks button below. As always, thank you for watching, and I'll see you in the next one.

</details>
