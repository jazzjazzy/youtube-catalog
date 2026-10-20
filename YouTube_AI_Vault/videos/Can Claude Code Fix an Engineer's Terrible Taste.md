---
title: "Can Claude Code Fix an Engineer's Terrible Taste?"
video_id: vl_fS1i6uAg
channel: "[[channels/Pocketful of AI]]"
uploaded: 2026-01-12
processed: 2026-07-06
duration: "17:22"
url: https://www.youtube.com/watch?v=vl_fS1i6uAg
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: beginner
use_case: [ai-frontend-design-polish]
tools: [Claude Code, Claude Code Frontend Design Plugin, Antigravity, Claude Browser Extension]
llms: [Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Can Claude Code Fix an Engineer's Terrible Taste?

![thumbnail](https://i.ytimg.com/vi_webp/vl_fS1i6uAg/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=vl_fS1i6uAg) | 📅 Uploaded [[uploaded/2026-01-12]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Pocketful of AI, who describes having "no design vocabulary," gives the exact same redesign prompt for a plain habit-tracker app to three systems: plain Claude Code, Claude Code with the new Frontend Design plugin, and Google's Antigravity (using Gemini 3 Pro High). Plain Claude Code made the app noticeably worse; the Frontend Design plugin produced the most polished, "finished product" result; Antigravity produced a rougher but genuinely creative result with details the host wouldn't have known to ask for.

**Watch this if:** you can build functional apps but can't articulate design taste ("make it prettier"), and want real evidence of whether an AI design plugin helps versus a base coding agent.

## Key Takeaways
- The same prompt (redesign the UI to feel "premium and professional" while keeping the existing layout, toggle, and grid-card structure, with no new features/gamification) was given to all three systems for a fair comparison.
- Claude Code without any plugin actually made the app look worse: it removed card borders in favor of a subtle hover shadow, shrank fonts and header spacing, and made the "see the whole year" overview page feel sparse and unfinished.
- Installing Anthropic's official Frontend Design plugin (`use skill frontend-design`) and giving the identical prompt produced a completely different, more premium result: new title/body fonts, a warm cream/forest-green/terracotta palette, subtle paper-like noise texture, colored status-ring halos, staggered fade-in animations, and card-style quarterly rows — while still preserving the original's clean, minimal structure.
- The plugin version kept useful details the plain version dropped (borders around cards/quarters) and was the host's clear favorite: "finished and polished... feels like a real product, not a prototype."
- Running the identical prompt in Google's Antigravity (fast mode, Gemini 3 Pro High) produced a rougher but more visually surprising result — the host specifically liked a colored edge treatment on the cards she "wouldn't have thought to ask for," though the overview page initially broke (a missing status-dot style) and ended up left-justified/oddly small once fixed.
- Both Claude Code (via its Chrome extension) and Antigravity have built-in browser access to visually test their own UI changes as they work, which the host says "levels the playing field" between the two tools.
- Overall verdict: the Frontend Design plugin wins for reliably shippable polish; Antigravity is worth it if you want more creative surprise at the cost of some rough edges; running Claude Code without a design-specific plugin/skill for pure aesthetic work is actively risky — it can make things worse rather than better.

## 🛠 Tools & Software
- [[topics/Claude Code]] — run twice: once with no design plugin (control) and once with the Frontend Design plugin, using identical prompts against the same habit-tracker app.
- [[topics/Claude Code Frontend Design Plugin]] — Anthropic's official plugin, installed and triggered via `use skill frontend-design`; produced the video's best-reviewed redesign result.
- [[topics/Antigravity]] — Google's IDE, run in fast mode with Gemini 3 Pro High on the same prompt as a third comparison point.
- [[topics/Claude Browser Extension]] — used to grant Claude Code its own browser for visually testing the redesigned UI during the plugin run.

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — Gemini 3 Pro (High) is the model used to power the Antigravity redesign attempt; also separately consulted by the host (off-camera) to critique her original app's look.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Before asking Claude Code to redesign a UI purely on vague instructions ("make it prettier"), install and trigger a dedicated frontend-design skill/plugin rather than relying on the base agent.
- Write a redesign prompt that explicitly states what must NOT change (layout, key toggles, feature scope) so the agent focuses purely on visual polish.
- If comparing coding agents/tools for design output, hold the prompt, starting app, and constraints identical across every run for a fair side-by-side.
- Try Antigravity with a high-reasoning model (e.g. Gemini 3 Pro High) if you want more creative/unexpected design choices, but budget time to fix rough edges afterward.

## 🔗 Related Videos
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Antigravity, Claude Code, Gemini
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Antigravity, Claude Code
- [[videos/7 new open source AI tools you need right now]] — shared: Claude Code, Gemini
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Gemini
- [[videos/Claude Code + Karpathy Slides Just Changed Presentations Forever (MARP System)]] — shared: Antigravity, Claude Code
- [[videos/Claude Code + Karpathy's Autoresearch = GOD MODE!]] — shared: Claude Code, Gemini
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Browser Extension, Claude Code
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude Browser Extension, Claude Code

## Timeline
- `0:00` — Intro: no design vocabulary, an app that looks like a "Soviet-era apartment block," and the test setup (3 systems, identical prompt).
- `2:01` — The habit-tracker app being redesigned: three states per week, quarter view and full-year overview.
- `2:44` — The exact redesign prompt: premium/professional feel, keep layout/toggle/grid, no new features, stay minimal.
- `3:30` — Test 1: Claude Code with no plugin — described changes vs. actual (disappointing) visual result.
- `6:05` — Installing the Claude Code Frontend Design plugin and running the same prompt.
- `7:26` — Frontend Design plugin result: new fonts, warm palette, card borders/hover halos, staggered animations — host's early favorite.
- `10:14` — Test 3: Antigravity in fast mode with Gemini 3 Pro High, including a UI bug (broken status dots) that gets self-fixed.
- `13:32` — Side-by-side of all four versions (original, Claude Code control, plugin, Antigravity) on both the detail and overview pages.
- `15:26` — Wrap-up verdict: plugin wins on polish, Antigravity wins on creative surprise, plain Claude Code made things worse.

## Transcript
<details>
<summary>Full transcript</summary>

My front-end design skills are basically non-existent — I tend to create apps that look like this. When working on the script for this video, I handed a screenshot of my app to Gemini, and it basically told me my app was the digital equivalent of a Soviet-era apartment block. Yeah, that one stung a little. So I thought I'd put the new Claude Code Frontend Design plugin to the test today — I'm eager to see if this can save me from myself.

To give this a fair test, I'm taking the same prompt and giving it to three different systems. One is Claude Code control: I'll open a branch of this repo in regular Claude Code, give it the prompt asking it to enhance the design, and see what it comes back with. In another branch of the same repo, I'll install the Frontend Design plugin into Claude Code and give it the identical prompt, hoping for something different enough to be discernible and workable. Basically, I don't have the vocabulary to describe the designs I'm looking for — I generally say things like "make this prettier," "make it elegant," "make it fun and colorful." I don't even have the language to describe what makes something more visually appealing, let alone ask for it correctly. So I'm really hoping this plugin can do a lot of the heavy lifting. And just for kicks, I'm also going to ask Google's Antigravity IDE to do the same thing — partly because I actually really like the tool, and partly because I've seen a lot of people in comments say they like designing with Antigravity. I'm curious whether, given the same prompt, it comes up with something different, or better.

This is the app we're working with: I set myself a 2026 challenge to build an app every week — 52 weeks, 52 apps — and the first one was a habit-tracking app. In the spec I actually asked for it to be very plain and simple: each week has three states (successful, didn't ship, or future project), viewable either by quarter or as a full-year-at-a-glance overview. I figured this would make a good testbed.

Test one: Claude Code control, no plugin. Here's the prompt I'm handing to all three systems: "Context: I have a simple 52-apps habit tracker that I built. I love the simplicity, but it is extremely plain, vanilla, and feels unfinished. Your goal is to redesign the UI and make it feel premium and professional without sacrificing the clean, minimal aesthetic. I want this to look like a finished product, not a developer prototype. Constraints — do not break these: do not change the core layout, keep the details/overview toggle and the grid-based card structure, do not add new features (no gamification, no social sharing, no complexity), and keep it minimal — I don't want clutter, I want elegant simplicity." Claude Code without the plugin said it: shifted the color palette from cold grays to warm stone tones, used brighter emerald green and rose pink status colors for visual punch, tightened letter spacing on headers with uppercase quarter labels, added layered shadows and colored glow rings on status indicators instead of flat borders, and general polish. Sounds great on paper — but seeing it side by side with the original, the host was completely underwhelmed: it actually looked worse. The "tightened" header font just looked smaller; the clean borders around cards and the status button were removed and replaced with a barely visible hover shadow, making things look fuzzy rather than crisp. The overview page — whose entire point was seeing the whole year at a glance — got smaller, more distant title indicators and more empty space, making it feel like something was missing. Overall verdict: disappointing, and to her eye, an actual downgrade — a fail.

Test two: Claude Code with the plugin. In a fresh branch, the host installs the official Frontend Design plugin (scoped locally to avoid affecting other project copies), restarts Claude Code to load it, and runs Claude with the Chrome browser option enabled so it can open the Chrome extension and visually test its work. After confirming the plugin is enabled, she runs `/init` and instructs Claude to "use the skill frontend-design." Claude tests in the Chrome browser extension, asks for various permissions (all granted), and reports: "The design is complete and looking premium. Here's what was transformed" — new fonts for title and body text; a warm cream background with forest green (success) and terracotta ("didn't ship") status colors described as sophisticated rather than alarming; subtle light halos and a subtle paper-like noise texture overlay for depth; status indicators with colored rings/halos; staggered fade-in animations on page load; and quarterly rows in the overview given card treatment — all while keeping the calm, minimal philosophy. Reviewing it live, the host immediately likes the more elegant, distinctive font, and appreciates that borders around individual cards were kept (now with an added shadow per week) plus uppercase text for a crisper look, including on the editable date field. Each quarter now gets its own self-contained hover card instead of just being separated by a line break, which she likes a lot. On the overview page, it again gives more breathing room but doesn't feel like it's missing anything — she can still see the whole year at a glance, and prefers the new card-like "collection" feel over the original's more perfunctory "thumbtacks on a card" look. She's fine with keeping red/green status colors (as originally requested) and concludes this version clearly adds refinement and elegance.

Test three: Antigravity. To keep things fair (since neither Claude Code run used planning mode), she runs Antigravity in fast mode using Gemini 3 Pro High for the best possible outcome, giving it the exact same prompt. She likes that Antigravity also has its own browser to visually test its changes — now that Claude Code has the Chrome extension too, it "levels the playing field" between the two, and it's fun to watch both work semi-autonomously. The initial result includes a font change she likes and a card treatment that's new to her, and she can still see the whole quarter at a glance with the three toggles intact — but the overview page is broken. Giving Antigravity a chance to fix it, the agent apologizes, explaining it "accidentally removed the specific styles for the status dots during the redesign," and then successfully fixes the overview page. Comparing again: the font looks subtly different and arguably a touch better (a "rounder Q"); she really likes the outlined-card treatment, calling the overall result a genuine, creative improvement — though the fixed overview page ends up left-justified, too small, and not centered, which she notes would be an easy fix but wasn't the point of an out-of-the-box test.

Final side-by-side of all four versions (original, Claude Code control, plugin, Antigravity) at 100% scale: the Claude Code control is her least favorite — smaller fonts, fuzzier, less crisp than the original. The plugin version looks "pretty nice," with an elegant font, good color changes, and a nice bordered-quarter treatment. Antigravity's font is a touch rounder and its card border/detail treatment looks "really nice," though its overview ends up cramped and left-justified — an easy fix, but not something that happened out of the box.

If she had to pick one today: the plugin version, no contest — the font, colors, and card treatment all feel finished and polished, like a real shippable product rather than a prototype (her usual outcome). But Antigravity genuinely surprised her: the colored edge treatment on the cards was something she wouldn't have known to ask for, and while less refined than Claude's plugin output, it was creative in a way Claude's wasn't — with maybe another 10 minutes of polish, she'd happily use it too.

Her takeaway: if you're like her — no design vocabulary, and the best you can say is "make it prettier" or "make this polished and elegant" — the Frontend Design plugin is 100% worth trying; install it and let it do its magic. The gap between Claude Code with and without the plugin was night and day: without it, Claude Code actually made the app worse (she didn't think that was even possible); with it, the app felt complete enough to ship and walk away. She'll link the plugin in the description, since there are a few different UI design plugins out there, and encourages subscribing for more "testing the tools so you don't have to" content. Thanks for watching — see you next time.

</details>
