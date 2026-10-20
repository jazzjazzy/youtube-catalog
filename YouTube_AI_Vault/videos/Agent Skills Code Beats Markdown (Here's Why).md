---
title: "Agent Skills: Code Beats Markdown (Here's Why)"
video_id: IjiaCOt7bP8
channel: "[[channels/Sam Witteveen]]"
uploaded: 2026-03-27
processed: 2026-07-05
duration: "16:18"
url: https://www.youtube.com/watch?v=IjiaCOt7bP8
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [web-scraping, agent-skill-optimization]
tools: [Claude Code, Hacker News]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Agent Skills: Code Beats Markdown (Here's Why)

![thumbnail](https://i.ytimg.com/vi_webp/IjiaCOt7bP8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=IjiaCOt7bP8) | 📅 Uploaded [[uploaded/2026-03-27]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Agent Skills (originally Claude Skills, now an open standard adopted by OpenAI and DeepMind) work because of progressive disclosure — a small metadata footprint until a skill is actually invoked. This video argues the real leverage is in the `scripts/` folder: using code and a sandbox to do the heavy lifting instead of markdown instructions, illustrated through a deep dive on scraping-skill mistakes (raw HTML dumps, re-deriving page structure every run, unbounded pagination) and fixes (HTML stripping, cached CSS selectors, JSON schemas, batching, incremental runs).

**Watch this if:** you're building Claude/Agent Skills that call scripts and want to stop burning tokens on avoidable mistakes.

## Key Takeaways
- Agent Skills started as Claude Skills but quickly became an open standard adopted beyond Anthropic (OpenAI, and DeepMind's Antigravity/Gemini CLI harnesses), with directories like skills.sh and marketplaces like skillsmp.com emerging around it — argued to be an easier-to-use standard than MCP.
- Skills work via progressive disclosure: a lightweight `skill.md` (metadata plus core instructions) tells the model what's available for very few tokens, and only once a model decides to use a specific skill does its fuller content load into context.
- A skill's structure typically includes `skill.md` (required), a references/templates/examples folder, an optional assets folder for images, and — the focus of this video — a `scripts` folder holding actual code the model can run as-is or rewrite, executed in a sandbox to generate or retrieve context.
- Mistake #1 (often the most expensive): using the web-fetch tool to pull an entire page's raw HTML — a Hacker News front page alone was ~34,000 characters (~8,000+ tokens); stripping script/style/nav/footer tags cut that to under 1,000 tokens, a roughly 90% reduction that compounds fast across 50-100 scraped pages.
- Mistake #2: having the model re-derive page structure (CSS selectors, classes) on every single run — instead, ask Claude once to extract the relevant selectors (e.g. article title, points, comment count for Hacker News) and hardcode those into the script so subsequent runs skip that discovery step entirely.
- `skill.md` should act as the orchestrator (deciding what to scrape and what to do with results) while the actual scraping script does the parsing and returns clean, structured output — usually JSON or markdown — rather than raw text the model has to parse itself.
- Define a strict output schema directly in the script where possible (e.g. title/URL/price/discount fields for price-comparison scraping); if the script can't enforce it, specify the schema in `skill.md` so extraction stays consistent.
- Push as much decision-making as possible into code rather than model logic — this saves tokens, lets you delegate the task to a cheaper sub-agent model, and makes parallelization (e.g. batched multi-threaded searches instead of 15 sequential round trips) much easier.
- Build in explicit limits and stop conditions (e.g. max web-fetch/search calls, max pagination depth) in the orchestrator — without them, pagination-heavy scraping can silently balloon to tens of thousands of tokens per page and flood the context window.
- Design for incremental runs: have the skill check for a previously saved report/file and only scrape what's newer, rather than starting from scratch every time; hardcoding known values (proxies, category names, usernames) into the script further reduces per-run overhead.

## 🛠 Tools & Software
- [[topics/Claude Code]] — its built-in web-fetch tool is the specific example used to illustrate the raw-HTML token-waste mistake, and Claude is used throughout to design and refine the scraping scripts
- [[topics/Hacker News]] — used as the running example scraping target throughout the video, from raw-HTML token counts to extracting article title/points/comments via cached CSS selectors

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model Agent Skills originated with, used throughout the video's examples to design scraping scripts and extract page-structure metadata

## 📡 Protocols & Standards
- [[topics/MCP]] — directly contrasted with Agent Skills, argued to be a less easy-to-use standard for giving models new capabilities

## ✅ Action Items
- Audit any scraping skill for whether it's returning raw HTML — strip script/style/nav/footer tags to cut token usage by up to ~90%.
- Ask Claude once to extract the CSS selectors/classes you need from a target page, then hardcode them into the script instead of re-deriving structure every run.
- Make `skill.md` the orchestrator and push actual parsing/extraction logic into a script that returns clean JSON or markdown.
- Define a strict output schema (in the script if possible, in `skill.md` otherwise) for anything you plan to compare across sources.
- Add explicit max-call/max-depth limits to prevent pagination from silently flooding the context window.
- Build incremental-run logic (checking for and diffing against previously saved output) instead of re-scraping everything from scratch each run.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, MCP
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, MCP

## Timeline
- `0:00` — Intro: Agent Skills as an open standard beyond Claude
- `0:18` — Claude Skills / Agent Skills background and adoption
- `1:02` — skills.sh and the skills marketplace ecosystem
- `1:38` — Why skills work: progressive disclosure and context engineering
- `2:48` — Skills structure: skill.md, references, assets, scripts
- `4:56` — Scraping skills as the example for the rest of the video
- `6:51` — Mistake: using the web-fetch tool to return entire raw HTML pages
- `9:58` — SKILL.md as the orchestrator, script as the executor
- `13:42` — Designing for incremental runs and hardcoded values

## Transcript
<details>
<summary>Full transcript</summary>

Claude Skills, now more broadly Agent Skills, have become the key tool for helping models and agent harnesses get things done efficiently. What started as Claude-only quickly became an open standard — arguably easier to use and understand than MCP — with OpenAI adopting it for their models and, more recently, people at DeepMind adopting it for coding harnesses like Antigravity and Gemini CLI. Directories like skills.sh (searchable) and marketplaces like skillsmp.com have sprung up around this proliferation of community-authored abilities. This video focuses specifically on scripts — using code and a coding sandbox inside a skill to get things done far more efficiently than markdown instructions alone. Skills work because they're built on context engineering (also called harness engineering, or jokingly "conditional probability engineering") — getting the right tokens to a model at the right time. Progressive disclosure means a model only needs a small amount of markdown telling it what skills/tools exist; the fuller

skill content only loads into context once the model decides to actually use it. A skill's core required piece is `skill.md` — metadata plus core instructions. Beyond that, skills commonly include a references folder (examples of expected output, calling conventions), an optional assets folder (images and similar), and — the focus here — a scripts folder holding actual code files. This all works because many models and agent harnesses now have sandbox access: an example script can be run as-is or rewritten, executed in a sandbox,

and used to generate or retrieve context passed back to the model, or produce a direct output for the user. Skills are structured instruction sets for approaching a task, and code execution lets them use bash, CLIs, Python scripts, and API calls. A common mistake across skill builders is never optimizing the code scripts for the specific task — the instructions are specific but the code stays generic and token-wasteful. Scraping skills are a good illustration: people often reach for the most generic scraping script, which sometimes works and sometimes silently fails without an obvious reason, especially since many sites actively try to block scraping agents. [Sponsored segment: DataImpulse residential proxies, offering ethically-sourced IPs across 195 countries starting at $1/GB, with tutorials for Scrapy/Playwright/Puppeteer and support for mobile IP spoofing.] Mistake number one, potentially the most expensive: having a skill use the web-fetch tool to pull back an entire page of raw HTML.

The web-fetch tool built into Claude Code is genuinely useful when it needs to quickly grab docs or context from elsewhere, but at scale (e.g. scraping 50+ pages) returning every piece of HTML is wasteful — a single Hacker News front

page alone comes back at roughly 34,000 characters, about 8,000+ tokens. Simply excluding script, style, nav, and footer tags in the scraper cuts that to under 1,000 tokens — nearly a 90% reduction. That's negligible for one page, but scraping 100 pages daily for news updates means burning nine times the tokens for the same result unless this is fixed. The next common mistake: re-deriving page structure (which CSS classes/selectors to use) on every single run when you already know what you're scraping. If you don't know the structure yet, ask Claude to identify it once — for example, extracting

the CSS selectors for Hacker News article titles, URLs, points, and comment counts — then hardcode those selectors into the script going forward, rather than burning ~8,000 tokens rediscovering structure on every scheduled run. `skill.md` should function as the orchestrator, deciding what to scrape and what to do with results, while the actual

scraping script does the parsing and returns output in the easiest format for the model to use — usually JSON or markdown. For example, extracting title/URL/summary fields, converting to JSON, and returning that structured object rather than raw text. Beyond that, define a strict output schema — ideally directly in the script (e.g. title, product name, URL, current price, discount for price-comparison scraping across multiple sites) so results are comparable; if the script can't enforce this, specify the schema in `skill.md` instead. The

overarching goal is having scripts do as much heavy lifting as possible so the model isn't making decisions that could be pre-made in code — this saves tokens, allows delegating the task to a cheaper sub-agent model, and makes parallelization easier (e.g. batching multiple searches via threads instead of waiting through 15 sequential round trips, each adding to the conversation's context). Next, build in explicit limits and stop conditions — for tasks involving pagination or "load more" buttons, define a max number of web-search/web-fetch calls directly in the orchestrator logic in `skill.md`. Without this, a

technically-working scraping skill can go 5-10 pages deep, picking up 30,000-40,000 tokens per page and quickly flooding the context window, versus a properly-limited version doing only ~2,000 tokens per page across a capped 3 pages (with logic to go deeper only if the target information isn't found). This leads to designing for incremental runs: rather than scraping from scratch every time, the skill should check where it left off (e.g. against a previously saved report or database) and only

fetch what's newer — achievable in `skill.md` with an "incremental mode" that checks for an existing previous report, finds the most recent matching file, and returns only newly-scraped items versus what's already saved. Scripts also let you hardcode known values — proxies, category names, usernames — to prefill and skip unnecessary steps. The common thread across all these patterns is being intentional about tokens: what enters the context window, what leaves it, and what should never touch it at all. While Claude Code and modern models are already quite capable at raw web-fetch and extraction, a skill meant to run daily for a specific business use case deserves more deliberate design. As skills become central to how agents are built, there's a risk of throwing out years of established efficiency best practices even as capability grows — and given current token costs, those practices are worth holding onto.

</details>
