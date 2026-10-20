---
title: "Claude Code Just Got Another Huge Upgrade"
video_id: X6EGzi9qm3E
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-03-24
processed: 2026-07-05
duration: "8:10"
url: https://www.youtube.com/watch?v=X6EGzi9qm3E
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [computer-use-automation, remote-device-control]
tools: [Claude Code, Claude Cowork, Dispatch, ClickUp, OBS, Chrome, Playwright]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Just Got Another Huge Upgrade

![thumbnail](https://i.ytimg.com/vi_webp/X6EGzi9qm3E/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=X6EGzi9qm3E) | 📅 Uploaded [[uploaded/2026-03-24]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Nate Herk demos Anthropic's new "Computer Use" research preview for Claude Code and Claude Cowork, which lets Claude natively control the mouse, keyboard, and take screenshots to operate desktop apps (Mac only for now). He shows it sending a file through ClickUp, calculating a number and saving it in Notes remotely via Dispatch, and covers the current browser-automation limitations.

**Watch this if:** you want Claude Code to click around and operate real desktop apps (not just write code) — including from your phone while you're away from your computer.

## Key Takeaways
- Computer Use is in research preview for both Claude Cowork and Claude Code, Mac OS only (desktop app), with Windows support planned for a few weeks out; only available on Pro and Max plans, not Teams/Enterprise.
- It's enabled in the desktop app's general settings; Claude will request accessibility/screen-recording permissions and per-app access (Finder, ClickUp, etc.) the first time it uses them in a session.
- Demo 1: told to find a specific PDF in Downloads and send it as a ClickUp DM, Claude took iterative screenshots, zoomed in to locate the paperclip/attach button, searched Downloads, attached the file, and asked for confirmation before sending.
- Demo 2: paired with the new Dispatch feature, Nate sent a message from his phone telling Claude to calculate a multiplication and save the result in Notes — Claude opened Calculator and Notes on his actual local Mac and completed the task remotely.
- Biggest current limitation: no in-browser clicking/typing for security reasons — in Safari it explicitly refuses and suggests using the Chrome extension or a Playwright CLI-style tool instead for real web automation.
- If Computer Use tries to fall back to a Chrome extension or Playwright instead of acting locally, be more explicit in your prompt about which app/action you want it to control.
- Best use cases flagged: legacy desktop apps with no API, pairing Computer Use with scheduled tasks (e.g. "scan email every morning" or "pull a report every Friday"), and using a sandboxed app for Claude to click around and find bugs instead of manual QA.

## 🛠 Tools & Software
- [[topics/Claude Code]] — gets native desktop control (mouse, keyboard, screenshots) via the new Computer Use research preview.
- [[topics/Claude Cowork]] — the other Anthropic product that Computer Use also ships to in this research preview.
- [[topics/Dispatch]] — Anthropic's remote-trigger feature paired with Computer Use so a phone message can control the local desktop session.
- [[topics/ClickUp]] — demoed as the target app: Claude finds a PDF and sends it as a ClickUp DM attachment entirely via screenshots and clicks.
- [[topics/OBS]] — used as the video's own screen-recording app; Claude Code was told to open it and start recording via Computer Use as an intro demo.
- [[topics/Chrome]] — named as the workaround path (via its extension) for actual in-browser automation, since Safari access is read-only under Computer Use.
- [[topics/Playwright]] — mentioned as an alternative CLI-based option for legitimate web browser automation, since native Computer Use can't click/type inside a browser.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Enable Computer Use in the Claude desktop app's general settings, then fully restart the app if the toggle doesn't seem to take effect.
- Be explicit in prompts (name the exact app and action) if Claude tries to fall back to a Chrome extension or Playwright instead of controlling a local app directly.
- Pair Computer Use with Dispatch to trigger desktop actions remotely from your phone when you're away from your machine.
- Combine Computer Use with scheduled tasks for recurring desktop chores (daily email scans, weekly report pulls) instead of one-off manual prompts.
- For legacy apps with no API, use Computer Use to click through and extract/download what you need instead of building custom integration code.

## 🔗 Related Videos
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Chrome, Claude Code, ClickUp
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Chrome, Claude Code, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Cowork, Playwright
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Chrome, Claude Code, Playwright
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude Code, ClickUp, Playwright
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude Code, Claude Cowork, ClickUp
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Chrome, Claude Code
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, Playwright

## Timeline
- `0:00` — What is Computer Use.
- `0:52` — Starting OBS recording with Computer Use as an intro demo.
- `1:24` — How to enable Computer Use in the desktop app settings.
- `1:40` — Demo: sending a file via ClickUp using screenshots and clicks.
- `3:19` — Troubleshooting tips (explicit prompts, restarting the desktop app).
- `3:52` — Pairing Computer Use with the Dispatch feature.
- `4:13` — Demo: calculating a number and saving it in Notes from your phone.
- `5:07` — Limitations to know (Mac-only, research preview, plan restrictions).
- `5:47` — Browser-use workarounds (Chrome extension, Playwright).
- `6:42` — Best use cases: legacy apps, scheduled tasks, sandboxed QA testing.
- `7:51` — Final thoughts.

## Transcript
<details>
<summary>Full transcript</summary>

Anthropic just dropped another new feature which lets Claude Code actually control your computer, which means it can natively use your mouse, your keyboard, and take screenshots, and do things for you. Right now, it is in research preview in both Claude Cowork and Claude Code, and on Mac OS only, which is why you guys might notice in this video I'm on my laptop. But, the whole idea is that you can basically do anything on your desktop, no matter if you are sitting there or if you are out to lunch. Because you can also pair it with the new Dispatch feature, so you can literally reach your desktop from your pocket, shoot off a text, and it will control the computer locally and do what you need to do. Or when it's time to check the bill, but you're on the train, once again, shoot off a message and it will do what it needs to do on your actual local computer. So, today I'm going to show you guys a few demos, talk about when it's useful, and then I'm going to talk about the limitations as well. So, let's get into it.

So, this is the official post from Claude that just dropped about 2 hours ago and already has over 4 million views, which is insane. And just as a little intro teaser, I actually had Claude Code start up this recording for me. So, you can see here I said, "Use computer use to open up OBS and start recording." And what we're going to see is that it basically moves its screen over to the right. It has to navigate through my desktop and has to open up OBS. And now it's going to take a screenshot of this interface to understand where is the start recording button. You can see it just took a screenshot, and now it's going to say, "Okay, it's right here in the blue." And then it's going to click on it, and that is the video that you're watching right now. The recording was started by Claude Code.

So, once again, you can use this in Cowork and in Claude Code. So, today I'm going to be showing how you use it in Claude Code. Now, the only way right now is within the desktop app, which is not a huge deal. You basically just come down to your settings, you go over to the general settings down here in desktop app, and you can see at the bottom we have computer use, which lets Claude take screenshots and control your keyboard and mouse in apps that you allow. You will have to give it some accessibility like screen recording and other things like that.

So, let's just start off with a quick demo here where I'm saying, "Use computer use to find the how to use the ROI calculator PDF in my downloads and send it in ClickUp as a DM." So, what you'll see here is that first, I don't have those two apps open. I don't have Finder open or ClickUp. So, what I have to do real quick is I have to allow Claude to use these things. So, it's going to allow it to use the Downloads folder and then I'm going to have to allow it to use ClickUp as well. Now, you won't have to do that every time, but in that session, you may have to give it access.

Now, what it's doing here is it's pulled up ClickUp and it has to actually take screenshots and navigate through it. So, the first thing that it did is it found my DM. So, there it is. There's Nate Herk. This is where it's going to send that file. And now it has to figure out how to actually send an attachment. So, you can see what's going on on the right-hand side is it's continuously taking screenshots and then it's going to press different buttons and figure out what to do. Right here, you can see that it zoomed in on the bar and now it sees that it needs to click on this paper clip in order to attach a file. And just to be sure, it even zoomed in even more. It's going to take another screenshot and then it should click on the right button for us.

And now that it's in our Downloads, it's going to have to search for that correct PDF. So, you guys didn't see that, but it just clicked on the search bar on the top right. Now, it's searching and you can see that the files that popped up have changed and hopefully it's going to choose the right one. There we go. So, it found the right one. It's going to have to double-click, open it up. Now, you can see it's attached in our ClickUp message and hopefully it's going to be able to send that. It did come back and ask for confirmation because it was doing a send action. So, I'm just going to go ahead and say yes and it should open the computer back up, hit send and then tell us that it has been sent. As you can see, that has now been sent to myself.

So, a couple things. If you're having trouble getting this to activate or when you're telling it to use computer use, it's trying to use like a Claude in Chrome extension or something like Playwright, then you have to be more explicit in the prompts. The other thing to check on is make sure that your Claude desktop app is fully updated. So, you know, delete it, maybe download it again and then when you enable the setting, quit out of the desktop app and then open it back up again. And then you should see you're able to use it. And now that I've already allowed those certain tools like Finder and ClickUp in this session, next time it uses them, it won't have to ask me again for permission.

Now, really cool is when you pair this computer use functionality with the new Dispatch feature, which is also available right over here as you can see. This lets you control Claude from anywhere. So, I can control it right here from my phone, which means if I'm out and about and I realize, "Oh, shoot. I left that file locally in my Downloads folder and, you know, XYZ person needs it." I can just text Claude Code to open up my browser, grab the file, and send it to them.

Okay, so here's an example. I've got a message typed up in Dispatch right here and I'm going to shoot it off and you guys will see it pops through right there on my actual local machine. So, I'm saying use computer use to calculate 726 times 83,729 and it's going to open the calculator app and then the notes app. So, once again, because this is a new session, I have to allow it. And now it took control of the computer, as you can see. It opened up my calculator. It's going to have to clear out this current search and it's going to have to type in the new numbers, as you can see. And now it's going to have to open up the Notes app and store those results. So, there's the Notes app. You can see that it just added in a calculation result, which has our calculator function right there. And once again, as long as my computer is awake, which we can actually turn on natively with Claude Dispatch, then I can be anywhere from my phone and I can use Claude Dispatch to start a new session, use computer use, and do whatever I need.

Okay, so before we talk about some other cool use cases here, I did want to talk about the limitations. So, obviously right now this is in research preview, so sometimes it may feel a little slow or a little buggy. And right now it's only available for Mac OS within the desktop app for Cowork or Claude Code. So, it's going to be coming to Windows in just a few weeks here. Now, really the biggest one in my mind is the fact that it has native limitations for browser use. So, in an actual browser, it doesn't click around or type and that's for security reasons. But locally, within any of your apps, it can use those really well. So, even if you have different connectors like your Gmail app or your Slack app or ClickUp app, as you guys saw, it can use all of those perfectly fine.

So, let me just show you guys what I mean by that. Use your computer use to open up Safari, search for images of cute dogs, and save them to my downloads folder. So, I'll shoot this one off, and what we're going to see is it's able to open up Safari, but then it can't actually type or click. And you can see here it actually even says, "Safari is restricted to read-only access on the system. However, I can use Google Chrome extension to do this." So, basically what that means is if you want to do legit browser automation on the web, you would need to use Chrome extension or potentially like a Playwright CLI. But this is still super exciting because what's happening is Anthropic is shipping a new feature like every day. And what this shows us is that they're moving towards having all of these features natively within Claude Code. So, at some point Claude Code will be able to do this in the web and all this kind of other stuff. It's just going to take a little bit more time. But they're still shipping at an insane pace.

But people are still having really great results with this already. You can use your connected apps first, so Slack, calendar, other integrations. If there's no connector for the tool you need, it will ask for permission to open the app on your screen directly. You can assign a task from your phone, you can turn your attention to something else, and you can come back to finish work on your computer. So, you could tell Claude to scan your email every morning or pull a report every Friday, and it would handle it from there. Now, another way that you could actually use this is you could pair it with the scheduled tasks. So, you could actually have a scheduled task kick off computer use. So, it's pretty much going to be as if you have a real human working on your laptop.

And of course, right now in the research preview, it is only available on Pro and Max, not on the Teams or Enterprise plans. But like I said, there's a lot of unlocks here if you think about the different use cases, like maybe legacy apps that don't have an API, and you can just actually click around to do things, download reports, look at different information. Of course, pairing it with scheduled tasks or something like Dispatch is a huge unlock as well. And if you have certain things that you want to test, like maybe you're building out some sort of app and you're pulling that up in a sandbox environment and you're just having Claude Code click around, find the bugs, test features, rather than you having to sit there and do that manually.

I hope you guys are having as much fun as I am playing around with Claude Code and exploring all of these new features. It's definitely not been a boring few weeks if you're in the AI space. So if you enjoyed it, if you learned something new, please give it a like. Helps me out a ton. And as always, I appreciate you guys making it to the end of the video. I'll see you on the next one. Thanks, everyone.

</details>
