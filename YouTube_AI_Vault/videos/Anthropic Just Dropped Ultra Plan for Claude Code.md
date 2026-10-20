---
title: "Anthropic Just Dropped Ultra Plan for Claude Code"
video_id: UNhA17l6CWw
channel: "[[channels/Ray Amjad]]"
uploaded: 2026-04-06
processed: 2026-07-05
duration: "7:52"
url: https://www.youtube.com/watch?v=UNhA17l6CWw
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [claude-code-plan-mode-testing, ai-agent-planning-workflow]
tools: [Claude Code, tRPC]
llms: [Qwen, Gemma]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Just Dropped Ultra Plan for Claude Code

![thumbnail](https://i.ytimg.com/vi_webp/UNhA17l6CWw/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=UNhA17l6CWw) | 📅 Uploaded [[uploaded/2026-04-06]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Claude Code's new `/ultraplan` mode hands planning off to a cloud version of Claude Code with a nicer review UI (inline comments, approve/refine), and runs about 2x faster than local planning. After running 10 Ultra Plan vs 10 local-plan prompts side by side, the presenter finds the quality difference is inconsistent — because Anthropic is server-side A/B/C testing three different hidden planning modes, and users have no control over which one they get.

**Watch this if:** you want to know whether Claude Code's new Ultra Plan feature is actually worth using, and how it works under the hood.

## Key Takeaways
- `/ultraplan` sends your prompt to a cloud-hosted Claude Code session that researches and drafts a plan; you review it in a web UI, leave inline comments, then either approve-and-run in the cloud or teleport the approved plan back to your local terminal session.
- Across 10 matched prompts, Ultra Plan consistently finished about 2x faster than the local planning mode for the same prompt.
- Ultra Plan sometimes generates ASCII or Mermaid diagrams alongside the plan, and sometimes doesn't — this turned out to be tied to which underlying planning mode was assigned, not something the user controls.
- Digging through readable strings in the Claude Code binary revealed 3 hidden planning modes inside Ultra Plan: a simple plan, a visual plan (adds diagrams), and a "deep plan" — a multi-agent pipeline with dedicated agents for understanding the codebase, finding files to modify, identifying risks/edge cases, and critiquing the draft plan.
- Anthropic assigns which mode you get via a remote, server-controlled config — the user never picks it — which strongly suggests this is an A/B/C test to measure which planning prompt/mode users accept most, likely feeding future default-prompt or even model selection decisions.
- Quality gains were inconsistent: for risk-heavy changes like a dependency upgrade (tRPC v10 to v11), Ultra Plan's deep-plan variant caught more issues than local planning; for a simpler model swap, Ultra Plan offered no real improvement beyond a nicer review UI.
- The presenter's takeaway: skip relying on random Ultra Plan mode assignment and instead copy the "deep plan" (3 subagents + critique) system prompt directly as a custom skill, to reliably get the strongest planning behavior on demand.
- Ultra Plan is also useful for multitasking — spinning up several cloud plans from the terminal and reviewing them in a shared UI — and for quick, disposable prototyping since a bad plan can be discarded without polluting your main conversation.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the `/ultraplan` feature is demoed end-to-end: triggering a cloud plan, reviewing it in the web UI, leaving comments, and teleporting the approved plan back to a local session.
- [[topics/tRPC]] — used as a real example dependency upgrade (v10 to v11) where Ultra Plan's deep-plan mode caught more migration risks than the local plan.

## 🤖 LLMs Mentioned
- [[topics/Qwen]] — the local model (Qwen 3.5) being replaced in the presenter's own macOS app, used as one of the test prompts for comparing Ultra Plan vs local planning.
- [[topics/Gemma]] — Gemma 4, the model Qwen 3.5 is being swapped for in that same test prompt.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Try `/ultraplan` on a risky, blast-radius-heavy change (like a major dependency upgrade) where deeper risk auditing matters most.
- Don't assume Ultra Plan is always better — compare it against local planning for your own recurring prompt types before adopting it wholesale.
- Consider extracting the "deep plan" (multi-subagent + critique) system prompt as a custom skill to get that behavior reliably instead of leaving it to Anthropic's server-side assignment.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Gemma, Qwen
- [[videos/7 new open source AI tools you need right now]] — shared: Claude Code, Gemma
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: Gemma, Qwen
- [[videos/Pick the Wrong Gemma 4 and You'll Think It's Broken FOUR Models Compared]] — shared: Gemma, Qwen
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Code, Qwen

## Timeline
- `0:00` — Intro: Ultra Plan, a new planning mode in Claude Code, may underwhelm despite its name
- `0:14` — Demo: triggering `/ultraplan` with a prompt to swap Qwen 3.5 for Gemma 4 in a macOS app
- `0:46` — Reviewing the plan in Claude Code's web UI: reactions, inline comments, approve/refine
- `1:36` — Two observations: Ultra Plan runs faster on the cloud, and diagrams appear inconsistently
- `2:08` — Difference from normal plan mode: cloud hand-off, inline review, approve-and-run or teleport back
- `3:00` — Comparing 10 Ultra Plan runs vs 10 local plan runs for the same prompts
- `3:36` — Ultra Plan's deep-plan variant catches more risk in a tRPC v10-to-v11 migration than local planning
- `4:19` — Reverse-engineering the binary reveals 3 hidden Ultra Plan modes: simple, visual, and deep (multi-subagent + critique)
- `5:26` — Anthropic server-side assigns the mode via remote config, likely as an A/B/C test
- `6:47` — Other benefits: faster iteration, multitasking multiple cloud plans, disposable prototyping
- `7:19` — Conclusion: use the deep-plan prompt as a custom skill instead of relying on random assignment

## Transcript
<details>
<summary>Full transcript</summary>

Okay, so we have a brand new planning mode inside of Claude Code known as Ultra Plan. And I'll be going through that in this video as well as my own thoughts about this because despite the name, like Ultra being the name, you may actually be underwhelmed when using this new feature.

Now essentially, if you go to Claude Code and then you do /ultraplan, then you can give it a prompt. So for my application HyperWhisper, I basically want to upgrade Qwen 3.5 to Gemma 4 instead for the local model. So if I give it that prompt, can you upgrade Qwen 3.5 to Gemma 4 for the local model in the macOS application? And then pressing enter, it will say that it will run Ultra plan on the cloud, press enter, and then it will give you a session URL so you can like watch it planning and then actually respond to the plan that it gave you. So clicking on this URL over here, it should then take you to the Claude Code web like version. And then you'll see that the Ultra plan is in action.

Now I actually made 10 Ultra Plans yesterday. So I ran this prompt before and I ran 10 different prompts for a local planning mode and 10 different prompts for Ultra Plan mode. Now when the Ultra Plan is presented to you, you will see that it looks kind of like this. So they have a nice UI over here and you can select things over here and like leave a thumbs up, like emoji, smiling face. And you can leave comments in different areas over here. So like leaving a comment saying, use the recommended sampling parameters. And after reading through the plan, I could send these two comments back to Claude so I can adjust the plan on the cloud version. And I can press approve Claude's plan and start coding on the cloud version or teleport back to the terminal instead.

And you'll actually notice two different things here. Firstly, that Ultra plan is actually really fast on the cloud. So I noticed that it was up to 2 times faster than the local plan for the same prompt. And you'll also notice that sometimes you get diagrams in your Ultra plan, kind of like this ASCII diagram or this Mermaid diagram over here, but other times you will not see any diagrams at all. And then on your terminal, once the Ultra plan is ready, you will see Ultra plan ready over here. Press down, press enter, and then you can stop the Ultra plan, go back, or review in Claude Code web. So reviewing the web version, I could then press approve plan and teleport back to terminal. Now this will then send the plan back to the terminal, and then I can do implement here, like in this current session, or do start a brand new session for this plan. So starting a brand new session, it will then like move me over to that with the Ultra plan passed back in.

So essentially the difference from the normal planning mode is that you use a trigger word, Ultra plan. It hands it off to a web version of Claude Code that research and drafts a plan. You can leave inline comments to the plan. And then once you've approved the plan to your liking, you can either run it in the cloud or teleport back to the local session instead. And you will also notice that for other sessions, when you run the local plan, then you will see right over here and there'll be another option that says no Refine with Ultra plan on Claude Code on the web. So pressing that, it will then transport your local plan to the web version and then it will do a validation step on the cloud.

Okay, now the question that you probably have is that, is this Ultra plan actually better than the normal planning mode inside of Claude Code? Now yesterday I did like 10 different Ultra plans and 10 different local plans and then compared them for the same prompt. And I did notice some differences, but like I couldn't reliably get those differences. So some of the differences that I did notice is that for things that make small changes across the entire application, like updating a dependency, Ultra plan seemed to do a better job at auditing the blast radius and then flagging any risks compared to the local plan instead. Whereas the local plan just kind of assumed that any build step or build command would catch any things that missed. When upgrading a dependency. So in one particular case, I was migrating from tRPC version 10 to version 11, and the Ultra plan caught more potential issues compared to the Local plan. But in other cases, removing Qwen 3.5 and using Gemma 4 instead, it seemed that the Ultra plan didn't really have an impact and make the plan any better. So the only difference was that it basically presented a nicer UI for actually reviewing the plan and leaving comments at specific points.

So as a short aside, I do also have a free Claude Code newsletter. So if you are interested in getting the latest from someone who is using Claude Code like 10 hours every single day, then I do share this in my newsletter. There will be a link down below if you're interested, and signing up will give you access to a bunch of free videos from my masterclass.

So then I was wondering like, okay, why is Ultra Plan really good in some cases and like kind of mid or basically the same as a Local Plan in other cases? So I got Claude Code to do some digging through the binary readable strings over here, and essentially it discovered that there are 3 different planning modes inside of Ultra Plan. So there is the simple plan, the visual plan, and then free subagents with a critique plan. And this is the system prompt for each of the planning modes right over here. So the visual plan is basically the same as the normal plan, but it just generates some ASCII diagrams and like Mermaid diagrams as well, which is why sometimes I notice the Ultra Planner mode like generating Mermaid diagrams kind of like this and other times not. And then this is the most interesting planning mode. So they call this the deep plan and it's basically a multi-agent exploration with a critique pass. So they have one agent that understands relevant code and the existing architecture, another one to find all files that need modification, another one to identify potential risks, edge cases, and dependencies, and then another one to review the plan for missing steps, risks, and mitigations over here.

And essentially what Anthropic are doing behind the scenes is that they're using a remote config to decide which Ultra Plan mode that you will be sent to. And this is entirely server controlled, the user never actually picks this. So I noticed that sometimes I was getting a really good plan because they assigned me variant free, which had the 3 different subagents with a critique. And other times I was getting a pretty mid plan, which was the same as a local plan. And ultimately what I think is happening here is that Anthropic want to measure how many people are accepting each variant and then deciding which planning mode, planning prompt is better for users. So essentially this whole ultra planning thing is like an A/B/C test for us to figure out which system prompt they should be using going forwards for planning. But I think that this gives them the infrastructure to do other testing as well. So for example, for an upcoming model, they could use an upcoming unreleased model to generate either plan, and then they will measure how many people are accepting that plan to inform whether that prompt or that model is actually good for planning. So maybe with all this A/B testing that they're doing with Ultraplan, they'll get a better sense of how good planning works.

But ultimately, I want to know exactly which planning mode that I'm being assigned to. So I think that I will use the Ultraplan deep plan prompt directly as some kind of skill instead. So this will be down below for those of you who are interested in copying this, because just by reading through this prompt, it seems that this approach may actually be pretty good compared to the normal planning mode prompt.

Anyways, that said, you will find that the Ultra Plan is actually faster. In all 10 versions that I ran, Ultra Plan finished about 2 times faster compared to the Local Plan for the same prompt. I think that it is better for multitasking as well, because you can spin up many different Ultra Plans. From like your terminal and then review them all in like a nicer UI as well. And it can be quite handy for quick prototyping and iteration because you can fire off a change to the cloud version of Ultraplan and then see what that would look like. And then if the plan doesn't look good, you can just discard it quite easily without polluting the rest of the conversation.

Anyways, I think that I will stay away from Ultraplanning for now and just use the free ServAgents with a critique as a custom skill instead. Anyways, if you're interested in diving much deeper into Claude Code, then I do have an entire masterclass about this which many people from some of the world's biggest companies have already taken. It is the first and the most comprehensive Claude Code class that you'll find online. And there are many other ideas that are covered here that you will not find anywhere else on YouTube. I do update it every single day whenever a new feature is released or there's a new technique that I discover. If you do have any questions about this, then you can email me using the email you can see on the screen right now.

</details>
