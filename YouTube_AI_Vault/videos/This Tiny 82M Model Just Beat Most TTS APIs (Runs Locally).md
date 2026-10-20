---
title: "This Tiny 82M Model Just Beat Most TTS APIs (Runs Locally)"
video_id: bdf6BxyxCnQ
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-03
processed: 2026-07-05
duration: "5:41"
url: https://www.youtube.com/watch?v=bdf6BxyxCnQ
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [local-text-to-speech, voice-agent-tts]
tools: [Kokoro-82M, Python]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This Tiny 82M Model Just Beat Most TTS APIs (Runs Locally)

![thumbnail](https://i.ytimg.com/vi_webp/bdf6BxyxCnQ/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=bdf6BxyxCnQ) | 📅 Uploaded [[uploaded/2026-04-03]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Kokoro-82M, an 82-million-parameter open-source TTS model trained on under 100 hours of data, ranks near the top of TTS leaderboards despite its tiny size, running fast on CPU (even faster on Apple Silicon) with no GPU required. Better Stack installs it in about 30 seconds on a Mac M4 Pro and demos English and French speech generation, weighing it against both cloud TTS APIs and much larger open models.

**Watch this if:** you're building voice agents or local speech pipelines and want a free, private, low-latency TTS option that doesn't need a GPU.

## Key Takeaways
- Kokoro-82M is a StyleTTS2-based model with a lightweight vocoder — built to sound good without being huge, unlike larger open alternatives (XTTS, CosyVoice, F5 TTS) that run into the hundreds of millions to over a billion parameters.
- It's Apache 2.0 licensed, runs on CPU, and performs especially well on Apple Silicon, generating speech noticeably faster than typical paid cloud APIs in the demo.
- Setup took about 30 seconds via pip install into a conda environment, using the official repo's Python script unmodified — no GPU, no cloud dependency, no API key.
- Live demo generated natural-sounding English and French speech (saved as WAV files) with no perceptible cloud latency.
- Supports 8 languages and 54 voices with reasonably good control via their "Misaki" text-processing import, but does not support zero-shot voice cloning out of the box.
- Emotion control is essentially absent — output stays neutral, which is fine for narration but weak for anything dramatic; non-English voice quality is also still improving.
- Because it's so lightweight, more instances can run per machine than larger models, which matters for cost at scale, and running fully offline eliminates cloud latency spikes, API keys, and per-request billing.
- Overall verdict: not perfect (no voice cloning, limited emotion), but it solves the cost, latency, privacy, and deployment problems that most developers building voice features actually have.

## 🛠 Tools & Software
- [[topics/Kokoro-82M]] — the 82M-parameter open-source TTS model installed and demoed end-to-end: local install, English and French speech generation, and a breakdown of its architecture, languages, and limitations.
- [[topics/Python]] — the official Kokoro repo's script is run directly (in a conda environment) to generate speech locally with no code changes needed.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Try Kokoro-82M locally via pip install if you need low-latency, private TTS for a voice agent or local app.
- Test its 54 voices and 8 supported languages against your specific use case, keeping in mind weaker non-English voice quality.
- If you need zero-shot voice cloning or expressive/emotional delivery, evaluate alternatives (XTTS, CosyVoice, F5 TTS, or a cloud TTS API) instead.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: an 82M-parameter model beating larger TTS systems, running locally faster than paid APIs
- `0:30` — Why cloud TTS APIs and large open models both fall short for developers (cost, latency, hardware)
- `1:03` — What Kokoro-82M is and why developers are switching to it
- `1:31` — Installing Kokoro-82M via pip in about 30 seconds
- `1:45` — Live demo: local TTS generation on a Mac M4 Pro with no GPU
- `2:22` — English speech sample generated and played
- `2:39` — French voice sample generated and played (24kHz output)
- `2:50` — Architecture breakdown: StyleTTS2 with a lightweight vocoder, compared to larger models like XTTS and CosyVoice
- `3:25` — Limitations: no zero-shot voice cloning, neutral emotion, improving non-English voices
- `4:00` — What Kokoro-82M fixes: speed, offline use, privacy, and cost at scale
- `4:30` — What the presenter loved and disliked about it
- `5:20` — Final verdict on whether it's the best local TTS option for developers

## Transcript
<details>
<summary>Full transcript</summary>

An 82 million parameter model just beat much larger TTS systems and it runs locally on a laptop faster than most paid APIs. Last month I paid for a cloud TTS but still got some lag. That made no sense to me. How are some of these open-source models beating this? This is Kakoro 82M and it's already being shipped by some devs. Let's see how this works and better yet, how it sounds.

Okay, now if you're building with text to speech, you're usually choosing between two bad options. First option is obviously cloud API's, right? They're easy to start but now you've got these bills, latency spikes, and one more dependency every time your app speaks. Then the next option would be something like these big open models. But now you need a lot more hardware, more memory, and it's still, let's face it, not that fast. So the thing that's supposed to feel smooth ends up feeling slow, expensive, or it just plain breaks.

This is where Kakoro fits in. It was trained on less than 100 hours of data but still ranks at the top of leaderboards. It beats much larger models with a fraction of the size. It's Apache 2.0, runs on a CPU, and it flies on Apple silicon. And generates speech honestly insanely fast. So now local voice apps and real-time agents actually start to make more sense. If you enjoy coding tools and tips like this, be sure to subscribe. We have videos coming out all the time.

All right, now let me show you this. I'm running all this locally on a Mac M4 Pro. The setup takes like 30 seconds. I'll just run with this pip command here. I am in a conda environment but that's pretty much it. I've got this whole Python script from their official repo. I didn't have to change anything to test this out. It's just drag and drop. We get all these outputs. I can choose a voice and a language right here. But for the first round, I'm just going to leave it set as it is because honestly, it sounds really good. I'm going to run it and then let's listen.

Better Stack is the leading observability platform. That makes monitoring simple. It has AI, SRE, logs, metrics, traces, error tracking, and incident response all in one place.

Not going to lie, that was that was pretty good and it came out really fast. Now if I flip the switch, let's do French and switch to the French voice, change the text a little bit, and again let's run it.

Better Stack est la plateforme d'observabilité propulsée par l'IA. Il simplifie enfin le monitoring.

Okay, now my French is rusty so don't translate that word for word but that sounded pretty good as well. You guys can be the judge of that though. It all saves as a wave file so I can download them as I want. There's no cloud, there's no GPU. That was pretty crazy.

So what actually is Kakoro 82M? At a high level, it's a style TTS 2 model with a lightweight vocoder. All that means is it's built to sound good without being huge and that's really the key difference here. Most other options go bigger. So XTTS, Cozy Voice, F5 TTS, hundreds of millions to over a billion parameters. Then cloud tools like 11 Labs or OpenAI, they do solve the hardware problem but now we're paying per request and sending our data out. Kakoro goes the other direction. It's small, it's fast to start, and it runs locally. Plus it uses way less memory.

But the downfalls are it doesn't do zero-shot voice cloning out of the box. Instead, it focuses on efficiency and quality that we could actually ship a lot faster. We still get eight languages, 54 voices, and pretty good control with their import Misaki. I can see where all this is going to fit really well in different types of agents but you do not get any type of emotion, which is what I really wanted to see here. An AI without emotion is still going to sound heavily like AI, which I guess can be good at times, right? But it would be fun to play around with that emotion.

So why are devs actually using this? Well, if I didn't show you, let's touch on it. Because it fixes the stuff that usually breaks voice features. First is the speed. If your agent pauses too long, it stops feeling real. Kakoro cuts that delay way down. Then the offline use is here. There's no internet, there's no API keys. I don't have any random failures. That's great. The privacy is pretty big because Kakoro keeps everything local. So for me, for a lot of you, that might be a huge win. And finally, cost at scale. Because it's so lightweight, you can run way more instances on one machine.

What's great and what's not? I loved it's fast and small. It sounds natural for long-form content. That was really cool. I've played around with a bunch of these. It is Apache 2.0 so you could ship it and after setup, it's basically free. All of these are really, really nice. Now I love those. That was cool. But there are things that I didn't like. The no native voice cloning, it depends if you need voice cloning, okay? Could have had that. Emotion is pretty neutral. Great for narration, it's not great for anything dramatic. I mean, there really is no ability to change emotion here. Plus a non-English voices are still improving. So that needs to be added, maybe not, depends on how you view this.

So is it perfect? No. But for the problems most of us actually have, cost, latency, privacy, deployment, it does seem to solve the right ones right now. Play around with it and let me know. Kakoro 82M proves you don't need a massive model to get really good TTS. Smaller means faster, faster means usable, and then usable usually means you can actually ship it. If you're building voice agents or local tools, this is worth trying out. If you enjoy coding tools and tips like this, be sure to subscribe to the Better Stack channel. We'll see you in another video.

</details>
