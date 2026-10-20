---
title: "Pick the Wrong Gemma 4 and You'll Think It's Broken | FOUR Models Compared!"
video_id: SLOqlEmuy5U
channel: "[[channels/DIY Smart Code]]"
uploaded: 2026-04-19
processed: 2026-07-05
duration: "9:00"
url: https://www.youtube.com/watch?v=SLOqlEmuy5U
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [local-llm-selection, hardware-sizing]
tools: [Ollama, LM Studio, llama.cpp, vLLM, Raspberry Pi]
llms: [Gemma, Qwen, Kimi, Claude Sonnet]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Pick the Wrong Gemma 4 and You'll Think It's Broken | FOUR Models Compared!

![thumbnail](https://i.ytimg.com/vi_webp/SLOqlEmuy5U/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=SLOqlEmuy5U) | 📅 Uploaded [[uploaded/2026-04-19]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Google shipped four open-weight Gemma 4 sizes on April 2nd — E2B (~2.3B), E4B (~4.5B), a 26B Mixture-of-Experts middle model (~4B active), and a 31B flagship — and picking the wrong one for your hardware makes the model feel broken rather than just under-provisioned. The video breaks down memory requirements, benchmark rankings, and which local-inference tool (Ollama, LM Studio, llama.cpp, vLLM) fits each tier, plus a free speed trick pairing the big and small models together.

**Watch this if:** you're about to download a Gemma 4 model and want to match the right size to your phone, laptop, or GPU instead of guessing.

## Key Takeaways
- E2B (~2.3B params, 3-5GB memory) is built for phones and Android features like on-device summaries; Google demoed it on a Raspberry Pi at around 5 words/second, but it's not built for coding work.
- E4B (~4.5B params, 5-6GB memory) runs comfortably on any modern laptop including a base MacBook Air, good for local chat and single questions but not for long multi-step agent chains.
- The 26B middle model uses a Mixture-of-Experts trick so only ~4B parameters are active at once — it needs ~24GB system memory to load (16-18GB for weights) but runs at roughly 4B-model speed, ranks 6th among open models on the independent LMArena leaderboard, and keeps a 250K-token context window.
- The 31B flagship needs 20-24GB of GPU memory, ranks 3rd among open models on LMArena, scores ~89% on a hard math Olympiad-style benchmark, hits master level on a competitive programming site, and beat every Claude Sonnet model on an agentic virtual-business benchmark.
- Head-to-head against Qwen 3.5 and Kimi K2.5 on hard problems, Gemma 4 31B lands in the same range — roughly on par despite far fewer active parameters.
- A free speed trick: running the 31B and E2B together (speculative decoding, since they share the same vocabulary) gives about a 29% average speed boost, jumping to 50% for code, if you have ~24GB total memory.
- Three early-adopter gotchas: a file-format bug broke tool calling and produced garbled text (fixed via updated re-uploads/runtime), don't override Google's baked-in recommended sampling settings, and a small unofficial tweak reportedly helps tool-calling-loop reliability.
- On tooling: Ollama is the easiest path on Windows/Mac/Linux (one command to download any size), LM Studio offers the same with a GUI, and llama.cpp or vLLM squeeze more speed for the 31B on advanced setups.

## 🛠 Tools & Software
- [[topics/Ollama]] — recommended as the easiest one-command way to download and run any Gemma 4 size on Windows, Mac, or Linux
- [[topics/LM Studio]] — offers the same local-run capability as Ollama but with a chat-window GUI instead of a terminal
- [[topics/llama.cpp]] — recommended for advanced users squeezing more speed out of the 31B flagship
- [[topics/vLLM]] — mentioned alongside llama.cpp as an advanced-user option for running the 31B faster
- [[topics/Raspberry Pi]] — Google's own demo platform for E2B, shown running near-instant responses on a $100 board

## 🤖 LLMs Mentioned
- [[topics/Gemma]] — the four Gemma 4 sizes (E2B, E4B, 26B, 31B) are the entire subject of the video, compared by hardware fit, memory, and benchmarks
- [[topics/Qwen]] — Qwen 3.5 used as one of the two rival models in the honest head-to-head hard-problem comparison against Gemma 4 31B
- [[topics/Kimi]] — Kimi K2.5 used as the other rival model in the head-to-head comparison, both landing in the same range as Gemma 4 31B
- [[topics/Claude Sonnet]] — cited as one of the larger closed models that Gemma 4 31B beat on an agentic virtual-business benchmark

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Match your hardware to the right Gemma 4 tier using the 30-second decision tree: phone/Pi → E2B, 8-16GB laptop → E4B, ~24GB system memory → 26B middle model, 24GB+ GPU → 31B flagship.
- If you have ~24GB and want a free speed win, pair the 31B with E2B via speculative decoding instead of buying new hardware.
- Before assuming a downloaded Gemma 4 model is broken, check for the known file-format bug and grab the patched re-upload or runtime update.
- Don't override Google's recommended sampling settings baked into the model card — use them as the starting point.

## 🔗 Related Videos
- [[videos/Qwen Coder Next Locally Can It Replace Paid AI Models]] — shared: Claude Sonnet, LM Studio, Ollama, Qwen
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Kimi, LM Studio, Qwen
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: Gemma, Ollama, Qwen
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Sonnet, Gemma, Qwen
- [[videos/The Real Reason NVIDIA Is Buying Hugging Face]] — shared: Kimi, Qwen, llama.cpp
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Sonnet, Ollama, Qwen
- [[videos/Anthropic Just Dropped Ultra Plan for Claude Code]] — shared: Gemma, Qwen
- [[videos/Best 120b Model for Offline Use Nemotron 3 Super Out Now]] — shared: Qwen, vLLM

## Timeline
- `0:00` — Intro: four Gemma 4 tiers, pick wrong and it feels broken
- `0:29` — The four versions Google shipped in April 2026
- `0:55` — E2B: fits on a phone, demoed on Raspberry Pi
- `1:35` — E4B: runs on 8GB laptops, good for single questions
- `2:13` — The 26B middle model: MoE trick, speed meets quality
- `3:08` — The 31B flagship: benchmark king, agentic test results
- `4:11` — Honest head-to-head vs. Qwen 3.5 and Kimi K2.5
- `4:37` — The free 29-50% speed trick pairing 31B + E2B
- `5:12` — How to run it: Ollama, LM Studio, llama.cpp, vLLM per OS
- `5:52` — Three early-adopter fixes: file format bug, settings, tool-loop tweak
- `7:26` — 30-second decision tree to pick your tier

## Transcript
<details>
<summary>Full transcript</summary>

Four Gemma 4 models, four tiers of hardware. Pick the wrong one and you'll think the model is broken. One year ago, Google's best small model got one math problem in five right. This year's version gets nine in 10 — but only if you pick the right version for your machine, and most people aren't. On April 2nd, Google shipped four sizes of Gemma 4, all free, all open source. The two small ones run on phones and laptops and can listen to audio and look at images. The middle one is the sweet spot, using a clever trick to stay small in memory but run fast. The big one is the flagship that showed up in the leaderboards.

E2B is the smallest, around 2.3 billion parameters, taking up about 3 to 5GB of memory. This is the model Google is building into the next generation of Pixel — it will live inside Android doing summaries and quick replies without sending data to the cloud. Google demonstrated it running on a Raspberry Pi, a $100 board, with near-instant responses; community tests on the Pi 5 clocked it around five words per second, fast enough to chat with. Where E2B wins: phone apps, Android features, anything where privacy matters more than raw power. Where it loses: coding — think of it as a helpful assistant, not a senior engineer.

E4B doubles the capability, around 4.5 billion parameters, about 5 to 6GB of memory. This runs comfortably on any modern laptop including a basic MacBook Air, with the same image and audio abilities as E2B. Good for local chat, asking questions about your documents, or voice input apps — anything where you type or talk to a model on your own laptop. It's not built for agents that chain lots of steps together; for single questions it's great, for long multi-step workflows, step up a tier.

The middle model is around 25 billion parameters total, with the clever trick that only a small part of it, about 4 billion, is active at any one time — meaning it takes around 16 to 18GB to load but runs at the speed of a 4 billion parameter model. On the independent leaderboard that ranks AI models head-to-head, it placed sixth among all open models, right behind its flagship sibling, at a fraction of the running cost. Plan for around 24GB of system memory — the weights take 16-18, the rest covers context and headroom. Apple silicon or a mid-to-high gaming GPU works. You get flagship quality without flagship slowness, and the full long memory window, a quarter million token context. One warning: if you compress it too aggressively, quality drops fast — stick with the recommended version.

This is the one that made headlines: around 30 billion parameters, plan for 20 to 24GB of graphics memory (17-20 for weights plus headroom for context). On that same leaderboard it's ranked third among all open models. On a hard math benchmark, the kind of problems high school Olympiad students solve, it's got around 89%. On a competitive programming site it's at master level — a few steps below grandmaster but ahead of the vast majority of human competitors. And on an agentic test where AI models run a virtual business, this one beat much larger closed models, including every Claude Sonnet. For a 30 billion parameter open model, that's the real story.

Here's the honest test the comment section keeps asking for: run the same hard problem against Qwen 3.5 or Kimi K2.5, the models critics say beat it. Gemma 4 31B lands in the same range on that head-to-head leaderboard — basically on par, with far fewer active parameters doing the work. Benchmarks tell one story, real-world runs tell a closer one. Where it wins: desktop workstations, a single decent graphics card, anyone who'd trade a bit of speed for flagship quality.

And if you have the hardware for this one, there's a speed trick most reviewers missed: run the big model and the small model together. The small one makes quick guesses, the big one double-checks them. Because they share the same internal vocabulary, it works smoothly. A community benchmark measured an average speed boost around 29%, jumping to 50% for code, if you have the memory to load both at once — around 24GB total at a standard context window. This is the biggest free speed win available right now — no new hardware, just pair two models that already share DNA.

How do you actually run these? On Windows or Mac, the easiest path is a tool called Ollama — one line to install, one command to download any Gemma 4 version, done. If you prefer a chat window over a terminal, LM Studio does the same thing with a nicer interface. On Linux, Ollama works the same way. Advanced users can squeeze more speed out of llama.cpp or vLLM, especially for the big 31B. For phones, there's a full walkthrough on running E2B on mobile in a dedicated short.

Before you download anything, three things early adopters got wrong. First, the file format: early downloads had a bug that broke tool calling and produced garbled text — the fix is already live, grab the latest re-uploaded version or update your runtime to the patched release. Second, the settings: Google baked the recommended values right into the model, don't change them, use them as your starting point. Third, if you're building something that calls tools in a loop, some users report a small tweak helps with reliability — not official, but worth trying if your agent keeps getting confused. Fix those three things and your numbers match Google's.

Here's the decision in under 30 seconds: phone or Raspberry Pi, E2B. Laptop with 8 to 16 gigs, E4B. Around 24 gigs of memory, the middle 26B, best quality-to-speed ratio with the full long memory window. 24 gigs of graphics memory or a Mac with 32 gigs unified, the 31B flagship, the benchmark king. Got 24 gigs and some time to set it up? Pair the 31B with the small E2B for a free speed boost. One thing to skip: don't try to use any of these as a fully autonomous agent yet — they're strong for chatting and coding in one shot, but for long chains of tool calls, closed models still do better. Use Gemma 4 as a coding helper, not an autopilot. Gemma 4 is the strongest open release this year, but only if you match the model to your machine.

</details>
