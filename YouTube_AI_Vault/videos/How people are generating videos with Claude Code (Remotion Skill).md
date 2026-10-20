---
title: "How people are generating videos with Claude Code (Remotion Skill)"
video_id: 7OR-L0AySn8
channel: "[[channels/Leonardo Grigorio - Build & Ship with AI]]"
uploaded: 2026-01-22
processed: 2026-07-06
duration: "4:56"
url: https://www.youtube.com/watch?v=7OR-L0AySn8
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [ai-video-generation, remotion-agent-workflow]
tools: [Remotion, Claude Code, Bun, Tailwind CSS]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# How people are generating videos with Claude Code (Remotion Skill)

![thumbnail](https://i.ytimg.com/vi_webp/7OR-L0AySn8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=7OR-L0AySn8) | 📅 Uploaded [[uploaded/2026-01-22]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Remotion shipped agent skills that let you generate entire animated videos by prompting Claude Code in the terminal; the video sets up a fresh Remotion project with Bun and Tailwind, installs the Claude Code skill, and prompts an agent to build a YouTube-UI animation from scratch, then iterates by screenshotting the render and feeding it back to Claude to fix a misaligned cursor.

**Watch this if:** you want to generate motion-graphics style videos by describing them in natural language instead of hand-coding animations.

## Key Takeaways
- Remotion now ships agent skills for multiple coding agents (Claude Code, Codex, Cursor, Gemini, Antigravity) that teach the agent how to build Remotion compositions.
- A new project starts with `bun create video`, choosing a blank template and Tailwind, then `bunx skills add remotion-dev/skills` (or npx) to install the agent-specific skill — the video installs the Claude Code variant.
- After `bun i` to install packages and `bun dev` to launch the local Remotion preview (localhost:3000), Claude Code is run with `--dangerously-skip-permissions` and prompted directly to build the animation.
- A single natural-language prompt ("create a web window interface that is opened inside of a YouTube video... [channel name]") produced a working YouTube-UI mockup with a typing terminal animation in a couple of minutes, entirely without hand-written code.
- Iteration is done visually: screenshotting the rendered output and sending it back to Claude Code to fix issues (e.g. "the cursor should be bigger and it isn't exactly on top of the buttons") rather than describing the bug in words alone.
- Reminding the agent of your toolchain matters — the presenter had to explicitly tell Claude not to run `npm run dev` (already running) and to use Bun instead of npm.
- The result wasn't perfect (cursor still didn't land precisely on the like/subscribe buttons) but produced a nearly complete animated interface from a single conversational session — described as "absolutely fantastic" for a non-sponsored, from-scratch build.

## 🛠 Tools & Software
- [[topics/Remotion]] — the video-generation framework whose new agent skills are the subject of this video; used to scaffold and render the animated composition
- [[topics/Claude Code]] — the coding agent prompted (with `--dangerously-skip-permissions`) to build the animation and iterate on screenshots
- [[topics/Bun]] — package manager/runtime used to scaffold the project (`bun create video`), install packages (`bun i`), and run the dev server (`bun dev`)
- [[topics/Tailwind CSS]] — chosen as the styling option when scaffolding the new Remotion project

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Scaffold a new Remotion project with `bun create video`, pick the blank template, and enable Tailwind.
- Install the Claude Code Remotion skill via `bunx skills add remotion-dev/skills` (or the npx equivalent).
- Run Claude Code with `--dangerously-skip-permissions` inside the project and prompt it directly to build a specific animated composition.
- Iterate by screenshotting the rendered output and sending the image back to the agent with a specific visual complaint, rather than describing bugs purely in text.
- Explicitly tell the agent which package manager and dev-server commands are already running so it doesn't spawn conflicting processes.

## 🔗 Related Videos
- [[videos/Claude HeyGen Just Changed Content Creation Forever]] — shared: Claude Code, Remotion
- [[videos/Claude Ralph - The Bizarre Anthropic Plugin That Every Developer Is Missing]] — shared: Bun, Claude Code
- [[videos/The Claude Code Skill Boris Cherny Runs on Every Project]] — shared: Claude Code, Remotion
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Bun, Claude Code

## Timeline
- `0:00` — Intro to Remotion Agents: what the new agent skills enable
- `0:34` — Installing Agent Skills: `bun create video`, template/Tailwind choice, skill install
- `1:32` — Prompting the Interface: one-shot prompt to build the YouTube-UI animation
- `2:31` — Fixing Cursor Animations: screenshot-driven iteration to align the cursor with buttons
- `4:20` — Final Result & Review: watching the rendered output and takeaways

## Transcript
<details>
<summary>Full transcript</summary>

This has got to be one of the coolest things that you've seen today. Basically, Remotion now has agent skills. And what that means is that we can create entire videos like this one by just using claude code. So, in this video, we'll go through exactly how you can do that.

First, you'll want to create a folder. Go inside of that folder and once in there, type in bun create video. As simple as this. Now, here you'll want to select a template. Select blank. Let me zoom out a bit. And yes, I want to use Tailwind. If all goes well, you'll probably see the enjoy remotion message at which you'll type in bunks skills add reotion-dev/ skills or just go with npx. Hit enter. It'll ask you which skill you want to install. So there's anti-gravity, cloud code, codeex, cursor, gemini. I'll go with cloud code. And I'll actually cancel my installation since I've already gone through this process. But now that it created the project, let me just type in bun I to install all of the packages. All right. Now with all the packages installed, let me zoom out. Type in bundev. Wait for it to open the localhost 3000 or whatever port is available. You should now see something like this. If yours opens up without being inside of the composition, it'll probably be just gray area. So, click on my comp and it should open up this interface.

Now, we can go over to Claude. Let me run it with dangerously skip permissions. Okay, now it's time to get creative. My prompt will be this. I haven't tested this before, by the way, but create a web window interface that is opened inside of a YouTube video. And then place in the name of my channel. The video shows the Cloud Code terminal interface and it starts typing, "This is way too cool." So, as simple as this. Um, let's actually take a screenshot of how the claude terminal looks like. So, has that as context. And now, just hit enter and let's see what it builds for us.

It's been around 2 minutes now, and it's the first time something happens. But I feel like it's been creating a bunch of different components. Let me hit Yeah, this is actually way too cool. Just imagine where we'll be with this in a few months from now. It's opening up a bunch of different instances. So, let me tell Claude don't run npm rundev as it is already running. And don't use npm, use button.

Okay, but what should we do now? I think I'm going to make it scroll down and click on the like button and subscribe like have that nice interaction. So, I added make sure that at the end when it's done typing this is way too cool. It seems as if the user is scrolling down inside the YouTube page and it shows a cursor clicking on the like button then on the subscribe button. Oh, and by the way, for more context, if you want to see how they built this example, uh there's an entire video that's actually in like 10x the speed, but I mean you can you might want to use it as a reference for prompting. Uh by the way, those prompts are here as well. But it's really about knowing what you want to build and aiming towards building something that can be kind of drawn into a web interface. Not like uh draw myself in a YouTube video like produce my entire video for me.

Let's see how it's going with that. Seems pretty cool. So it already presume that the video will reach 2.5,000 views. Uh seems like it's done actually. Let's watch. So play it. Scrolls down. There's a cursor there. the c. So, the cursor really isn't clicking on the like button nor on the subscribe because it's like all the way up here. Let me take a screenshot of this and send it over to Claude. So, all I said is the cursor should be bigger and it isn't exactly on top of the buttons. Okay, it seems like it changed the cursor's position, but it's not quite there yet. One thing we can do is just find out where are these positions. This could be a bit tricky.

All right, so this is what we got. It types in this is way too cool, then goes over to the like button, kind of clicks that. So, it seems like it dashes through the like button and then goes already up to subscribe. But yeah, we could improve this in many different ways, like just adding the other thumbnails and videos here, making sure this description is bigger, uh correcting this cursor, like making it bigger overall. But just the fact that we built all this by talking to an AI agent is absolutely fantastic. This video isn't sponsored at all, but as a content creator, I know how hard it is sometimes to just build these type of things. And just knowing that AI agents can do all this for us already is pretty amazing. So, make sure to check out Remotion. Their link will be in the description of the video as well as the description to as well as the prompt GitHub links and this expost. Thanks for watching and I'll see you guys in the next video. Intellect.

</details>
