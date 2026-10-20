---
title: "Open-Source Dictation Is Here… Goodbye Subscriptions"
video_id: mIL4sZa8M0E
channel: "[[channels/Better Stack]]"
uploaded: 2026-07-10
processed: 2026-07-13
duration: "4:33"
url: https://www.youtube.com/watch?v=mIL4sZa8M0E
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [voice-dictation, local-speech-to-text]
tools: [FluidVoice, Wispr Flow, Superwhisper, Homebrew, VS Code]
llms: [Parakeet]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Open-Source Dictation Is Here… Goodbye Subscriptions

![thumbnail](https://i.ytimg.com/vi_webp/mIL4sZa8M0E/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=mIL4sZa8M0E) | 📅 Uploaded [[uploaded/2026-07-10]] | 🗓️ Processed [[created/2026-07-13]]

## TL;DR
> FluidVoice is a free, open-source Mac dictation app that runs entirely on-device: the Parakeet model transcribes speech while a second local model ("Fluid Intelligence") cleans up capitalization, punctuation, and formatting in real time. The video demos it in an editor, compares it against Apple's built-in dictation, Wispr Flow, and Superwhisper, and concludes it's the only option that is simultaneously free, private, and smart about formatting — with the caveats that it's Mac-only, the editor model is a ~3.5 GB download, and it's slower on Intel Macs.

**Watch this if:** you dictate code comments, commits, docs, or prompts on a Mac and want to drop a paid cloud dictation subscription.

## Key Takeaways
- FluidVoice processes everything locally — voice audio never leaves the machine, which removes both the privacy concern and the subscription cost of cloud tools like Wispr Flow.
- Two-model pipeline: Parakeet does speech-to-text, then a local "Fluid Intelligence" model acts as a live editor fixing capitalization, punctuation, and structure before the text lands at your cursor.
- Install is one Homebrew command (`brew install --cask fluidvoice`); setup is just mic + accessibility permissions and a hotkey.
- Demoed dictating a code-review request in an editor: output arrived correctly capitalized, punctuated, with technical terms spelled right — no cloud round-trip, no spinner.
- Claimed ~4× faster than competing dictation tools; on Apple Silicon (M-series) it's fast enough to feel instant, on Intel it runs but slower.
- Limitations: Mac-only today (iOS/Windows waitlisted), ~3.5 GB editor model download, and non-English dictation may need tuning.
- Recommended pattern: use FluidVoice as the daily driver on Mac, keep a cross-platform tool around for other devices.

## 🛠 Tools & Software
- [[topics/FluidVoice]] — the subject of the video: free open-source local dictation app for Mac, demoed end-to-end
- [[topics/Wispr Flow]] — paid cloud competitor used as the main comparison point (subscription + audio leaves your machine)
- [[topics/Superwhisper]] — paid alternative compared; good but lacks FluidVoice's local formatting cleanup
- [[topics/Homebrew]] — one-line install path (`brew install --cask fluidvoice`)
- [[topics/VS Code]] — editor used for the live dictation demo

## 🤖 LLMs Mentioned
- [[topics/Parakeet]] — local speech-to-text model that powers FluidVoice's transcription, paired with the "Fluid Intelligence" editor model

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install FluidVoice: `brew install --cask fluidvoice`, grant mic + accessibility permissions, set a hotkey.
- Test it against your current dictation tool on a code comment or commit message and compare formatting quality.
- Budget for the ~3.5 GB Fluid Intelligence model download before installing.
- If on Windows/iOS, join the waitlist and keep a cross-platform dictation tool for now.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Why Mac's built-in dictation isn't good enough and paid tools mean another subscription
- `0:27` — FluidVoice intro: free, open-source, fully on-device — privacy and cost wins
- `0:55` — How it works: Parakeet transcribes, Fluid Intelligence cleans up formatting live
- `1:21` — Live demo: dictating a code-review request, output lands formatted at the cursor
- `2:05` — Comparison: ~4× faster than alternatives; vs Apple Dictation, Wispr Flow, Superwhisper
- `2:43` — Benefits recap: free, private, fast on Apple Silicon, actively maintained
- `3:11` — Limitations: Mac-only, ~3.5 GB model download, slower on Intel, non-English needs tuning
- `3:42` — Verdict: worth it for most Mac devs who don't want another subscription
- `3:55` — Best usage pattern: daily driver on Mac + cross-platform fallback elsewhere
- `4:18` — GitHub link and Homebrew install command in description

## Transcript
<details>
<summary>Full transcript</summary>

just to talk to your computer instead of typing it all out. You end up with another subscription to something like Whisper Flow. And yeah, it's good. You'd think the free thing we already have on Mac would be good enough, but it's not. This is Fluid Voice. It runs completely on your own machine, and it's growing in popularity as a strong competitor to Whisper Flow and all the others. Fluid Voice is a free open-source Mac app that turns your voice into text and every part of that happens on your own computer. Nothing ever gets shipped off to a server somewhere, which is a huge win. Two reasons this is good for us. And there are the exact two things devs complain about. First, your voice and whatever you're dictating might be code or private and this never leaves your Mac. Second, you're not paying another monthly bill to do it.

Here's how simple this is. A model called parakeet listens and writes down what you say. Then a second local model called fluid intelligence acts like an editor sitting right next to you fixing your capitalization, punctuation and structure as you talk. You hit one hotkey that you set speak and the cleaned up text drops into whatever your cursor is already at into cursor cla notes. Doesn't really care which one. Now, this is super simple to spin up, so I'll keep the demo short, too. It's a oneline install. You open it, give it mic and accessibility permissions. Every Mac app makes you do this, so you have to do it anyways. And then you can choose a hotkey or use the one builtin. So, there's no real difference here. Now, watch this. I hold the key and I just talk normally here. Can you check over my code and make sure it's set up with some good practices to prevent bugs?

And it didn't just collapse. Look at what it just did. It capitalized the line, punctuated it, kept my technical word spelled right, and formatted it like an actual comment. I didn't fix one thing. No spinner, no waiting because there's no cloud to actually wait on here. So, where does this actually sit next to everything else? Well, this is actually four times faster than using other ones already out there. And on top of that, this is where it gets interesting. The dictation already on your Mac is free, and for a text message, it's fine. for a commit message or a doc, someone actually going to read that. It's probably not so great. Whisper flow is the paid, so you'd expect it just wins here. But it's subscription, your audio goes to a cloud. For a lot of us, that second part is a deal breaker before we even get to the price. Super whisper and the rest are good tools. Still cost money. They don't quite match the local cleanup Fluid Voice is actually doing. So, the free one that was supposed to be the weakest, it's the only one that's free, open-source, and does the smart formatting right there on our machine. On Apple Silicon, it's fast enough that you can forget it's even thinking.

Now, before you run off and install this, it's great that it's free, right? There's no subscription. It's great that it's private. Our voice stays on our Mac. On M series machines, it's fast and the formatting is actually pretty good, and it's open source and actively worked on, so problems are getting fixed. But on the flip side of things, it's Mac only right now. iOS and Windows are on the wait list. So if you live on Windows, this isn't your tool just yet. The editor model is about 3 and 1/2 gigs, so it's a real download. It's not a quick one. It's best, like I said, on the silicone chips. It does run on Intel. It's just slower. And if you dictate in a language other than English, you might have to tune it to get it just right. But you should know all that now, not after you spend 10 minutes trying to download this the hard way.

You'd probably expect me to say it's worth it now, but I won't. For most Mac devs, yeah, okay, this might be worth giving a shot. It's worth it if you don't want another monthly payment just to dictate things for you, which come on, who does want that? Use it for boring typing, email, docs, code comments, Slack messages. Heck, talk to Claude. On a Mac M4 Pro, it's really nice because it's all local and it's quick. If you need Windows or iOS right now, sorry, but this can't help you. So, here's what you could actually do. Run it as your everyday tool in Mac and keep something crossplatform around for when you're not on Mac. You get the best of both worlds and it costs you nothing you're using Mac. The GitHub link and the brew command are both in the description below. If you enjoy coding tips and tricks like this, be sure to subscribe to the Better Stack channel. We'll see you in another video.

</details>
