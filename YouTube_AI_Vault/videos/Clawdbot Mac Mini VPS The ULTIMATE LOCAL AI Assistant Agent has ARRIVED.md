---
title: "Clawdbot + Mac Mini / VPS: The ULTIMATE LOCAL AI Assistant Agent has ARRIVED!"
video_id: ikDNH4aG-lI
channel: "[[channels/AICodeKing]]"
uploaded: 2026-01-25
processed: 2026-07-06
duration: "9:12"
url: https://www.youtube.com/watch?v=ikDNH4aG-lI
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [personal-ai-assistant-setup, home-server-hardware-selection]
tools: [Open Claw, Claude Code, Discord, Unraid]
llms: [GLM]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Clawdbot + Mac Mini / VPS: The ULTIMATE LOCAL AI Assistant Agent has ARRIVED!

![thumbnail](https://i.ytimg.com/vi/ikDNH4aG-lI/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=ikDNH4aG-lI) | 📅 Uploaded [[uploaded/2026-01-25]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A short, simple tutorial on installing and configuring ClawdBot (built on top of Claude Code) as an always-on, chat-accessible personal assistant with scheduled/cron-style tasks, followed by a hardware comparison of where to run it: Mac Mini M4 for power-efficient local always-on use, a $5/month VPS for easier networking, or budget options like an old laptop, a used Optiplex, or a Beelink Mini PC.

**Watch this if:** you want a quick install walkthrough plus a clear-headed comparison of Mac Mini vs. VPS vs. budget hardware for hosting a 24/7 AI agent.

## Key Takeaways
- ClawdBot is described as an "always-on" wrapper around Claude Code that can appear as a person in a chat channel (like Discord) and do coding or non-coding tasks (e.g. checking step-tracking data) around the clock.
- The built-in Scheduler lets you set up cron-style jobs through natural language (e.g. "tell me Nvidia stock prices every day at 10pm" or "ping me at 10:00 about the meeting") without needing to manually configure cron syntax.
- Installation is a single command, followed by a `claudebot onboard` wizard that asks you to pick a model provider (the GLM Coding Plan is called out as the cheapest/best option), configure channels (Discord, Slack, WhatsApp), and optionally add skills.
- The web interface exposes channels, connected instances, sessions (Claude Code sessions, splittable by message count), a Scheduler for cron jobs, a skills config, a nodes section for allow/deny lists, and authentication provider settings.
- Mac Mini M4 ($599) is popular because it draws only 5-7W idle (up to ~70W at load), can run 24/7 in a closet with negligible power cost, and doubles as an emergency computer.
- A $5/month VPS is recommended as more capable per dollar and much easier for firewall/domain configuration than a local machine, at the cost of not being fully local.
- Budget alternatives: repurpose an old laptop/desktop with Linux, buy a used Optiplex (~$60), or get a Beelink Mini PC (~$270) with a large SSD running Unraid (or a similar NAS OS) in a containerized setup — which can double as network storage, something the Mac Mini can't do.

## 🛠 Tools & Software
- [[topics/Open Claw]] — the always-on personal assistant ("ClawdBot") installed and configured via the onboarding wizard, web interface, and channel/scheduler setup
- [[topics/Claude Code]] — the underlying engine ClawdBot wraps; its sessions appear directly in ClawdBot's session view
- [[topics/Discord]] — the recommended channel for chatting with the agent for easy 24/7 access
- [[topics/Unraid]] — suggested OS for running ClawdBot in a containerized setup on budget hardware (e.g. a Beelink Mini PC), doubling as NAS storage

## 🤖 LLMs Mentioned
- [[topics/GLM]] — called out as the cheapest and best-value model provider option during onboarding

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install ClawdBot with the single provided install command, then run the onboard wizard to pick a provider, channel, and skills.
- Try the GLM Coding Plan as a budget-friendly model provider if cost is a priority.
- Set up at least one natural-language scheduled task (e.g. a daily stock or reminder ping) to see the Scheduler/cron feature in action.
- Decide your hosting approach based on priorities: Mac Mini M4 for lowest-hassle always-on local power efficiency, a cheap VPS for easier networking/firewall setup, or a budget PC/NAS box (Optiplex, Beelink + Unraid) if you also want extra storage.

## 🔗 Related Videos
- [[videos/Agent memory resolved]] — shared: Claude Code, GLM, Open Claw
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: Claude Code, Discord, Open Claw
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Open Claw
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Open Claw
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, GLM
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: Claude Code, Discord
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: GLM, Open Claw
- [[videos/Hermes The Self-Improving Agent That Gets Smarter Every Day]] — shared: GLM, Open Claw

## Timeline
- `0:00` — Intro: why ClawdBot finally clicked, and what this tutorial covers
- `0:39` — What ClawdBot is: an always-on Claude Code wrapper reachable like a person in Discord
- `1:34` — Scheduled tasks and pings: natural-language cron jobs (e.g. daily stock updates)
- `2:42` — Installing ClawdBot with the single install command
- `2:55` — Onboard wizard: choosing a provider (GLM Coding Plan) and configuring channels/skills
- `3:40` — Web interface tour: channels, sessions, Scheduler, skills config, nodes, settings
- `5:16` — Mac Mini M4 recommendation: power efficiency and always-on convenience
- `6:13` — VPS alternative: $5/month, easier firewall/domain setup, less "local"
- `6:45` — Budget hardware options: old laptop/desktop, used Optiplex, Beelink Mini PC with Unraid

## Transcript
<details>
<summary>Full transcript</summary>

Hi, welcome to another video. So, there is something that has been trending for a while and it is called Claudebot. I actually didn't quite get the hype until now, but after using it for a bit, I think that I finally understand it. And I want this to be a simple but effective tutorial on how you can set it up and what you should configure it with. We will go step by step.

First, let's talk about what it is and how you should go about setting it up. Claudebot is kind of like Claude code, but it can be called upon like a person. So, let's say that you use something like Discord to talk with people. Then Claudebot can basically appear there as a person that is available 24/7 and does the work for you. It is really amazing if you think about it. But it is not just that because it is built on clawed code. You can configure it to do almost anything including coding for you. Or maybe you want it to check your step tracking and motivate you to be more active. So it is really useful even if you do not want to code. It is kind of like a clawed coworker but more easily accessible and active. I say active because it runs basically 24/7 and you can give it scheduled tasks and it pings you directly about that thing. So let's say that you ask it to ping you when it is 10:00 about joining a meeting. Then it will send you a message on any of your configured channels immediately, which is really awesome. Or you can also ask it to do scheduled tasks. So you can ask it to tell you about the Nvidia stock prices every day at 10 p.m. and it will just tell you about it every day with a ping. You can also just chat with it as a bot. It is very amazing. Like it is really good. You can configure it on anything, including the device that you are probably watching this on except for mobile phones. Most of my viewers are apparently on desktop, so that checks out. Many people are configuring it on things like the Mac Mini. I want to give my recommendations on the machine that you can configure it on towards the end of the video, but let's first get it installed.

So you would have to get it installed with this simple command. Once that is configured, you can go ahead and run the Claudebot onboard command and it will give you multiple options. First, select the provider you want to use. It works with a ton of them, including the GLM coding plan. So that can be the cheapest and best option. Anyway, you can then configure the channels as well. You can configure Discord, Slack, WhatsApp, and everything here. I will go with no channels and just the Claudebot interface for now. You can then also configure some skills that will allow it to do much more stuff, which is all great. Then just follow the onscreen instructions and you should see this interface. It will give you the port on which it is started and you can ask it to do whatever you want.

You would generally want to have it set up on a channel like Discord for super easy access, but the interface is also fine. There are a ton of channels here. You also get these options under channels where you can refresh the channels and stuff like that. You also have the connected instances listed here along with sessions. Sessions are basically just the clawed code sessions. You can make it break up your sessions based on the number of messages and everything. There is also the scheduler. This is where the tasks will be created when you ask it to do something at a later time. This creates a cron job. So claudebot will execute it at the expected time which is kind of cool for sure. It can be daily, hourly, or whatever it is that you want to configure. You don't need to come here to configure it manually if you don't want to as Claudebot can do it with natural language. So there is that you can also configure the skills that you wanted to have here in the skills config option as well. There is also the nodes option that allows you to set up allow lists, deny lists, and everything that you may need for the best deployment and stuff like that. In the settings, you also get all kinds of config for authentication providers and everything as well.

But now let's talk about Mac Mini. So, if you are active on the Twitter space, then you would see that everyone is apparently buying a Mac Mini to run Claudebot on it. Now, you may wonder why. Well, this is because the Mac Mini M4 is like $599 and it is very capable and super power efficient. You can basically install Claudebot on it, throw it in a closet, and let it run 24/7 without thinking about power costs, and it just works. You can just have an AI assistant that Siri wanted to be, but keep it all local, which is kind of awesome. But I would like to say that if you can afford to pay $600 for a really good agentic assistant, then I would recommend it for sure.

But you don't actually need that to be very honest. You can get something like a VPS, which can be more capable and costs only $5 a month. Yes, it might not be super local like you may want, but it does indeed save you a lot of time in configuring firewalls for best security. You can connect it to a domain for easy access, which is all very tricky when you try to do it on a local machine. A VPS will also come in handy for you to do other stuff as well.

If you do want a lowerc cost machine but locally, then you may also have things like an old laptop or desktop lying around, you can resurrect that, install Linux on it, install Clawbot, and let it run in a closet. You will get some cool output from the junk you already have. If you're going for something super cheap and secondhand, then an Optiplex that goes for around $60 might also be super good for your use case. However, I think that the best option for you might be something like this Beink Mini, which costs about $270. You can place a 512 GB or 1 TB SSD in it, install something like Unrade on it and run Claudebot in a containerized environment. Or you can just install Omar and use that. It will cost you a bit less and you can add up to six slots of storage in it. So it will also come in handy as an NAS for you, which unfortunately the Mac Mini can't do. However, if you want no hassle and a thing that just works for this specific thing and is super efficient, the Mac Mini only draws like 5 to 7 W at idle and at max load, it can go to about 70 W, which is extremely efficient. It can also come in handy as an emergency computer if something breaks. So, it is not a bad option by any means, but you can also save some money if you want by running it on your current computer.

I mean, I won't stop you from buying a Mac Mini because I like new and shiny stuff just as much as you. So, go ahead and run Claudebot on the new shiny Mac Mini that you want. That is mostly about it. I am enjoying Claudebot a lot and I would recommend that you check it out as well. Overall, it is pretty cool. Anyway, share your thoughts below and subscribe to the channel. You can also donate via super thanks option or join the channel as well and get some perks. I'll see you in the next video. Bye.

</details>
