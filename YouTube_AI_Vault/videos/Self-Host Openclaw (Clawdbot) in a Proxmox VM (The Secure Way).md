---
title: "Self-Host Openclaw (Clawdbot) in a Proxmox VM (The Secure Way)"
video_id: DG7p0BfO6UI
channel: "[[channels/Nightly Ventures]]"
uploaded: 2026-01-30
processed: 2026-07-06
duration: "16:56"
url: https://www.youtube.com/watch?v=DG7p0BfO6UI
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [self-hosted-ai-agent-security]
tools: [Open Claw, Proxmox, Telegram, Node.js, Ollama]
llms: [Claude Opus, ChatGPT]
protocols: [SSH]
transcript: true
tags: [youtube, ai-automation]
---

# Self-Host Openclaw (Clawdbot) in a Proxmox VM (The Secure Way)

![thumbnail](https://i.ytimg.com/vi_webp/DG7p0BfO6UI/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=DG7p0BfO6UI) | 📅 Uploaded [[uploaded/2026-01-30]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Open Claw (formerly Moltbot/Clawdbot) is a shell-access AI agent that hit 60k+ GitHub stars in three days, but hundreds of instances are already exposed on the internet with no authentication. This walkthrough sets it up on Proxmox the secure way: an isolated VM (not an LXC container), a dedicated non-root user sandbox, a localhost-only gateway (outgoing polling instead of open inbound ports), and a pairing flow for new chat users, then demos it managing the server live over Telegram.

**Watch this if:** you want to self-host an AI agent with real shell/filesystem access on your homelab without exposing it to the internet.

## Key Takeaways
- Open Claw differs from a chatbot like ChatGPT because it has shell access, filesystem access, and persistent memory between sessions — it knows what system and environment it's actually running in.
- Security decision #1: use a full VM instead of an LXC container, because an LXC shares the host kernel — if Open Claw is compromised inside an LXC, the attacker may reach the Proxmox host; a compromised VM can just be deleted with hypervisor isolation intact.
- Security decision #2: create a dedicated non-root "clawdbot" user so a compromised process is contained to a sandboxed account, not the root user.
- Security decision #3: bind the gateway to localhost only, with no inbound ports opened — Open Claw polls Telegram's servers for new messages every few seconds (all outgoing requests), so no open port is needed to receive messages.
- A swap file is added before install because Open Claw is a Node package that compiles dependencies, skills, and plugins, and can need more memory than expected.
- Open Claw ships with a built-in security audit command that catches misconfigurations (e.g., a missing/blank token, permission issues) after onboarding.
- Pairing adds a further layer: even if someone knows the Telegram bot's username and messages it, Open Claw won't act on their behalf until a pairing code generated on the server is entered to approve them.
- Live demo shows the agent reporting real CPU/memory/disk usage, correctly retaining conversation context, cleaning the npm cache on request, and even discovering (via internet access) that it had been renamed from Clawdbot to Moltbot mid-recording.
- The setup uses an Anthropic API key with Opus 4.5, but the presenter notes Ollama could be swapped in to run a fully local model instead.

## 🛠 Tools & Software
- [[topics/Open Claw]] — the shell-access AI agent being self-hosted; configured via its onboarding wizard, built-in security audit, and Telegram pairing flow.
- [[topics/Proxmox]] — the homelab hypervisor used to create an isolated Ubuntu 24 VM to host Open Claw, chosen over an LXC container for hypervisor-level isolation.
- [[topics/Telegram]] — the chat client integrated with Open Claw via a bot API token, used to send commands and receive responses, with polling instead of inbound webhooks.
- [[topics/Node.js]] — installed as the runtime Open Claw and its skills/plugins are built on.
- [[topics/Ollama]] — mentioned as an alternative to the Anthropic API for running a fully local model with Open Claw.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4.5 is the model configured via the Anthropic API key during Open Claw's onboarding wizard.
- [[topics/ChatGPT]] — used as a contrasting example: asked to check disk space, it returns generic commands with no awareness of the actual system or environment, unlike Open Claw.

## 📡 Protocols & Standards
- [[topics/SSH]] — used to connect a terminal to the new VM (OpenSSH server installed during setup) instead of relying on the Proxmox browser console.

## ✅ Action Items
- Provision a dedicated VM (not an LXC) for any AI agent with shell/filesystem access, so a compromise can be isolated and destroyed without risking the host.
- Create a dedicated non-root user for the agent process rather than running it as root.
- Configure the agent's gateway to bind to localhost only and rely on outgoing polling (e.g., to Telegram) instead of opening inbound ports.
- Run any built-in security audit tool after onboarding and fix flagged issues (missing tokens, permission problems) before going live.
- Enable the pairing/approval mechanism for any chat integration so unknown users can't act through the bot even if they find its username.
- Consider Ollama for a fully local model if you want to avoid sending data to a third-party API.

## 🔗 Related Videos
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Node.js, Open Claw, SSH
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: ChatGPT, Claude Opus, Open Claw, Telegram
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Opus, Node.js, Ollama, Telegram
- [[videos/This is the CHEAPEST and EASIEST way to set up ClawdBot]] — shared: ChatGPT, Claude Opus, Open Claw, Telegram
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: Claude Opus, Open Claw, Telegram
- [[videos/Hermes Agent Full Setup Tutorial How to Setup Your First AI Agent (Gemma 4)]] — shared: Ollama, Open Claw, Telegram
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: ChatGPT, Open Claw, Telegram
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude Opus

## Timeline
- `0:00` — What makes Open Claw (Clawdbot) different from a typical AI chatbot.
- `1:52` — Creating the Proxmox VM (Ubuntu 24, chosen over an LXC container for isolation).
- `4:15` — Setting up a dedicated non-root user for Open Claw.
- `5:20` — Installing Node.js and Open Claw (Clawdbot).
- `6:01` — Telegram bot setup (API token, privacy settings, user ID).
- `6:49` — Onboarding wizard and gateway security (localhost-only bind, Anthropic API key with Opus 4.5).
- `9:27` — Running Open Claw's built-in service and security audit, fixing flagged issues.
- `11:34` — Pairing mechanism and live demo (server overview, npm cache cleanup, internet access, self-rename discovery).
- `15:23` — What's next: exploring Ollama for local models and building skills/automations.

## Transcript
<details>
<summary>Full transcript</summary>

This new AI agent amassed over 60,000 stars on GitHub in only three days. Everyone's buying Mac minis to run local models, but as homelabbers we already have a server at home, so this covers setting up Clawdbot (Open Claw) on Proxmox. First, what makes it different: asking ChatGPT to check disk space just returns generic commands with no awareness of the system or environment it's running in. Open Claw is aware of that and can do much more — it has shell access, filesystem access, and persistent memory between sessions, and can connect to many chat apps, voice agents, or web interfaces, plus be extended with skills and plugins. That power is exactly why a security researcher found hundreds of Open Claw gateways exposed to the internet with no authentication — AI agents with shell access, open to anyone. This walkthrough explains every security decision made to avoid that.

First, create a new VM (named "clawdbot") on Ubuntu 24. Security decision #1: use a VM, not an LXC container. LXCs are lightweight because they share the host kernel — if Open Claw gets compromised in an LXC, it might reach the Proxmox host itself. VMs have hypervisor isolation: if an attacker owns the VM, just delete it and the Proxmox host stays safe. Configuration uses mostly defaults, a modern chipset, QEMU agent, 32GB disk, a couple of cores, host CPU type for full feature access, and no memory ballooning since Open Claw is a Node package that can pull in unpredictable amounts of memory. During Ubuntu install, OpenSSH server is added so the presenter can use their own terminal instead of the browser console.

After SSHing in, run updates (especially security packages). Security decision #2: create a dedicated "clawdbot" user rather than using root, so a compromised process is contained to a sandbox. One gotcha: the service didn't start without exporting the current user ID into an environment variable. A swap file is added to give the Node compiler more room, since Open Claw pulls in dependencies, skills, and plugins as Node packages and compilation can need extra memory.

Node.js is installed via its repository, then Open Claw is installed globally. Telegram is chosen as the interface, requiring a new Telegram bot: get the API token, disable group privacy (so the bot reads all messages, not just mentions), and get the user's Telegram ID via a user-info bot.

Open Claw's onboarding wizard handles configuration: manual configuration is chosen, using an Anthropic API key with Opus 4.5. Security decision #3: bind the gateway to loopback only, so it's accessible only within the VM — no ports opened to the network or internet. Instead of waiting for inbound messages, Open Claw polls Telegram's servers every few seconds for new content — all outgoing requests, no incoming connections needed. Tailscale isn't added since the server will only be used locally for now. The Telegram integration is enabled with the saved token, skills and hooks are skipped for now, and pairing is left at its default. After onboarding, a message about system user services being unavailable appears, so a systemd service is configured manually to keep Open Claw running after logout/reboot.

Open Claw includes a built-in security audit, which flags an issue (a blank/missing token that wasn't generated by the install script — fixed manually) and a permissions issue that Open Claw can fix itself. Re-running the audit confirms the fixes.

Pairing is the final security layer: by default, anyone who knows a Telegram bot's username can message it, but Open Claw won't act on unknown senders — instead it sends them a pairing code that must be entered on the server terminal to approve them. After pairing, the live demo begins: asking Open Claw the current date correctly returns the real date and UTC timezone (unlike typical chatbots that default to a stale training-cutoff date), a request for a formatted CPU/memory/disk overview works, and a follow-up about the largest files on disk shows it retains conversation context. Asking it to clean the npm cache works live. Given internet access, it discovers via Hacker News headlines that it has been renamed from Clawdbot to Moltbot mid-recording.

Recap: this is a self-hosted AI agent that can actually do things (not just chat), accessible securely from anywhere via phone — using a hypervisor-isolated VM instead of an LXC, a dedicated user sandbox, a localhost-bound gateway with only outgoing connections, and a pairing process for new users, avoiding the fate of the hundreds of exposed instances found online. The presenter is currently using an Anthropic API key but notes Ollama would allow running a fully local model instead, and plans to explore skills for home automation and other workflows.

</details>
