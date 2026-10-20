---
title: "Claude Code 'Interview' Mode in 6 Minutes"
video_id: vgHBEju4kGE
channel: "[[channels/Developers Digest]]"
uploaded: 2026-01-01
processed: 2026-07-06
duration: "5:47"
url: https://www.youtube.com/watch?v=vgHBEju4kGE
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [spec-driven-development]
tools: [Claude Code, Cursor, Kiro]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code 'Interview' Mode in 6 Minutes

![thumbnail](https://i.ytimg.com/vi_webp/vgHBEju4kGE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=vgHBEju4kGE) | 📅 Uploaded [[uploaded/2026-01-01]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Inspired by a tweet from Claude Code's Tariq, this video shows an "interview first, spec second, code last" workflow: instead of writing one big prompt, you ask Claude to interview you using the Ask User Question tool, generate a detailed spec.md from your answers, then start a fresh session to implement it. A live demo builds out a Next.js marketing-site spec this way, and the video packages the pattern as a reusable Claude Code skill.

**Watch this if:** your AI coding agent keeps making assumptions (auth method, session strategy, UI details) you didn't actually want and you end up reworking large chunks of generated code.

## Key Takeaways
- The core idea, from Claude Code's Tariq: "start with a minimal spec or prompt and ask Claude to interview you using the Ask User tool, then make a new session to execute these specs."
- Workflow order: interview first, spec second, code last — slow down on planning to speed up overall delivery and avoid rework.
- The Ask User Question tool asks multiple-choice/clarifying questions mid-session; for big features Claude might ask dozens of questions, producing a much more detailed and controlled spec.
- Example prompt used: "Read the spec.md and interview me using the ask user question tool about literally anything — technical implementation, UI/UX concerns, trade-offs, etc. Make sure the questions are not obvious. Be very in-depth and continue interviewing me continually until it's complete. Then write the spec to the file."
- Without this step, a vague prompt like "add authentication" leaves Claude to guess (JWT vs OAuth vs session-based) — decisions you might later wish you'd routed through a managed service like WorkOS or Clerk instead.
- Interview mode is a precursor to, not a replacement for, Claude Code's existing Plan Mode — you can interview first, then move into planning for a stronger overall outcome.
- The interview pattern is packaged as a reusable Claude Code skill so it triggers automatically and calls the native Ask User Question tool without re-writing the prompt each time.
- Reframes prompt engineering: instead of trying to write the "perfect" one-shot prompt, you let the AI-driven discovery process surface requirements you hadn't consciously thought of yet.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent demoed running the interview skill via the Ask User Question tool, then producing a spec.md from a Next.js marketing-site prompt.
- [[topics/Cursor]] — mentioned alongside Claude Code as another agentic tool where the same over-eager, assumption-heavy prompting problem shows up.
- [[topics/Kiro]] — Amazon's IDE credited as the first place the presenter saw this spec-driven development workflow.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Before starting a large feature, prompt Claude Code to interview you via the Ask User Question tool and write the answers to a spec.md file first.
- Package your preferred interview prompt as a reusable Claude Code skill so it triggers automatically instead of retyping it each time.
- Use interview mode as a precursor to Plan Mode rather than a replacement for it, on genuinely large or ambiguous features.
- Start a fresh session to implement once the spec is written, rather than continuing in the same interview session.

## 🔗 Related Videos
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Drawbridge Builds Websites By Sight (NEW Plugin)]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Cursor
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: Claude Code, Cursor
- [[videos/Claude Code is Amazing Until It DELETES Production]] — shared: Claude Code, Cursor
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Cursor

## Timeline
- `0:00` — Intro: a new-year approach to planning projects in Claude Code by slowing down before coding.
- `0:14` — Origin: Tariq's tweet on spec-based development — interview first, spec second, code last.
- `0:59` — The Ask User Question tool explained: multiple-choice clarifying questions mid-session.
- `1:19` — Example interview prompt: read spec.md, interview in-depth until complete, then write the spec.
- `2:14` — Why this matters: vague prompts (e.g. "add authentication") lead to unwanted assumptions and rework.
- `2:52` — Live demo: prompting Claude Code to interview about a Next.js marketing-site build.
- `3:54` — Clarifying that interview mode complements, not replaces, existing Plan Mode.
- `4:14` — Packaging the interview prompt as a reusable Claude Code skill.
- `4:44` — Why it works: narrowing the solution space and surfacing buried assumptions before code is generated.
- `5:25` — Closing takeaway: try the interview process on your next large feature instead of one-shot prompting.

## Transcript
<details>
<summary>Full transcript</summary>

It's the first day of the year, and I thought, what better way to kick off the year than to show you a fresh way of how you can plan your projects within Claude Code. In this video, I'm going to be showing you how to get better outcomes by slowing down, spending more time being interviewed by Claude before actually kicking off the process, and beginning to code. Now, the origin of this came from Tariq, who works at Claude Code. He recently tweeted, "My favorite way to use Claude Code to build large features is spec-based. Start with a minimal spec or prompt and ask Claude to interview you using the Ask User tool, then make a new session to execute these specs." This got a ton of attention, and it really resonated with people, because I think a lot of us have had the experience — whether you're using Cursor, Claude Code, or any of these agentic systems — where you'll put in a prompt and it will go through and build out a bunch of stuff that you might have otherwise not wanted it to do.

There's a lot of nuances that go, especially for larger prompts, that arguably most of the time you probably want to have a little bit more input on, but you might not have originally thought that within your initial prompt. The idea with this is interview first, spec second, code last. Now, in terms of the approach for this, there's the method within Claude Code, the Ask User Question tool. You might have seen this if you've used Claude Code before, where it asks you two or three questions about implementation details. Further, he mentioned for big features or for new projects, Claude might ask me 40 questions, and I end up with a much more detailed spec that I feel I had a lot of control over.

The prompt that I've been using for this is: "Read the spec.md and interview me using the ask user question tool about literally anything. Technical implementation, UI and UX concerns, trade-offs, etc. But make sure the questions are not obvious. Be very in-depth and continue interviewing me continually until it's complete. Then write the spec to the file." So the idea with this is really to slow down to speed up. Now, a lot of people's first experience when they're leveraging tools — whether it's Claude Code, Cursor, Lovable, Bolt — generally what they do is they'll put in a prompt, and there might be a couple of questions, and then it will spin off and start to build out your application. But the idea with this is really just to slow down to speed up. So most people, they'll jump right into coding. And the thing with this is it will allow you to have a better understanding of what it's actually doing. The more time that you spend planning, the less time that you're going to spend reworking what Claude might have already done.

The first time that I saw this sort of spec-driven development workflow was from Kiro, which is an IDE that was built by Amazon, and this is a similar sort of idea. Now, the idea with this is when you give Claude a prompt, Claude is going to make a ton of different assumptions. If we take the example of adding authentication to an application, if you just ask Claude to add authentication to your application, it could go off — it could implement a JWT, it could maybe not do OAuth, it could do session-based. And the idea with this is at the end of it, you might realize, "oh, I actually wanted to leverage a managed service, something like WorkOS or Clerk, or whatever it might be." This is going to get to those details much sooner, where you don't actually have to rework everything. Instead of prompting Claude, Claude is going to prompt us, and instead of guessing, Claude is going to ask — clarify — instead of you having to rework all of those different assumptions.

Now, if you're not familiar with the Ask User Question tool within Claude Code, this is what it looks like. It's going to ask you a number of questions mid-session, multiple choice options, and then it will continue with your option. Now, just to demonstrate this, I'll do this with a relatively broad prompt — I'll say "build me a Next.js app, interview me about what I want." What I've actually done is I've gone ahead and implemented what Tariq had within the prompt, and I've added that within a skill. What we'll see here is it will trigger the interview skill, which I'll show you in just a moment. And then from here we can see — "let me interview you and understand what you want to build within here." It's like, what am I actually building? A web app, a marketing site? I'll say I'm building a marketing site, and it's for developers. And then as soon as I send in those answers, it's just going to go through the process and it's going to continue to ask me more clarifying questions. "So, this is a developer tool or SDK?" You can also add in your own information as well, where you can type things to answer the questions as well. I can say we're going to have a "book a demo" page, and we're just going to submit that. That's basically the core idea.

Now, one quick aside that I do want to mention: Claude Code has had Plan Mode for quite a long time, which is excellent — it explores your codebase, it can design implementation files, and it will actually write a plan. And the interview mode is not to substitute the Plan Mode — it can almost be used as a precursor for planning. You can interview, and then you can go through the planning phase, and this ultimately will ideally lead to much better outcomes.

Now, in terms of actually adding an interview skill, it can be very straightforward. So you can use exactly what Tariq said — you can have "read the plan, use this tool, ask me about the technical implementations" — or you can build your own variation of this depending on what you want to do. You can specify potentially the number of questions or whatever it is within the skill file, and it will trigger automatically. And the nice thing with skills is it's going to follow the process, and it will be able to latch on and trigger those native tools within Claude Code.

It's pretty clear why this works. You're going to be making all of those different decisions up front. You're narrowing the space of all of the possible solutions that Claude could generate for you. Instead of discovering buried assumptions during code review, you can actually confront all of those decisions when they're cheap to change, before it actually writes and uses all of those tokens to generate the feature that you're asking of it.

Now, one of the more traditional prompt engineering methods was around crafting really perfect instructions, or as close to it as you could get. Whereas with spec-driven development, AI will help you discover what you actually want, because it might not necessarily be as clear as you think right away. So instead of just getting everything right within one prompt, you're going to be going through a discovery process, and all of those different questions will ideally help reveal the requirements that you might not have otherwise even thought that you had.

Next time you have a large feature to build, I encourage you to try this out. Don't just try and get it all within one prompt — actually try out the interview process. Ask it to interview you about this plan, leveraging that Ask User Question tool, and you'll be surprised, I think, at the results that you'll get. Otherwise, I'll put the links to some of this within the description of the video. But if you found this video useful, please like, comment, share, and subscribe.

</details>
