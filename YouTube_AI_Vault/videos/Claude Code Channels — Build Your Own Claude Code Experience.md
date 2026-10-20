---
title: "Claude Code Channels — Build Your Own Claude Code Experience"
video_id: 1NnpC6NlNmg
channel: "[[channels/Matt Maher]]"
uploaded: 2026-03-26
processed: 2026-07-05
duration: "15:32"
url: https://www.youtube.com/watch?v=1NnpC6NlNmg
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [remote-claude-code-access, custom-mcp-channel-building]
tools: [Claude Code, Cursor, VS Code, Discord, Claude Agent SDK]
llms: [ChatGPT]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Channels — Build Your Own Claude Code Experience

![thumbnail](https://i.ytimg.com/vi/1NnpC6NlNmg/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=1NnpC6NlNmg) | 📅 Uploaded [[uploaded/2026-03-26]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Matt Maher explains Anthropic's new Claude Code "Channels" feature — an open architecture that lets external tools (Discord, Telegram, iMessage, or a custom app) talk to a running Claude Code session. He demos the built-in Remote Control feature, an official Discord channel, and then builds his own custom web app (chat + file browser) that connects to Claude Code through a self-built MCP server.

**Watch this if:** you want to reach a running Claude Code session from your phone or a custom interface instead of being tied to your desktop terminal.

## Key Takeaways
- The "folder process" (consolidating all context into one place for Claude Code) makes a desktop session extremely powerful, but also ties you to your desk — Channels is Anthropic's answer to that tension.
- Remote Control (Claude mobile/desktop app) lets you view and message the same running Claude Code session from anywhere, fully secured through Anthropic's own auth layer — but it's read-poor: you can't browse files or see much beyond chat output.
- Anthropic shipped official Channels integrations (Discord, Telegram, iMessage) plus a reference application showing exactly how to build your own channel via MCP.
- A channel is just an MCP server that Claude Code listens to; whenever the external source (Discord, a custom web app, etc.) sends a message in, it flows directly into the live session.
- Matt builds his own custom "channel app" — a full UI with chat, a document viewer, and a file tree — connected to his running Claude Code instance through one MCP server, using `--dangerously-skip-permissions` in development mode.
- The bigger pattern: Claude Code acts as the back-end "engine" (memory, context, tools, file access) while you wrap any UI you want around it via the open channel architecture — no need to rebuild session/context management yourself.
- This fits a broader Anthropic philosophy of open, inspectable architectures (MCP, computer use via accessibility APIs, and now channels) that invite developers to build against them.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the running session/back-end engine that Channels connects external interfaces to; also the tool being extended.
- [[topics/Cursor]] — mentioned as part of the presenter's usual desktop coding setup alongside Claude Code.
- [[topics/VS Code]] — mentioned as an alternative editor he sometimes uses instead of Cursor in his daily workflow.
- [[topics/Discord]] — demoed as one of Anthropic's official Channels integrations; messages sent from Discord are relayed into the live Claude Code session.
- [[topics/Claude Agent SDK]] — referenced as the kind of agent SDK you'd otherwise have to hand-build session/context/tool management for, which channels avoid needing.

## 🤖 LLMs Mentioned
- [[topics/ChatGPT]] — compared to the mobile Claude experience: "just as smart" on a phone, but lacking the tuning/context of the desktop Claude Code session.

## 📡 Protocols & Standards
- [[topics/MCP]] — the underlying mechanism for Channels: a custom channel is built as an MCP server that Claude Code sessions connect to.

## ✅ Action Items
- Try Claude Code's built-in Remote Control from the mobile or desktop Claude app to message a running session away from your desk.
- Set up the official Discord channel plugin to relay messages between a Discord bot and a live Claude Code session.
- Use Anthropic's reference channel application as a template to prototype your own MCP-based channel (chat UI, file browser, or dashboard).
- Run new channel apps with an explicit dev-mode flag rather than skipping permission checks blindly, and treat it as experimental until stable.

## 🔗 Related Videos
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Agent SDK, Claude Code, Cursor, Discord
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor, MCP, VS Code
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude Code, MCP
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor, MCP
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude Code, MCP, VS Code
- [[videos/Claude Code Skills Just Got Even Better]] — shared: ChatGPT, Claude Code, VS Code
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Cursor, MCP
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Cursor, MCP

## Timeline
- `0:00` — Intro: how a great Claude Code desktop setup ties you to your desk.
- `2:06` — The "folder process" — consolidating notes, code, and references into one context source.
- `4:13` — Answer 1: Remote Control via the Claude mobile/desktop app, demoed live.
- `7:04` — Channels example: Discord — setting up a bot and relaying messages into Claude Code.
- `9:19` — "Write your own" — the open MCP-based channel architecture and reference app.
- `10:16` — Matt's custom Channel App: chat, document viewer, and file tree wired to a live session.
- `13:22` — Conclusion: Claude Code as a back-end engine, and why the open-architecture pattern matters.

## Transcript
<details>
<summary>Full transcript</summary>

So, this is going to sound a little bit crazy, but the better your AI setup gets, the more it kind of ties you to your desk. And I don't mean that casually. If you've done the work, if you've consolidated your context and set up your tools, built a real working environment with something like Claude Code or maybe Cursor, then you've created something probably incredibly powerful to you, and you've also created something that works best when you're sitting right in front of it. So, Claude Code shipped something recently called Channels, and it changes how you interact with your AI from anywhere. I'm going to show you what Channels are, how the built-in ones work, and then incredibly, in a very short period of time, how I built my own. I built a full application using the Channels architecture very easily. And that's where this really gets interesting.

But first, let me show you how the best setup with AI actually starts to lock you to your desk a little bit. If you've seen any of my previous videos recently, you know I talk a lot about what I call the folder process. And I won't bore you, but the short version here is that you take all the context that matters for a piece of work, your notes, your documents, your code, your references, whatever it is, and you consolidate it into one place where AI can touch all of it at once. That's a super bloom event. The amount of intelligence you can bring to bear on your problems when everything is consolidated and accessible is actually transformative. But once you've built that fantastic localized work environment, you're right back at your desktop. You need your computer all the time because that's where your most useful collaborator lives with all of its context. I mean, I can open ChatGPT on my phone, and it's just as smart as the Claude Code session on my desktop. But the desktop session with all of the tuning, the tools, the memory, and the context is a million times more useful. And that's the tension. The folder process made your desktop incredibly powerful, and it also anchored you to it.

So, I want to very briefly show you what it looks like when I do work. I have Cursor here open. It might be Visual Studio Code or something like that on any given day. And inside of there, I have Claude Code open in basically a terminal window in the middle. This is how I always work. This is what my environment looks like. And the vast majority of the work I do these days, with or without code, is done exactly like you see here, because this is my favorite collaboration mechanism. So, what you're seeing is a content-in folder, just the way I organize it. I put all of my walks and all of the information that I want to put in as context. Now, what you're seeing here is this literal project, the script and the understanding, and in fact, the application that I wrote for the communication tools, really for the Channels stuff that we're talking about right here. These are all the different walks, and really kind of the prompt for building the Channel app. What happens then is Claude here will actually write all of its outputs into the output folder. So, what it's doing is it's constantly creating kind of consolidations and reads and understandings, and then we kind of flow-edit that on an ongoing basis. So, there's a bunch of back and forth that's going on here, and that's the actual secret — I need to freely be able to give it what I think is important, and then we work together toward kind of a common goal.

But okay, so let's run an example here. Take a look at all of my walks and the final script, and name five things that didn't make it into the final script that it feels like I really thought were really important in the walks. Okay, and here it is. What does it tell us that we're not going to talk about? We're not going to talk about zombie processes and MCP life cycle concerns. All right. Channel as an automatable interface, the subscription cost angle, code work done right, the meeting notes example, and a concrete why. Sorry about that. This is the full experience. When I'm here at my desk with this in front of me, this is the best AI working experience I've ever had. The problem is really now when I walk away from this.

So, Anthropic's first answer to this was something that they called remote control. And it's good. I use it actually pretty frequently. I think it's actually a great feature. The idea is simple. When you've got Claude Code instances running somewhere, like on your machine, you can connect to it from the Claude mobile app or their desktop app, which is kind of an interesting pattern. You're looking at the same session, the same conversation, and you kind of keep interacting with it just the same way that you would if you were standing in front of it. It's completely secured through Anthropic's own authorization. You're not opening a port on your machine. The connection stays at Anthropic's layer. You log in with your account, and you see your running session.

So, really cool. Let me show you what that looks like just for a second so that we can see. Okay, so let's do this quickly so that you can see. I can rename this instance down here and call it script. Just so that we know what it is. You'll see it puts a nice little tag here. I come to — let's use the desktop client, but this would be my mobile client. In fact, why don't we pull up the mobile client? It might be more obvious using that. And say, "Okay, so we want to go to Claude Code." This is actually using my mobile phone here that's connected. So, this is a real connection through my mobile phone, not on the desktop here. And you can see that we have this idle script conversation going on here. If I go into it, the last thing that was said here is five, the meeting notes example, and the meeting notes example. I can say, "Hello." And it does hello, or I can say, "Give me the info from the walk time estimate output." And that's a file down here. And you can see it's just poking my information directly back into the conversation. It's outputting it here, as well as outputting it on your mobile device. So, this is remote control, and it's really a way to disconnect and continue working.

So this session works perfectly well with the Claude app. Definitely not a bad thing. But really, the biggest shortcoming and difficulty here is I can't actually see files. Now, I happen to be reading these over here and could see that I had a file called walk time estimate, so that's what I named up here. I though can't really see all of the files. I can tell Claude here to list the files for me, tell me the names of the walks we have, tell me which one is which, read them out to me, print them out here. So, you can get your way into some of the files that are being created, but it's pretty painful. So, this is really actually truly just a remote control. You might want to throw in information and say, "Can you do this?" Watch it work, make sure it's doing what you want it to do, and then just let it kind of work. You can't really execute and see anything here. And it's also very difficult to kind of create new files from here. So, it isn't the desktop experience. It's not really meant to be, but that is one of its shortcomings.

Okay, so let's take a very quick look at some of these official channels. One of the official channels is Discord. Adding the Channels kind of identifier and a channel that I want to allow, which is one of the plugins that Anthropic released with this, which is a Discord. I will come into this, and it's telling me that it's listening for channel messages from Discord. It's experimental, inbound messages will be pushed, yada yada yada. Let's take a look at Discord. Over here, I've gone through a little bit of gyration to create a bot and app that is called Channel Test. It's just the name of the bot that I've added, and I've made a relationship between the two. Pretty simple, but a couple extra steps. But now, when I push a message in through here from Discord, of course, we see it happening in the background, and it's going to go count all of the different walks that we have, and it will come back. And hopefully, and it sends back, "Hey, there are seven walks." All right. So, in any case, now that it's hooked up, not the easiest thing in the world to do, then it's going to work. And this might work because I use Discord already. I have it on my phone, those kinds of things. So, this might be the way that I communicate back and forth.

What Channels actually is, at the simplest level, obviously, is just another way to communicate into a running Claude Code session. So, your Claude Code instance basically says, "I want to listen to this message source." And then, whenever that source, Discord, Telegram, iMessage, or even a web app, sends information in, that message, of course, comes directly in, like we've already seen. So, that works, and those three channels are useful, but they're not really the point. What Anthropic also shipped alongside those is a reference application. It was a web kind of application that you can pull up, a working example of showing exactly how Channels are built and how to build your own MCP. The architecture is open, and anyone can build a channel now. And that's the real play. They didn't just give us three messaging integrations, they gave us the blueprint and said, "Go build your own interface into a running Claude Code session."

So, I took that as a challenge. All right, so I'm going to show you this very briefly. You don't really need to care about this. This though is the amazing thing that I think Channels is actually doing for us. You can see here that right now, I'm having to call Claude with a dangerously load development channels, and then the name of the channel app that I have. And my channel app is just listed right up here. So, we're going to run this, and you'll see it will come in and say, "We've noticed that you're running this dangerously load kind of thing. Are you sure you're in dev mode right now? I think I'd prefer you use this." So, I'm going to say, "Yes, I'm in development mode." So, this is just only for development right now. I have no idea how I become a non-experimental and become an official server, what that looks like going forward. This is the current path. So, what we just did when we ran this, is it ran an MCP server. Inside of my MCP server also runs a web server. So, they're paired together. You don't have to worry about that, but what it gives us is an opportunity to build our own application.

And so, what I'm sharing here is an application that I very quickly built. I just asked it to build out kind of a control panel for the MCP communication that we're doing. So, that's all this will send to and a list of the files and things like that. So, we can say hello here and what we should see in the background back here as we've been noticing before is the hello coming through our channel app. That again is just a name that I called it. And so, it is connected to this repository proper and I can see things within here. So, if I came and said how many walk files are there? Then of course, that goes through, comes back and responds with how many hopefully seven walk files there are. So, there are seven walk files in the content-in directory. And if you come over here, we can see indeed there are seven walk files inside of this directory.

Um and so, I wanted to show you this was a very easy system to build and in fact, I used almost exclusively this application that I built to then work back and forth to create all of this extra context for the application or for the script that we're going through. This is really eye-opening. The idea that I'll be able to host this on my local server and just have this running against a local repo that can always be open, but I actually have behind the scenes the full-blown version of Claude Code with all of the context that I'm used to working with. And then of course, I can turn this into a web app and allow it to deploy outside of my environment if I like. So, I can open up a port so that I can get to it on my phone. All of these kinds of things become available to us as we can see here. And so, that's the full circle. This is again my actual phone. I can walk around and use this and I'm always connected with the full-blown version of what's going on. Now, admittedly by definition, you can't see anything. I had to build the availability to be able to see the different files, those kinds of things. That was just something that I asked for. It is very very similar to what we were seeing with a remote control, except we now have the capability to write whatever we want.

And this is a way to actually think about building actual connectivity to Claude Code instances inside of applications instead of trying to create your own version of that same agentic framework or kind of harness inside of an application. If you've ever used Claude SDK or any kind of other agent SDK and you're trying to build all of those moving parts, you're not going to do as good as something like Claude Code, of course. So, you may as well just connect to it if you can. And of course, the thing is anyone can do this. The channel architecture is open. You build an MCP server that follows three rules, point it at Claude Code sessions and you've got a channel. What you put in the other end is up to you. I built a chat app that you can see with file browsing, but someone else could build a mobile app, a CI integration, monitoring dashboard. Really, whatever makes sense for the work that you have in front of you.

So, step back for a second and think about what we just saw because this is the part that I think matters more than any single feature. We saw Claude Code running as a back-end engine. It's doing all the hard work, the memory, the context, the tools, all the things we're used to from Claude Code, file access, history, and everything else. Everything that makes it powerful. And I wrapped a UI around it using a channel. I didn't rebuild session management. I didn't rebuild context handling. I just connected to the running harness and built the interface I wanted. And this is the same pattern that Anthropic keeps repeating. MCP is an open standard. Anyone can build servers and clients. Computer use is built on accessibility APIs, open and inspectable. And now channels, open architecture, build what you want. They keep building things that can be built against. And I don't think it's an accident. I think that's an architecture philosophy. And if you're paying attention to where this is all going, dispatch, headless sessions, persistent instances, channels is one layer in a stack that's going to keep growing. The distance between Claude Code in my terminal and Claude Code as a service I can reach from anywhere through anything is getting shorter. And channels is a big step in that direction.

Okay, so channels might not be something that you need today. Some people do, some people don't. If you're working at your desk with Claude Code right there at your terminal, you're already really using the best experience you could possibly use. If you don't have a need to escape that, you're awesome. Keep going. But understanding what Anthropic is building here, the open layers, the architecture that invites you to build against it, that might matter quite a bit because the next time you walk away from your desk and you wish you could reach your system, channels is how you get there. And what you build with it is entirely up to you.

All right. If you like this kind of stuff, I just keep sharing it. This is the kind of stuff I love doing. This was all an accident discovery when I looked into channels. So, I just wanted to share what I was seeing. Please subscribe. Thanks for coming along for the ride on this one and I'll see you in the next one.

</details>
