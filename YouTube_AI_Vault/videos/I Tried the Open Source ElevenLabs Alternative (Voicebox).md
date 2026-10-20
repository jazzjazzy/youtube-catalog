---
title: "I Tried the Open Source ElevenLabs Alternative (Voicebox)"
video_id: RL_PDX_BVxw
channel: "[[channels/Better Stack]]"
uploaded: 2026-06-17
processed: 2026-07-05
duration: "7:39"
url: https://www.youtube.com/watch?v=RL_PDX_BVxw
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [local-voice-cloning, ai-agent-voice-output]
tools: [Voicebox, ElevenLabs, Ollama, Docker, Whisper, Piper, Claude Code, Cursor, Chatterbox TTS]
llms: []
protocols: [MCP, REST]
transcript: true
tags: [youtube, ai-automation]
---

# I Tried the Open Source ElevenLabs Alternative (Voicebox)

![thumbnail](https://i.ytimg.com/vi_webp/RL_PDX_BVxw/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=RL_PDX_BVxw) | 📅 Uploaded [[uploaded/2026-06-17]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Better Stack tests Voicebox, a free open-source local AI voice studio ("the Ollama of voice") that does voice cloning, text-to-speech, system-wide dictation, and MCP-based agent voice output — a local-first alternative to ElevenLabs that trades some polish and consistency for privacy, zero cost, and full control.

**Watch this if:** you want voice cloning, dictation, or agent voice output without a subscription, API keys, or sending your voice data to the cloud.

## Key Takeaways
- Voicebox is a free, open-source, local-first AI voice studio — described as "Ollama for voice" — bundling voice cloning, text-to-speech, system-wide Whisper-powered dictation, a multi-track editor, MCP support, and a local REST API into one Tauri desktop app.
- The desktop app installs far faster than Docker (the reviewer's Docker setup took nearly 30 minutes vs. the desktop app being quick) and needs no subscription, API keys, or character limits since everything runs on-device.
- Live demo: cloned a voice from a short recording, generated speech from typed text entirely locally, and used system-wide dictation via a global hotkey that typed directly into the code editor.
- Via MCP, coding agents like Claude Code and Cursor can call Voicebox as a tool to speak responses back to you (e.g. "Build failed, three test modules broke") instead of only outputting text.
- Compared to ElevenLabs: ElevenLabs still wins on hosted quality and consistency for heavy daily use, but Voicebox wins on privacy, cost (free/unlimited), and data control — and it consolidates what used to require separate tools (Piper, Whisper, custom scripts) into one app.
- It's still early software (released this year) — expect rough edges, especially on Windows around GPU detection, model setup, and exports (restarting the app fixed the reviewer's issue on Mac). Long-form consistency and emotion control still lag ElevenLabs, though picking a model like Chatterbox TTS Turbo helps with emotion.

## 🛠 Tools & Software
- [[topics/Voicebox]] — the free, open-source local AI voice studio being reviewed: cloning, TTS, dictation, editing, agent integration
- [[topics/ElevenLabs]] — the cloud-based paid voice AI tool Voicebox is compared against as the incumbent quality benchmark
- [[topics/Ollama]] — used as the framing analogy: "Voicebox is trying to be that for voice" the way Ollama is for local text models
- [[topics/Docker]] — one install path for Voicebox, found slow (~30 min) compared to the desktop app
- [[topics/Whisper]] — powers Voicebox's system-wide dictation feature
- [[topics/Piper]] — cited as one of the separate open-source tools Voicebox replaces by bundling everything into one app
- [[topics/Claude Code]] — an agent that can speak back to the user via Voicebox's MCP integration
- [[topics/Cursor]] — another agent that can use Voicebox's MCP integration for voice output
- [[topics/Chatterbox TTS]] — the specific TTS model recommended (Turbo variant) for better built-in emotion control

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — Voicebox exposes an MCP server so Claude Code/Cursor can trigger speech output as a tool call
- [[topics/REST]] — Voicebox ships a local REST API alongside its desktop app

## ✅ Action Items
- Download the Voicebox desktop app (not Docker) from voicebox.sh or its GitHub releases for the fastest setup.
- Clone your own voice from a short recording and test local text-to-speech generation before committing to a cloud tool.
- Enable system-wide dictation with a global hotkey to speak notes/comments directly into your editor.
- Wire up the Voicebox MCP server so Claude Code or Cursor can speak status updates back to you instead of just printing text.

## 🔗 Related Videos
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Cursor, ElevenLabs, MCP
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, Cursor, Docker, MCP
- [[videos/The Best MCP Servers of 2025]] — shared: Claude Code, Cursor, Docker, MCP
- [[videos/Claude Code But It's Entirely Local]] — shared: Claude Code, Ollama, REST
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor, MCP
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: Claude Code, Cursor, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor, MCP
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Cursor, MCP

## Timeline
- `0:00` — Voicebox: free local AI voice for developers
- `0:40` — What Voicebox is and why developers care
- `1:53` — Live demo begins: voice cloning, TTS, and dictation
- `2:20` — Cloning a voice and generating local AI speech
- `3:13` — Using Voicebox for dictation inside the editor
- `3:30` — Giving Claude Code a voice with Voicebox via MCP
- `4:00` — Voicebox vs. ElevenLabs and other open-source voice tools
- `5:45` — Real talk: pros, cons, and current limitations
- `6:55` — Is Voicebox worth it for developers?
- `7:17` — How to get started with Voicebox, MCP, and local AI voice

## Transcript
<details>
<summary>Full transcript</summary>

They say this is the llama of voice AI. It clones voices, generates speech, dictates into any app, and talks to agents in voices you actually own. This is Voice Box, and that's what it says right here. It's free and a local alternative to 11 Labs, and honestly, this was insane. It has around 30,000 stars on GitHub. It runs locally, and in the next 60 seconds, I'm going to show you cloning, local voice generation, and dictation inside an editor. How useful is this for us, and how easy is it to get going in the first place? We are about to find out.

Now, Voice Box is an open-source local AI voice studio. The simple way to think about it is this: Ollama is for local text models, Voice Box is trying to be that for voice. So it's not just text-to-speech — it does voice cloning, system-wide dictation, creative editing, and it even has stories and timelines, and it connects to AI agents. So this gives us real control and even more privacy. I want to build things without asking "how many credits did I just use to test this?" Voice Box doesn't ask that, because Voice Box runs on our machine. So there's no subscription, there's no character limits. Plus, it brings together cloning, Whisper-powered dictation, a multi-track editor, a Tauri desktop app, MCP support, and a local REST API. So instead of five separate tools, you get one desktop app with everything.

I'm going to do three things in this video: clone a voice, make it speak, and then use dictation inside the editor. After that, I'll show you why the agent integration is actually super interesting. Now I'm running this on my Mac M4. Here is Voice Box. I already have a voice profile ready, but the flow was really simple. Now you can spin this up with Docker, yes, but I did that and it took nearly 30 minutes to get the containers going. So for this, I opted instead to get the desktop app, which was way faster and it's honestly really good. I can name the audio here, add a description, and even tell it how to act with the models. Then I can either record myself speaking or upload a short file for it to analyze, while also dropping in the transcription of that audio.

Now I'll type a line that I would actually want to use: "As a developer, this gives me complete control over voice AI without cloud costs and all that privacy stuff." I'll choose my voice profile, choose the model I want, and hit generate. The first run has to download the model, so it might take some time. But after that, we get waveforms — let's take a listen. That audio was generated locally from my machine and I cloned my own voice. There was no browser tab, I didn't need API keys.

But here's the part that feels like a real workflow: system-wide dictation. I could hit a global hotkey and say whatever I'm thinking in the moment, and it lands directly inside my editor. That was pretty useful for notes, comments, or anything like that — all these little moments where talking is actually faster than typing, that's huge. This is not only for you talking to the computer — your agents could actually talk back now. Claude Code, Cursor, or your own local agent can trigger speech through Voicebox instead of just dumping it into your terminal. We're already getting feedback from our AIs — why not have it speak to us?

Now let's compare this with tools we already know, for obvious reasons: 11 Labs. 11 Labs is great, bravo, I've done comparisons on that before. It's hosted, the quality is amazing, but it's cloud-based and subscription-driven — we're paying for that, and we're putting our stuff up in the cloud. Voice Box is the complete opposite: it's local, it's free, it's unlimited, we control all the data going into it. 11 Labs may still win if you're using it all day, but I think I'll be keeping Voice Box — I loved how easy it was, and honestly it sounds really decent too. For us devs, the best tool is not always the one with the prettiest output; sometimes it's the one you can actually control.

Then there's the whole open-source side. You could already use tools like Piper, Whisper, and a bunch of separate scripts, but the key thing is they're all separate — one tool for transcription, one for cloning, one for TTS, one for UI, all smooshed together. Voice Box packages the whole workflow into one studio app: input, output, editing, profiles, dictation, agent integration, and you could also use the MCP server. That means Claude or Cursor can call Voice Box like a tool — instead of your agent only replying with text, it now speaks back to you. Imagine your coding agent saying, "Build failed, three test modules broke the auth module." That sounds unreal until you realize how many times a day you're already getting feedback from your tools — Voice Box just gives those updates an actual voice.

So why did I like this one so much compared to others? Privacy and cost — those are the really big wins for me, easy wins. For voice samples, audio, internal content, or anything sensitive, local-first is what we want. Then there's the agent integration, which I didn't put into the full test here, but devs are already talking about integrating it into Claude Code and Cursor — Voice Box gives those systems a voice layer without needing a hosted speech provider. The workflow was pretty neat, and if you're on Apple Silicon especially, local performance is one of the reasons this felt so good.

But here's the thing to keep in mind: it dropped this year, it's still early, so there's going to be problems. Some users will hit rough spots if they're on Windows, especially around GPU detection, model setup, and exports — if that happens, just restart the app (I had the issue on my Mac, restarting fixed it). Long-form consistency can also still fall behind 11 Labs, and emotion control, while improving, depends on the model you choose — if you choose Chatterbox TTS Turbo, you then have those emotions built in.

So should you install Voice Box? Honestly, it was super easy, and it's absolutely worth trying because it takes away a lot of the friction from workflows that we're just piecing together. The main value isn't just voice quality — it's the control we're given: control over data, control over cost, control over integration. Getting started was dead simple: go to the Voice Box website or GitHub releases, download the installer for your platform, launch the app, and pull the local models you need. The core idea here is really strong, and it's already useful enough to actually install.

</details>
