---
title: "My Claude Code Can INSTANTLY Watch Any Video (Here's How)"
video_id: QZMljuD10sU
channel: "[[channels/Brad - AI & Automation]]"
uploaded: 2026-04-29
processed: 2026-07-05
duration: "8:36"
url: https://www.youtube.com/watch?v=QZMljuD10sU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [video-content-analysis, obsidian-second-brain-automation]
tools: [Claude Code, yt-dlp, ffmpeg, Whisper, Groq, OpenAI, Obsidian, GitHub]
llms: [Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# My Claude Code Can INSTANTLY Watch Any Video (Here's How)

![thumbnail](https://i.ytimg.com/vi/QZMljuD10sU/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=QZMljuD10sU) | 📅 Uploaded [[uploaded/2026-04-29]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Brad gives away a free Claude Code skill that makes Claude "watch" any video (YouTube, Instagram Reels, Looms, local files) instead of just reading its transcript, by combining timestamped frame screenshots with a per-second transcript. It runs entirely on free/local tools — yt-dlp downloads, ffmpeg extracts frames and audio, YouTube captions are pulled for free when they exist, and Groq's free-tier Whisper transcribes when they don't — processing a 45-minute lecture in under two minutes for about $1 in Claude usage.

**Watch this if:** you regularly need to extract information from videos (research, competitor content analysis, debugging screen recordings) and don't want to manually scrub and re-watch them.

## Key Takeaways
- Anthropic has no video model, so by default Claude can only read a video's transcript and misses everything that happens visually on screen — which the skill argues is often "half the interesting stuff" in any video.
- The skill decomposes a video into the two things Claude already understands, pictures and text: yt-dlp downloads the source (supports 1,000+ sites), ffmpeg extracts periodic screenshots plus a clean audio track, and the two are handed to Claude together with aligned timestamps.
- Typing `/watch <url>` in Claude Code processed a 45-minute Sam Altman YC lecture in under two minutes, including catching on-screen graphs never mentioned in the spoken transcript.
- Transcription cost is nearly zero in practice: YouTube's own free captions are pulled directly when available; Whisper (hosted on Groq, chosen for speed, or OpenAI) only kicks in for uncaptioned sources like raw MP4s, Looms, or Reels, and Groq's free tier (2 hours of transcription per hour) comfortably covers daily use.
- Frame extraction is capped at 100 frames for anything over 30 minutes, so a 30-minute and a 1-hour video cost roughly the same — about $1 of Claude usage per run; three parallel full test runs across the video burned under 10% of one session.
- Beyond passive summarizing, the skill supports zoom/start-time/end-time flags to focus frame extraction on a specific window (e.g. a 10-second segment inside a 2-hour video) without burning the whole context window — useful for tasks like breaking down a video's hook or finding the exact frame where a bug/crash starts in a screen recording.
- Brad's own favorite use case: feeding every competitor's video into Claude via the skill so it watches each one (frames, audio, everything) and writes structured notes on what made it work directly into his Obsidian-based "second brain," turning passive content-watching into automated competitor intelligence.

## 🛠 Tools & Software
- [[topics/Claude Code]] — runs the `/watch` skill to ingest a video's frames plus transcript together and answer questions about it in the terminal
- [[topics/yt-dlp]] — downloads the source video/audio from any of 1,000+ supported sites
- [[topics/ffmpeg]] — extracts periodic screenshots and a clean audio track from the downloaded video
- [[topics/Whisper]] — transcribes audio to text only when a video lacks existing captions (raw MP4s, Looms, Reels)
- [[topics/Groq]] — the preferred host for Whisper transcription, chosen for speed and a generous free tier (2 hours of transcription per hour)
- [[topics/OpenAI]] — named as an alternative host for Whisper transcription
- [[topics/Obsidian]] — the "second brain" knowledge base the skill feeds structured video notes into automatically
- [[topics/GitHub]] — hosts the free, installable repo for this Claude skill

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — named as one of the few models that can actually process video natively, but ruled out here as too expensive and not well integrated with Claude

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install the free `/watch` skill from Brad's GitHub repo to give Claude Code the ability to process video frames plus transcript together.
- Use the zoom/start-time/end-time flags to analyze a specific window of a long video instead of the whole thing when you only need a segment.
- Point the skill at a screen recording to have Claude pinpoint the exact frame where a bug or crash state begins.
- Feed competitor or reference videos into the skill and have Claude write structured takeaways straight into an Obsidian knowledge base.

## 🔗 Related Videos
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Gemini, GitHub
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Gemini, GitHub
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude Code, Gemini, GitHub
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, GitHub
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, Obsidian
- [[videos/7 new open source AI tools you need right now]] — shared: Claude Code, Gemini
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude Code, Obsidian

## Timeline
- `0:00` — Intro: giving Claude Code the ability to instantly watch any video for free
- `0:52` — Demo: a 45-minute YC lecture watched, analyzed, and queryable in under 2 minutes
- `2:43` — Setup: free GitHub install, dependency setup, transcription API auth
- `3:43` — Under the hood: why Claude can't watch video, and the yt-dlp + ffmpeg pipeline that fakes it
- `5:18` — The cost math: ~$1 per run, frame cap at 100, nearly-free transcription via captions/Groq Whisper
- `6:30` — Use case: analyzing a video's hook (visual setup, words, pattern interrupt) for content research
- `7:03` — Use case: debugging screen recordings by finding the exact frame before a crash
- `7:42` — Use case: feeding every competitor video into an Obsidian second brain automatically

## Transcript
<details>
<summary>Full transcript</summary>

When you give Claude Code the ability to instantly watch any video on the internet for free, it becomes genuinely unstoppable. With this Claude skill, Claude can understand video as well as it reads PDFs — hours-long YouTube videos, Instagram Reels, Looms, local files, anything. Before, Claude was just guessing; now it can watch the whole thing frame by frame instantly. A bunch of transcript tools were tried before developing this one and they all fell short — they either cost too much or only ever read the transcript and missed half the video. This skill gives Claude the frames and the audio together, so it actually sees what's happening on screen.

Here's what it looks like on a 45-minute video done in a few minutes: a YC lecture from Sam Altman about how to start a startup is playing on one side. Grab the URL, go to Claude, type `/watch`, paste the URL. Claude grabs the subtitles from YouTube for free, extracts the frames, and analyzes them together. This is better than just pulling the transcript because Claude can actually grab the frames — in this lecture, Sam shows a bunch of graphs, important context that a transcript-only tool would miss entirely, since half the interesting stuff in a video isn't said out loud, it happens on screen. This skill pulls frame-by-frame screenshots and pairs them with a per-second timestamped transcript for the full picture. Just two minutes into the actual lecture, while Sam is still introducing the topic, Claude has already ingested the whole thing — a structured summary of everything the speaker covers, ready to query and put to work right in the terminal. A 45-minute video watched, analyzed, and applied in under 2 minutes.

There's no expensive API doing the heavy lifting. The skill is free on GitHub — install commands handle setup, dependencies, and authenticate with a transcription API that's pretty much free. Under the hood the pipeline is simple: Claude can't actually watch video because Anthropic doesn't have a video model yet. Other providers like Google's Gemini can, but they're expensive and don't integrate nicely with Claude, so a heavy content habit gets costly fast. The smarter way: a video is just frames and a transcript, so split it into those two pieces and hand them to Claude in formats it already reads — pictures and text — using two of the oldest, most battle-tested command-line tools around, yt-dlp and ffmpeg. These aren't MCPs, not some new wrapper, no third-party service in the middle — they install once, locally, for free, and are what nearly every video tool you've used is probably built on under the hood. yt-dlp is the download (like a universal "save video" that works across the internet); ffmpeg is the video engine, turning the download into periodic screenshots and a clean audio file ready for transcription via Whisper. With both pieces, Claude flips through screenshots like a flipbook while reading the transcript like a script, timestamps aligned so it knows what's on screen when something is said.

The only real cost is transcription and Claude usage, and transcription is nearly free: the skill pulls existing captions directly when they exist, and only falls back to Whisper (hosted on Groq, preferred for speed, or OpenAI) when they don't. Most videos cost literally nothing to transcribe. This exact skill has also been used to grow a personal "universal context layer" for content research. On the token-budget worry: the skill scales frame count to video length and caps anything over 30 minutes at 100 frames, so a 30-minute and a 1-hour video cost about the same, roughly $1 per run. Running every test in this video three times in parallel burned under 10% of one session — over 5 hours of video watched live by Claude with transcription included. Groq's free tier gives 2 hours of transcription per hour, more than most people realistically need; two weeks of daily use and still on the free tier.

Because it works on any URL yt-dlp supports (1,000+ sites) and on locally downloaded files, this opens use cases beyond the obvious. For content research: take a winning video and ask Claude to break down the hook — the visual setup, the exact words, where the pattern interrupt lands, and what's on screen at that moment — work that used to take 10 minutes of pausing and scrubbing per video, now just a paste. For developers: drop in a 30-second screen recording of a UI bug and ask what happens right before the crash; Claude reads the surrounding frames, finds the state change, and names the exact frame where the issue starts. The skill also has zoom, start-time, and end-time flags to focus frame extraction on a specific window, so you can ask about a 10-second segment of a 2-hour video without burning the whole context window.

The favorite personal use case is feeding a "second brain": a knowledge base kept in Obsidian with notes, snippets, and content ideas, where the bottleneck has always been throughput — too much good content, not enough time to watch and write it all up. Every competitor whose content is considered great gets fed to Claude, which uses the watch skill to watch each video (frames, audio, everything) and comes back with a clean structure of notes on what made it work, built straight into the second brain. Over time the second brain and the skill compound — more videos watched, more context, getting smarter automatically. The full second-brain setup (content research, competitor intel, every podcast video in one searchable Obsidian layer) is covered in a separate video.

</details>
