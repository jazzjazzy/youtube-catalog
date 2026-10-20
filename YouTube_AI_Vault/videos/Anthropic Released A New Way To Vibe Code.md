---
title: "Anthropic Released A New Way To \"Vibe Code\""
video_id: XWp4k9K6oK8
channel: "[[channels/AI LABS]]"
uploaded: 2025-12-05
processed: 2026-07-06
duration: "4:40"
url: https://www.youtube.com/watch?v=XWp4k9K6oK8
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [long-running-agent-context-management]
tools: [Claude Code, Next.js, Puppeteer, Git, BMAD]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Released A New Way To "Vibe Code"

![thumbnail](https://i.ytimg.com/vi_webp/XWp4k9K6oK8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=XWp4k9K6oK8) | 📅 Uploaded [[uploaded/2025-12-05]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Anthropic published a two-agent workflow (an initializing agent plus a coding agent) for keeping long-running Claude Code tasks reliable across repeated context compaction. The host applies it to build an online Python compiler in Next.js, using a claude.md file, a features.json with initially-failing tests, Puppeteer for browser testing, and disciplined git commits after each verified feature.

**Watch this if:** Claude Code keeps forgetting what it was building mid-task, or marks features "done" that don't actually work, on any feature that takes more than one context window.

## Key Takeaways
- Long-running Claude Code tasks fail for two reasons: repeated context compaction erases memory of progress on a half-implemented feature, and weak testing capability leads Claude to mark untested features as complete even when they don't work.
- The fix is an initializing agent (sets up the project once) plus a coding agent (implements one feature at a time), inspired by how real engineering teams structure work — originally meant for custom-built agents but applicable directly to Claude Code.
- Initialization step 1: generate a claude.md file (via the init command) as the project's root-level overview document.
- Initialization step 2: generate a features.json (JSON, not markdown, for easier context management) listing every feature with its test steps, all tests marked initially failing so Claude is forced to actually test them.
- Since Claude can't see the rendered browser UI, Puppeteer is connected for real browser-based testing of each feature.
- Initialization step 3: an init script to start the dev server, plus a progress.md file Claude must update after every run — and a hard rule that Claude may only mark features implemented after testing, never edit the features list otherwise.
- The single most important practice: commit to git in a mergeable state after each verified feature — git logs become the source of truth for what's done, letting a session resume exactly where it left off by reading git history and progress.md rather than re-reading all the code.
- Compared to BMAD: this workflow used only 84% of context after implementing many features versus BMAD hitting compaction twice, and skipped BMAD's separate agent-calling overhead — though BMAD remains a more complete out-of-the-box system that could borrow this workflow's git discipline.

## 🛠 Tools & Software
- [[topics/Claude Code]] — runs both the initializing agent and the coding agent across the whole workflow described.
- [[topics/Next.js]] — the framework for the example project (an online Python compiler) built feature-by-feature using this workflow.
- [[topics/Puppeteer]] — connected so Claude can perform real browser-based testing of features it can't otherwise visually verify.
- [[topics/Git]] — commits after every tested feature are described as the most critical practice, forming the resumable record of project progress.
- [[topics/BMAD]] — compared directly against this workflow on context efficiency and agent-calling overhead.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model running Claude Code throughout, whose context-compaction and under-testing failure modes this whole workflow is designed to fix.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Generate a claude.md project overview file via the init command before starting any large feature build.
- Create a features.json listing every feature plus test steps, with all tests initially marked failing.
- Connect Puppeteer (or similar) so Claude can browser-test UI features, not just unit-test code.
- Require Claude to update a progress.md and commit to git after every feature it verifies as working, and never let it hand-edit the features list otherwise.
- When resuming a long task in a new session, prompt Claude to read git logs and progress.md rather than re-scanning the whole codebase, then implement the next not-done feature.

## 🔗 Related Videos
- [[videos/You Need Claude Sandboxes 90 Faster AI Coding]] — shared: BMAD, Claude, Claude Code, Git
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, Puppeteer
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: BMAD, Claude Code, Git
- [[videos/Claude Cluster is Insane Upgrade Your Claude Code Workflow]] — shared: Claude, Claude Code, Git
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, Puppeteer
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, Git
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Next.js, Puppeteer
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Git

## Timeline
- `0:00` — Intro: limited context window makes Claude Code forget progress on long tasks.
- `0:22` — Anthropic's two identified failure causes: repeated compaction erasing progress, and untested features marked complete.
- `0:54` — The fix: an initializing agent plus coding agent, adapted from custom-agent workflows to Claude Code.
- `1:18` — Initialization: generating a claude.md file via the init command.
- `1:28` — Generating features.json with test steps, all initially marked failing.
- `1:46` — Connecting Puppeteer for browser-based testing.
- `2:05` — Init script, progress.md tracking, and the rule against editing the features list improperly.
- `2:21` — Why git commits after each tested feature are the most important practice.
- `3:24` — Comparison to the BMAD method: context usage (84% vs. two compactions) and workflow overhead.
- `4:25` — Sponsor/outro: automator.dev services pitch.

## Transcript
<details>
<summary>Full transcript</summary>

The main problem with AI agents is the limited context window which restricts what they remember from previous actions. When we give Claude Code a larger task, it compacts multiple times while attempting a single feature, forgetting the main task it was asked to implement, making it less effective for long running tasks. Anthropic just released a solution that is based on how real teams work in an actual engineering environment.

They identified two key reasons for why it fails on long tasks. Many of us have tried to oneshot entire applications or big features, and doing too much causes the model to run out of context. After repeated compaction, the context window is refreshed with the feature only half implemented and no memory of the feature's progress, leading to incomplete implementation. The second issue is that due to less testing capability, Claude marks untested features as completed — it assumes the feature is complete even if it doesn't actually work properly.

Their solution was using an initializing agent and a coding agent in harmony, inspired by how real software teams work. This workflow is originally meant for agents you build yourself, but I realized it could apply to Claude Code instances as well. The first agent focuses on properly initializing your coding agent, and you have to be patient here because it takes a little time.

I have an empty Next.js project, and I want to build an online Python compiler. Before starting, create a claude.md file using the init command. This file is a document for your codebase, at the root of your project, containing an overview and all important information. Next, generate the features list JSON in the project root. It should list all features and their corresponding testing steps, with all tests marked as initially failing, so Claude is forced to test them. We use JSON instead of markdown because JSON files are easier to manage in the context. Since Claude can only test the code, not the interface we see in the browser, I connected Puppeteer for browser testing.

After that, create an init script to guide starting the dev server, and a progress tracking file so the system can keep track of project completion status. For guidelines, Claude needs to update progress.md after each run and test each feature after implementation. The most important practice is committing to git — we underestimate how crucial it is to commit in a mergeable state. Git commits with clear logs show what's completed and let you revert if implementation fails. Finally, Claude should not change the features list beyond marking features as implemented.

With the environment ready, we move to the coding part. The idea was to implement each feature one by one from the features JSON. Claude also made descriptive commit messages after each tested feature and launched the browser when needed. Once it verified the app was working, it updated the JSON fields from false to true and updated progress.md with what had been completed so far. Finally, it committed the changes and verified the commit was successful.

The advantage of this incremental approach is that even if the session terminates, you can resume exactly where you left off. Everything is tracked in the git logs, so you don't have to worry about breaking code. Claude can understand the project from the git logs and progress file, not from the code itself, so you can resume the session easily. Your next prompt is simply to implement the next feature marked not done. This approach also reduces Claude's tendency to mark features complete without proper testing. Each iteration ensures the app is built end to end with real testing, helping identify bugs that are not obvious from code alone. We repeat this cycle until all features are marked true.

You might think this is similar to the BMAD method. It shares similarities, but I think Claude's workflow is better in some ways. It was easier since you didn't call agents separately, and context utilization was better too. After implementing so many features, it only used 84% of context where BMAD would have already hit compaction twice because of the large stories that it makes. That said, BMAD is still an out-of-the-box full system. This is still an idea that needs to be implemented, but BMAD could use some things from this, such as the git system.

After teaching millions of people how to build with AI, we started implementing these workflows ourselves. We discovered we could build better products faster than ever before. We help bring your ideas to life, whether it's apps or websites. Maybe you've watched our videos thinking, "I have a great idea, but I don't have a tech team to build it." That's exactly where we come in. Reach out at hello@automator.dev.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
