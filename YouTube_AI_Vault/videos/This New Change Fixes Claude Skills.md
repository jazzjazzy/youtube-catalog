---
title: "This New Change Fixes Claude Skills"
video_id: Hy_XOB83MQc
channel: "[[channels/Rob Shocks]]"
uploaded: 2026-01-30
processed: 2026-07-06
duration: "9:21"
url: https://www.youtube.com/watch?v=Hy_XOB83MQc
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [skill-invocation-reliability]
tools: [Claude Code, Cursor, Gemini CLI]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This New Change Fixes Claude Skills

![thumbnail](https://i.ytimg.com/vi/Hy_XOB83MQc/sddefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Hy_XOB83MQc) | 📅 Uploaded [[uploaded/2026-01-30]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Skills only get invoked by AI agents about 50% of the time even when they're clearly relevant, because the model doesn't reliably know a skill exists. Research from a Vercel engineer shows two fixes — a one-line pointer in agents.md (53% → ~79%) and a compressed documentation index baked directly into agents.md (→100%) — that dramatically raise the call rate.

**Watch this if:** your carefully written Claude Code or Cursor skills keep getting ignored and you want a concrete fix instead of just writing a "better" skill description.

## Key Takeaways
- Skills, rules, and commands are all fundamentally "just prompts" that get injected when the model decides it needs them — the core problem is the model not reliably deciding to invoke them.
- Vercel's own Next.js skill was only being called ~50% of the time even though it kept the agent using outdated APIs past the model's training cutoff.
- Adding a single explicit instruction to agents.md ("first explore the project structure then invoke the nextjs doc skill") raised the call rate from 53% to ~79% — but wording matters a lot, making this approach fragile.
- Bypassing skills entirely and injecting a compressed, indexed version of the documentation directly into agents.md pushed the success rate to 100%.
- The compressed index is unreadable to humans but structured so an agent can navigate straight to the relevant doc fragment without loading everything into context.
- Recommendation: put your primary framework docs (Next.js, Django, FastAPI, your own codebase) as a compressed reference index directly in agents.md; keep secondary/less-critical skills in the regular skills folder.
- Explicitly prompting the agent to use a named skill, or firing skills via hooks after a task completes, remains the most reliable way to guarantee invocation today.

## 🛠 Tools & Software
- [[topics/Claude Code]] — one of the coding agents whose skill-calling reliability is being diagnosed and improved.
- [[topics/Cursor]] — used to demonstrate installing the Next.js skill and viewing the generated agents.md index.
- [[topics/Gemini CLI]] — named alongside Claude Code and Cursor as a tool that recognizes and picks up agents.md files.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Audit your skills folder and identify which ones are "primary" (core framework/codebase docs) vs "secondary" (nice-to-have references).
- Move primary documentation into a compressed, indexed block inside agents.md instead of relying on the agent to discover a skill on its own.
- Try running the Vercel skills installer command in a Next.js project to see the generated compressed agents.md index as a working example.
- Set up hooks in Claude Code or Cursor that automatically fire a specific skill after a task completes, to guarantee invocation for critical workflows.
- Explicitly name the skill you want used in your prompt rather than assuming the agent will find it.

## 🔗 Related Videos
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/The HTTP Header Trick That Cuts AI Agent Costs in Half!]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/Vibe Kanban Claude Code This is SO GOOD CONVERT Claude Code in a PROJECT MANAGER]] — shared: Claude Code, Cursor, Gemini CLI
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Gemini CLI
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Claude Code, Gemini CLI

## Timeline
- `0:00` — The problem: a well-built skill gets ignored by the agent even when it's an obvious fit.
- `0:57` — Quick recap of what skills are and how they pack extra info/resources for the model.
- `1:34` — Example: a Next.js best-practices skill created for Cursor/Claude Code.
- `2:42` — Introducing agents.md and how tools like Cursor, Claude Code, and Gemini CLI pick it up.
- `3:46` — Skill-calling tip #1: adding a one-line pointer to agents.md raises the call rate from 53% to ~79%.
- `4:24` — Sponsor break (Brilliant).
- `6:30` — Skill-calling tip #2: compressing full documentation into an indexed agents.md block raises success to 100%.
- `7:53` — Final takeaways: prompt explicitly for the skill you want, or use hooks to force invocation.

## Transcript
<details>
<summary>Full transcript</summary>

So, let me know if this feels a little bit familiar. You set up the perfect skill and then you watch your AI agent completely ignore it when you feel like it was a really obvious call. It's kind of frustrating, right? So, here's the thing about skills in AI development. They're genuinely useful. Basically, you can pack a ton of information on any given topic into a skill and then let the AI use that as they need to. Yeah, but there's a catch. The agent has to know that the skill actually exists and a lot of the times it can't find this. So in this video we're going to look at some recent research from Vercel which will improve your skills from being called only half the time up to 80% of the time and in some cases even all the time.

So first of all this is kind of a known and common problem with skills, rules, and context. To really simplify it back to first principles, a rule is pretty much the same as a skill, the same as a command. And all of these are the same as a prompt — you have saved prompts that get injected or used by the model whenever it needs them. A skill can have some extra resources and examples, but whatever marketing you wrap around them, they're still just prompts. With the skill, I can ask Cursor or Claude Code to just create that skill for me — it's got some front matter with a name and a description of when it's called. In theory this Next.js skill makes sure the agent adheres to the most recent methods and APIs, because models have a cutoff date and don't know anything past that particular date.

So literally last week, Vercel released a set of agent skills and a little installer so you can install skills into Cursor and Claude Code — over 32,000 skills are listed at skills.sh. The big problem is that skills aren't always being called — only 50% of the time in instances where they were really useful. A clever engineer at Vercel, Jude Gao, decided to get to the bottom of this — what do we need to tweak to make sure skills get called when we want them? His approach was to include more context in the agents.md file to let the agent know the skill was there. If you don't know what an agents.md file is: in Claude Code you type /init and it creates a summary of your project so every new conversation has context about best practices. Tools like Cursor, Claude Code, and Gemini will all pick up on and recognize an agents.md file.

The benefit of agents.md is that it's always in context — so why not put everything, including skills, into it? The problem is the bigger the agents.md file gets, the more confused the agent becomes and the more likely it is to miss vital instructions, no matter how big the context window is. So the first tip got skill calling up from 53% to just under 80%: keep the skill installed as usual, but add a line to agents.md like "first explore the project structure then invoke the nextjs doc skill for documentation." The issue is even small wording changes produce different results, so prompt syntax matters a lot and you don't want to rely on that too heavily.

[Sponsor segment for Brilliant omitted from technical summary.]

The next thing the team tried took the success rate from 79% up to 100%: a shotgun approach where they bypassed skills completely and injected all the Next.js documentation into the agents.md file. To avoid overloading the agent's context, they built a compressed index into agents.md that pointed to all the other docs needed. It looks complicated and doesn't work for human eyes, but it's perfect for an agent. You can run a command in any Next.js project that detects your Next.js version and installs the relevant docs, choosing agents.md as the output format so Claude and Cursor both recognize it — opening the file shows all the relevant documents compressed into a reference structure kept in the project folder.

So how do you take advantage of this yourself? Whatever documentation is important to your project — Python and Django, FastAPI, Rust, or your custom codebase — copy that documentation into a structured folder (you could use Claude Cowork or similar to help compress it), then generate a compressed index for those docs to add into your agents.md file. Put primary framework information as a reference index in agents.md; put secondary skills (front-end, back-end, or reference tools) pointed to from agents.md for roughly a 30% increase in pickup chance; and put everything else in the regular skills folder, project-local or in Cursor/Claude Code settings. These all increase the chance a skill gets called, but until agent tool calling is fully solved, you'll still deal with these issues. What I generally do, since I know what skills are available, is prompt the agent to use a particular skill directly, which dramatically increases the chance of it being picked up. You can also set up hooks in Cursor and Claude Code so that when an agent finishes a piece of work, it automatically fires a particular skill, giving a 100% chance of invocation.

</details>
