---
title: "Anthropic Just Connected Claude Code to Your Browser"
video_id: rXTvax9pyhs
channel: "[[channels/Ray Amjad]]"
uploaded: 2025-12-18
processed: 2026-07-06
duration: "7:57"
url: https://www.youtube.com/watch?v=rXTvax9pyhs
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [browser-automation-coding-agent, claude-code-feature-updates]
tools: [Claude Code, Claude in Chrome, Puppeteer, Warp]
llms: [Claude, Claude Opus, ChatGPT]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Just Connected Claude Code to Your Browser

![thumbnail](https://i.ytimg.com/vi_webp/rXTvax9pyhs/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=rXTvax9pyhs) | 📅 Uploaded [[uploaded/2025-12-18]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A walkthrough of every Claude Code feature shipped in the past week, headlined by Claude Code now being able to control the Claude in Chrome browser extension directly — spawning tabs, navigating sites, reading console logs, and driving multi-step browser tasks as a potential replacement for Puppeteer-style MCP servers. The video also covers reduced terminal flickering, a mobile QR-code link, a changed thinking-mode shortcut, prompt suggestions, better syntax highlighting, a first-party plugin marketplace, a token-usage status line field, and a quick model-switch shortcut.

**Watch this if:** you use Claude Code daily and want a fast rundown of every new feature from the last release cycle, especially the new Claude-in-Chrome integration.

## Key Takeaways
- Claude Code can now connect to and control the Claude in Chrome browser extension: after `claude update`, run `/chrome` inside Claude Code to check the extension is installed/enabled, then connect and manage permissions.
- Demoed live: Claude Code opens a new browser tab, navigates to ChatGPT, enters a prompt, reads the response, and can debug itself using console log access if it hits a browser error mid-task.
- This tightly-coupled setup is positioned as a replacement for separately-run browser-automation MCP servers (e.g. a Puppeteer MCP server) — Claude Code can pair it with sub-agents, skills, and other MCP servers directly.
- Running Claude in Chrome inside a sub-agent to keep the browser session's context out of the main window doesn't work yet, but the presenter expects it to be added and would "perfect" the feature.
- Several smaller changes shipped: reduced terminal flickering, a `/mobile` command showing a QR code to the iOS/Android app, and prompt suggestions (press Tab to autofill, or disable them via `/config`).
- The thinking-mode shortcut changed from Tab to Option+T (Mac) / Alt+T (Windows) — Warp terminal users need to enable "left option key is meta" in settings for this to register correctly instead of showing a dagger symbol.
- Claude Code added a first-party plugin marketplace (`/plugins`) with official plugins like a Chrome DevTools plugin, a code-review plugin, an Opus-migration plugin, and a Context7 plugin; marketplaces can have automatic updates disabled to pin a version.
- Other updates: improved code-diff syntax highlighting, a token/context-usage field available for custom status lines (`/statusline`), removal of the `#` shortcut for adding to CLAUDE.md, thinking mode now on by default with Opus 4.5, and Option+P (Mac) / Alt+P (Windows) to switch models mid-prompt before submitting.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the subject of the video; walked through its newest features, most notably direct control of the Claude in Chrome browser extension, plus terminal, marketplace, and status-line updates.
- [[topics/Claude in Chrome]] — the Chrome/Chromium browser extension that Claude Code can now connect to and drive directly (navigating tabs, reading console logs, executing multi-step browser tasks).
- [[topics/Puppeteer]] — cited as the kind of standalone browser-automation MCP server that the new Claude Code + Claude in Chrome integration could replace.
- [[topics/Warp]] — referenced with a specific settings fix ("left option key is meta") needed for the new Option+T thinking-mode shortcut to work correctly.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model underlying Claude Code throughout the demoed browser-control workflow.
- [[topics/Claude Opus]] — thinking mode is now on by default when using Opus 4.5.
- [[topics/ChatGPT]] — used as the live demo target: Claude Code navigates to ChatGPT via the browser extension, submits a prompt, and retrieves the answer.

## 📡 Protocols & Standards
- [[topics/MCP]] — Claude Code's new browser control is framed as work alongside (and potentially replacing) browser-automation MCP servers; the new plugin marketplace also includes an MCP-related Chrome DevTools plugin.

## ✅ Action Items
- Run `claude update` then `/chrome` inside Claude Code to connect and manage permissions for the Claude in Chrome extension.
- Try letting Claude Code drive a multi-step browser task (navigate, fill a form, read the result) instead of maintaining a separate Puppeteer/browser MCP server.
- If using Warp and the new Option+T thinking shortcut shows a dagger instead of toggling thinking mode, enable "left option key is meta" in Warp's settings.
- Check `/plugins` for the new first-party marketplace and try the official Chrome DevTools, code-review, or Context7 plugins.
- Set up a custom status line via `/statusline` that surfaces the new context/token-usage field.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Claude Code Skills Just Got Even Better]] — shared: ChatGPT, Claude, Claude Code, Claude Opus
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, MCP, Puppeteer
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, Claude Opus, MCP

## Timeline
- `0:00` — Intro: rundown of every Claude Code feature added in the last week.
- `0:22` — Claude Code connects to and controls the Claude in Chrome extension; setup via `/chrome`.
- `1:09` — Live demo: Claude Code drives a browser tab to ChatGPT, submits a prompt, retrieves the answer.
- `2:05` — Console log access lets Claude Code self-debug browser errors while executing tasks.
- `3:08` — Framed as a replacement for standalone browser-automation MCP servers (e.g. Puppeteer MCP).
- `3:31` — Reduced terminal flickering; `/mobile` QR code for the iOS/Android app.
- `3:49` — Thinking-mode shortcut changes from Tab to Option/Alt+T; Warp "left option key is meta" fix.
- `4:32` — Prompt suggestions (Tab to autofill) — can be disabled via `/config`.
- `4:59` — Improved syntax highlighting for code diffs.
- `5:18` — New first-party plugin marketplace via `/plugins`.
- `5:41` — Token/context usage field added for custom status lines.
- `6:08` — `#` shortcut for CLAUDE.md removed; thinking mode on by default with Opus 4.5.
- `6:17` — Option/Alt+P to switch models mid-prompt before submitting.

## Transcript
<details>
<summary>Full transcript</summary>

Okay, so we will be going over every single feature of Claude Code that was added in the last week. But before getting started, it's worth me mentioning that I have a Claude Code masterclass where I go through every single feature of Claude Code as well as a bunch of bonus content and techniques, some of which you won't find anywhere else here on YouTube. And since I've never accepted a sponsor on the channel and never plan to, my classes and also applications like HyperWhisper basically keep the channel going.

Anyways, getting started. Claude Code can now control Claude in Chrome. So if you don't know already, this is a browser extension for Google Chrome and Chromium-based browsers. So when you sign into your account and click on the button, then you can see you have Claude on the right hand side here, and you can do like any basic tasks like getting it to summarize a page and so forth. But the interesting thing here is that now Claude Code can connect and control your browser via this extension. So firstly you want to make sure you're on the latest version of Claude Code by doing `claude update`, and then after that you can run `claude` and then you want to run `/chrome`, and then you can see the extension is installed and the status is enabled. So you may need to run connect extension or something, and then after that you can go to manage permissions and then basically see all the permissions that Claude in Chrome has access to.

And then, using my application HyperWhisper — there will be a link down below to this — I can basically say something like, "can you go to ChatGPT and then ask ChatGPT a question and then give me the answer back," and then press enter, and then you can see that it spawns up a brand new tab for me, like a brand new window, where it's going to start executing on things. And you can see Claude Code can see the available tabs that it has access to, and in Chrome at least it kind of has this tab group that it can control. "Can you ask ChatGPT why they should take Ray Amjad's masterclass Claude Code class," and then press enter, and then we should see actually executing on things. And now you can see it's actually executing because it goes to chatgpt.com, it then takes a screenshot I think to basically understand how things are looking. So if we put this on the left hand side, you can see then it enters information into ChatGPT on the right hand side, presses enter, and then it snoozes for about 3 seconds and it's like still waiting.

And one of the things that it actually has access to is any console logs inside the browser. So when Claude Code is executing and actually doing things within your browser like pressing buttons, clicking around, entering text, then it can debug itself if it runs into a console/browser error. And of course, you can get it to do many other things as well. Previously, you could have used like Claude in Chrome to go on LinkedIn or another website and scrape data. But here it's like much nicer because the two are linked together. So then you can use Claude Code to connect an MCP server, use any sub-agents, connect to skills, and basically do everything else Claude Code can do with the browser basically attached onto it. So this can be useful for people who are using like the Puppeteer MCP server or something like that — you can probably replace that with this Claude in Chrome connected to Claude Code.

And now ChatGPT basically gave a bunch of the reasons why you should take the class, and then Claude Code actually scrolls down through the web page to gather all the information and then it will provide it back to me. So this should open up a bunch more use cases, because whilst we did have similar things before, we now have a more tightly coupled solution with Claude Code that should perform better as well. And then we have the answer that Claude Code gave from ChatGPT.

So I just tried to get it to run Claude in Chrome with Claude Code inside a sub-agent, because it does fill up the context window when it's doing a bunch of things and I only want the final result, but currently it doesn't seem to be able to do that for some reason. So I think if that was added then this feature would basically be perfected. You can also say "are there any console errors" for example, and then Claude in Chrome would read the console log messages as well.

Anyways, we now have reduced terminal flickering, and there's a good post on Twitter by one of the developers about why this was an issue for such a long time, and yeah, you can read through that yourself, it's pretty interesting. If you do `/mobile` now, then you can see that it shows a QR code to go to the iOS store or Android store to download the mobile app.

Unfortunately, they changed the thinking toggle from Tab to Option+T instead, which basically means that previously if you press Tab then that would turn on thinking. Now, if you press Option+T on your keyboard if you're on macOS, or Alt+T if you're on Windows, then that should show thinking mode. But you can see it shows a dagger for me right now, and that's like something built into macOS. So what you want to do is if you're using Warp, then you want to go to settings in the top right, search for "meta," and where it says "left option key is meta," you want to turn that on. And now if you press Option+T, it should then turn off and on thinking. So if you're seeing a dagger on macOS after pressing Option+T, then you want to go to your settings on your terminal and find a setting that's kind of like this: left option key is meta.

In some cases, Claude Code may also show you prompt suggestions when it thinks you're about to do something. So you can see in this case the person commits the changes locally on their computer and then it suggests push the changes. So you can press Tab and then that will autofill the prompt and then you can press enter. So I personally found this behavior to be pretty annoying when it came to coding, so what I do is I just go to `/config` and then when it says prompt suggestions I just turn that off instead.

Claude Code now also has improved syntax highlighting to show which changes were actually made to your codebase. So this is what it currently looks like, and if I go to a previous example, this is what it kind of looked like before. So you can see putting them side by side, the new one does look better because of the color scheme and the line number being highlighted and a few other things.

When it comes to plugins, there's now a first-party marketplace. If you do `/plugins`, then you can see all the official Claude Code plugins that they have available — so like Chrome DevTools, a code review plugin, an Opus migration plugin, Context7. So this is what the official marketplace looks like on GitHub. And then for these marketplaces, you can also disable automatic updating to preserve an older version of the marketplace on your computer.

They now also add a brand new currency/usage field to the status line input, which means that you can now have more accurate status lines. So if you do `/statusline` and then after that you say something like "can you basically make a pretty simple status line that has like a battery and it shows an amount of context that I've used in the current context window so far," and you can see this is the kind of status line that it now came up with, which should be pretty accurate because it now has access to that current usage information.

They did remove the hashtag shortcut for adding things to the CLAUDE.md file, so maybe they will use that for something else in the future. Thinking mode will now be on by default when you're using Opus 4.5. Now when you're in the middle of writing a prompt, you can switch out the model to a different one before pressing enter by pressing Option+P on macOS or Alt+P on Windows. And this is pretty handy because otherwise you would have pressed enter, then stop the agent, then switch the model, and then press enter again.

And those are basically all the changes that I thought were worth talking about. And also I was watching this video or podcast episode of the creator of Claude Code talking about Claude Code itself, and I really begin to understand why it's such a good coding agent, because they're not focused on their competitors. Whilst many competitors like Codex CLI, Factory CLI, and so forth are looking at the new features that Claude Code has introduced and adding it to their own coding agents, Claude Code is still kind of leading the way because he just doesn't look at what the competitors are doing. He says that he just builds things that are useful to Anthropic employees and also their users, instead of doing anything like looking at competitors. So I guess that's probably one reason why Claude Code is always one step ahead of everyone else.

Anyways, if you are interested in learning more about how you can be using Claude Code effectively and a bunch of advanced techniques to get the most out of it, then I do cover that in my Claude Code Masterclass that will be linked down below. And if you are interested in hearing from me on a more regular basis in your email inbox, and you're having the algorithm only tell you when videos are published, then I do have an email newsletter that I just started, and I will be sharing a bunch of techniques I'm discovering, any thoughts that I have on new models, research papers I have been reading, and a bunch of other things as well. It is brand new and there will be a link down below if you're interested, and if you do reply to any of the emails from the email newsletter then I will try to reply to you as well. And finally, if you're interested in the application that I was using throughout the video for voice to text, then that will also be linked down below. It's my own application, and since I don't accept sponsors, applications like these and classes basically help keep the channel going.

</details>
