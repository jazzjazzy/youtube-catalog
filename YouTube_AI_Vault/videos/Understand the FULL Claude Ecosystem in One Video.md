---
title: "Understand the FULL Claude Ecosystem in One Video"
video_id: MS7E5TXNviM
channel: "[[channels/Futurepedia]]"
uploaded: 2026-06-24
processed: 2026-07-06
duration: "12:47"
url: https://www.youtube.com/watch?v=MS7E5TXNviM
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [claude-product-selection]
tools: [Claude Code, Claude Cowork, Claude Desktop, Claude Design, Claude Skills]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Understand the FULL Claude Ecosystem in One Video

![thumbnail](https://i.ytimg.com/vi_webp/MS7E5TXNviM/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=MS7E5TXNviM) | 📅 Uploaded [[uploaded/2026-06-24]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A structured map of the entire Claude product line: the four core products (Chat to think, Cowork to delegate, Code to build, Design to create), the universal layer that extends all of them (Skills, Connectors, Plugins), the memory/context layer (Projects, account memory, CLAUDE.md), and the autonomous layer (computer use, Dispatch, scheduled tasks, Claude Code routines). Aimed at people confused about which product to reach for when.

**Watch this if:** you use one Claude product and want a clear mental model of everything else in the ecosystem and when each piece applies.

## Key Takeaways
- Framework for the four products: **Chat to think, Cowork to delegate, Code to build, Design to create** — all included in one paid subscription and side-by-side as tabs in the desktop app.
- Cowork and Code both run locally against a folder you point them at; Cowork is "Claude with a to-do list" (emails, documents, file organization), Code builds real software through natural language alone.
- **Skills** are repeatable expertise packages — underneath just a folder of instructions Claude reads first. You can say "package what we went through as a skill" and reuse it across Chat, Cowork, and Code.
- **Connectors** link Claude to Gmail, Slack, Google Drive and hundreds of other tools with permission controls; **Plugins** bundle skills + connectors around a role or tool (e.g. Figma plugin, legal plugin) via Anthropic's plugin marketplace.
- **Projects** carry custom instructions, uploaded files, and auto-refreshing memory — but Chat projects and Cowork projects don't sync (import is possible). Account-level memory applies to Chat only; Code uses a CLAUDE.md file created with `/init`.
- Autonomous layer: **computer use** (Claude operates your desktop), **Dispatch** (control a Cowork session from your phone), **scheduled tasks** (recurring Cowork runs like a morning brief), and **Claude Code routines** (schedule/GitHub/API-triggered runs that work even with your computer off).

## 🛠 Tools & Software
- [[topics/Claude Code]] — the "build" product: apps, automations, Chrome extensions through plain English; CLAUDE.md via `/init`; routines for triggered autonomous runs.
- [[topics/Claude Cowork]] — the "delegate" product: local folder workspace, email/document/file tasks, Dispatch remote control, scheduled tasks.
- [[topics/Claude Desktop]] — the app where Chat, Cowork, and Code sit as adjacent tabs.
- [[topics/Claude Design]] — the fourth, newer product: prompt/codebase/Figma-file in, working prototype, deck, or landing page out; hands off to Code to ship.
- [[topics/Claude Skills]] — repeatable instruction packages usable across all three core products; built-in (e.g. PowerPoint) or self-authored.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the whole video is a tour of the Claude product ecosystem.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Open the Claude desktop app and locate Chat, Cowork, and Code as separate tabs — all covered by the existing subscription.
- Package a workflow you've refined in chat as a skill ("package what we went through as a skill") and reuse it across products.
- Browse the connector list for the tools you already use and wire up one (e.g. Gmail or Google Drive) with scoped permissions.
- Set up a Project with custom instructions + reference files for a recurring area of work instead of re-explaining context per chat.
- Try one scheduled task in Cowork (e.g. a morning brief from calendar + email) and, if you use Claude Code, look at routines.

## 🔗 Related Videos
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Cowork, Claude Desktop
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude, Claude Code, Claude Desktop, Claude Skills
- [[videos/Andrej Karpathy Just Fixed Claude Codes Biggest Weakness]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Cowork
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills
- [[videos/How to Use Claude Code Skills Like the 1 (its easy actually)]] — shared: Claude, Claude Code, Claude Skills

## Timeline
- `0:00` — Claude has grown from a chat box into a full ecosystem; goal: every product, every feature, when to use which.
- `0:26` — The three core products share one subscription; framework: Chat to think, Cowork to delegate, Code to build.
- `1:06` — Chat: conversational thinking partner; syncs across mobile, web, desktop.
- `1:43` — Cowork: point it at a folder, hand it tasks (emails, research, presentations, file organization), review the finished result.
- `2:29` — Code: builds apps, sites, automations entirely through natural language — "now you are a developer."
- `3:15` — Design: fourth product at claude.ai/design; prompt/codebase/Figma in, prototype/deck/landing page out, hand-off to Code.
- `4:41` — Universal layer begins: Skills as repeatable expertise packages, including self-authored ones.
- `6:06` — Connectors: Gmail, Slack, Google Drive, Asana and hundreds more, with a permissions list.
- `6:46` — Plugins: skills + connectors bundled per role/tool; Anthropic plugin marketplace (Figma plugin, legal plugin).
- `7:57` — Projects: custom instructions, file uploads, auto-refreshing memory; Chat and Cowork projects don't sync.
- `9:08` — Memory: account-level memory is Chat-only; Claude Code uses CLAUDE.md generated by `/init`.
- `10:22` — Autonomous layer: computer use, Dispatch (phone control of Cowork), scheduled tasks (morning brief example).
- `11:29` — Claude Code routines: saved prompt/repo/connector configurations triggered by schedules, GitHub events, or API calls.
- `12:00` — Recap of all four layers: products, universal, memory/context, autonomous.

## Transcript
<details>
<summary>Full transcript</summary>

Claude has gone from a box you type into to an entire ecosystem of products, features, and ways to automate, connect, and build powerful workflows. But, the more powerful it gets, the more overwhelming it becomes to understand and use it all. So, today I'm breaking down the entire Claude ecosystem simply. Every product, every feature, and exactly when to use which one. I'll start with the three main products. The flagship tools that are your primary ways to interact with Claude. You've probably heard of each of these, but a lot of people are still unsure of how they're different and when it's best to use each one. So, here's the simple framework. Chat to think, co-work to delegate, and code to build. That's the completely boiled down version. I'll expand on each. The first thing to know is all three come with one paid subscription. So, even if you haven't used the others, you do already have access. They all look and feel similar on the surface. You type into a prompt box and they get to work. But, they each serve very different purposes.

Starting with chat, this is the one everyone's familiar with. You ask a question or give an instruction, Claude responds, you iterate back and forth. It's a conversation. And that's exactly when you want it, when the work is the conversation. Thinking something through, writing, research, working out an idea. It's a partner you work with to help think your way through anything. And these chats sync across mobile, web, and desktop. You can start a chat on your phone and continue it on your computer. Co-work and code are different. Both of these run directly on your computer. You point them at a folder and that's their workspace. And this is where Claude starts becoming more than a chatbot. Co-work is where Claude starts going out and doing things for you. Reading your emails, drafting replies, pulling research together, building documents and presentations, organizing files. You hand it a task, you walk away, and you can come back to finished work. That's the delegate part. You're not in the loop for every little step, you're just reviewing the result.

A simple example is having it organize your messy desktop. It can analyze all the files and images, then organize them into cleanly structured folders. Or something more advanced. Say you have a meeting tomorrow. Co-work can find it on your calendar, read your notes, build the presentation, and draft a follow-up email to send afterward. All without you touching it. Co-work is Claude with a to-do list and the ability to go and check things off. Code is where Claude starts building things for you. Apps, websites, automations, Chrome extensions, productivity tools. It writes all the actual code to create whatever you describe. And before you think, "I'm not a developer, this isn't for me." You interact with Claude Code entirely through natural language. You just describe what you want, and it builds it. Then you ask for changes and new features in plain English. A complete beginner can sip their morning coffee while describing a game or an internal tool or dashboard, then have something working before lunch. So now, you are a developer.

With Chat, Co-work, and Code, the easiest way to access all three together is on the desktop app. When you open it, they'll each be on separate tabs right next to each other. And there is a fourth product called Design. It's newer and feels a little more separate right now, but it is definitely worth knowing about and using. You can find it in the Claude sidebar or at claude.ai/design. You give it a prompt or hand it a codebase, a Figma file, your brand assets, then it gives you back a working prototype, a slide deck, a one-pager, a landing page, even an animation. You don't need to know any design tools, you just describe what you want it to look like. And when you're done designing, you can hand the whole thing straight to Code to ship. The four products all serve different purposes. So, put simply, Chat helps you think, Co-work lets you delegate, Code lets you build, and Design lets you create. These are already incredibly powerful on their own. You could jump in today and get real work done. But, there's a whole layer of features that plug into each of them, and that's where things get really interesting.

If you want to be able to actually implement what I'm talking about with Claude Chat into your work, we have a free guide for you. It's broken into four parts: getting started, core features, real-world applications, then advanced implementation. It also covers use cases like content creation, data analysis, and strategic planning with frameworks and prompts you can use right away. So, whether you're just getting started or trying to level up, there's something actionable in there for everyone using Claude. That's a free guide, just click the link in the description.

Now, on to the features that expand the capabilities of the three core products. What's cool is they work across Chat, Co-work, and Code. And these first three are found by clicking Customize. First, skills. Just think of these as expertise packages that help Claude execute a task in a repeatable, consistent way. And there are a lot of skills built in by default. For example, if you ask Claude to create a PowerPoint, it already has a PowerPoint skill it reads before starting. That way you get a well-designed, perfectly editable deck on the first try without having to explain how you want it formatted. Where it gets really interesting is you can create your own. If you've gone back and forth with Claude getting exactly right, you can just say, "Package what we went through as a skill." Then it builds it for you. From that point on, anytime you do that task again, Claude calls the skill automatically and executes all those steps in the same way. Like say you create content. You could have a skill that writes in your voice and creates a visuals in your brand style. Then you don't have to feed it that context and custom prompting every time. And you could use that skill in Chat when you're drafting something, use it in co-work to automate content creation, or build it into a custom tool through code. You can use the same skill to create in a consistent style across all three products. And what this really is underneath is just a folder of instructions and guidelines that Claude reads first. That's it. Then you have a reusable workflow that never has to be re-explained.

Next is connectors. These link Claude to the tools you already use: Gmail, Slack, Google Drive, Asana, and then hundreds more. Just search the list for whatever you use, and they'll most likely already have a connector built in. Just click connect, sign in to your account, and Claude can now directly take actions through that tool or pull data from it. And you control what access it has through a simple permissions list, so you're always in control of what Claude can and can't do. And just like skills, these work across all three products. Pull in data to ask questions about in chat, automate tasks that use those tools in co-work, or build them into custom personalized tools through code.

Then there are plugins. The easiest way to think about these is skills and connectors bundled together around a specific role or tool with some additional instructions on top. Anthropic has a whole plugin marketplace with pre-built bundles for specific use cases. Like take the Figma plugin. It bridges the gap between Claude and a design workflow with skills that create in the right formats and connectors that pass information back and forth between the two. Or there's a legal plugin for legal teams. It comes pre-loaded with skills for drafting briefs and contracts, organizing research, and managing knowledge. Plus the connectors those workflows depend on. There's a huge library of these for specific roles, tools, and industries. If there's a part of your workflow that feels repetitive, see if there's a plugin for it. These are all related and easy to mix up. So, skills help you repeat tasks, connectors connect your tools, and plugins bundle those together.

Next, there's a group of features that work differently depending on which product you're on, but each help to give Claude memory and context. The first one completely transforms how useful Claude can be, and most people don't bother to set them up. Projects. These are folders for organizing related chats, which is already useful, but they're far more powerful than that. Inside each project, you can add custom instructions that guide how Claude behaves. Then you can upload files that give it additional context, and it comes with built-in memory that refreshes automatically. So, Claude remembers across every conversation in that project, and then learns more over time. You can go as deep or shallow as you want. At the simplest level, it could just be a way to organize all your chats around a topic, or you could build something much more powerful like a full marketing project with custom instructions about your writing voice and tone, skills you want it to use, brand guidelines, and the uploads, a list of clients, past campaign results, and your content calendar. Then every time you open that project, Claude already knows all of that. You don't have to start from scratch in each new chat. Your context persists, so it's always loaded and ready. And one thing to note, projects in chat and projects in co-work are separate from each other. They work the same way, but they don't sync. Although you can import a project you have in chat over to co-work instead of having to copy-paste.

And now I mentioned memory within projects. Claude updates that automatically each day and carries it across every chat in that project, but there's also account-level memory, which works the same way but across your entire account outside of projects. But that one only applies to chat. It's not like a unified memory layer across all three products. It's Claude chat's way of knowing you over time, your preferences, how you like to work, context about your life and business. Memory in Claude code works differently. Instead of automatic memory, Code uses something called a cloud.md file. I won't spend much time on this, but once you have a project going, you just type /init and Cloud analyzes everything in the folder and your conversation and then creates the file for you. It lives right there in that project folder alongside your code and it holds all the persistent context about that project and updates it as you work. So, that file is like a project brief with everything Cloud needs to know to keep building consistently. Some people do also create cloud.md files manually for their co-work projects. They work well there, too. So, projects persist your context, memory learns who you are, and cloud.md briefs Cloud Code or co-work on how to work.

Cloud has also been building in features that work without you, where Cloud doesn't have to wait for you to prompt it. Computer use is exactly what it sounds like. Cloud can take control of your desktop, opening apps, navigating browsers, filling out forms, and moving files. You just give it a task and it operates your computer to complete it. You know, it's still early, so you will run into some issues, but it's a glimpse at where these tools are headed. Dispatch lets you control a co-work session from your phone. You can kick off a task, check in, or redirect it from wherever you are. Scheduled tasks is the one to pay attention to right now with co-work. Instead of kicking off tasks manually every time, you can set them up once and then have Cloud run them automatically on a schedule. A simple example is a morning brief. Cloud checks your calendar, scans your email, pulls in anything relevant from your connected tools, then has a full summary waiting for you before your first meeting. But, it can go well beyond that. A weekly competitive research report, a daily social media draft pulled from your latest content, an end-of-day summary sent to your team. Anything you find yourself triggering manually on a regular basis, scheduled tasks can handle on its own. Cloud Code has its own version of this, too. Cloud Code routines allow you to save configurations of prompts, repositories, and connectors and set them to execute automatically without having to leave your computer on. You can trigger them using schedules, GitHub events, or API calls. And that one is more for experienced Cloudcode users. Computer use gives Cloud control, dispatch takes CoWork remote, scheduled tasks automated, and routines trigger code automatically when your computer is off.

So, that is a lot and there was some advanced ones at the end. So, here's a recap of the full picture. Four products, chat to think, CoWork to delegate, code to build, design to create. Then there's a universal layer that helps you repeat with skills, connect your tools, and bundle with plugins. Then a context and memory layer that lets you persist your work, learn over time, and brief Claude on how you work. Then an autonomous layer where Claude can control your desktop, go remote, automate CoWork, and trigger code to run on its own. That's the full Claude ecosystem. I have videos going deeper into each product. So, I made a Claude ecosystem playlist with those, so it's easier to dive into whichever one you think applies to you most.

</details>
