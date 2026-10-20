---
title: "Claude Skills: Build Your Own AI Employees"
video_id: 2Vcn2bAu2FA
channel: "[[channels/Greg Isenberg]]"
uploaded: 2025-12-24
processed: 2026-07-05
duration: "19:59"
url: https://www.youtube.com/watch?v=2Vcn2bAu2FA
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [claude-skills-setup, copywriting-review-automation]
tools: []
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Skills: Build Your Own AI Employees

![thumbnail](https://i.ytimg.com/vi/2Vcn2bAu2FA/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=2Vcn2bAu2FA) | 📅 Uploaded [[uploaded/2025-12-24]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A beginner-friendly walkthrough (no Claude Code required, just the web/Mac app) for enabling Claude Skills, using the "create a skill together" flow to build a conversion-focused copywriting review skill for a design agency, installing and testing it against real App Store screenshots and website copy, and then improving skills over time using a 10-step "think like an expert, not steps" iteration process.

**Watch this if:** you've never made a Claude Skill before and want a real end-to-end example, not just theory.

## Key Takeaways
- Skills aren't enabled by default — turn them on via Settings → Capabilities → Skills (preview), where you can then create one via three paths: "create with Claude" (conversational), "write skill instructions" (for skills easy to describe upfront), or upload an existing skill file/zip.
- The "create a skill together" flow has Claude ask scoping questions (what apps/websites you build, how you'll provide copy for review — screenshots, Figma files, pasted text — which elements to critique, and what a helpful review should look like: before/after suggestions, scored assessment, prioritized fixes).
- Skills beat Projects for ongoing, day-to-day work because Projects are inherently scoped to a specific timeframe/campaign (e.g. a Christmas campaign), while a skill like a copywriting reviewer should work the same regardless of which specific project or campaign you're using it for.
- The generated skill included a `skill.md` (step-by-step review workflow with scoring system and output template), a conversion-frameworks doc (AIDA, PAS, BAB, value proposition formulas), and an element-guidelines doc (best practices per copy element — headlines, CTAs, pricing, etc.) — all in plain markdown, which Anthropic has said is intentional because it's simple and easy for non-technical users to read and edit.
- Installing a self-created skill is as simple as clicking "copy to your skills" (or manually uploading the `.skill` file under Settings → Capabilities → Skills) and starting a new chat.
- Live test: fed the skill real App Store screenshots and website copy for a calorie-tracking app; it scored the existing copy (as low as 3/10), diagnosed specific problems (generic messaging, no differentiation, wasted headline space), and produced concrete before/after rewrites with psychological rationale for each (e.g. "Track calories in 3 seconds" vs. the generic original).
- Referencing a "Boring Marketer" tweet, the video lays out a 10-step process for leveling up a skill over time: understand the problem, explore where Claude fails without guidance, research the domain deeply, synthesize principles, draft, self-critique against quality criteria, iterate, test on real scenarios, and finalize into an optimal structure.
- The underlying philosophy: make the skill think like an expert practitioner producing final output, not documentation to follow step-by-step — every section in the skill should "earn its place" through ruthless constraint.
- Skills aren't static — once built, edit and refine them based on real output you don't like, gradually turning the skill into something that behaves like an employee who already knows your business without needing to be re-briefed each time.
- For maximum control over skills (beyond the web/Mac app shown here), the video notes that running them inside a terminal-based platform like Claude Code is where you get the most control — though that setup isn't covered in this beginner episode.

## 🛠 Tools & Software
None identified.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the entire video is about setting up and using its Skills feature (via the web/Mac app), from enabling it in settings to the "create a skill together" flow and live testing

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Enable Skills under Settings → Capabilities → Skills (preview) if you haven't already.
- Use the "create a skill together" flow and answer Claude's scoping questions as if briefing a new employee.
- Build a skill for a genuinely recurring task (like copywriting review) rather than a one-off campaign — that's what Skills are for versus Projects.
- Test a new skill against a real, concrete example (real screenshots, real copy) rather than a hypothetical one.
- Apply the 10-step iteration process (understand → explore failures → research → synthesize → draft → self-critique → iterate → test → finalize) to improve a skill after its first version.
- Edit the generated markdown files directly when you want to refine a skill's frameworks or output template.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: why Skills make Claude's output more consistent
- `0:40` — Enabling Skills: Settings → Capabilities → Skills preview
- `1:21` — Creating a new skill: the three paths, and scoping questions for a copywriting review skill
- `6:34` — Why Skills beat Projects for "always-on" ongoing work
- `7:49` — Reviewing the generated skill: skill.md, frameworks doc, element guidelines
- `10:34` — Installing the skill (copy to skills / upload)
- `11:28` — Testing the skill on real App Store screenshots and website copy
- `16:14` — How to improve a skill over time: the 10-step process

## Transcript
<details>
<summary>Full transcript</summary>

A beginner's guide to setting up Claude Skills, using just the web app or Mac app (not Claude Code), to get more consistent, higher-value output. Skills aren't enabled by default — go to Settings → Capabilities, scroll down to the Skills preview feature, and enable it. Creating a new skill offers three options: "create with Claude" (build complex skills through conversation), "write skill instructions" (for skills that are easy to describe outright), or upload an existing skill zip/file. For most people, "let's create a skill together" is the way to go — it onboards you using Claude's own skill-creator skill, first asking what functionality the skill should provide (working with specific formats/data, following particular workflows, integrating with tools/APIs, applying domain-specific knowledge, or something else). The example built here: a design agency owner wants a skill that reviews app and website copy for conversion rate, essentially acting like a specialized copywriter for apps and websites. Claude responds

that this would be valuable and asks clarifying questions: what kind of apps/websites are typically built (mobile apps with embedded AI, or SaaS), how copy will be provided for review (screenshots, Figma files, or pasted text — whatever's easiest), which specific elements to critique (headlines, CTAs, value props, product descriptions, hero sections, pricing pages, onboarding flows — "all of the above" in this case), and what a helpful review should look like (specific before/after suggestions, scored assessment, prioritized issues by impact) — treating the exchange like briefing a new employee. A useful tip before building your first skill: ask Claude, given what you do, for a list of ten skills you should consider creating — the copywriting reviewer here would just be one of them. Once scoped, Claude confirms

the plan (a conversion copywriting review skill covering all copy elements, with scored assessments, prioritized before/after suggestions, and support for screenshots, Figma files, and pasted text) and starts building the skill structure. The value proposition of a skill over a single chat is consistency — a one-off chat conversation loses context over time, while a skill bakes in the right context permanently so output stays consistent and business-aware. A natural question is why not just use a Claude Project instead — but Projects are inherently scoped to a specific timeframe (e.g. a Christmas campaign), whereas skills should function like members of your team, working the same way regardless of which specific campaign or project you're in — more suited to day-to-day operations than time-bound work. Checking

in on the build, Claude works through setting up the skill structure, removing unneeded example files, creating reference materials, and writing the main skill.md with the review workflow. These are plain markdown files — deliberately so, since Anthropic reportedly explained that markdown "just works" and is easy for non-technical people to read and edit, rather than something more complex. Watching the build process show key principles and quality standards taking shape, the finished

skill (an "LCA conversion copy review skill") includes: skill.md (the step-by-step review workflow with a scoring system and output template), conversion-frameworks.md (core copywriting frameworks like AIDA — attention, interest, desire, action — PAS, BAB, and value-proposition formulas), and element-guidelines.md (specific best practices per copy element — headlines, CTAs,

pricing, etc.). How it works: when asked to review copy, it automatically loads the conversion frameworks and guidelines, analyzes each element with specific scoring, prioritizes fixes by conversion impact (critical/high/medium/low), and provides before/after examples with psychological rationale. To use it, the `.skill` file gets uploaded to Claude, then any app or website copy can be submitted for review. Installing involves downloading the skill, clicking "copy to your skills" (which adds it automatically), or manually uploading it again under Settings → Capabilities → Skills, then starting a fresh chat to test it. For a live test, App Store screenshots of a popular calorie-tracking app (Cal AI) are captured along

with its website copy, and the skill is invoked directly: "please use the conversion review skill to look at these App Store screenshots and provide better copy," including the website copy as well. Claude examines conversion copywriting best practices for the app category first, then produces a detailed critique — noting the existing copy relies on generic AI messaging without concrete differentiation, that the App Store screenshots use vague headlines failing to communicate value, and that the website buries compelling features under technical language. Top priorities identified: rewrite headlines around specific outcomes, clarify the unique AI capability (depth-sensor-based volume calculation), and lead with transformation rather than features. Looking at

the actual screenshots — "Make calorie tracking easy with AI... snap a picture of your food, then let us do the rest" — the skill flags this as too generic (every calorie tracker claims to be easy) and scores it harshly (3/10), then offers alternatives: "Track calories in 3 seconds — no manual logging, get exact portions using iPhone depth sensing" (praised for a specific time frame, addressing friction points, and highlighting the unique tech), and a transformation-focused alternative leading with a results

claim ("Lost 17 lbs without counting a single calorie... join 5 million users hitting their goals daily"). For the website copy ("Meet Cal AI. Track your calories with just a picture"), the skill flags wasted headline space and no emotional hook, recommending "The only calorie tracker that actually knows portion sizes — your iPhone depth sensor measures exact food volume," followed by prioritized improvements, notes on what's already working, and a closing summary. Referencing a tweet from "Boring Marketer" about getting the most out of Claude Skills — "the trick to creating

effective skills is to make your AI think like an expert, not just follow steps" — a 10-step improvement process is laid out: understand the problem, explore where Claude fails without guidance, research the domain deeply, synthesize principles from that research, draft the initial skill, self-critique against quality criteria, iterate to fix gaps based on feedback, test on a real scenario, and finalize into an optimal structure. The underlying philosophy: make Claude think and produce like an expert practitioner rather than following documentation step by step, and constrain every section of a skill ruthlessly so each part earns its place. Skills should never stay static — once you see output you don't like, you edit the skill itself and iterate from there. The natural progression is: first, create your initial skills; second, keep iterating on them until they function like an employee who already knows your business without needing re-briefing; and third, for maximum control, run skills inside a terminal-based platform like Claude Code rather than just the web or Mac app shown in this episode.

</details>
