---
title: "How to Build 24/7 Claude Agents. Easy."
video_id: ehg4fhydTgs
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-04-14
processed: 2026-07-05
duration: "16:27"
url: https://www.youtube.com/watch?v=ehg4fhydTgs
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [cloud-agent-scheduling, claude-code-automation-migration]
tools: [Claude Code, GitHub, ClickUp, YouTube Data API, Playwright]
llms: [Claude]
protocols: [MCP, webhooks, OAuth]
transcript: true
tags: [youtube, ai-automation]
---

# How to Build 24/7 Claude Agents. Easy.

![thumbnail](https://i.ytimg.com/vi/ehg4fhydTgs/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=ehg4fhydTgs) | 📅 Uploaded [[uploaded/2026-04-14]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Claude Code's new "routines" feature runs prompts on a schedule, API call, or GitHub event entirely on Anthropic's cloud infrastructure — no laptop required. The video walks through setup, the environment-variable and stateless-repo gotchas that break naive migrations (ClickUp worked, a cookie-dependent Playwright automation didn't), security/access levels, quotas, and how routines compare to local scheduled tasks and `/loop`.

**Watch this if:** you have Claude Code automations tied to your local machine and want them running in the cloud on a schedule instead.

## Key Takeaways
- Routines are a one-shot, autonomous prompt configured once that can trigger on a schedule (min. 1 hour interval), an API call, or a GitHub event (new PR/push/issue/release), running on Anthropic's web infrastructure with no local machine required.
- Each run clones your linked GitHub repo (reading your CLAUDE.md, scripts, and skills), executes the prompt, and then destroys the cloud clone — so `.env` secrets never make it in (they're gitignored) and must instead be added as environment variables inside the routine's Cloud Environment settings.
- Network access has three levels — trusted (Anthropic-vetted domains only), full (any domain, needed to get a ClickUp message to actually send in this demo), and custom (allow specific domains) — with full carrying real prompt-injection/exfiltration risk if the run reads untrusted content.
- Because routines are stateless and only see what's in the GitHub repo/APIs, browser-automation flows that depend on local cookies (e.g., a Playwright-driven community engagement bot) don't work remotely unless re-architected around an authenticated API/endpoint.
- Prompts need to be more explicit than local ones — e.g., telling the agent to read an API key "directly from the environment variable, don't look for a .env" was required to get a YouTube comment-analysis routine working after a failed first attempt.
- Quotas: 5 routine runs/day on Pro, 15/day on Max, 25/day on Team/Enterprise (metered overage available for orgs); each run gets 4 vCPUs, 16GB RAM, and 30GB disk.
- Routines vs. desktop scheduled tasks vs. `/loop`: only routines need no machine on and survive restarts with full autonomy (no permission prompts); scheduled tasks and `/loop` need the machine on but allow sub-hour intervals and local file access, and `/loop` doesn't survive restarts at all.
- Routines preserve the full agentic "workflow-agent-tools" loop (reading CLAUDE.md, self-correcting mid-run) rather than degrading to a plain script — unlike pushing a workflow to the cloud as a bare Python job.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent whose new "routines" feature (cloud-hosted scheduled/triggered prompts) is the entire subject of this video
- [[topics/GitHub]] — routines require a linked repo that gets cloned per run and read for CLAUDE.md/scripts/skills; GitHub events (PRs, pushes, issues, releases) can also trigger routines
- [[topics/ClickUp]] — used as the first test routine (sending a message), requiring the Cloud Environment's network access to be set to "full" before it would work
- [[topics/YouTube Data API]] — used in a second test routine to fetch and analyze 50 recent YouTube comments, requiring an explicit prompt fix to read the API key from environment variables instead of a `.env` file
- [[topics/Playwright]] — used in an existing local automation (community engagement posting) that failed to migrate to a remote routine because it depends on locally-stored browser cookies unavailable in the stateless cloud run

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying Claude Code and its new routines feature throughout the video

## 📡 Protocols & Standards
- [[topics/MCP]] — referenced when explaining that routine "connectors" are how a routine can use your MCP services
- [[topics/webhooks]] — GitHub-triggered routines fire off similarly to a webhook in response to new PRs, pushes, issues, or releases
- [[topics/OAuth]] — connectors (Slack, ClickUp, etc.) are added via OAuth, the same way you'd connect them to Claude chat or Claude Cowork

## ✅ Action Items
- When migrating a local Claude Code automation to a routine, explicitly instruct it to read secrets from environment variables rather than a `.env` file, since the cloned repo never includes gitignored files.
- Set network access to "full" only when a connector genuinely needs it (as with ClickUp here); default to "trusted" and use "custom" for specific extra domains to limit exfiltration risk.
- Don't try to migrate cookie-dependent browser automations to routines as-is — replace them with an authenticated API/endpoint call, since each run is stateless and destroys its cloned environment afterward.
- Keep routine-linked repos scoped and lean (or use a dedicated repo per routine) rather than pointing a routine at a massive project repo, to avoid burning context/session limits on irrelevant CLAUDE.md content.
- Always test a routine with "run now" multiple times, watching and correcting it live, before letting it run unattended on a schedule.

## 🔗 Related Videos
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, GitHub, OAuth, webhooks

## Timeline
- `0:00` — What Are Routines?
- `1:04` — Setting Up a New Routine
- `2:15` — API "Gotchas"
- `6:10` — What Won't Work Remotely
- `8:29` — Environments, Security & Limits
- `10:02` — Routines vs Scheduled Tasks
- `14:52` — Common Questions
- `16:04` — Final Thoughts

## Transcript
<details>
<summary>Full transcript</summary>

Claude Code has launched routines — you configure a prompt once, and it can run on a schedule, from an API call, or in response to an event, running on Anthropic's web infrastructure, so your laptop doesn't need to stay open. You can create routines as a scheduled trigger in the terminal, at claude.ai/code on the web, or in the desktop app. Scheduled tasks can be local or remote (linked to a GitHub repository); setting one up involves naming it, writing the prompt, choosing the model, repository, and cloud environment, setting the cadence (hourly, daily, weekdays — minimum interval is 1 hour), configuring connectors (Slack, Gmail, or plain API keys), and setting permissions. Routines are meant to be one-shot prompts run with nobody around, so they need to be specific enough to never require clarifying questions.

First test: a routine that sends a message to ClickUp, without adding a ClickUp connector. It requires a linked GitHub repository — the routine clones the repo (reading CLAUDE.md, scripts, skills) and destroys the clone after finishing. Since `.env` files are gitignored (correctly — you shouldn't push secrets to GitHub), the cloned repo has no API keys. Instead, API keys go into the routine's Cloud Environment settings (name, network access, environment variables) — e.g., adding a YouTube API key and ClickUp API key there. Access levels matter too: by default it's "trusted" (only Anthropic-vetted/verified sources), but ClickUp required switching to "full" access before the test message would actually send successfully.

Second test: a routine using the YouTube Data API to grab and analyze 50 recent comments. The first attempt failed because the agent tried to find a `.env` file (which doesn't exist in the cloned repo) instead of reading the API key from the environment variable — updating the prompt to explicitly say "use it directly from the environment, don't look for a .env" fixed it immediately.

Third example: an existing local automation using Playwright CLI to post community engagement content in a school platform without a public API. Migrating this to a remote routine failed because the browser spins up with no cookies — the routine only has access to the GitHub repo, not local session cookies — so every run is stateless and the cloned environment is destroyed afterward (except when the routine modifies the codebase, in which case it creates a new branch instead of just deleting everything). Cookie/session-dependent automations like this would need to be rebuilt around an authenticated API, header, or cookie-based endpoint to work remotely.

Usage limits exist too: on the $200/month Max plan, up to 15 routine runs per day; Pro is lower (around 3-5), Team/Enterprise around 25/day, with metered overage available for some orgs. Each routine run gets 4 vCPUs, 16GB RAM, and 30GB disk.

Because routines work off a cloned repo, they automatically read CLAUDE.md every run — for a large project with lots of context that may not be relevant to a specific automation, it may be better to use a dedicated, smaller GitHub repo per routine, since all that context still consumes Claude Code session limits just like a normal chat session. Three trigger types recap: scheduled, API call (another automation can POST to trigger a routine), and GitHub events (new PRs, pushes, issues, releases — functioning like a webhook).

Comparing routines to desktop scheduled tasks and the `/loop` command: routines run on Anthropic's cloud (no machine needed), while the other two need your machine on. All three don't require a kept-open session. Routines and desktop scheduled tasks survive restarts; `/loop` does not (it must live within a specific session). Routines have no local file access (repo/API only); the other two do. Routines run fully autonomously with no permission prompts; the other two have configurable permissions. Minimum interval for routines is 1 hour; the other two can run as often as every minute.

On environments: `.env` is gitignored unless deliberately pushed (risky, especially with collaborators) — instead put API keys in the Cloud Environment's environment variables. Network access options are trusted, full, none, or custom (specific allowed domains), plus optional setup scripts that run before Claude Code launches (e.g., to install packages). Trusted only reaches known, Anthropic-vetted services (Anthropic itself, version control providers, some cloud platforms); full risks Claude being tricked by malicious content it reads into exfiltrating data externally — practically low-risk for private repos you control, but worth acknowledging. Connectors are OAuth-based (Slack, ClickUp, etc.), same as connecting them to Claude chat or Cowork.

Security-wise: think about what could happen if a routine runs unattended without careful permission scoping, especially around API triggers and GitHub branch/PR handling, since everything runs as you. Persisted vs. destroyed: Claude's branches get pushed to your GitHub repo and the run history/session stays visible for review, but the actual cloned cloud environment itself is destroyed after each run. Rule of thumb: if something is purely local and Claude Code can't reach it via the GitHub repo or an API, it won't work in a routine.

Why this beats plain automation: it keeps the full agentic "workflow, agent, tools" loop intact — the agent reads CLAUDE.md, looks at its scripts, decides what to do, and self-corrects on errors mid-run — rather than degrading into a bare Python script that only executes tools/workflow without agentic reasoning.

Speed-run FAQ: No cron syntax needed (natural-language scheduling). No local file access — only the GitHub repo or APIs. Any available model can be chosen. You can watch a run live via "run now," and even talk to or interrupt it mid-run. MCP services work through connectors. Routines are tied to your individual account, not shared with teammates (untested on team plans). Cost is just normal subscription usage. Failed runs are stored in history for review (and you can have a routine notify you on failure). You should test a routine multiple times with "run now," watching and correcting it, before trusting it to run unattended.

</details>
