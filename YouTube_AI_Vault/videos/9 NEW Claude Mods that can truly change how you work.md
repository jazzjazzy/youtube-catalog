---
title: "9 NEW Claude Mods that can truly change how you work"
video_id: lDrAZ1wAyVs
channel: "[[channels/Jay E - RoboNuggets]]"
uploaded: 2026-10-08
processed: 2026-10-20
duration: "12:47"
url: https://www.youtube.com/watch?v=lDrAZ1wAyVs
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [claude-code-customization]
tools: [Claude Code, Savvy Progress, Claude Skins, You Should Know, Filetree, Cache Tax, Blast Radius, Claude Reflect, Terminal Browser, Replay Theater, Kling]
llms: [Claude Opus, Claude Fable]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# 9 NEW Claude Mods that can truly change how you work

![thumbnail](https://i.ytimg.com/vi_webp/lDrAZ1wAyVs/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=lDrAZ1wAyVs) | 📅 Uploaded [[uploaded/2026-10-08]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> Anthropic's new "mods" feature (shipped October 1) lets Claude Code build features into its own interface: unlike skills (a how-to handbook) or MCP connectors (plugs into other apps), a mod runs inside Claude Code and changes what you see on screen by watching, changing, or handling events. Jay walks through nine mods worth installing — Savvy Progress, Claude Skins, You Should Know, Filetree, Cache Tax, Blast Radius, Reflect, Terminal Browser, and Replay Theater — then shows how to build your own by just describing it, since Claude Code ships a built-in plugin-authoring skill with hot reloading.

**Watch this if:** you use Claude Code in the terminal or desktop app and want progress bars, subagent dashboards, cost warnings, deletion guards, or any custom UI you can describe in a sentence.

## Key Takeaways
- A mod is a small add-on that changes how [[topics/Claude Code]] looks and works; it listens for events (like a command being run) and can watch, change, or handle them — different from skills (task handbooks) and [[topics/MCP]] connectors (plugging into other apps).
- Mods work in the terminal and the desktop app's code tab, but (at recording time) not in the VS Code extension, and they need Claude Code v2.1.287 or newer.
- [[topics/Savvy Progress]] adds a task progress bar plus a live subagent panel showing each helper's model, progress, and rough API cost — with customizable pixel-claw mascots.
- [[topics/You Should Know]] (built by Anthropic, enabled via `/plugin enable cc-plugin-you-should-know@builtin`) runs a second agent that flags important details buried in walls of text — e.g., surfacing what a [[topics/Kling]] video generation would cost; note it increases token usage, while most other mods are deterministic code.
- [[topics/Cache Tax]] warns you before a message that would reload a cold prompt cache (which goes cold after ~1 hour) and estimates the token/credit cost; `/keepwarm` pings the session to keep the cache warm while you step away.
- [[topics/Blast Radius]] intercepts risky commands like folder deletions, shows exactly which files would be lost, and forces a human to click Proceed — insurance against even frontier models like [[topics/Claude Opus]] or [[topics/Claude Fable]] wiping a project.
- [[topics/Claude Reflect]] turns corrective feedback ("no", "this doesn't look good") into a prompt to save a permanent rule in your CLAUDE.md or skill file — RLHF on a personal, micro scale.
- Building your own mod is just describing it: Claude Code's built-in plugin-authoring skill constructs it, hot reloading shows it in the current session, and asking Claude to "save it as a plugin" makes it permanent (mods are temporary by default).

## 🛠 Tools & Software
- [[topics/Claude Code]] — the host application; mods are its new extension surface, shipped October 1 and on by default in the latest version.
- [[topics/Savvy Progress]] — progress bar above the prompt plus a live panel of every subagent with model, progress, and cost.
- [[topics/Claude Skins]] — reskins how Claude Code displays its work (icons for tool calls, colored edits) with seven themes and support for any palette you describe.
- [[topics/You Should Know]] — Anthropic's built-in mod running a side agent that lifts important points out of long outputs; steerable toward costs, customer issues, etc.
- [[topics/Filetree]] — token-free file panel showing which files Claude is reading/editing; files shimmer while touched and turn green when committed.
- [[topics/Cache Tax]] — prompt-cache cost guard that estimates reload costs before you hit send and offers `/keepwarm`.
- [[topics/Blast Radius]] — Anthropic sample mod that stops destructive commands and requires an explicit human Proceed, listing the files at risk.
- [[topics/Claude Reflect]] — captures your feedback moments and offers to write them as permanent rules into CLAUDE.md or skill files.
- [[topics/Terminal Browser]] — opens a real web browser beside the terminal chat to review built pages or GitHub PRs without leaving the terminal.
- [[topics/Replay Theater]] — Anthropic sample mod adding a replay button that steps through every file edit Claude made in a turn (works for articles too, not just code).
- [[topics/Kling]] — the video-generation model used in his You Should Know test, where the mod flagged the generation cost.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — cited as a frontier model that can still wipe out a project in edge cases, motivating Blast Radius.
- [[topics/Claude Fable]] — cited alongside Opus as a smart model that still benefits from a human-in-the-loop deletion guard.

## 📡 Protocols & Standards
- [[topics/MCP]] — contrasted with mods: a connector plugs Claude into another application, while a mod changes Claude Code itself.

## ✅ Action Items
- Run `claude update` (or check the desktop app popup) to get v2.1.287+ so mods are available.
- Enable You Should Know with `/plugin enable cc-plugin-you-should-know@builtin` and steer what it watches for (costs, customer issues).
- Start with Claude Skins as a safe first mod — it only changes the display.
- Install Cache Tax if you run long sessions, and use `/keepwarm` before stepping away.
- Add Blast Radius (or something like it) before letting agents run loose on real projects.
- Build a custom mod by describing it in Claude Code, accept hot reloading to see it live, and ask Claude to save it as a plugin when you like it.
- Remember cost mechanics: mods are free by default, but any mod that calls a model in the background consumes your Claude usage.

## 🔗 Related Videos
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Fable, Claude Opus, MCP
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Opus, MCP

## Timeline
- `0:00` — Anthropic ships mods: describe a feature and Claude Code builds it into itself
- `0:39` — What mods are: October 1 release, works in terminal and desktop app (not yet VS Code extension); mods vs skills vs MCP connectors
- `2:02` — Mod 1 Savvy Progress: progress bar plus live subagent panel with model, progress, and cost per helper
- `3:02` — How a mod works: Claude Code emits events, and a mod watches, changes, or handles them
- `3:57` — Mod 2 Claude Skins: reskin tool calls and edits; seven themes, any palette on request
- `4:34` — Mod 3 You Should Know: Anthropic's side agent flags buried important info (Kling generation cost example); costs extra tokens
- `6:05` — Mod 4 Filetree: live file panel — shimmering while touched, green when committed; useful even for non-devs (tax-filing example)
- `7:04` — Mod 5 Cache Tax: pre-send warning with token/credit estimate before a cold cache reload; `/keepwarm` keeps it warm
- `8:15` — Mod 6 Blast Radius: stops risky deletes, lists affected files, requires a human Proceed click
- `9:04` — Mod 7 Reflect: feedback trigger words become saved rules in CLAUDE.md or skill files
- `9:39` — Mods 8-9: Terminal Browser (web browser beside the chat) and Replay Theater (step through every edit after a turn)
- `10:43` — Build your own: v2.1.287+, built-in plugin-authoring skill, hot reloading, save-as-plugin to persist

## Transcript
<details>
<summary>Full transcript</summary>

So, Entropic just shipped one of the biggest Cloud Code updates we've ever had, and they're calling it mods. The idea is simple. If you can describe a feature that you wish Claude Code had, it can now build that feature into itself. So, Cloud Code can become almost any tool that you need. And in this video, I'll walk you through the nine mods that are genuinely worth installing and tweaking so that by the end of this, you can master Claude mods and make full use of them to make your systems smarter and faster. And if you're new, my name is Jay. I spent over a decade working with brands you probably know have been in AI since my masters in data science and now I'm leading our AI business and one of the largest AI communities globally. But first, what are mods? So, a mod is just a small add-on that basically changes how cloud code looks and how it works. It came out on the 1st of October and if you've updated Claude Code to the latest version, then it's already switched on for you and ready to use. It works in the Cloud Code terminal and in the code tab of the desktop app, but at the time I'm recording this, it doesn't seem to be available yet in the VS Code extension. So, make sure you're using it inside Cloud Code in the terminal or the desktop app.

Now, you might be thinking, if you already have skills and you already have MCP connectors, then how are mods different? Well, a skill basically just tells Claude how to do a job. It's like a handbook for certain tasks, right? And a connector just plugs Claude into another application. But a mod runs inside Cloud Code and actually changes it. So it can change exactly what you see on screen. So if you want Cloud Code to have extra buttons, a side panel, or even a miniame to play while Claude is working, that's all entirely within the realm of possibilities. And making a mod is really easy because all you need to do is to ask Claude. I'll show you a few examples so that by the end of this video, you'll have a clear idea of what mods to use or tweak for your setup. And every one of these, by the way, I put into this PDF guide, which you can just send that straight to Claude, and you can have your agent grab these or customize them to your liking. And it's just a matter of asking your agent to set them up for you. So, the link for that is just in the description below if you need it. But for now, here are the ones I've tried, have liked, and think will be useful for you as well.

Number one is Savvy Progress. Now, I really like this one because it's the right mix of being useful while also being quite fun and delightful. Now, what it does is it puts a progress bar above your prompt. So, you can see how close Claude is to finishing your task. But for heavier, longer tasks where a team of sub agents is doing the work, it also shows you a live panel of every sub aent. If that's new to you, sub agents are basically these helper claws that your main agent can spawn. And each one of them basically takes a piece of the larger job. And for each helper, you can see its model, how far along it is, and roughly what it's costing you in API credits. Now, that's already useful by itself, but the even better part is that you can actually customize how these little pixel cla. So, if you want one that looks like a designer, you can do that. If you want one that looks like a developer, you can do that too, just by asking Claude to customize their looks. So, apart from giving you more information about your work, especially long running tasks that are done better with helper agents, it just makes using sub agents a much nicer experience with this view.

Now, you might be curious, how does a mod actually change what's on your screen? Well, every time Claude does something like running a command, for example, Claude Code actually sends out a little signal called an event. And a mod is just a small piece of code that listens for those events so that when one comes through, the mod can do one of three things. It can watch that event, it can change it, or it can handle it itself. Savvy Progress actually uses all three. So, it watches every time Claude starts a helper. And every time that helper asks the model to do something, it notes the model, the tokens, and roughly what it costs. and it changes your view so that it draws the area above your prompt. It adds its progress bar and also shows you that side panel if you're using sub agent. And when you open the agents panel, it draws that whole panel by itself, including all your custom claw mascot crabs. And the good news is you don't need to know any of this to make one mod. Cloud code actually comes with a built-in skill now for building them. So you just describe what you want and Claude builds it out for you.

Number two is Claude skins. Now, this one is really simple, but it's probably one of the very first mods that you can try without really changing your workflow because what it does is reskin how cloud code shows it work. So, your tool calls gets their own icons. Your edits can show up in a specific color if you want. Right now, this open source repo comes with seven themes like Noah and Tokyo. But because this is Cloud Code, you can give it pretty much any design system or color palette that you want and you can just have it build it out. So, if you're looking for a great first mod that is quite safe to start with, then this is a good candidate because it only changes the display and you can customize it to fit your setup. Number three is you should know. This mod is actually built by Entropic themselves and it runs a second agent on the side that reads what Claude writes and flags anything important that you might miss. Now, that's pretty crucial, especially when Claude gives you a wall of text as an output, which more often than we'd like to admit, we don't actually read in full. In my testing, I asked Claudeco to generate a video with a model like Cling, and it flagged that I should probably know how much that would cost if I ran it through key AI, which is the provider that I use. If that was buried in a wall of text, I might not have seen it. But with this little pop-up, it lifted the important point right out.

And you can steer what it looks out for, by the way. So, if you're more worried about costs, customer issues, or anything your automations might miss, you can tweak this mod to surface that. Do note that this particular mod, it does run a second age. So, it can increase your token usage, but for a lot of mods that I'll mention here, most of those are actually run using deterministic code. So, they don't really require you to use an LLM in order to run them. And by the way, if you want to learn how to build and sell AI systems that businesses actually pay for, then that's pretty much all we do over at the Robbernuggets community, where not only do you get access to the Cloud Living Masterass, which we update every week and takes you from zero to mastery with the latest on AI, but you also get access to our agents as a service course, which walks you through how to actually get paid for all these AI skills that you are learning. You also get to be part of a genuinely great community of AI builders. In fact, you can see just some of the recent wins our members are getting from the program right here. So, if you want to start earning from AI, then check that just in the pin comment below. Now, back to the video.

Number four is File Tree. So, this is one example where it doesn't really cost any tokens to run because what it does is just give Claude code a really nice file panel on the right that shows exactly which files Claude is working on, which matters most, especially when you're working on real software. Because when you're working in production code, it's important to know exactly what Claude is reading, editing, or changing. With this mod, a file shimmers in the tree when Claude is touching it. And when the change is committed, meaning it's saved, it turns green. So, at a glance, you always know exactly which files Claude is working on. And if you're not a developer, it's still useful whenever you're working across lots of files. To give one instance, let's say you're preparing a tax filing with multiple documents. With this mod, you can see exactly which ones COD has opened and which ones it has changed. and it gives you a much nicer UI instead of relying on a chat reply that you always need to read every time in order to get the gist of what your agent just did. It's much more interactive and in my view much easier on the eye.

Number five is cash tax. Now, this is a mod that can actually save you money because if you don't know what the prompt cache is, it's basically this short-term memory that Claude keeps during your conversation. and it keeps that shorter memory so that it doesn't have to reread the whole conversation that you have with it every time that you send the prompt. So, it's there to stop your tokens from being burnt. But after a while, usually about an hour on a normal Claude subscription, it goes cold. And once that prompt cash is cold, the next prompt that you send actually makes Claude reread your entire conversation, which can really eat into your usage limits. So, what cash tax does is stop you before a message that would cost you to reload your entire conversation and show you an estimate of what that would cost in tokens and API credits. So, you know exactly how much you'll spend before you hit send. That really matters in long sessions because the bigger or longer your conversation is, the more that that one message would cost. And if you're stepping away, you can actually type /keepwarm as part of this mod. Or you can just have the mod turn it on for you by default. And what it does is it will ping the session with a tiny message right before the cash goes cold so it's still warm when you get back.

Number six is blast radius. Now this one again Antropic made themselves and it might just save your entire project because when Claude is about to run something risky like deleting a whole folder. It stops first. It shows you exactly which files would get deleted. It shows you even a proceed button and a cancel button that you have to press yourself. Now, you might not think that your agent would ever delete your files, but I've seen so many edge cases already where even a smart Frontier model like even Opus or Fable would wipe out someone's entire project. There are some real horror stories out there. And if you don't want to become one of them, then you can try out this mod or something like it. So, with Blast Rages, this kinds of commands get stopped automatically and an actual human has to be in the loop to press proceed before any of the files get deleted. And with Blast Rages, it actually shows you which of those files would be gone the moment that you do that.

Number seven is reflect. Now, this mod is a bit like reinforcement learning from human feedback, but on a more micro scale and personalized to you. Because when you give Claude a piece of feedback with trigger words like no or this doesn't look good or I wish we'd done it this way, what happens with this mod is that a small band would pop up above your prompt asking if you want to save that as a permanent rule in your claw.md file or your skill file. And what you do is just click save and claude writes that rule in for you. It's a more granular way to choose what Claude reflects on and to make sure the things you've already corrected on are fixed or done better the next time that you use it. Number eight is the terminal browser. Now, this one is for people who use Cloud Code in the terminal because what it does is it opens a real web browser right beside your chat. So, if Claude builds you a web page, you can look at it and review it without ever leaving the terminal. Of course, it can also open GitHub pull requests the same way. So, you save the time and the headsp space of jumping between Claude and a browser to check every change to your code or to your design. Everything now stays in one place. So, if that's a feature you've been missing because you work mainly in the terminal, then this mod may be for you.

Number nine is Replay Theater. Now, this last one is another of Entropic's own sample mods, and it's called Replay Theater. And what it does is after Claude finishes a turn, a replay button actually shows up. And when you press it, it steps through every file edit that Claude just made. So you get a rundown of what it did and can understand the changes to your workspace. And again, even though this was originally created by Entropic for Code, it's actually not limited to just that use case. If you're writing an article, for example, it can let you replay exactly what Claude changed in your draft. So if it made major changes, you can pinpoint exactly where they are in that article. And the great thing about this is that mods are entirely modifiable to your liking. And the way you do that is really easy. First, you just need to make sure that cloud code is up to date because mods need this version 2.1.287 or newer. In the terminal, you can just type cloud update or in the desktop app, there will be a popup that shows you if you're on the latest version. Then just open cloud code, describe the modification that you want. And Claude Code comes with a built-in skill for this. It's called plug-in authoring. So Claude already knows how mods are put together. It'll start building it.

And then it'll ask if you want to turn on hot reloading for this session. What that means is it will just allow that session to sort of reload or restart itself so that when you turn that on, your mod would show up in that session as soon as Claude finishes building it. And if you don't like something or you want to tweak a feature, just tell it what to change the way you talk to a normal person. One thing to know is that a mod that Claude builds for you is temporary by default. So when you find one that you like, ask Claude to save it as a plugin and install it and it will be there every time that you open CL code. Now, by default, mods don't really cost anything extra, but you of course do need a paid plan because that includes cloud code. And also, any mod that needs to call on a model in the background uses your cloud usage like everything else. So, there you go. That's all nine of them. As usual, I hope that was useful. I think mods are a really good move by Entropic and I hope OpenAI follows suit because I think the era of more malleable software is definitely coming soon. And the fact that Entropic, one of the biggest and most influential companies right now, is opening up their own application to modification is a good step towards software that can be hyper customized to our needs. I hope that gave you an idea of the mods you could build for your own workspace. And again, the PDF guide is just down below if you need it. Send that to your cloud code to pick out the ones that are useful for your setup or to customize. As usual, thanks for watching till the end. And if it was useful, then consider tapping subscribe down below because it helps me a lot to put out more educational stuff like this. I'll see you all next time. Cheers. [music]

</details>
