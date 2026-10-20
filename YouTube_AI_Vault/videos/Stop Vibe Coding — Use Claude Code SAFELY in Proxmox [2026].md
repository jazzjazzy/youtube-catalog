---
title: "Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]"
video_id: 3C-LarI4480
channel: "[[channels/ServersatHome]]"
uploaded: 2026-04-23
processed: 2026-07-05
duration: "10:43"
url: https://www.youtube.com/watch?v=3C-LarI4480
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [safe-ai-agent-sandboxing, homelab-claude-code-deployment]
tools: [Claude Code, Proxmox, Docker, VS Code, Watchtower, Superpowers, Git, GitHub, TrueNAS]
llms: []
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]

![thumbnail](https://i.ytimg.com/vi_webp/3C-LarI4480/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=3C-LarI4480) | 📅 Uploaded [[uploaded/2026-04-23]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Evan (ServersatHome) walks through a one-command script that provisions an Ubuntu Proxmox LXC container fully loaded for Claude Code — full-trust permissions, agent teams, a dev toolkit (Node, Python, Go, Rust, Docker), browser-based VS Code (Code Server), Watchtower auto-updates, and the Superpowers plugin — so Claude Code can run with real system power in a disposable, isolated sandbox instead of directly on a host machine. He runs the script live and shows a real personal invoicing tool he built entirely inside it.

**Watch this if:** you run a homelab (Proxmox especially) and want to let Claude Code run with full permissions safely instead of on your main machine or host.

## Key Takeaways
- Claude Code can run shell commands, edit files, and install packages with real system power — useful, but exactly why it should run in a disposable LXC rather than on a Proxmox host or main machine; if it breaks something, you destroy the container and spin up a fresh one in minutes.
- The script provisions an Ubuntu LXC, installs standard Linux tooling plus build-essentials, Python, Go, Rust, and Docker, then installs Claude Code natively and sets every tool permission (file read/write, bash, web fetch/search) to allow — "full-trust mode" — which is appropriate only because the container itself is the sandbox.
- Agent teams are enabled, letting Claude Code spawn parallel sub-agents on different parts of a task (e.g. one on backend, one on frontend of a refactor).
- Superpowers (by Jesse Vincent) is called out as one of the most important additions: it forces Claude Code to brainstorm before touching code, use isolated git worktrees, break work into small verifiable tasks, follow test-driven development, and use systematic debugging on bugs — plus it blocks documented "excuses" Claude Code invents to skip skills, acting like a senior developer reviewing the agent's process in real time.
- The container also ships with a remote-control feature (drive Claude Code inside the LXC from Claude in a web browser), a Watchtower container to auto-update any Docker containers you add, and a Code Server VS Code web front end for easier file editing.
- Running the script takes about 5 minutes end-to-end and results in a container using ~400MB RAM and ~6GB disk at idle, immediately dropping into the project directory where typing `claude` connects you.
- The host demonstrates a real personal tool — "Time Tracker," a small invoicing app for consulting work — built entirely inside Claude Code in this setup, but is explicit that even sandboxed, safely-built code still needs human code review before being released or trusted with sensitive access; he only feels safe running it locally with no outside access.
- He flags MCP servers as a growing source of both power and danger for Claude Code (e.g. a still-limited community MCP server for TrueNAS), suggesting more capability — and more risk — is coming as MCP integrations mature.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agentic coding tool the entire container is built to run safely, installed natively with full-trust permissions and agent teams enabled
- [[topics/Proxmox]] — the virtualization host the script targets, provisioning the isolated Ubuntu LXC container that sandboxes Claude Code
- [[topics/Docker]] — installed inside the LXC so Claude Code builds things in disposable Docker containers that can later be exported to the main host
- [[topics/VS Code]] — deployed as a browser-based Code Server front end for editing files without needing the command line
- [[topics/Watchtower]] — a Docker container installed to auto-update any other Docker containers spun up inside the LXC
- [[topics/Superpowers]] — the skills library that enforces brainstorm-plan-test-implement-review discipline and blocks Claude Code's excuses for skipping steps
- [[topics/Git]] — Superpowers has Claude Code create isolated git worktrees so its work doesn't pollute the main branch
- [[topics/GitHub]] — hosts the creator's personal repo containing the setup script that's curled and run on Proxmox
- [[topics/TrueNAS]] — used as the LVM storage backend selected during the container provisioning walkthrough

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — flagged as an emerging source of major capability and risk for Claude Code, illustrated by a still-limited community MCP server for TrueNAS

## ✅ Action Items
- Run Claude Code inside a disposable Proxmox LXC (or similar VM/container) rather than on your host machine or main desktop.
- Install Superpowers before letting Claude Code run with full-trust permissions, so it's forced through a brainstorm/plan/test/review workflow instead of freewheeling.
- Add a Watchtower container so any Docker containers Claude Code spins up stay patched automatically.
- Set up the Code Server VS Code web front end for easier manual review/editing of what the agent produces.
- Treat anything built this way as needing real human code review before it's exposed outside your own local network.

## 🔗 Related Videos
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Git, GitHub, Superpowers
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Git, MCP, Superpowers
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, GitHub, MCP, VS Code
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude Code, Docker, GitHub, MCP
- [[videos/Every Claude Code Command in 13 minutes! (10x your productivity)]] — shared: Claude Code, GitHub, MCP, VS Code
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Docker, GitHub, MCP
- [[videos/Planning In Claude Code Just Got a Huge Upgrade]] — shared: Claude Code, Git, GitHub, VS Code
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, GitHub, MCP

## Timeline
- `0:00` — Intro: why AI coding tools need to be used responsibly, not just vibe-coded into production
- `1:06` — Architecture overview: why an isolated LXC is the right call for Claude Code
- `1:39` — Script overview: building the Ubuntu container and installing the dev toolkit
- `4:08` — Superpowers: enforcing brainstorm-plan-test-implement-review discipline
- `6:15` — Running the script live on Proxmox, provisioning the container end to end
- `8:34` — Demo: Time Tracker, a real invoicing tool built entirely inside Claude Code
- `9:46` — Conclusion: MCP servers, growing power and risk, and closing thoughts

## Transcript
<details>
<summary>Full transcript</summary>

There have been a lot of stories lately about people doing a terrible job by coding apps and some pretty famous failures. But tools like AI are here to stay. And if we're going to use them, we should learn how to use them responsibly — understanding what they're doing, giving them a safe environment to work in, and not just blindly piping code into production. Claude Code is Anthropic's agentic coding tool that runs directly in your terminal. It reads your files, writes code, runs commands, and manages git workflows all through natural language. It's powerful, and because it's powerful, you want to give it a sandbox, not the keys to your whole server. This video shows a Proxmox script that creates a pre-built container specifically designed to run Claude Code safely — a one-command setup that builds a lightweight LXC container running Ubuntu 24.04, filled with everything you need to use Claude Code.

Why an LXC is the right call: Claude Code can run shell commands, edit files, install packages — real power over your system. That's what makes it useful, but also why you don't want it running on your main machine or Proxmox host directly. An LXC gives you a lightweight isolated environment — if Claude Code does something unexpected, like installing a package that breaks something or writing to a file it shouldn't, it's all contained. You can destroy the container and spin up a fresh one in minutes, keeping the host clean. The code lives in the presenter's personal GitHub repo, and he walks through it since you should never run code from someone on YouTube without looking at it first.

The script sets defaults for building an LXC, looks for (or fetches) the Ubuntu 24.04 template, creates and starts the container, then downloads standard Linux tools Claude might need (curl, wget, unzip, nano, tmux, etc.), followed by build-essentials, make, automake, Python, ripgrep, rsync, npm, Postgres, Go, Rust, and Docker. By default it builds inside Docker containers even though it's already inside an LXC, so you can eventually delete the LXC and just extract the Docker containers for modularity once something is stable. Then it installs Claude Code via the native installer and configures permissions in "full-trust mode" — every tool permission (file reads/writes, bash commands, web fetches/searches) set to allow, so Claude doesn't stop to ask "are you sure?" on every command. In a normal desktop environment you'd want those guardrails on, but in an isolated LXC built specifically for this, you don't need them. It also enables agent teams, letting Claude Code spawn parallel sub-agents on different parts of a problem — e.g. one agent on the backend, another on the frontend of a refactor.

By default the script enables several Anthropic-made plugins plus one that isn't: Superpowers, created by Jesse Vincent. Superpowers is a skills library that enforces a structured development workflow on Claude Code — it's forced to brainstorm and think through design before touching code, create isolated git worktrees so it doesn't pollute the main branch, break work into small verifiable tasks with clear success criteria, follow test-driven development (writing tests before implementation), and use systematic debugging instead of randomly guessing at fixes when it hits a bug. It also builds in an anti-rationalization system — the excuses Claude Code invents to skip skills were documented and explicitly blocked, like having a senior developer reviewing the AI's process in real time. This is a huge part of what makes the script's setup "responsible": it turns Claude Code from a powerful but undisciplined agent into something that follows brainstorm-plan-test-implement-review engineering practice. Logging into the LXC by default drops you straight into the project directory.

There's also a remote-control feature enabled by default, letting Claude in a web browser talk to Claude Code inside the LXC. Two Docker containers are installed from the start: Watchtower, to keep any Docker containers you install updated, and Code Server for a browser-based VS Code front end, useful for dragging files in or editing code without the command line. At the very end, the script sets up auto-updates so a long-running LXC keeps getting security patches.

Running it: copy the curl command from the top of the script and paste it into the Proxmox shell. It picks the next available container ID, prompts for hostname, root password, CPU cores (4), RAM (10GB), swap (2GB), and disk (30GB), storage backend (TrueNAS LVM in this case, most viewers would use local-lvm), DHCP or static networking, and DNS. After confirming the summary, the container builds in about 5 minutes, ending at "provision complete." Back in Proxmox, the container is running at nearly 0% CPU, about 400MB of memory, and around 6GB of boot drive space. Logging into the console drops you at `Claude Code/project`, and typing `claude` connects immediately.

The presenter stresses that even with these safe containers, building inside Claude Code and releasing it into the wild still requires real coding and security knowledge — Claude is getting very good at security, but human code review is still necessary before shipping anything publicly. For personal tools, though, this is genuinely useful: he shows "Time Tracker," a small invoicing app built entirely inside Claude Code for his consulting work, letting him log time entries, bill clients at an hourly rate, create and mark invoices as paid, manage clients, and configure business settings like billing frequency and payment terms. He won't share the container itself since he's not confident the code is secure enough to distribute, but running it locally with no outside access keeps it safe from anyone hacking him or accessing information they shouldn't.

Claude is getting ridiculously powerful — with things like MCP servers and the ability to run directly on the bare metal of any server, there's a lot of possibility and a lot of danger. He notes this is likely his only video on the topic for now until the community MCP server for TrueNAS (currently written by Chris Moore with very limited abilities) becomes more capable, and asks viewers whether and how they're using AI tools responsibly in their own homelabs.

</details>
