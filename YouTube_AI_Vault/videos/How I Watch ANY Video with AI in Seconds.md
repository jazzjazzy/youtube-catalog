---
title: "How I Watch ANY Video with AI in Seconds"
video_id: qSuCPooR3E4
channel: "[[channels/Brad Bonanno - AI Automation]]"
uploaded: 2026-10-02
processed: 2026-10-20
duration: "8:07"
url: https://www.youtube.com/watch?v=qSuCPooR3E4
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [video-content-analysis, content-research]
tools: [Watch Skill, ChatGPT, Claude Desktop, Google AI Studio, WhisperX]
llms: [Gemini, Claude, Claude Fable]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# How I Watch ANY Video with AI in Seconds

![thumbnail](https://i.ytimg.com/vi/qSuCPooR3E4/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=qSuCPooR3E4) | 📅 Uploaded [[uploaded/2026-10-02]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> Watch is a free agent skill that gives Claude or ChatGPT the ability to understand video: it sends a link plus your question to Gemini's agentic video model (which scored higher on Google's 50-question video-understanding test while using 87% fewer tokens), and Gemini decides where to look — pictures, audio, and transcript together — returning findings with timestamps instead of hundreds of screenshots. Brad demos three uses (finding one detail in Karpathy's 3.5-hour LLM video, correlating YouTube retention drops with on-screen content, and piping video notes into an LLM wiki), then walks through install in Claude and ChatGPT, the free Gemini API key, updating, and when the local WhisperX-based engine still wins.

**Watch this if:** you want Claude or ChatGPT to answer questions about any video — yours or anyone else's — for free, without burning your own usage allowance on screenshot-feeding.

## Key Takeaways
- Models like [[topics/Claude Fable]] can't understand video out of the box; the [[topics/Watch Skill]] fixes that by delegating the watching to [[topics/Gemini]]'s agentic video understanding, where the model decides which parts of the video to inspect more closely.
- The YouTube link goes straight to Google's supported API — no downloading, no blocking — and the analysis runs on Google's free API tier: up to 8 hours of YouTube video per day, with no automatic billing when you hit the limit.
- Use case 1: needle-in-haystack retrieval — describe a half-remembered moment ("a tool that displays text as colored pieces with numbers") in a 3.5-hour Karpathy video and get the tool's name, website, and timestamp back; works on your own folder of screen recordings too.
- Use case 2: give [[topics/Claude]] your retention analytics and have Watch analyze the footage around the drops — it can't say why viewers left, but it lines each drop up with what you were saying and showing, and patterns emerge across your catalog.
- The skill supports 1,300+ sites including TikTok and Instagram, and works on competitors' content, not just your own.
- Use case 3: pull explanations and visual examples out of videos you watch and save them into an LLM wiki (linked notes your AI can read later).
- Setup is a one-time plugin install (Claude desktop: customize → plugins → add the Watch repository as a marketplace; same flow in ChatGPT desktop), then `/watch` and a free API key from [[topics/Google AI Studio]] — no billing enabled.
- The original local engine remains: it prepares frames plus a transcript (with [[topics/WhisperX]] transcribing on-device when captions are missing), with Efficient/Balanced/Token Burner frame settings — worth the extra Claude allowance when Claude must see actual frames, like recreating a motion graphic.

## 🛠 Tools & Software
- [[topics/Watch Skill]] — the free agent skill at the center of the video: hands a link and question to Gemini and returns timestamped findings to your AI.
- [[topics/ChatGPT]] — second supported host app; install flow shown via its desktop plugin menu.
- [[topics/Claude Desktop]] — primary install target: customize menu → plugins → add the Watch repo as a marketplace → install.
- [[topics/Google AI Studio]] — where you create the free-tier Gemini API key (no billing required).
- [[topics/WhisperX]] — new local-mode addition that transcribes audio on your computer for free when captions aren't available.

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — the agentic video model doing the actual watching on Google's free tier; beat the non-agentic approach on Google's own 50-question test with 87% fewer tokens.
- [[topics/Claude]] — the orchestrating assistant: receives Watch's findings, analyzes retention data, scripts new videos, and writes notes into the LLM wiki.
- [[topics/Claude Fable]] — cited as a best-in-class model that still can't understand video natively, motivating the skill.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Watch in Claude desktop (customize → plugins → add the Watch repository as a marketplace) or ChatGPT desktop, then run `/watch` to configure.
- Create a free Gemini API key in Google AI Studio, confirm the project is on the free tier, and let the agent store it (or paste it into your env file manually).
- Test needle-in-haystack retrieval: describe a moment you half-remember from a long video and ask for the timestamp.
- Export your YouTube retention data and ask Watch to explain the three biggest drops against the actual footage.
- Pipe recurring video notes into an LLM wiki so your AI can reuse them in later sessions.
- If updating an older Watch install, hit update in the plugin marketplace, then explicitly ask to switch to the Gemini engine — updates keep your old preferences.
- Choose engines per job: Gemini for questions and moment-finding; local (Balanced + WhisperX) when Claude needs to inspect real frames.

## 🔗 Related Videos
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Claude, Gemini
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: ChatGPT, Claude, Gemini
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: ChatGPT, Claude, Gemini
- [[videos/The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing]] — shared: ChatGPT, Claude, Gemini
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: ChatGPT, Claude, Gemini
- [[videos/You Need Claude Sandboxes 90 Faster AI Coding]] — shared: ChatGPT, Claude, Claude Desktop
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Gemini
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude

## Timeline
- `0:00` — Hook: AI can now watch videos free; Google's agentic version answers more correctly with 87% fewer tokens
- `0:30` — How it works: Watch sends link + question to Gemini, which looks where it needs to and returns timestamped findings
- `1:10` — No downloads, no blocks: the YouTube link goes to Google's supported API on the free tier
- `1:38` — Use case 1: finding the tokenizer demo buried in Karpathy's 3.5-hour LLM deep dive from a vague description
- `2:31` — Use case 2: lining up retention drops on the 100k-view Book-to-Skill video with what was on screen
- `3:20` — Works across 1,300+ sites (TikTok, Instagram) and on other people's content
- `3:53` — Use case 3: saving explanations and visuals from videos into an LLM wiki
- `4:30` — Setup: free tier limits (8 hours of YouTube/day), plugin install in Claude desktop and ChatGPT desktop, `/watch`
- `5:33` — Free Gemini API key via Google AI Studio; store it with the agent or in your env file
- `5:59` — Updating an existing install and switching engines (preferences persist)
- `6:23` — Local mode: frames + transcript, WhisperX on-device transcription, Efficient/Balanced/Token Burner settings
- `7:07` — Engine choice: Gemini for most jobs; local when Claude must inspect actual frames (motion-graphic recreation)

## Transcript
<details>
<summary>Full transcript</summary>

AI can now watch videos for free without burning up your usage limit. Up until now, the only way that AI could watch video meant feeding it hundreds of screenshots, but Google just released something that lets AI understand video perfectly, and you can get it for completely free. Look at this test from Google. Across 50 video understanding questions, the agentic version gets more answers right while burning 87% fewer tokens. So, I plugged it straight into the watch skill, and now you can use it with any AI tool. Here's how it works and the best three use cases for it. Even the best models like Fable and Astra can't understand video out of the box. So, watch is a free agent skill that you can give your AI to give it a way to understand videos. Once it's connected, you just hand it a link and tell it what you want to know. So, I'll give it Alex from Mozie's video how to win with AI in 2026 and ask my Claude to break down the hook and why this video works. Behind the scenes, the watch skill sends the link and my question to Gemini. Gemini looks through the video, finds the parts that it needs, and sends the analysis back to my AI with the timestamps. That's what agentic video understanding means here because Gemini can decide where to look more closely.

It uses the pictures, the audio, and the transcript together to answer your questions. And the YouTube link goes straight to Google's supported API, so there's no downloading involved and you never get blocked. My AI gets the findings instead of hundreds of screenshots, and the video analysis runs completely free on Google's free API tier. This works exactly the same in ChatGPT as well. And I'll actually show you how to set up both of them at the end of this video. And now that I've got the answer back main Claude conversation, I can ask Claude to use that information that I just got from the video to help me script my next one. Let me show you what else you can do with watch. First up is using AI to find one tiny detail buried in hours of footage. So, let's test it on Andrej Karpathy's deep dive into LLMs like ChatGPT. It's a three and a half hour long video, and somewhere in here is a tool that breaks text into tokens. Say you remember seeing that tool, but you've forgotten what it's called. All I need to do is describe what I remember and ask Watch to find it. "Watch this video, find the demonstration where Kapathy types text into a tool that displays it as colored pieces with numbers beside it. Tell me the tool's name and website, and give me the timestamp." And we're going to open up that timestamp against it to check if that's the actual screen.

There it is. That's the useful part right here. You can ask it about something that only appears for a few seconds and have the AI look for it, and it works on your own footage, too. So, if you've got a folder of screen recordings and a shot where I open a particular menu, I can have my Claude use Watch to find it, then give that section straight to my editing tools. Number two is using AI to work out what was happening in your video when people stopped watching, and then help you actually improve it. I'm using my Book to Skill video here as the example. This is the video where I gave Claude five of the best business books of all time and turn them into skills. It's got about 100,000 views, and because it's my video, I have the actual retention data. So, we can see where people leave, then I can look at what I was saying and showing at that specific point. So, I'll give Claude the numbers and then have Watch analyze the footage around those drops. "Watch this video, use the retention analytics to figure out the three biggest audience drops, and tell me what caused it." Now, Claude can't tell me exactly why somebody clicked away, but it can line up the drop with the actual content and help me look for a pattern. And then, once we apply this to multiple videos in my catalog, we can start to incorporate all of those learnings into my scripting for the next videos.

And this doesn't just work on YouTube, either. You can actually apply this to any social media because the skill supports over 1,300 sites, including TikTok and Instagram. And you don't have to point it just at your content, either. You can point it at other people's content and figure out what made their videos work. So, that's using Watch to improve your content, but before we get into the next one, if you want to build an AI operating system that runs your entire business, that's what we'll do in my next Founder OS Bootcamp. I'll hand over my exact setup, all of my AI playbooks, and teach you to adapt them into your business. Join the waitlist below to get first access. And number three is having AI take notes on the videos that you watch and save them straight into your LLM Wiki. Because you've probably watched something useful, thought you'd remember it, then have to go and find that entire explanation again a week later. So, I want to use AI to keep the useful parts somewhere it can read the next time that we're working on something. Here, I'm using the same Kaparthy video from the first demo, and I'll ask Watch to pull out the explanations and visual examples, then hand them to Claude to save those into my LLM Wiki. These notes are being saved into an LLM Wiki, which is just a collection of linked notes that your AI can read. But, you could just as easily have your AI build these out into documents for your notes as well.

So, now that you've seen what you can do with the Watch skill, let me show you how to get it installed in 5 minutes. The Watch skill itself is free, and the Gemini model it uses underneath has a free API tier, so this entire thing should cost you zero. Because on the free Google tier, you get up to 8 hours of YouTube videos per day. And if you hit that limit, you just wait for it to reset. It doesn't automatically start charging you. Claude still uses his own allowance for the analysis and to put the answer to work, but Gemini handles all of that video analysis using Google's allowance, so it's essentially free. And the best part is you only need to do this setup once in the environment where you want to use Watch. After that, you can just give it a video as part of whatever you're working on, and it'll just work. And if you want the detailed instructions for the setup in ChatGPT and Claude, head to the link below where I've got the full setup guide that steps you through the entire process. But, if you're in Claude desktop, open the customize menu, go to plugins, add the Watch repository as a marketplace, then install Watch. For ChatGPT desktop, head to the plugin menu as well, and then add a marketplace, hit install plugin, and you're done. Once you're done that, open up a new chat and type {slash} watch and go through the setup process.

For the Gemini backend to work, we'll need an API key, which is what lets your AI connect into Gemini. Head to Google AI Studio, go open API keys, click create API key, and select your project. Check that the project is on the free tier. You don't need to enable billing to get started. Give that API key to your agent and it'll save it for you. If you're not comfortable doing that, you can just ask it to open your environment file and save it there manually. Now, give it a video link and ask it to use watch to watch the video. If you've already installed a previous version of the watch skill, all you have to do is jump into your plugin marketplace and hit update. Then ask it to select the Gemini engine or the new local transcription option we'll talk about in a second. If you install it as a standalone skill, ask it to update it from the same repository and start a new session. One thing to watch out for, updating keeps your existing preferences. So, if you want to use Gemini, ask your agent to switch engines and add your key. And if you don't want to use Gemini at all, the original workflow is still there. Choose local and the skill prepares frames and a transcript for your AI to read, and this version of the skill adds Whisper X, which transcribes your audio on your computer completely free when captions aren't available.

For the local setup, there are settings that control how many frames Claude sees and how many tokens it uses. Efficient adds a smaller selection of frames for a quick look. Balanced picks frames around scene changes like a new slide or a screen demonstration, and token burner removes the cat entirely for more coverage, but uses way more of your Claude allowance. I'd start with balanced and choose a Whisper X for the local transcription if you want to go the local route. Let the model finish its one-time installation and then you're ready to use it. I use Gemini for most things like asking questions about a YouTube video or finding a particular moment. It handles the watching entirely, so we never have to download the video, we just hand the URL. Claude takes the findings, so that saves Claude having to read all of those frames, but there actually still jobs where I want to use the original local engine. Say I'm recreating a motion graphic. I want Claude to see the actual frames directly while it's building, so we can inspect the layout, pull another frame at that specific timestamp, and then compare that ref with its own render. With Gemini, it's working from Gemini's description. With local, Claude can inspect the pictures itself. That uses more of your Claude allowance, but that direct visual reference can be worth it when you're trying to get an animation looking right or something that needs that particular level of detail.

But, the good news is that you can pick your engine at whatever time and switch up whenever you need. So, you don't have to pick one forever. The setup guide for the watch skill is free at the link below. There you'll find the link to download it directly. And if you want to join my next Founder OS Bootcamp, that's going to be down there as well. If this video was useful, hit subscribe. Thanks for watching.

</details>
