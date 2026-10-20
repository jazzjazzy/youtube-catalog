---
title: "We Just Hit the Local LLM Tipping Point (Colibri)"
video_id: 19xCOJxWU0A
channel: "[[channels/Devsplainers]]"
uploaded: 2026-07-13
processed: 2026-09-11
duration: "8:00"
url: https://www.youtube.com/watch?v=19xCOJxWU0A
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [local-llm-inference]
tools: [Colibri, llama.cpp, ds4, vLLM]
llms: [GLM, Claude Opus, DeepSeek]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# We Just Hit the Local LLM Tipping Point (Colibri)

![thumbnail](https://i.ytimg.com/vi_webp/19xCOJxWU0A/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=19xCOJxWU0A) | 📅 Uploaded [[uploaded/2026-07-13]] | 🗓️ Processed [[created/2026-09-11]]

## TL;DR
> Colibri, a 1,300-line C engine (no Python, no GPU), runs GLM-5.2 — a 744B-parameter open model that outranks Claude Opus on LLM Arena — on a laptop with 25GB of RAM. The loophole is mixture-of-experts sparsity: only ~40B parameters (8 of 256 experts per layer) work per token, so Colibri pins the ~10GB dense core in RAM and streams the other 21,504 experts off the SSD by exact byte offset, with an LRU cache, async prefetch, and a usage log that pins your personal hot experts. Speeds run 0.1-1 token/sec — slow, but 8,000 frontier-quality tokens a day, fully offline.

**Watch this if:** you want to understand how MoE expert streaming turns the SSD into a memory tier and whether a frontier model on consumer hardware is actually usable.

## Key Takeaways
- [[topics/GLM]]-5.2's 4-bit weights are 370GB — normally $40k of GPUs or a 256GB Mac Studio — yet [[topics/Colibri]] runs it in 25GB of RAM because the model is 15x bigger than the memory it runs in.
- Mixture of experts is the trick: each layer has 256 experts and a router activates only 8 per token (~5% of 744B parameters); the rest can live on disk.
- Experts are unlabeled, overlapping blobs — there's no "coding subset" you could extract and keep, so streaming, not pruning, is the answer.
- Colibri pins the dense core (attention, embeddings, one shared expert, ~10GB) in RAM and reads missing experts (19MB each) off the SSD at exact byte offsets, evicting the least-recently-used; a usage log makes it measurably faster the more you use it.
- [[topics/llama.cpp]]'s mmap falls short because page faults are the OS guessing blind and blocking the thread; Colibri's router knows which 8 experts are needed and fetches them asynchronously, even pre-running the next layer's router (72% prediction accuracy).
- Benchmarks: 0.1 tok/s on a budget SSD, 0.28 on a top PCIe 5 drive, 0.37 on a 128GB Framework laptop, 1 tok/s ceiling on an M5 Max. Streaming won't wear out your SSD — reads don't wear flash, writes do.
- The trend is bigger than one repo: antirez's [[topics/ds4]] streams [[topics/DeepSeek]] experts off a MacBook SSD, llama.cpp has open expert-cache proposals, and [[topics/vLLM]] is building its own offloading — serious runtimes now treat the SSD as a memory tier.
- Use it where quality outranks the clock: overnight refactors, air-gapped machines, work that legally can't leave the building — not interactive chat.

## 🛠 Tools & Software
- [[topics/Colibri]] — the 1,300-line C engine that streams GLM-5.2's experts off the SSD with a pinned dense core, expert cache, and async prefetch.
- [[topics/llama.cpp]] — the mmap comparison point: memory-mapping loads blind via page faults, while Colibri fetches router-selected experts deliberately; it also has open expert-cache proposals.
- [[topics/ds4]] — antirez's Metal-and-C engine doing the same expert streaming for DeepSeek models on a MacBook.
- [[topics/vLLM]] — building its own version of expert offloading, evidence the technique is going mainstream.

## 🤖 LLMs Mentioned
- [[topics/GLM]] — GLM-5.2 by Z.ai, the 744B-parameter MoE model being run; 256 experts per layer, 8 active per token.
- [[topics/Claude Opus]] — the benchmark reference: GLM-5.2 sits above it on the latest LLM Arena leaderboard.
- [[topics/DeepSeek]] — the model family antirez's ds4 streams off a MacBook SSD.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- If your job is interactive, run the biggest model that fits in fast memory instead and keep your 60 tok/s — expert streaming is for quality-over-latency work.
- Try Colibri for overnight, air-gapped, or data-cannot-leave-the-building jobs where 8,000 tokens/day of frontier output is a win.
- Don't fear SSD wear from streaming (pure reads); do watch for thermal throttling on cheap drives under sustained load.
- Watch the prediction accuracy number — if next-layer expert routing becomes mostly predictable, the disk penalty largely evaporates.

## 🔗 Related Videos
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: Claude Opus, GLM
- [[videos/How Hermes Agent Can Save You 85 (Or More) in BG Task Token Cost]] — shared: Claude Opus, GLM
- [[videos/I Stopped Using Grep and My Agent Got 10x Faster]] — shared: Claude Opus, GLM
- [[videos/Pick the Wrong Gemma 4 and You'll Think It's Broken FOUR Models Compared]] — shared: llama.cpp, vLLM
- [[videos/Someone open-sourced a hedge fund (53k stars on GitHub)]] — shared: DeepSeek, GLM
- [[videos/Someone open-sourced a hedge fund — I ran it locally on Qwen3 with Ollama]] — shared: DeepSeek, GLM
- [[videos/The Real Reason NVIDIA Is Buying Hugging Face]] — shared: DeepSeek, llama.cpp
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Opus, GLM

## Timeline
- `0:00` — A 744B model on a 25GB laptop; GLM-5.2 above Claude Opus on LLM Arena
- `0:54` — The impossible math: 370GB at 4-bit, $40k of GPUs or a 256GB Mac Studio
- `1:19` — Why naive SSD reading fails: ~30 seconds per token on the fastest drive
- `1:47` — Mixture of experts: 256 experts per layer, router picks 8, 248 sleep
- `2:20` — Experts are unlabeled overlapping blobs — no coding subset to keep
- `2:48` — Only ~40B parameters (~5%) do work per token
- `3:01` — Colibri's split: ~10GB dense core pinned in RAM, 21,504 experts on SSD
- `3:32` — The per-token cycle: cache check, exact byte-offset reads, LRU eviction
- `4:03` — The usage log pins your personal hot experts; it gets faster with use
- `4:23` — Why llama.cpp mmap falls short: blind page faults vs router foreknowledge
- `5:07` — Benchmarks: 0.1 tok/s budget SSD up to 1 tok/s on an M5 Max
- `5:40` — SSD wear myth: reads don't wear flash; throttling is the real risk
- `6:21` — The trend: antirez's ds4, llama.cpp proposals, vLLM offloading
- `7:13` — Should you run it: overnight refactors, air-gapped machines, legal constraints

## Transcript
<details>
<summary>Full transcript</summary>

744 billion parameters running on a machine that costs less than one cooling fan from an H100 GPU. Not a Temu knockoff either. GLM 5.2, an open model that sits above Claude Opus in the latest LLM Arena benchmarks, answering correctly from a laptop with 25 GB of RAM. The model is 15 times bigger than the memory it's running in. The engine pulling this off is called Colibri, 1,300 lines of C. No Python, no GPU, and the loophole it exploits is hiding inside every big AI model you've used this year. By the end of this video, you'll know exactly how a model that can't fit in your computer runs on it anyway, and why the number everyone's laughing at is the wrong thing to look at. Try and wrap your mind around it.

GLM 5.2's weights, compressed down to 4 bits per number, take up 370 GB. You'd normally need half a data center of GPUs lying around. Call it $40,000 or a Mac Studio with 256 gigs of unified memory. Anything less and the model refuses to load. The obvious workaround is reading the model straight off the SSD instead. For a normal model, that idea is dead on arrival. Every parameter is needed for every single token, so you'd be pulling all 370 GB off the disk for every word. On the fastest consumer SSD money can buy, that's almost half a minute per word. Good luck writing your code like that. So, why does Colibri work? Because GLM 5.2 is not built like a normal model. GLM 5.2 is a mixture of experts model. Inside each layer, instead of one giant block of neurons, there are 256 smaller ones called experts. In front of them sits a tiny piece of the network called the router. Every time a token comes through, the router scores all 256 experts and picks the eight best suited for that exact token at that exact layer. The other 248 stay asleep.

Now, take experts with a grain of salt. People picture a math guy, a code guy, a poetry guy, and figure you could keep the code guy and delete the rest. Experts are really unlabelled blobs of learned weights with messy, overlapping jobs, and the router's choice changes token by token, layer by layer. The same word gets different experts in a different sentence. There is no coding subset to keep. Add it up, and out of 744 billion parameters, only about 40 billion do any work per token, around 5%. The rest of the model is, at any given moment, that weight, and that weight doesn't need to be in RAM. That's the concept Colibri rides on. Split the model into the parts every token touches, the attention layers, the embeddings, one shared expert, add up to just under 10 GB at 4-bit precision. Those get pinned in RAM permanently. The other 21 and 1/2 thousand experts, 19 MB a piece, sit in a 370 GB file on the SSD.

Then, for every token, the dense core in RAM does its work, and the router names its eight experts for this layer. Colibri checks a cache it keeps in the spare RAM. Already loaded, multiply and move on. Missing, the engine reads that exact expert off the SSD at its exact byte offset, multiplies, and evicts whichever expert has gone unused longest. Repeated across all 75 layers, and the next token starts the cycle over. A fully cold token touches about 11 GB of disk reads. That's insane, but routing is cute. A small crowd of favorite experts handles most of the traffic, so Colibri keeps a usage log on disk. And on the next launch, it pins your personal hot experts into whatever RAM is left over. The engine measurably gets faster the more you use it.

Of course, there was pushback when this released. Llama.cpp can already memory map a model bigger than your RAM. True, but memory mapping is the operating system guessing. It faults pages in blind, one small read at a time, blocking the whole thread while it waits, with no idea which weights are important. Colibri knows. The moment the router picks its eight experts, the engine requests all of them from the disk at once, asynchronously, while the CPU keeps crunching. It even runs the next layer's router early on partial information, so experts are loading before they're needed. A page fault can't see the future. A router can, a little. You're all waiting on the catch, right? On the author's laptop, this runs at a tenth of a token per second. A 500 token answer takes an hour and a half. The community benchmarked up the hardware ladder. A budget SSD gets you .1 tokens per second. A top PCIe 5 drive, .28. A 128 gig Framework laptop, .37. And an M5 Max with a monster internal SSD tops the chart at one token per second. That's the ceiling today.

And no, this won't kill your SSD. Streaming is pure reads, and reads don't wear out flash. Writes do. The real risk is a cheap drive thermally throttling after hours of running flat out. So, given the speed, is it useless then? Depends what you're counting. A tenth of a token per second is also 8,000 tokens a day. Several long frontier quality answers every day from a laptop with no internet connection. Grandpa still remembers running a PC overnight to download movies. Now, they can generate the answers instead. If this were one weird repo, it would be a party trick. There's more.

The same season, antirez, the guy who wrote Redis, shipped DS4, a metal and C engine that streams deep six experts off a MacBook's SSD. Llama CPP has open proposals for exactly this kind of expert cash, and vLLM is catching its own version. Serious runtimes are starting to treat the SSD as a memory tier instead of a filing cabinet. The great unlock everyone's eyeing is prediction. Colibri already guesses the next layer's experts with 72% accuracy. Every point that number climbs, more discrete finish in the background before anyone's waiting on them. If routing turns out to be mostly predictable, the disk penalty largely evaporates, and streaming starts to feel like running the model for real.

Should you run this? Well, not for a back and forth on your day job. In that case, just grab the biggest model that fits in your fast memory and enjoy your 60 tokens per second. Colibri is for jobs where quality outranks the clock. Overnight refactors, air-gapped machines, work that legally can't leave the building. The bigger point survives either way. For the price of one consumer SSD, the floor for touching a frontier model dropped out of the data center and onto a desk.

</details>
