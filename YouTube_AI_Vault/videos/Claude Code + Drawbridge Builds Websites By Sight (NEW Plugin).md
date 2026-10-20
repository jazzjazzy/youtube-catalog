---
title: "Claude Code + Drawbridge Builds Websites By Sight (NEW Plugin)"
video_id: K0j_ADBkN9I
channel: "[[channels/Jay E - RoboNuggets]]"
uploaded: 2026-03-26
processed: 2026-07-05
duration: "8:51"
url: https://www.youtube.com/watch?v=K0j_ADBkN9I
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [visual-bug-annotation, remote-agent-control]
tools: [Drawbridge, Claude Code, Chrome, Cursor, Telegram, Rubric]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code + Drawbridge Builds Websites By Sight (NEW Plugin)

![thumbnail](https://i.ytimg.com/vi_webp/K0j_ADBkN9I/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=K0j_ADBkN9I) | 📅 Uploaded [[uploaded/2026-03-26]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Jay demos Drawbridge, a free open-source Claude Code + Chrome extension that lets you draw and comment directly on your live browser UI so your agent sees exactly what to fix instead of you describing it in text. He installs it, annotates a real app he's building, and triggers the fixes remotely through a Telegram-connected Claude Code session.

**Watch this if:** you keep failing to get an AI coding agent to fix a visual/UI bug through text descriptions alone.

## Key Takeaways
- Drawbridge is a free, open-source Claude Code + Chrome extension: you annotate or comment on any element visible in your browser, and the agent (Claude Code) reads those annotations and implements the fix.
- It solves the "describing visuals in text" problem — models are good at code but still lack refined visual taste, so pointing/annotating beats prose descriptions.
- Two annotation modes shown: Comment (`C`) to leave a text note pinned to an element, and Annotate (`R`) to mark up a region — both get queued with a screenshot for the agent to pick up.
- Comments are written to a clean markdown file (`mot_tasks.md`) plus a `.mot` folder with per-task JSON (title, comment, bounding region, screenshot path) — a standardized visual feedback format for the agent to consume.
- Under the hood, Drawbridge gives the agent more than pixels: the screenshot, the underlying HTML, and your comment together, so it can pinpoint exactly what to change.
- Three run modes: step (one task at a time, pauses for approval — max control), batch (groups related tasks, one approval per batch), and yolo (fully autonomous, no approvals).
- Jay controls his long-running Claude Code session remotely through a Telegram bot, so annotations made in the browser get picked up simply by messaging "I made a few more comments on Drawbridge, can you pick them up?" from his phone.

## 🛠 Tools & Software
- [[topics/Drawbridge]] — the free open-source Claude Code + Chrome extension for annotating UI directly on-screen; installed, demoed, and explained end to end.
- [[topics/Claude Code]] — the agent that reads Drawbridge's markdown/JSON task queue and implements the visual fixes.
- [[topics/Chrome]] — hosts the Drawbridge browser extension (loaded via Chrome's developer-mode "load unpacked").
- [[topics/Cursor]] — mentioned as an alternative agent that can also be pointed at the Drawbridge repo to guide installation.
- [[topics/Telegram]] — used to remotely message a long-running Claude Code terminal session so Drawbridge comments can be triggered from a phone.
- [[topics/Rubric]] — teased as the presenter's own visual "command center" console for explaining agent architecture (AGENTS.md, skills) to non-developers.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Point Claude Code or Cursor at the Drawbridge GitHub repo and let it walk you through installation.
- Load the Drawbridge Chrome extension manually via `chrome://extensions` → Developer mode → Load unpacked, then connect it to your project's local workspace folder.
- Use Comment/Annotate mode to mark up a live UI issue instead of writing a long text description or taking manual screenshots.
- Pick step mode while you're still trusting the tool, and move to batch or yolo once you're confident in its fixes.

## 🔗 Related Videos
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Chrome, Claude Code
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Chrome, Claude Code
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Chrome, Claude Code
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Chrome, Claude Code
- [[videos/Claude Code 'Interview' Mode in 6 Minutes]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Cursor
- [[videos/Claude Code 2.0 Has Arrived (It's Insane)]] — shared: Claude Code, Telegram

## Timeline
- `0:00` — The problem: describing visual UI bugs in text doesn't work well with agents.
- `1:10` — What Drawbridge is: a free Claude Code + Chrome extension for on-screen annotation.
- `2:10` — Demo: annotating a drop-down and icon color/icon-type change in a live app.
- `3:20` — Sending the annotations to a Claude Code session via Telegram and watching it work.
- `5:05` — How to install Drawbridge, including the manual Chrome extension load step.
- `6:05` — Under the hood: `mot_tasks.md`, the `.mot` folder, and per-task JSON with screenshot + HTML context.
- `6:45` — The three run modes: step, batch, and yolo.
- `7:50` — Why visual interaction layers (Drawbridge, Rubric) are a growing trend for working with agents.

## Transcript
<details>
<summary>Full transcript</summary>

So, you're trying to fix something on your website with your AI agent and it just doesn't get it. And you describe it again, but it's still wrong. The problem isn't your agent. It's that you're trying to explain something visual in text. And it's pretty much the difference between texting an employee that something looks off on this particular page versus just pulling up their screen and pointing at it directly. Well, there's a free Claude Code extension called Drawbridge. You draw directly on your screen, annotate the problem, and your agent sees exactly what you mean without you having to describe it in big blocks of text. In this video, I'll show you how to install it and how you can use it to improve the way you work with your AI agents.

So, what is Drawbridge? It's a free open-source Claude Code and Chrome extension. Where if you're, for example, creating your website, your app, or your dashboard, you can pretty much annotate anything visible in your browser and your AI agent like Claude Code reads those annotations and implements the fixes for you. And it solves the problem of miscommunication between you and your agents, especially when it comes to visual design. Because even though AI models are really great at code, they're not yet that great when it comes to visuals. They don't have that perfected human taste yet.

And just to demo it quickly, what I have here is a mini app that we're developing for our community that basically replicates Higgs Field or Google Flow Studio and puts it right within your AI agent's command center. And right here on my Telegram where I have my Claude Code session connected, which if you're curious how this works, it's basically a long-running session that I have here in my terminal where I have Claude Code connected. And essentially, when I send a message here on Telegram, it just sends it here. So, it's just much more convenient, at least for me.

And usually, let's say I want to move this drop-down to the left so that it's beside these options here. Is I would need to either describe it through a long prompt just to be specific that this is what I wanted to move. Or if I wanted to change the color of these icons, then I can either describe it or take a screenshot of each and every one of these and send it to my agent. But since I have this Drawbridge extension installed, so you can see I just press that and that brings up this panel of to-do. What I can do here is, let's say I want to do a comment, so I can just click on C and that will immediately let me choose the elements on this website. So, let's say this one. Hey, so this particular drop-down, I wanted I think it's in the middle for some reason. Let's put it right beside the rest of the filters here on the left, please. And then apart from that, you can also do an annotate by pressing on R. And let's say this particular icon. So, can you turn all of these icons into yellow? And actually, change the icon to be that of an image as well. Because I think right now it is not yet as descriptive. Again, if I submit that, that will just add another queue with a screenshot.

So now, if I go back to my Claude Code agent, I can just say, "So, I made a few more comments on Drawbridge. Can you just pick them up?" And if I send that, basically, the agent will get to work. And on Telegram, a lot of the processing is already abstracted. But if you look at what's happening under the hood here, what it's basically doing is it received that message from me on Telegram and then it immediately saw those two tasks that I assigned to it along with the screenshots for it to specifically know what it is that I'm talking about. And the other thing that it's doing for more visual tracking is it actually changed those tasks as doing so that you know that it is currently doing these particular tasks and then will mark them as done. So, you can see I have a couple of here already that I was testing. And there you go, now it says that these are done. So, if we refresh this, it was now able to specifically adjust that drop-down that we wanted it moved and for it to be an icon connoting an image.

So, I just found this to be a really useful, especially if you need to spot correct any changes on your visual interface. Like if you're developing a website, a web app, and you can't seem to pin down that particular change that you wanted, then being able to annotate your screen and show your agent exactly what you're talking about, I think is a big plus. And also, just the ability to batch all of these tasks together makes it a bit more seamless, I think. And you can also move these, by the way. So, if you want this to be docked to the left, that is entirely possible as well.

Now, real quick, we just released the Agentic AI masterclass for our members at Robo Nuggets, which takes you from zero to mastery when working with agents. There's a link to the community in the pinned comment below. We've got founders in there who landed their first client in weeks, live build sessions where we create this stuff together, and the actual templates behind what I showed in this video. The community is also the reason these lessons get made, so see that below if that's for you.

So, how do you install it? Well, the good news, as I said, is it is completely open-source thanks to this developer who published it in this link. And if you give that to your Claude Code or even Cursor instance, then it can guide you on how to install it. The only manual thing that you need to take care of is that it does come with this Chrome extension, right? And if you haven't installed a Chrome extension yet, all you need to do is to go to Chrome extensions, enable developer mode, and if you click on load unpacked, if you navigate to the folder of Drawbridge that your agent will copy for you, you can just choose this Chrome extension folder and select that. And once you do that and this extension is enabled, you will now have Drawbridge as a Chrome extension in your browser.

Now, the first time that you run this, it will ask you to connect to a local folder. And what you just need to do there is to connect it to the workspace that you are setting it up on. So, for example, I'll just connect this to this folder called Robo because that is the workspace that we are using Claude Code in. And if you select that, that will now fully set up Drawbridge for you. So, it's really easy and quite effective, honestly.

Now, since you're installing this, you might be curious on how it works under the hood. And basically, what it does is everything that you annotate and make a comment on, it lands in this clean markdown file in your project folder, the one that you just connected to Drawbridge. And it's called mot_tasks.md. And what that includes is the comment you just made, as well as a screenshot of that specific part of your UI. And that is basically what the agent reads. And if you want to see what that looks like, that is available in this .mot folder, where you can see here the running log of tasks that I assigned it to. And then for each of these tasks, there is just a bit more detail here in this JSON file that describes the title, what the comment is, the specific bounding region of that comment that you just made, and also a path to the screenshot. So, it's basically standardizing the way that you give these feedback points that are visual for your agent. And once you have it installed, for you to invoke it, all you need to do is to just say to your agent that you made some comments on Drawbridge and it will be able to pick that up.

Now, if you're designing user interfaces a lot, you might want to also know the three modes that you can run this Drawbridge plugin with. Because if you're a power user, you can actually choose between step, batch, or yolo every time you run Drawbridge. And just to explain these three simply, step is basically one task at a time. So, the agent fixes your first comment, it pauses, it waits for your approval, and it gives you the maximum control. And then batch just does as the name suggests. So, it allows your agent to group related tasks together and just have one approval per batch. It is faster than step, but it still gives you checkpoints. Now, yolo is basically fully autonomous. It processes everything without approvals. And the way that you select these modes is simply by telling Claude Code to do it.

And so, for this UI, you can see I just made two more comments. Hey, I just made a few more comments on the UI. Can you run Drawbridge in step mode, please? And when I do that, you can see that it is running through those two tasks for me one by one. So, for the first one, it told me that it's done. And here you can see that the name changed to sprint demo, which is what was my comment about. And then if you go to two, it would now apply the change as well. So, this is pretty useful, especially if you are trying to double-check what it's about to do and do some further polishing to your visuals. And when that's done, it just cleared the log here and it applied the change that I wanted. So, instead of a percentage, it now says five of 14 done, which was what my comment was about.

And by the way, you can see here when it did the step mode, you also see why this is much better than just taking a screenshot of your particular ask and giving it to your agent. Because if you just take a screenshot, all that really gives your AI model is just pixels. But now with Drawbridge, what's actually good about it is apart from the screenshot, it also gives the HTML, it gives your comment, and a lot of that context so that it can pinpoint exactly what it is that you're trying to change.

And this is quite interesting, right? Because I think Drawbridge is one signal in a much larger trend. Cuz we're building more and more tools to interact with AI agents visually instead of just relying on an IDE or the terminal, which is quite intimidating for most people and also a bit difficult to work with, especially if you're working on it visually. And that's also the reason why we're developing this Rubric console for our community, as well as when we do AI training, by the way. Because it's just so much more easy to visualize everything in a modality like this versus showing companies and clients a wall of code using the terminal view or the IDE view. Because with this visual layer, you can explain quickly what an AGENTS.md is and how it functions in relation to the core of the agent. And also, what skills are and also the fact that they are simply just markdown files that the agent reads. So, I think this whole visual trend will continue as companies like Anthropic are clearly developing these tools like Claude Code to be usable even by non-developers. And this whole Rubric command center, we're also making it available to our community members, by the way. So, if that's something you're interested in, then you can just check that out in the pinned comment below. Or if you want to learn more about how AI agents are architected, then you can watch this video next. That's it for this one. I'll see you guys next time.

</details>
