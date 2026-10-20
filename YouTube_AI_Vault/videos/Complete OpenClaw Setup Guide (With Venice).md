---
title: "Complete OpenClaw Setup Guide (With Venice)"
video_id: 5z9e5vLhUeY
channel: "[[channels/Venice]]"
uploaded: 2026-02-04
processed: 2026-07-06
duration: "9:19"
url: https://www.youtube.com/watch?v=5z9e5vLhUeY
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [private-autonomous-agents]
tools: [Open Claw, Venice AI, Telegram, Tailscale, Matrix, Raspberry Pi, GitHub]
llms: [Claude Opus, GLM]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Complete OpenClaw Setup Guide (With Venice)

![thumbnail](https://i.ytimg.com/vi_webp/5z9e5vLhUeY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=5z9e5vLhUeY) | 📅 Uploaded [[uploaded/2026-02-04]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A step-by-step setup guide for Open Claw (formerly Clawdbot/MoltBot), a viral persistent autonomous AI agent framework, paired with Venice AI as a privacy-preserving model provider. Covers the security/cost risks of running such agents unsupervised, one-line installation on macOS, configuring Venice as the model auth provider, wiring up a Telegram bot via BotFather, pairing the bot, switching models on the fly (including Claude Opus 4.5 via Venice), and a live demo scraping X and scheduling hourly automated tasks.

**Watch this if:** you want to set up Open Claw safely with a privacy-focused model provider and understand the real risks (cost overruns, prompt injection) before giving an autonomous agent access to your accounts.

## Key Takeaways
- Open Claw is a persistent AI agent framework with 50+ integrations that acts on its own without being re-prompted, reachable via messaging apps like WhatsApp or Telegram; it gained over 150,000 GitHub stars in about a week.
- Real risks include prompt injection attacks, system prompt leaks, runaway costs (one example agent spent $20 overnight just repeatedly checking the time), and the fact that this is hobby open-source software, not enterprise-hardened.
- Venice AI offers private inference: fully private with open-source models, and anonymized even when routing to proprietary models like Claude Opus, so provider-side logging doesn't expose your data.
- Venice's DIEM token gives $1/day of API credit that renews every 24 hours after a one-time purchase, effectively letting you "own" recurring intelligence credits for your agent.
- Strong recommendation to run Open Claw on a dedicated machine (Mac Mini, Raspberry Pi, or spare computer), never your main machine with sensitive data, given the framework's inherent risk.
- Installation is a one-line command from the Open Claw GitHub/quickstart, followed by `openclaw doctor` (gateway token setup) and `openclaw onboard` (setup wizard: choose Venice as model auth provider, paste an API key, pick a default model like GLM 4.7 or Claude Opus 4.5).
- Telegram integration requires creating a bot via BotFather (`/newbot`), pasting the bot token into Open Claw's config, then pairing the bot using a code exchanged between Telegram and the terminal.
- Once running, the agent can be redirected via chat to do things like scrape X (requires pasting your browser's X auth cookie token), and can be scheduled to repeat tasks hourly (e.g. "send me the hottest new AI posts every hour").

## 🛠 Tools & Software
- [[topics/Open Claw]] — the persistent autonomous agent framework installed, configured, and demoed throughout (formerly Clawdbot/MoltBot).
- [[topics/Venice AI]] — the privacy-preserving model provider configured as Open Claw's model auth provider, offering anonymized inference and the DIEM token for recurring API credits.
- [[topics/Telegram]] — the messaging channel set up (via BotFather) to communicate with the Open Claw agent.
- [[topics/Tailscale]] — recommended (via a linked advanced privacy guide) for more advanced, ultra-private Open Claw setups.
- [[topics/Matrix]] — recommended alongside Tailscale in the advanced privacy guide as an alternative messaging channel for more private setups.
- [[topics/Raspberry Pi]] — suggested as a dedicated, isolated machine to run Open Claw on instead of your main computer.
- [[topics/GitHub]] — where Open Claw's repository and one-line quickstart install command are found.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — used as an example of a proprietary model that Venice anonymizes access to; later set as Open Claw's active model (Opus 4.5) via `openclaw model set venice/claude-opus-4.5`.
- [[topics/GLM]] — chosen as the default private open-source model (GLM 4.7) during onboarding.

## ✅ Action Items
- Set up Open Claw on a dedicated/isolated machine (Mac Mini, Raspberry Pi, spare computer) rather than your primary machine.
- Read the linked advanced privacy guide before going further, especially if considering Tailscale/Matrix for extra privacy.
- Run the one-line Open Claw install command, then `openclaw doctor` and `openclaw onboard`, selecting Venice AI as the model provider with your API key.
- Create a Telegram bot via BotFather, add its token to Open Claw, and complete the pairing-code exchange to connect it.
- Try switching the active model on the fly with `openclaw model set venice/<model>` and test task automation (e.g. hourly scheduled scraping/summarization tasks).

## 🔗 Related Videos
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: Claude Opus, GitHub, Open Claw, Telegram
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: GitHub, Open Claw, Raspberry Pi, Telegram
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: GitHub, Open Claw, Telegram
- [[videos/Hermes Agent Full Setup Tutorial How to Setup Your First AI Agent (Gemma 4)]] — shared: GitHub, Open Claw, Telegram
- [[videos/Self-Host Openclaw (Clawdbot) in a Proxmox VM (The Secure Way)]] — shared: Claude Opus, Open Claw, Telegram
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Opus, GLM, Telegram
- [[videos/This is the CHEAPEST and EASIEST way to set up ClawdBot]] — shared: Claude Opus, Open Claw, Telegram
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Opus, GitHub

## Timeline
- `0:00` — Open Claw's viral rise: 150,000+ GitHub stars in about a week, persistent agent framework with 50+ integrations.
- `0:28` — Examples: an agent set up phone-calling infrastructure; another agent raised $10,000 overnight from a crypto wallet.
- `0:53` — Why to be both worried and excited: the models aren't new, only the agency framework is.
- `1:07` — Hidden costs: an agent that spent $20 overnight just checking the time; prompt injection and system-prompt-leak risks.
- `1:27` — Introducing Venice as the privacy solution: private open-source inference, anonymized proprietary model access.
- `2:11` — The DIEM token: $1/day in renewing API credit, bought once.
- `2:45` — Critical security warning: use a dedicated machine, not your main computer.
- `3:09` — Pointer to an advanced privacy guide covering Tailscale and Matrix setups.
- `3:39` — Running the one-line Open Claw installation command on macOS.
- `4:17` — Configuring Venice as the model auth provider with an API key; choosing GLM 4.7 as the default model.
- `4:49` — Setting up Telegram bot integration via BotFather.
- `6:12` — Pairing the Telegram bot with Open Claw and sending the first message.
- `7:07` — Switching models on the fly (e.g. to Claude Opus 4.5 via Venice).
- `7:27` — Live demo: scraping X for posts about Clawdbot, including passing an X auth cookie token.
- `8:46` — Setting up an automated hourly task (e.g. hottest new AI posts).
- `8:57` — Final warnings about the power/risk of the setup and a call to check the Venice Discord.

## Transcript
<details>
<summary>Full transcript</summary>

Open Claw (formerly MoltBot, formerly Clawdbot) is described as a persistent AI agent framework that acts on its own without needing to be prompted, with over 50 integrations and support for messaging apps like WhatsApp or Telegram. It gained over 150,000 GitHub stars in about a week. Examples cited: one person's Clawdbot learned to build phone-calling infrastructure; another gave their bot crypto wallet funds and told it to make more money, raising $10,000 in under 12 hours to buy new hardware, reportedly inspired by "Moltbook," a social network for AI agents. The underlying models aren't new — only the agency framework is — but real concerns exist: prompt injection attacks, system prompt leaks, and runaway costs (one bot spent $20 overnight just repeatedly checking what time it is). This is open-source hobby software, not enterprise-ready, so proper guardrails matter.

Venice is presented as the privacy solution: API inference can be completely private using open-source models, or you can use proprietary models like Claude Opus with your data anonymized when routed through Venice, avoiding logging on corporate AI servers. Venice also offers the DIEM token — $1 of Venice credit per day, bought once and renewing every 24 hours, effectively letting your agent "own" recurring intelligence and API credits.

Before installing, a strong disclaimer: use a separate/dedicated machine (Mac Mini, Raspberry Pi, or spare computer), not your main machine with sensitive information. A linked advanced privacy guide (recommending Venice plus tools like Tailscale and Matrix) is suggested for those wanting maximum privacy, though it's more complex than this walkthrough.

Installation on macOS: find the one-line install command on the GitHub repo or quickstart page, paste it into the terminal, and run it. This launches "OpenClaw doctor," generating and configuring a gateway token (defaults are fine for beginners), then opens a local dashboard automatically. Next, run `openclaw onboard` to start the setup wizard — confirm you understand the inherent risk, choose the quick start, select Venice AI as the model auth provider, choose API key auth, and paste in the Venice dashboard API key. Then pick a default model — the presenter selects a private open-source model, GLM 4.7. Next choose a communication channel; Telegram is easiest (though it runs through Telegram's servers — Matrix or Nostr are more private alternatives per the referenced guide). Setting up Telegram requires creating a new bot via BotFather (`/newbot`, choosing a name), getting an API token, and pasting it into the bot token configuration. Optional skill configuration follows (npm as default; skills like "Bird," a Twitter app, can be toggled with spacebar), followed by optional API key setup, hooks, and a gateway service restart.

To finish, the Telegram bot must be paired: click the link BotFather provided to message the bot, hit start, note the "access isn't configured" message, copy the pairing command from the terminal output, and paste the code from Telegram back into the terminal. After pairing succeeds, sending a test message confirms it's working. The docs' models page shows how to change the default model via `openclaw model set venice/<model>` — demoed switching to `venice/claude-opus-4.5` directly from the terminal, confirmed by asking the bot "what company powers you," which correctly replies "Claude Opus 4.5 running on Venice."

From there, the agent can be given tasks like creating a crypto wallet or scraping X for posts about Clawdbot; if credentials are missing, it asks for X auth cookie tokens (obtained via browser dev tools' Application tab), which get pasted into Telegram to enable the scrape. The agent can also be scheduled for recurring tasks, e.g. sending the hottest new AI posts every hour. The video closes with a warning to use this power carefully, a recommendation to review related privacy tutorials, and an invite to the Venice Discord to share what you build.

</details>
