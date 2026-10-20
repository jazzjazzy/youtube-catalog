---
title: "Chrome Just Became the Ultimate Agent Browser (Finally!)"
video_id: 51m_GGbXAng
channel: "[[channels/Better Stack]]"
uploaded: 2026-03-26
processed: 2026-07-05
duration: "6:00"
url: https://www.youtube.com/watch?v=51m_GGbXAng
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [browser-automation, live-browser-debugging]
tools: [Chrome DevTools MCP, Chrome, OpenCode, Claude Code, Agent Browser, Playwright]
llms: []
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Chrome Just Became the Ultimate Agent Browser (Finally!)

![thumbnail](https://i.ytimg.com/vi_webp/51m_GGbXAng/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=51m_GGbXAng) | 📅 Uploaded [[uploaded/2026-03-26]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Better Stack shows how Chrome 144+ lets the Chrome DevTools MCP server auto-connect to your actual running browser session — no more manual remote-debugging port setup or launching a fresh Chrome instance. The demo covers live performance auditing, fixing a UI bug by selecting an element in DevTools, and a lesser-known experimental CLI wrapper for agents who want to skip MCP context overhead.

**Watch this if:** you want your coding agent to debug real logged-in web sessions in your actual Chrome browser instead of a fresh automated instance.

## Key Takeaways
- Chrome 144+ adds an auto-connect option: with a remote-debugging flag toggled on in Chrome, the Chrome DevTools MCP server automatically detects your open browser session — no manual port/URL wiring needed.
- This lets an agent debug pages behind a login wall using your existing cookies/session, run Lighthouse audits for Web Vitals on a live site, and inspect a specific selected DOM element on request.
- Demoed live: selecting a "save" button in Chrome DevTools' inspector and asking the agent (via OpenCode) to restyle it to match another button — done correctly in a few seconds using the auto-connected session.
- Security-conscious users can instead pass a `browser-url` + isolated `user-data-dir` option so the agent gets a private Chrome profile without access to your real cookies/history.
- For those wary of MCP servers eating context, there's a little-known experimental Chrome DevTools CLI (documented in its `SKILL.md`) that wraps the same functionality as plain CLI commands via its own daemon, with no auto-connect support yet.
- The presenter's personal take: despite this upgrade, he's still primarily using Vercel's Agent Browser day to day, and considers Chrome DevTools MCP a genuine competitor now that both are converging toward CLI + skill-based agent workflows.

## 🛠 Tools & Software
- [[topics/Chrome DevTools MCP]] — the central subject: its new auto-connect capability, live debugging demo, and the hidden experimental CLI wrapper.
- [[topics/Chrome]] — the browser itself; version 144+ ships the remote-debugging auto-connect flag that makes this workflow possible.
- [[topics/OpenCode]] — the agent harness used to drive the Chrome DevTools MCP demo.
- [[topics/Claude Code]] — mentioned as the presenter's preferred terminal-based coding agent, motivating why an auto-connect Chrome MCP matters to him.
- [[topics/Agent Browser]] — referenced as the tool the presenter still primarily uses and compares against; links back to his earlier dedicated video on it.
- [[topics/Playwright]] — mentioned alongside Agent Browser as another tool that has added its own CLI/skills and MCP server, prompting the "will Chrome DevTools MCP need this too?" framing.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — the Chrome DevTools MCP server is the core mechanism being upgraded and demoed throughout the video.

## ✅ Action Items
- Update to Chrome 144+, enable the remote-debugging auto-connect toggle, and connect your MCP-enabled agent without manually exposing a debugging port.
- Use DevTools element selection plus a prompt like "restyle the element I selected to match X" to fix small UI issues without describing every navigation step to the agent.
- If running the MCP server in a sandbox or on a shared machine, use the `browser-url` + `user-data-dir` options for an isolated, cookie-free Chrome profile.
- Check out the experimental Chrome DevTools CLI skill if you want agent-driven debugging without adding another always-on MCP server to your context budget.

## 🔗 Related Videos
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Agent Browser, Claude Code, MCP, OpenCode
- [[videos/Your AI Coding Workflow NEEDS This New Agent Browser CLI]] — shared: Agent Browser, Chrome DevTools MCP, Claude Code, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude Code, MCP, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Chrome DevTools MCP, Claude Code, MCP, Playwright
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude Code, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, MCP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, MCP, Playwright
- [[videos/Claude Code Just Got Another Huge Upgrade]] — shared: Chrome, Claude Code, Playwright

## Timeline
- `0:00` — Introduction: Chrome DevTools MCP now auto-connects to a running session.
- `0:38` — Why the new Chrome is better for agents — no more manual remote-debugging setup.
- `1:22` — Setting up Chrome MCP with auto-connect enabled.
- `2:09` — Demo of basic MCP auto-connect usage: Lighthouse audit and login-gated page debugging.
- `4:04` — The experimental Chrome DevTools CLI — a hidden, lower-context alternative to the MCP server.
- `5:02` — Using the DevTools CLI with an agent to inspect a selected element.
- `5:29` — Conclusion and final thoughts, including a nod back to Agent Browser.

## Transcript
<details>
<summary>Full transcript</summary>

So, the Chrome team have finally shipped an update that lets the Chrome DevTools MCP server talk to a running instance of Chrome to do things like debug issues behind a login page, perform analysis on a live session, and even do some really cool debugging things like access an element that's been selected, specific errors, and even network activities. But, with other AI browser debugging tools like Agent Browser and Playwright adding a CLI with skills as well as an MCP server, is this something the Chrome DevTools MCP will have to add in the future? Hit subscribe, and let's find out.

A few months ago, Andras created a video giving a great overview of the Chrome DevTools MCP server, but at the time it could only launch a new Chrome session, or you could also connect it to a remote debugging port, but that required a lot of manual setup. But, now in Chrome version 144 and above with the remote debugging flag turned on, the Chrome MCP tool will now auto detect an open session, which can be used for debugging, which changes the game for me personally because I prefer to use Claude Code in the terminal, and means I don't have to use AI browsers like Dia, Comet, and even the Claude Chrome extension, or even useful AI debugging tools like React Scan.

Let's see these new Chrome DevTools MCP features in action. You'll first need to have the MCP server installed with the auto-connect option available. I'm using OpenCode, but this supports many agent harnesses, and inside Chrome you'll have to navigate to this URL and make sure you have this option turned on. Now, previously, you'd have to start a session with a command like this, and the agent will connect to the exposed port via HTTP. But, with the new way inside this UI, you can start Chrome as you normally would having access to all your cookies, history, and whatnot, and you can turn it off whenever you're done. Now, if you're security conscious, later on in the video I can show you how to connect to a more private version of Chrome.

But, after you've done those two things, so toggled on this option and connected to the MCP server with the auto-connect option, that should be it. I can ask my agent to check the performance of BetterStack, and inside Chrome I'll get this pop-up asking if I want to allow remote debugging, and then I'll have this banner up here. Now, the agent has been able to navigate to the BetterStack website, and now it's using the Lighthouse audit tool to give me some cool Web Vitals, Lighthouse scores, and some other details.

But, now let's do something useful. Here is a language learning app that I'm working on. I've logged in as an admin, navigated to content, a specific unit, and gone to this exercise, and I've noticed on the exercise modal that the save button down here is different from the other buttons on the site. So, instead of manually telling the agent to replicate my steps, so logging in and navigating to this specific page, I'm going to select this save button in the inspect tools, and then ask the agent if it can see the element I've selected. And after a while, it's able to see I have the save button selected. So, now I'm going to ask it to change the style of the save button to look like the new exercise button, which is the button over here if you can see it. And after a few seconds, it's changed the style of the button to exactly how I wanted it.

Note, if you're running the MCP server in a sandbox environment, you'd have to use the browser URL option with the port for remote debugging as HTTP, not WebSockets. And if you're security conscious, you'll need to add the user data directory with a specific location to the MCP server as an option, which will mean the agents won't have access to your existing cookies, passwords, browser history, and much more, and you'd have to re-login to those sites if you want the agent to have access to them.

Now, as cool as this is, if you've watched any of my previous videos, you'll know I'm not the biggest fan of MCP servers because they do use up a lot of context if you have a lot of them. But, luckily, the Chrome DevTools MCP server does allow you to do everything with a CLI, which not many people know about because it's kind of hidden because you'll have to go into the skills directory and then Chrome DevTools CLI to find out about this experimental feature, which gives your agent information on how to use it, and also some installation instructions if you haven't installed it already.

This is basically a thin wrapper around the MCP server, and if you already have it running inside an agent harness, this CLI won't use that because it uses its own daemon. This command gives you information about the default daemon that runs, and you can already see it's set the browser URL flag with some other flags like headless and isolated. But, you'll also notice that there's no auto-connect inside the available CLI options. So, if you haven't run Chrome via the terminal, you'd have to quit this existing one, and then run it like this making sure that if you have the remote debugging port flag, you have to have the user data flag. So, now with that in place, I can start the daemon like this, get the list of pages, which only shows one new tab cuz there isn't much at the moment.

But, of course, the real power comes when you use it with an agent. So, if I turn off the Chrome MCP tool, select this button in DevTools, and ask the agent to use the CLI to figure out what element is selected, and we can see it's been able to figure that out. Note, the information in the user data directory persists between sessions. So, this keeps all my cookies, browser information, and so on. Also, there are many more things the Chrome DevTools CLI can do, so I recommend you go ahead and check out the skill, and maybe in the future they may introduce the auto-connect feature.

So, there you have it, a quick run-through of some of the new cool features from the Chrome DevTools MCP server and CLI, which will definitely improve your debugging experience with coding assistants. As an Arc user, yes, I still use Arc, I really wish this feature would come to it in the future. But, until then, I'm happy to use Vercel's Agent Browser, which has been working really well for me. And if you know nothing about Agent Browser, check out this video I made a while back, although it has improved a lot since then. So, maybe it's time for me to make another video.

</details>
