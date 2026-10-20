---
title: "CloakBrowser made Claude agents undetectable (15k stars on GitHub)"
video_id: kVcOA5txllM
channel: "[[channels/Bitwise AI]]"
uploaded: 2026-05-19
processed: 2026-07-05
duration: "4:24"
url: https://www.youtube.com/watch?v=kVcOA5txllM
playlist: "[[Agents skills n8n]]"
type: review
difficulty: advanced
use_case: [browser-automation-detection-evasion, web-scraping-anti-bot]
tools: [CloakBrowser, Playwright, Chromium, Cloudflare, DataDome, Turnstile, PerimeterX, playwright-stealth, Patchright, rebrowser-patches, browser-use, Skyvern, LangChain]
llms: [Claude]
protocols: [CDP]
transcript: true
tags: [youtube, ai-automation]
---

# CloakBrowser made Claude agents undetectable (15k stars on GitHub)

![thumbnail](https://i.ytimg.com/vi/kVcOA5txllM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=kVcOA5txllM) | 📅 Uploaded [[uploaded/2026-05-19]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> CloakBrowser is a 14k-star, MIT-licensed drop-in Playwright replacement that bakes 57 C++ patches directly into a Chromium 146 binary so Claude computer-use, browser-use, Skyvern, and LangChain agents stop registering as bots to Cloudflare, DataDome, Turnstile, and PerimeterX. The video walks the three patches that matter (the `navigator.webdriver` getter, the CDP `Runtime.Enable` leak, and the `--enable-automation` compile-time flag) and explains why the monthly Chromium rebuild — not the patches themselves — is the real product.

**Watch this if:** your AI browser agent (Claude computer-use, browser-use, Skyvern, etc.) keeps getting blocked by Cloudflare/DataDome/PerimeterX and you want to understand source-level fixes versus JS stealth plugins.

## Key Takeaways
- Every mainstream agent browser framework — browser-use, Skyvern, LangChain, and Claude's computer use — is just a wrapper around Playwright, so they all share the same detectable fingerprint.
- Patch #1: vanilla Chromium's `navigator.webdriver` property returns `true` under automation; CloakBrowser flips that one line to `false` deep in the C++ source, dropping 27 detectable "tells" to zero.
- Patch #2 (the big one): every Playwright session sends a CDP `Runtime.Enable` command that leaks internal execution-context IDs, including Playwright's hidden execution world — Cloudflare grabs that ID from a deliberate error trace to out the agent. CloakBrowser fixes the leak in the engine itself rather than dodging the command.
- Patch #3: Chromium's `--enable-automation` switch lights up four tells at once (the "controlled by automation" bar, the webdriver property, a killed password prompt, and a tagged extension); CloakBrowser removes the defaults from the compiled binary instead of hiding the flag at launch.
- Against public detection tests, vanilla Playwright scores a Cloudflare trust score of zero, while CloakBrowser scores 30/30 — the agent just clicks through.
- CloakBrowser isn't a stealth plugin: playwright-stealth patches JavaScript after page load and Patchright/rebrowser-patches patch the client, but CloakBrowser recompiles the browser itself so fingerprints are "born different" rather than patched at runtime.
- The real cost is a 40GB Chromium checkout and a 10-20 hour release build (even Google's tuned perf hardware takes ~6 hours) — CloakBrowser's actual value is doing that build monthly and tracking upstream.
- Recommendation: use a stealth plugin plus a residential proxy for low-tier sites; reach for CloakBrowser only against enterprise-grade walls like Cloudflare Enterprise, DataDome, or PerimeterX. Caveat: it ships as a precompiled binary you can't audit without building it yourself, and using it on a logged-in account makes any ToS breach your problem, not the browser's.

## 🛠 Tools & Software
- [[topics/CloakBrowser]] — the audited tool: a drop-in Playwright replacement shipping Chromium with 57 compiled-in anti-detection patches
- [[topics/Playwright]] — the automation API/library that CloakBrowser is a source-patched, API-compatible replacement for
- [[topics/Chromium]] — the browser engine being patched at the C++ source level (version 146 in this video)
- [[topics/Cloudflare]] — the bot-detection wall CloakBrowser is tested and scored against (trust score, Runtime.Enable exploitation)
- [[topics/DataDome]] — named as one of the enterprise-grade bot walls that justifies reaching for source-patched Chromium
- [[topics/Turnstile]] — named alongside Cloudflare and DataDome as a bot wall that kills unpatched agent browsers
- [[topics/PerimeterX]] — named as another enterprise bot wall CloakBrowser targets
- [[topics/playwright-stealth]] — contrasted as a runtime JavaScript-patching approach, insufficient against deeper detection
- [[topics/Patchright]] — contrasted as a client-side patching approach, called out as not touching the compiled binary
- [[topics/rebrowser-patches]] — contrasted alongside Patchright as a client-side JS patch approach
- [[topics/browser-use]] — named as an agent framework that wraps Playwright and inherits its detectable fingerprint
- [[topics/Skyvern]] — named as another Playwright-wrapping agent framework affected by the same detection problem
- [[topics/LangChain]] — named as another framework whose browser agents are just Playwright wrappers

## 🤖 LLMs Mentioned
- [[topics/Claude]] — Claude's computer-use feature is cited as one of the agent stacks that inherits Playwright's bot-detectable fingerprint

## 📡 Protocols & Standards
- [[topics/CDP]] — Chrome DevTools Protocol's `Runtime.Enable` command is the source of the "boss leak" (patch #2) that outs automated browsers

## ✅ Action Items
- If your agent only scrapes low-tier sites, stick with a JS stealth plugin (playwright-stealth) plus a residential proxy instead of a recompiled browser.
- Reach for CloakBrowser only when your agent must get past enterprise-grade walls like Cloudflare Enterprise, DataDome, or PerimeterX.
- Remember CloakBrowser ships as a precompiled binary — audit the 57 patches yourself by building from source if that matters to your threat model.
- Confirm your target site's terms of service before running a logged-in agent through any bot-evasion browser; the legal exposure is yours, not the tool's.

## 🔗 Related Videos
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: CDP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Playwright
- [[videos/Claude HeyGen Just Changed Content Creation Forever]] — shared: Claude, Playwright
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Playwright
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Playwright
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Playwright
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Playwright

## Timeline
- `0:00` — Intro: AI agents dying at the bot wall
- `0:21` — Enter CloakBrowser: 14k stars, MIT licensed, one pip install
- `0:48` — Chromium leaks every agent: browser-use, Skyvern, LangChain, Claude computer-use all wrap Playwright
- `1:16` — Patch #1: the `navigator.webdriver` tell
- `1:41` — Patch #2: the CDP `Runtime.Enable` leak ("the boss leak")
- `2:15` — Patch #3: the `--enable-automation` flag deleted from the binary
- `2:36` — What the wall sees: trust score 0 vs. 30/30
- `3:02` — Not a stealth plugin: recompiled vs. runtime-patched
- `3:19` — The build-cost reality: 40GB checkout, 10-20 hour build
- `3:41` — When to actually use it, plus the legal caveat

## Transcript
<details>
<summary>Full transcript</summary>

Your AI agent can click buttons, book flights, fill forms, until it hits the bot wall. Cloudflare, Turnstile, DataDome, it dies. Because Chromium was built for QA testing, not for agents. So, someone fixed it at the source. The first browser built for AI agents. It's called Cloak Browser. 14,000 stars on GitHub, MIT licensed, maintained by Cloak HQ. And the part that feels illegal, you don't change your code. One pip install, swap one import, same Playwright API your agent already uses, but the binary underneath isn't Chrome. It's Chromium 146 with 57 C++ patches compiled into the source. Not injected by JavaScript, not patched at launch. Baked. Here's the problem. Every agent framework, browser use, Skyvern, LangChain, even Claude's computer use, is just a wrapper around Playwright, which means they all carry the same fingerprint. The browser quietly tells the website, "I'm being automated." in dozens of ways. Your $200 a month frontier model is driving a browser that snitches on it in the first 10 milliseconds. And JavaScript stealth tricks? Detection scripts see right through them.

Patch number one. Vanilla Chromium has a property called navigator.webdriver. Under any automation tool, it returns true. Instant tell. Cloak browser changes that one line to return false deep in the C++ source. Now, when detection scripts inspect the browser, they see a real unmodified property. 27 tells drop to zero. Patch number two. The big one. Every Playwright session sends a command called runtime enable to start the browser. Chromium answers by streaming back the internal IDs of every execution context, including the hidden world Playwright runs from. Cloudflare grabs that ID from a deliberate error trace and your agent is outed. Other stealth tools dodge the command. Cloak browser fixes the leak deeper in the engine, so it never happens at all. The hidden world still works. Detectors just can't see it. Patch number three, Chromium ships with a switch called enable automation. One flag lights up four tells, the yellow controlled by automation bar, the webdriver property, killed password prompt, a tagged extension. Stealth libraries hide the flag at launch. Cloak browser just removes the defaults from the binary.

So, what does a real website actually see? Vanilla Playwright? Automation flag true, Selenium globals leaked, GPU driver says Swift shader, network fingerprint screams headless. Cloudflare gives it a trust score of zero. The agent never reads the page. Cloak browser through the same wall? 30 out of 30 on every public detection test. The agent just clicks the button. This isn't a stealth plugin. It's not a disguise. Playwright stealth changes JavaScript after the page loads. Rebrowser and Patchright patch the client. Cloak browser recompiles the browser itself. Fingerprints aren't patched at runtime. They're born different. Cool, I'll just patch Chromium myself. Sure. A Chromium checkout is 40 GB. A clean release build 10 to 20 hours on a normal laptop. Even Google's perf engineers log six on tuned hardware. Cloak browser does the build, tracks upstream, and ships a fresh binary every month. That cadence is the product.

Real talk. If your agent only hits low-tier websites, a stealth plugin plus a residential proxy still works. Don't pull a recompiled browser for that. Reach for source level patches when your agent has to hit Cloudflare Enterprise, Data Dome, PerimeterX, the walls real customers sit behind. One caveat, it's a precompiled binary, so you can't audit 57 patches without doing the build yourself. And if your agent acts on a logged in account, the terms of service breach is on you, not the browser. The agent stack just got a real browser. Next question. Can it survive behavioral detection? Subscribe, we're testing that next.

</details>
