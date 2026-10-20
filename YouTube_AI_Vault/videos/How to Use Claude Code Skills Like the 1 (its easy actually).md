---
title: "How to Use Claude Code Skills Like the 1% (it's easy actually)"
video_id: 6-D3fg3JUL4
channel: "[[channels/Simon Scrapes]]"
uploaded: 2026-03-04
processed: 2026-07-05
duration: "16:33"
url: https://www.youtube.com/watch?v=6-D3fg3JUL4
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [claude-code-skill-design]
tools: [Claude Code, GSD, Claude Skills, Skills MP, SkillHub]
llms: [Claude, Nano Banana]
protocols: [webhooks]
transcript: true
tags: [youtube, ai-automation]
---

# How to Use Claude Code Skills Like the 1% (it's easy actually)

![thumbnail](https://i.ytimg.com/vi_webp/6-D3fg3JUL4/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=6-D3fg3JUL4) | 📅 Uploaded [[uploaded/2026-03-04]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Most people install hundreds or thousands of Claude Code skills assuming more is better, but that's actually why their agents get slower and less predictable. This video breaks down how skills really work under progressive disclosure (YAML summary, skill.md process, and lazily-loaded reference/scripts/assets), why a small curated set massively outperforms a huge generic library, and where to source or build skills properly.

**Watch this if:** you're accumulating Claude Code skills/plugins and want to understand why fewer, well-built ones consistently beat a giant marketplace-installed library.

## Key Takeaways
- A skill is a folder with a skill.md (the SOP: what to do, in what order, what good looks like) plus optional scripts (executable), references (knowledge/examples), and assets — not just a "good system prompt."
- Progressive disclosure means only the skill's YAML front matter (name + description) loads into context up front; the skill.md body and its linked files load only once Claude decides to use that skill.
- "Point, don't dump": keep the skill.md lean and push deep knowledge (e.g., 139 marketing approaches) into reference files the skill.md points to, loading different reference files only when relevant (e.g., title formulas vs. content structure templates).
- Because only name+description are always loaded, skills scale in theory — but Anthropic's own docs cap the entire available-skills list at 15,000 characters, so loading hundreds/thousands of skills crowds that budget and creates crossover/cannibalization between similar skills.
- Real testing found skill activation as low as 20% with a basic setup and poor description, and only around 84% even with optimized descriptions and hooks — with 500+ generic skills competing, output quality becomes highly inconsistent.
- Skills are increasingly discussed as a new software layer: Anthropic's Cowork/plugins launch reportedly triggered a $285B software-stock sell-off (Intuit, Adobe, Salesforce) because a well-built skill can replace chunks of a dedicated SaaS tool.
- Three sources for skills: Anthropic's official skills (installed via `npx skills add`), community marketplaces (Skills MP with 280K+ indexed, SkillHub with 7K+ AI-evaluated skills), and building your own — the last being where real, business-specific value lives.
- Rather than writing skills from scratch, you can use a skill-building skill (like GSD creator Tash's agent-skill-creator) to generate properly structured skills that follow the same summary/process/reference conventions.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the platform whose skill system (progressive disclosure, YAML front matter, skill.md, reference files) is explained throughout.
- [[topics/GSD]] — Tash's GSD framework includes an agent-skill-creator skill (installed via `npx skills add glittercowboy`) used to build properly structured skills.
- [[topics/Claude Skills]] — Anthropic's official skills repo (e.g., PDF manipulation) shown being installed via `npx skills add anthropics/skills --skill pdf [--global]`.
- [[topics/Skills MP]] — a community marketplace with over 280,000 skills indexed from GitHub, searchable by category.
- [[topics/SkillHub]] — a community marketplace with 7,000+ AI-evaluated skills, searchable by category, use case, or role.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying Claude Code and every skill example discussed.
- [[topics/Nano Banana]] — referenced as the model behind an image-generation/editing skill example that runs a script (`generate_image.py`) rather than a lengthy skill.md.

## 📡 Protocols & Standards
- [[topics/webhooks]] — mentioned as part of what a Stripe best-practices skill helps Claude reference (Stripe webhooks and API calls).

## ✅ Action Items
- Audit your installed Claude Code skills/plugins and cut anything generic or overlapping rather than chasing marketplace volume.
- Restructure any bloated skill.md files by moving deep knowledge into separate reference files, loaded conditionally.
- Try installing Anthropic's official PDF skill via `npx skills add anthropics/skills --skill pdf` to see the recommended structure firsthand.
- Use a skill-creator skill (e.g., GSD's agent-skill-creator) to scaffold new skills instead of hand-writing every one from scratch.
- Aim for a curated library of ~20-30 well-built, specifically-described skills tailored to your own workflows rather than hundreds of generic ones.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills, Nano Banana
- [[videos/Andrej Karpathy Just Fixed Claude Codes Biggest Weakness]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Every Claude Code Workflow Explained (& When to Use Each)]] — shared: Claude, Claude Code, GSD
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, Nano Banana
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, webhooks

## Timeline
- `0:00` — Intro: the 1% use fewer, properly built skills instead of installing hundreds or thousands.
- `0:41` — What a skill actually is: a folder with skill.md plus optional scripts, references, and assets.
- `1:51` — Progressive disclosure explained via a real "marketing ideas" skill's YAML front matter and body.
- `4:03` — "Point, don't dump": pushing deep knowledge into reference files instead of the skill.md itself.
- `4:57` — Conditional reference loading example: an SEO content-writer skill with separate title-formula and content-structure files.
- `5:31` — Script execution example: an image-generation/editing skill that calls a Python script rather than inlining instructions.
- `6:50` — Why this matters economically: the Cowork/plugins launch and the reported $285B software-stock sell-off.
- `7:46` — Skills becoming a new software layer, plus the marketplace ecosystem (Skills MP, SkillHub, Stripe/Cloudflare/Vercel/Sentry skills).
- `9:59` — Three sources for skills: Anthropic's official skills, installed via `npx skills add`.
- `11:01` — The danger of loading hundreds/thousands of skills: the 15,000-character list limit and real-world activation-rate testing (20-84%).
- `13:52` — Building your own skills: where the real, business-specific value comes from.
- `14:20` — Using a skill-creator skill (GSD's agent-skill-creator) to build properly structured skills, and closing takeaway.

## Transcript
<details>
<summary>Full transcript</summary>

I see this trend where people are installing hundreds or sometimes even thousands of Claude Code marketplace skills. They think that more equals better, and that's exactly what the 99% are doing. But it's the same reason why their agents are getting slower, less predictable, and harder to scale. Over the last few months, I've been reverse-engineering what actually works, building skills from scratch, testing out community builds, and crawling through the official docs. The 1% don't use more skills, they use fewer, and they build them properly.

A skill is just a folder with step-by-step instructions on how to create something valuable. The folder is made up of a skill.md file — the step-by-step process instructions for exactly what Claude should do — and a bunch of optional supporting files: scripts that can actually be executed, references like examples, and assets showing exactly how output should look. The skill.md file is effectively a standard operating procedure for an AI agent: here's what to do, here's the order, here's what good looks like, here's what to avoid, and it points to scripts/references/assets if relevant.

The really clever bit is progressive disclosure: we only give Claude the right information at the right time. Only the YAML front matter (name and description) loads into the initial prompt — think of it as the summary. Looking at a real "marketing ideas" skill, the name is "marketing ideas" and the description tells Claude exactly when to use it. We install it locally, then the skill.md body has the full process instructions — Claude won't load this until it knows it's going to use the skill from reading the description. This skill checks for a product-marketing-context file first, then suggests 3-5 relevant ideas.

Here's where "point, don't dump" comes in: we're not loading the skill with all 139 marketing categories directly in skill.md — that would load immediately as soon as we know we're using the skill. Instead skill.md has just the key task-specific questions, output format, and top ideas by use case, pointing to reference files where the actual knowledge lives. YAML front matter is the summary, skill.md body is the process, and linked reference/script/asset files only load when skill.md says to load them.

You don't just need one reference file either — you can load specific reference files only when needed. An SEO content-writer skill has two reference files: title formulas for ideating titles, content structure templates for structuring content — each introduced only when relevant. We can also have scripts to execute code — for example, a skill that generates or edits Nano Banana Pro images just says which script to run with which prompt depending on single-image editing vs. composing multiple images. The skill.md stays simple and concise; the executable script logic isn't loaded into context.

This is why skills scale — you're not overloading Claude's context window even installing thousands, because only the summary (name + description) of each loads. You're giving Claude a toolkit it reaches for when needed. But more isn't necessarily better, which I'll come back to.

Here's why you should care: what's happening with skills is bigger than a nice Claude Code feature. People are comparing skills to entire software products now. In early 2026, when Anthropic launched Cowork and their new plugins feature (bundles of skills, agents, hooks, and commands), it triggered a massive sell-off in software stocks — $285 billion wiped off companies like Intuit, Adobe, Salesforce. Investors panicked because if an AI agent with the right skills can do what a $50/month subscription does, why keep paying for separate tools? I'm not saying SaaS is dead — the stock prices were overvalued based on the old SaaS model — but skills are becoming a new layer of software. A well-built skill with the right reference files, scripts, and assets can do what used to require a dedicated SaaS tool with its own UI, custom to your own business with a few prompts. A lead-generation skill can replace parts of an outreach stack, a content-creation skill can replace a copywriting tool, an SEO skill can replace chunks of Ahrefs or Surfer.

Marketplaces of these skills are already blowing up: Skills MP has over 280,000 skills indexed from GitHub, searchable by category. SkillHub has 7,000+ AI-evaluated skills, searchable by category, use case, or role. Even companies like Stripe, Cloudflare, Vercel, and Sentry are launching their own skills that interact with their platforms — for example, a Stripe best-practices skill that lets Claude reference documentation about Stripe webhooks and API calls. It's becoming a total ecosystem, and the people who get really good at building and customizing skills tailored to their specific business (with years of context and process) will have a massive advantage over anyone who just installs a generic one. For agencies, skills become productizable too — build once, deploy for multiple clients, charge higher rates.

So where do you actually get these — build or download? Three sources. First, Anthropic's official skills — a good way to see how good skills are built, mostly doc transformation (docx, PDF creation/editing), each with a skill.md and scripts. Install with `npx skills add anthropics/skills --skill pdf`, or add `--global` to install across all projects.

Second, community marketplaces — Skills MP and SkillHub, searchable by category, use case, or role. But here's the trap nobody's talking about: there's a trend of people saying "just install 500 or 1,000 skills into your Claude Code setup." Remember progressive disclosure — Claude scans the name and description of every skill to decide which to use, so more skills means a noisier menu. Anthropic's own docs say there's a 15,000-character limit for the entire available-skills list that gets loaded. Loading 1,000 skills eats that budget and creates crossover skills that cannibalize each other — if you have two SEO skills, which does Claude pick? Most community-built skills also don't follow the summary/process/reference architecture — everything's crammed into one skill.md with no references, so when quality issues arise you can't tell if it's a process problem or a knowledge problem. Someone tested skill activation rates: as low as 20% with a basic setup and poor description, and only around 84% even with proper hooks and optimized descriptions on just four or five well-built skills — imagine 500 generic ones with vague descriptions fighting for attention. A small number of properly built skills with specific trigger descriptions will massively outperform a huge library of generic ones.

Third source: building your own — where the real magic happens, because no marketplace skill knows your business, domain expertise, brand voice, and process like you do. Rather than writing from scratch, you can use a skill to create a skill: Tash, creator of the popular GSD (Get Sh*t Done) framework, built an agent-skill-creator skill that follows the same conventions discussed today — a router plus step-by-step procedure, with references kept in separate linked files. Install with `npx skills add glittercowboy --skill create-agent-skill` (add `--local` if you just want to try it locally). Following this convention helps you debug, iterate, and troubleshoot: if the skill isn't following the process, that's a skill.md issue; if it needs more information, that's a reference-file issue. Start simple, put process in skill.md, use front matter as the summary fed to Claude, put expertise/brand voice in reference files, iterate every time you use the skill, and only add scripts when you need execution power.

Skills are organized expertise that plug into Claude Code, and they're being called a new business model because they're replacing chunks of what used to need separate SaaS tools. The real takeaway: stop loading thousands of generic skills, and build a curated set of really well-crafted ones — even if you install someone else's promising skill, reformat it and build on the reference context to make it relevant to your own business and brand.

</details>
