---
title: "Your AI UI Looks Generic… This Fixes It (DESIGN.md)"
video_id: pY52H5gKhGg
channel: "[[channels/Better Stack]]"
uploaded: 2026-05-07
processed: 2026-07-05
duration: "5:35"
url: https://www.youtube.com/watch?v=pY52H5gKhGg
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [ai-generated-ui-consistency, design-system-for-ai-agents]
tools: [DESIGN.md, Cursor, Claude Code, v0, Figma, Google Stitch]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Your AI UI Looks Generic… This Fixes It (DESIGN.md)

![thumbnail](https://i.ytimg.com/vi_webp/pY52H5gKhGg/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=pY52H5gKhGg) | 📅 Uploaded [[uploaded/2026-05-07]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> DESIGN.md is a plain-Markdown design-system format, open-sourced by Google, that tells AI coding tools (Cursor, Claude Code, v0) exactly how a product should look and feel — colors, fonts, spacing, layout rules, and the intent behind them — so generated UIs stop looking like generic default Tailwind output. The video runs a same-prompt, with/without comparison and weighs it against Figma and raw JSON tokens.

**Watch this if:** your AI-generated UIs technically work but look cheap and generic, and you want a repo-native way to give coding agents real brand/design context.

## Key Takeaways
- DESIGN.md is a plain Markdown file combining structured design tokens (exact hex colors, font families, border radius, spacing) with prose explaining the intent behind them (e.g., "this blue is the primary accent and should feel clear and trustworthy").
- Google open-sourced it on April 21st and the community "awesome-design-md" repo passed 70,000 GitHub stars within about two weeks.
- Live demo: the same "build a modern dashboard" prompt with no DESIGN.md produces a generic, default-Tailwind-looking dashboard; adding a Stripe-style DESIGN.md to the same prompt produces a dashboard with consistent color, spacing, and a real point of view.
- It's positioned as filling a gap between existing formats: Figma is human-readable but lives outside the repo, JSON tokens are machine-readable but don't explain intent, and Cursor Rules/CLAUDE.md tell an agent how to behave but aren't a design system — DESIGN.md is human- and machine-readable, version-controlled, and lives next to the code.
- Developers are sharing community DESIGN.md files for Linear, Stripe, Notion, and Vercel, eliminating the need to repeat prompts like "make it clean, make it modern, use better spacing" on every generation.
- Honest caveats: it's one file, so output quality is capped by what you put into it — a weak DESIGN.md still produces weak output, and setup requires someone to actually author a good one.
- Verdict: worth using, especially for solo devs, prototypes, and AI-heavy workflows already using Cursor, Claude Code, or v0 — start from a template in the awesome-design-md repo and customize it for your own brand.

## 🛠 Tools & Software
- [[topics/DESIGN.md]] — the open-source Markdown design-system format that is the entire subject of the video, demoed live with a before/after dashboard comparison
- [[topics/Cursor]] — named as one of the AI coding tools that benefits from having a DESIGN.md file in the repo
- [[topics/Claude Code]] — named as one of the AI coding tools DESIGN.md targets; also the tool whose CLAUDE.md convention is contrasted with DESIGN.md
- [[topics/v0]] — named as another AI coding tool that produces generic UIs without design context
- [[topics/Figma]] — contrasted against DESIGN.md as a human-readable but repo-external design tool
- [[topics/Google Stitch]] — the Google product/team behind DESIGN.md's release and documentation

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Grab a starter DESIGN.md template from the awesome-design-md GitHub repo instead of writing one from scratch.
- Customize the template's tokens and intent notes (colors, typography, components, accessibility) for your own brand before generating UI.
- Re-run your existing AI UI prompts with the DESIGN.md file dropped into the repo and compare the output to your current baseline.
- Treat DESIGN.md as a floor, not a ceiling — invest real effort in the intent/prose sections, since a thin file still produces thin output.

## 🔗 Related Videos
- [[videos/Google Stitch 20 Antigravity Free Design-to-Code Workflow Nobody Talks About]] — shared: DESIGN.md, Figma, Google Stitch
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor
- [[videos/Claude Code 'Interview' Mode in 6 Minutes]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Drawbridge Builds Websites By Sight (NEW Plugin)]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Cursor
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: Claude Code, Cursor
- [[videos/Claude Code is Amazing Until It DELETES Production]] — shared: Claude Code, Cursor

## Timeline
- `0:00` — Why AI-generated UIs still look generic
- `0:32` — What is DESIGN.md?
- `1:10` — Live demo: same prompt, with and without DESIGN.md
- `2:11` — How DESIGN.md actually works: tokens plus intent
- `2:35` — Why AI needs design context, not just values
- `3:00` — DESIGN.md vs. Figma vs. JSON tokens vs. Cursor Rules/CLAUDE.md
- `3:45` — Why developers are switching to DESIGN.md
- `4:15` — Pros and cons of DESIGN.md
- `5:00` — Is DESIGN.md actually worth using?

## Transcript
<details>
<summary>Full transcript</summary>

AI coding tools are getting scary good. Cursor, Claude Code, v0, you can go from an idea to a working app in minutes, but then you open the UI and it just looks off. The code works, but the UI still feels really cheap. Now, compare that to Stripe, Linear, Vercel, really any big platform. So, what are they doing differently? It's just one simple file. It's called Design MD and Google just open-sourced it. I'll show you how to inject this in your code in just a couple minutes.

Now, Design MD is a plain Markdown file that tells AI agents how your product should feel and look. Colors, fonts, spacing, buttons, layout rules, accessibility notes, everything. So, instead of guessing your brand, the AI reads the file and follows it. There's no Figma export, no JSON mess, there's no 10-paragraph prompt that I need to do every time to get perfect. Google open-sourced it on April 21st and within just a couple weeks, it's already blown up on GitHub to well over 70,000 stars.

All right, now this is really cool. Let me show you why this actually matters. Okay, I'm going to go with the same prompt here, build a modern dashboard. First, there is no Design MD file. It generates and yeah, this is a classic AI dashboard. Technically works, right? But it has default Tailwind energy, it just looks like it. Random buttons, we have our generic cards here. There's no real identity to anything you're actually building out. Now, if I run the same prompt again, but this time I add a Stripe-style Design MD file, or really any Design MD file you want for another brand, and look at the difference. The colors line up, the spacing feels cleaner, the buttons look like they actually belong together. The whole screen has a point of view. Same AI, same prompt, but now it's different context. Without Design MD, the AI is guessing. What should the site look like? With Design MD, the AI has rules based on other proven platforms that already look really good.

So, what's actually inside this file? Think of it like a design system the AI can read. At the top, you usually have structured tokens. Stuff like exact hex colors, font families, border radius, spacing. These are hard rules, but the important part is what comes after that. Markdown. This is where you explain the intent. Not just use this blue color, but this blue is the primary accent and it should feel clear and trustworthy. That matters because AI doesn't just need numbers, it needs judgment. A good Design MD usually covers color palette, typography, components, layouts, accessibility, so the AI gets two things at once. The exact values and the reason behind them. And that is why the output stops drifting away from what we're actually trying to go for.

Now, the obvious question is, do we really need another design system format? We already have Figma, we already have JSON tokens, and we already have Cursor Rules and CLAUDE.md, but each one of these solves a different problem. Figma is a UI. It's great for humans, but it usually lives outside the repo. JSON tokens are great for machines, but they do not explain our taste for the website or the intent we're going after. Cursor Rules and CLAUDE.md tell the agent how to behave, but they're not really a design system. Design MD sits in all of this. It's human-readable, it's also at the same time machine-readable, it's version-controlled, and agent-native. That's the big change here. Your design system is no longer trapped in a design tool, it lives right next to your code within this markdown file.

And this is why it's blown up in just 2 weeks and devs are paying attention. The community repo is now over 70,000 stars, right? That's super fast. People are sharing design.md files for linear, stripe, notion, and Vercel. And the reason behind it is simple. Nobody wants to keep typing, "Make it clean. Make it modern. Use better spacing. Make it more like this website." Come on, that gets old so fast. With design.md, you stop repeating yourself. You give the AI the design rules once, then every screen starts from the same foundation. That's the real win here. The design across all screens, speed. There is less rework. There's less fixing the same ugly button for the 10th time.

All right, now honest take here, it's not perfect. It's a great start, right? But it is one file. It lives in your repo. It works across tools. It includes accessibility guidance, and setup is basically zero, which is great, super easy to drop in. Also, the file is only good at what you put in it. A weak design.md is obviously going to give you a weak output. But for solo devs, prototypes, AI-heavy workflows, this is a really practical upgrade. So, should you use it? Yeah, probably so. Especially if you're already building with Cursor, Claude Code, v0, start with a template from the awesome repo. It's in the description. Drop it in your project, then customize it for your own site, your own brand. Your goal is not to make the AI creative. Your goal is to stop making it guess. Because once the rules are clear, the UI is going to get more consistent, and your app starts to feel less like an AI demo and more like a real product.

</details>
