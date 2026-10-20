---
title: "Claude + HeyGen Just Changed Content Creation Forever"
video_id: EbJu9T30nfI
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-04-15
processed: 2026-07-05
duration: "20:17"
url: https://www.youtube.com/watch?v=EbJu9T30nfI
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [ai-video-content-pipeline, avatar-voice-cloning-automation]
tools: [HeyGen, ElevenLabs, Claude Code, Remotion, FFmpeg, Playwright, Google Drive]
llms: [Claude, ChatGPT]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude + HeyGen Just Changed Content Creation Forever

![thumbnail](https://i.ytimg.com/vi/EbJu9T30nfI/sddefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=EbJu9T30nfI) | 📅 Uploaded [[uploaded/2026-04-15]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> The creator reveals his entire YouTube appearance was an AI clone made with HeyGen's new Avatar 5 model plus an ElevenLabs voice clone, then shows how Claude Code orchestrates the full pipeline — chunking scripts, generating HeyGen clips via API, upgrading them to Avatar 5 with a Playwright workaround, and handing off to Remotion for automated motion-graphics editing — turning a 5-hour production job into an overnight, hands-off run.

**Watch this if:** you want to build an automated pipeline that turns a raw script into a finished, edited talking-head video without recording yourself.

## Key Takeaways
- HeyGen's new Avatar 5 model (trained on 10M+ facial-expression data points) crosses the uncanny valley — natural gestures and lip movement from just a 15-second webcam clip or uploaded footage, a big jump from the more robotic Avatar 3/4.
- Voice cloning is a two-stage process: HeyGen's built-in voice clone isn't good enough, so the creator imports a professional ElevenLabs voice clone (trained on ~2 hours of audio, though ElevenLabs says 30 minutes minimum) into HeyGen via AI Studio.
- Clips need to stay short: HeyGen caps Avatar 5 generations at 3 minutes, and ElevenLabs audio quality degrades past about a minute, so scripts are chunked into 45-60 second sentence-boundary segments.
- Claude Code researched the HeyGen and ElevenLabs API docs and now fully orchestrates the pipeline — pulling scripts from Google Drive, chunking them, generating audio, sending it to HeyGen, and handing clips off for editing — run overnight with zero manual clicking.
- Avatar 5 can't be generated via the HeyGen API yet (only Avatar 3/4 can), so a Playwright script opens the HeyGen dashboard, creates a new revision, swaps the avatar to Avatar 5, and downloads the upgraded result as a workaround.
- Remotion handles final assembly: it transcribes the finished video, aligns motion-graphics text/animations to the exact second something is said, and renders in a localhost browser preview.
- Cost breakdown: HeyGen creator plan (~$30/mo, limited Avatar 5 generations), ElevenLabs creator plan (~$22/mo, ~100 minutes of audio), Claude Code ($20-200/mo), plus HeyGen API usage at roughly $4/minute of generated video (~$50 for a 10-minute video) — pitched against a human alternative of $35-75/hour freelance editing plus voiceover/studio costs.
- Framed as shifting the content bottleneck away from production/post-production (now largely automated) and back toward ideas, scripting, and strategy — where the human stays essential.

## 🛠 Tools & Software
- [[topics/HeyGen]] — AI avatar platform; Avatar 5 model, voice import, and AI Studio audio-to-video generation are the core of the video-creation half of the pipeline
- [[topics/ElevenLabs]] — used to create a professional voice clone (from ~2 hours of audio) that gets imported into HeyGen for far more natural-sounding narration than HeyGen's native clone
- [[topics/Claude Code]] — the orchestration layer: researches the HeyGen/ElevenLabs APIs, pulls scripts from Google Drive, chunks them, and drives the entire script-to-video pipeline autonomously overnight
- [[topics/Remotion]] — used to transcribe the finished HeyGen clips and auto-sync motion graphics/text animations to the exact timestamp of the spoken words
- [[topics/FFmpeg]] — used alongside Remotion in the editing/stitching step of the pipeline
- [[topics/Playwright]] — automates a browser workaround that upgrades API-generated Avatar 4 clips to Avatar 5 by clicking through the HeyGen dashboard, since Avatar 5 isn't yet API-accessible
- [[topics/Google Drive]] — where Claude Code is instructed to find and pull the raw scripts that feed the pipeline

## 🤖 LLMs Mentioned
- [[topics/Claude]] — powers Claude Code, the orchestration layer that ties HeyGen, ElevenLabs, Playwright, and Remotion together into one automated pipeline
- [[topics/ChatGPT]] — referenced in passing when addressing the "is this authentic" objection (viewers care that it's not just a ChatGPT-written script, even if the avatar/voice are cloned)

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Record a 15-second webcam clip (or upload existing footage) in HeyGen to generate an Avatar 5 clone, and separately build a professional voice clone in ElevenLabs.
- Chunk long scripts into 45-60 second, sentence-boundary segments to stay within HeyGen's clip cap and avoid ElevenLabs audio-quality degradation.
- Have Claude Code research the target APIs (HeyGen, ElevenLabs) directly rather than hand-rolling integration code, then have it orchestrate script pull → chunk → voice → avatar → edit end-to-end.
- If a needed feature (like Avatar 5) isn't API-exposed yet, consider a Playwright-driven browser workaround as an interim automation step.
- Budget realistically: expect roughly $50 in HeyGen API costs for a 10-minute video, plus ~$70+/month in HeyGen/ElevenLabs subscriptions, versus $300+ for human freelance editing/voiceover per video.

## 🔗 Related Videos
- [[videos/How To Make Passive Income On Day 1 With Claude (New Method)]] — shared: ChatGPT, Claude, ElevenLabs, HeyGen
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, FFmpeg, Playwright
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, Claude Code
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Playwright
- [[videos/Claude Code Skills Just Got Even Better]] — shared: ChatGPT, Claude, Claude Code
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Playwright
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, Playwright

## Timeline
- `0:00` — The AI Clone Reveal
- `0:40` — The Three-Tool Stack
- `1:05` — Output Demo
- `2:28` — Setting Up HeyGen & ElevenLabs
- `6:35` — Generating Avatar Videos
- `8:59` — Automating with Claude Code
- `11:13` — Editing with Remotion
- `13:05` — Why This Matters Now
- `15:13` — Objections & Pricing
- `19:42` — Final Thoughts

## Transcript
<details>
<summary>Full transcript</summary>

Today's video shows how the creator automated hours of recording content using Claude Code and HeyGen — the video's on-camera presenter is actually an AI clone made in about 10 minutes, the creator's first time revealing this. Claude Code acts as a complete orchestration layer around three tools that take a raw script to a finished, edited video in minutes: HeyGen for the avatar/clone, ElevenLabs for voice cloning, and Remotion for editing everything together into professional-looking motion graphics, after showing a sample output first.

This matters now because HeyGen released a new model, Avatar 5, a big step up from the more robotic Avatar 3/4 — natural head movement and lip sync learned from the creator's own footage. Setting up the avatar clone starts in HeyGen: record a quick 15-second script read for an instant clone, or upload footage (the creator uploaded ~10GB) for a higher-fidelity result. HeyGen can auto-clone your voice too, but the quality isn't good, so the creator instead imports a professional voice clone built in ElevenLabs. In ElevenLabs, creating a voice offers an instant clone (fast, lower quality) or a professional clone (needs at least 30 minutes of audio; the creator used about 2 hours) with tunable speed, stability, similarity, and style settings. The resulting audio clip is downloaded and uploaded into HeyGen's AI Studio, where it gets transcribed and synced to the chosen avatar (Avatar 3, 4, or the new 5) to generate the final clip.

There are real limitations: HeyGen caps Avatar 5 generations at 3 minutes, and ElevenLabs audio starts degrading in resemblance past about a minute of continuous speech (also subject to a 5,000-character limit), so the sweet spot is roughly 45 seconds to a minute per chunk — sentence-boundary chunks only, so clips can be stitched seamlessly. With 10-minute scripts to record, manually chunking, generating, and stitching everything would be extremely manual, so the creator asked Claude Code for help; it researched the HeyGen and ElevenLabs API documentation and built full automation. Now the workflow is: tell Claude Code to pull scripts from Google Drive, chunk them into part 1/2/3/4 segments of the right length, send each chunk to HeyGen, and assemble the resulting clips — run overnight with zero manual intervention (e.g., "process lessons 5.0 through 5.4," go to sleep, wake up to finished output).

One catch: Avatar 5 isn't accessible via the HeyGen API yet — only Avatar 3/4 are — so the automation generates the initial video with Avatar 4, then a Playwright script opens the HeyGen dashboard, clicks into the generated clip, creates a new revision in AI Studio, swaps the avatar from 4 to 5, regenerates, and downloads the upgraded version. This is a stopgap until Avatar 5 becomes API-accessible. A separate Remotion project handles the final edit: it transcribes the stitched video, and because it knows exactly what was said at what timestamp, it times motion-graphic text/element animations to sync precisely with the narration, rendering in a localhost preview. The plan is to fold the Remotion project into the HeyGen Studio project as a single "skill" — drop in a script, get a full finished video in one shot.

Three shifts make this a big deal: (1) the avatar has crossed the uncanny valley, removing the need for perfect lighting/quiet environments since Avatar 5 is trained on 10M+ facial data points and creates a convincing digital twin; (2) Claude Code can orchestrate an entire multi-tool production pipeline rather than just generating one asset, effectively replacing a 3-4 person production crew and compressing a 5-hour pipeline into an overnight job; (3) the bottleneck in content creation has moved from production/post-production to ideas, scripting, and strategy, where humans remain essential. Cited stats: 91% of businesses use video as a marketing tool, 67% of non-video marketers plan to start this year, and 24% cite cost as the main barrier to video.

The creator addresses three anticipated objections. "It's fake/not authentic" — he agrees to an extent, notes his own channel will never be a pure AI avatar, but argues most viewers care whether the thoughts/script are genuinely the creator's, not whether the pixels were recorded live. "Won't this flood the internet with AI slop?" — he argues AI writing/content already floods feeds regardless, and removing the production bottleneck just means more content competing on idea quality; bad content with a good avatar is still bad content. "Won't this kill video editor jobs?" — he argues the job changes rather than disappears entirely, and people with subject-matter expertise will be the ones building the best AI-powered systems in their niche.

On cost: HeyGen's creator plan runs about $30/month (limited Avatar 5 generations), ElevenLabs' creator plan about $22/month (~100 minutes of audio), and Claude Code $20-200/month for the orchestration. HeyGen API usage is billed separately — roughly $4 per one-minute clip, so a 10-minute video costs close to $50. Compared to a human alternative (a freelance video editor at $35-75/hour, a 10-minute video potentially running $300+, plus voiceover/studio costs into the thousands for course material or ads), the creator argues the investment is worthwhile if it buys back meaningful time — e.g., 10 hours/week (40 hours/month) for roughly $251/month works out to about $6/hour to buy back your own time.

A full breakdown of Remotion is planned for a future video. The HeyGen Studio project and a supporting document are shared for free in the creator's community, linked in the description.

</details>
