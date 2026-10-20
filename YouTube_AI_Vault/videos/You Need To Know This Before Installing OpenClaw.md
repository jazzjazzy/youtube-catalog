---
title: "You Need To Know This Before Installing OpenClaw"
video_id: M3P0hQMQtq0
channel: "[[channels/AI LABS]]"
uploaded: 2026-02-04
processed: 2026-07-06
duration: "7:32"
url: https://www.youtube.com/watch?v=M3P0hQMQtq0
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [self-hosted-ai-agent-security]
tools: [Open Claw, WhatsApp, Discord, Docker, Ollama, ClawHub, OpenRouter, OpenAI]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# You Need To Know This Before Installing OpenClaw

![thumbnail](https://i.ytimg.com/vi_webp/M3P0hQMQtq0/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=M3P0hQMQtq0) | 📅 Uploaded [[uploaded/2026-02-04]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A hands-on security and cost audit of Open Claw (formerly Clawdbot/MoltBot), the fastest-growing open-source AI agent project. The team hit unstable WhatsApp integration (needing Discord instead), found a simple hourly email-check job could cost ~$128/month due to full-conversation-history being resent on every query, and documents Cisco's finding that a community ClawHub skill was "functionally malware" — plus Open Claw's own policy that treats prompt injection as out of scope.

**Watch this if:** you're about to self-host Open Claw and want to know the real token costs and security holes before you connect it to sensitive accounts or channels.

## Key Takeaways
- Open Claw was rebranded twice in 3 days (Clawdbot → MoltBot → OpenClaw) due to a naming conflict with Anthropic's Claude, and became the fastest-growing open-source AI project in history — but "open-source" doesn't mean free, and "self-hosted" doesn't mean secure.
- WhatsApp channel integration repeatedly disconnected with 408 errors during testing; Discord was more stable and easier to set up.
- Because Open Claw resends the full conversation history plus built-in memory/reasoning/skill context on every query, a simple daily email-summary cron job alone was estimated at ~$128/month — and switching to smaller models didn't meaningfully cut costs, since the issue is architectural (how much context is sent), not model choice.
- Response times degraded as context built up in one continuous session — from ~2-12 seconds on a fresh session up to 119 seconds once context had accumulated significantly (analyzed by having Claude review the logs).
- Community suggestions to control cost: increase the heartbeat interval beyond 2 hours, clear the session before sleep, and set up API budget alerts on providers like OpenAI or Google Cloud.
- Running models locally via Ollama avoids per-token costs but requires hardware capable of running LLMs, so cost/effort tradeoffs remain either way.
- Credentials and session data are stored in plain, human-readable JSON files, and Open Claw can execute shell commands, access disk files, and run scripts — meaning any compromise or bad skill has real system-level consequences.
- Cisco's open-source skill scanner found 9 security issues (2 critical, 5 high severity) in a single community ClawHub skill, including one that was functionally malware — silently curling data to an external server controlled by the skill's author.
- Open Claw's security policy explicitly treats prompt injection attacks as out of scope; models with their own built-in guardrails (OpenAI, Anthropic) were more resistant to credential-leaking prompt injection attempts in testing, though not immune.
- Recommended mitigations: only install verified/scanner-passed skills, avoid connecting sensitive accounts, use a separate low-privilege account, and sandbox the whole setup with Docker or a dedicated VM; revoke tokens for channels no longer in use.

## 🛠 Tools & Software
- [[topics/Open Claw]] — the self-hosted AI agent framework under review, tested end-to-end for setup difficulty, cost, and security.
- [[topics/WhatsApp]] — the channel integration that repeatedly failed with 408 disconnect errors during testing.
- [[topics/Discord]] — used instead of WhatsApp after it proved more stable and easier to set up.
- [[topics/Docker]] — recommended for sandboxing an Open Claw installation so it can't reach other system resources.
- [[topics/Ollama]] — suggested as a way to run models locally and avoid per-token API costs, at the expense of needing capable hardware.
- [[topics/ClawHub]] — the community skill marketplace where a scanned skill was found to be functionally malware.
- [[topics/OpenRouter]] — mentioned as one of the model-routing options Open Claw supports.
- [[topics/OpenAI]] — the API provider used in the team's own cost-testing setup, and cited as having built-in guardrails against some prompt injection attempts.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — used by the team to analyze Open Claw's response-time logs, revealing the pattern of degrading performance as context accumulated.

## ✅ Action Items
- Before installing, budget for token costs, not just setup time — test with a single cron job first to estimate a realistic monthly cost.
- Set API usage alerts/budgets with your model provider (OpenAI, Google Cloud, etc.) so costs can't spiral unnoticed.
- Increase the heartbeat interval beyond the default and clear sessions periodically to reduce resent-context token costs.
- Run Open Claw inside Docker or a dedicated VM, using a low-privilege account with no sensitive data or credentials.
- Only install ClawHub skills that are verified or have passed a security scan (Cisco's scanner is open source), and revoke channel tokens you're no longer using.

## 🔗 Related Videos
- [[videos/Someone open-sourced a hedge fund — I ran it locally on Qwen3 with Ollama]] — shared: Claude, Docker, Ollama, OpenRouter
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: Claude, Discord, Open Claw, WhatsApp
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, ClawHub, Open Claw
- [[videos/Hermes Agent Full Setup Tutorial How to Setup Your First AI Agent (Gemma 4)]] — shared: Docker, Ollama, Open Claw
- [[videos/How OpenClaw Works (and why you should build your own)]] — shared: Claude, Discord, Open Claw
- [[videos/Suna The FREE Open Source Alternative to Manus AI]] — shared: Claude, Docker, OpenAI
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Discord, OpenRouter
- [[videos/Agent memory resolved]] — shared: Claude, Open Claw

## Timeline
- `0:00` — Framing question: is Open Claw the closest thing to AGI, or a security nightmare? Cisco's "security nightmare" characterization and flawed security policy noted.
- `0:40` — Background: rebranded from Clawdbot to MoltBot to OpenClaw in 3 days due to naming conflict with Claude.
- `1:10` — Setup experience: installation worked, but WhatsApp integration kept disconnecting (408 errors); Discord used instead.
- `2:00` — Mention of the team's own step-by-step install guide/community resource.
- `2:30` — Cost breakdown: open-source isn't free — you pay in tokens; a daily cron job alone estimated at ~$128/month.
- `3:20` — Explaining why smaller models don't reduce cost much: it's about how much context/conversation history is resent per query.
- `4:00` — Demo: an hourly email-check automation burning through OpenAI API credits quickly; heartbeat and session-length cost factors.
- `4:40` — Response-time degradation analysis (2-12s to 119s) using Claude to review logs; recommendation to monitor/budget API costs.
- `5:10` — Local inference via Ollama as a cost-avoidance option, with hardware caveats.
- `5:30` — Security concerns: plain-text JSON credential/session storage; shell command and file-system access risks.
- `6:00` — Cisco's skill scanner findings: 9 issues (2 critical, 5 high) in one ClawHub skill, including a functionally-malware skill exfiltrating data via curl.
- `6:40` — Prompt injection: explicitly out of scope in Open Claw's security policy; guardrail-equipped models (OpenAI, Anthropic) resisted some attempts but aren't immune.
- `7:00` — Final mitigations: minimal necessary skills, separate low-privilege accounts, Docker/VM sandboxing, and revoking unused channel tokens.

## Transcript
<details>
<summary>Full transcript</summary>

Framed as a question — is Open Claw the closest thing to AGI, or a security nightmare — the video opens with Cisco calling it a security nightmare and noting flaws in the project's own security policy, with people exploiting its architecture to access sensitive credentials through exposed endpoints. Open Claw is a self-hosted AI assistant that became the fastest-growing open-source project in history, but open-source doesn't mean free and self-hosted doesn't mean secure. Originally "Clawdbot," it was rebranded to "MoltBot" due to a naming conflict with Anthropic's Claude, then finally "OpenClaw" — the fastest rebranding the team had seen, spanning just 3 days.

Testing the setup (following the official documentation step by step), installation itself worked, but channel integrations were troublesome: WhatsApp kept disconnecting due to 408 errors, preventing messages from being sent. Discord, by contrast, had a stable connection and an easier setup, so it was used instead. The team created their own complete setup guide (available via their AI Labs Pro community) to help others avoid the issues encountered.

On cost: Open Claw is open source, so setup itself is free, but you pay in tokens, not subscriptions. It supports many popular models and OpenRouter, but its architecture means costs can spiral — it operates with built-in memory, reasoning, and skill/channel integrations rather than plain system prompts, so even a simple daily cron job was estimated at around $128/month, because each query sends a lot of accumulated information — and that's just one job among the many typical Open Claw use cases. Switching to smaller models didn't meaningfully lower costs for many users, indicating the problem is architectural (how much gets sent per query), not the model itself. Setting up an hourly email-check-and-summarize automation using an OpenAI key burned through API credits quickly because the full conversation is resent with each query for context continuity. A periodic "heartbeat" to check server status and run scheduled tasks compounds this; community suggestions include increasing the heartbeat interval beyond 2 hours and clearing sessions before idle periods. Growing conversation length also slowed response times — analysis using Claude to review the logs showed response times climbing from about 2-12 seconds on a fresh session up to 119 seconds as context built up, with tool calls adding further overhead. Recommendation: monitor API costs, set alerts, and budget carefully with providers like OpenAI or Google Cloud. Running models locally via Ollama avoids these costs but requires hardware capable of running LLMs, so cost is still a factor either way, just shifted to hardware.

On security: personal AI agents like Open Claw are described as a security nightmare because credentials and session data (including device and identity details) are stored in plain, human-readable JSON files accessible to anyone with system access. Even running locally isn't automatically safe, since Open Claw can run shell commands, access disk files, and execute scripts — risky capabilities if misused. Cisco tested this and found real problems: scanning community ClawHub skills with their now open-source skill scanner uncovered 9 security findings (2 critical, 5 high severity) in just one skill, which was found to be functionally malware — explicitly instructing the bot to run a curl command sending data to an external server controlled by the skill's author. Saving passwords in plain text compounds the risk of any single bad instruction.

Beyond skills, prompt injection is a separate concern: Open Claw's security policy explicitly states injection attacks are out of scope, meaning the project isn't responsible for resulting information leaks. The recommendation is to favor models with built-in guardrails (OpenAI, Anthropic), which proved more resistant to obvious credential-leaking prompt injection attempts in testing (their own OpenAI-based setup refused to give up credentials even when told the requester was a "server owner") — though such guardrails can still potentially be bypassed with cleverer injections. For skills, only add what's strictly necessary, avoid anything touching passwords or sensitive systems unless required, and either use the (now open-source) Cisco scanner on community skills or stick to verified ones.

Final practical advice: since Open Claw can access nearly all of a system, use it with a separate account containing no sensitive data, and even then, ensure any access it has can't cause serious harm — sandboxing with Docker (isolated containers) or a dedicated VM is the best approach, and unused channel integrations (e.g. an old Discord token) should have their access revoked.

</details>
