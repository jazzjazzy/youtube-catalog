---
title: "Claude Code But It's Entirely Local..."
video_id: 4qs21EBOkn8
channel: "[[channels/Samuel Gregory]]"
uploaded: 2025-12-09
processed: 2026-07-06
duration: "8:35"
url: https://www.youtube.com/watch?v=4qs21EBOkn8
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [local-llm-coding-assistant]
tools: [LM Studio, Ollama, Claude Code, Claude Code Router]
llms: [Qwen Coder, Devstral, GPT-OSS-20B]
protocols: [REST]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code But It's Entirely Local...

![thumbnail](https://i.ytimg.com/vi_webp/4qs21EBOkn8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=4qs21EBOkn8) | 📅 Uploaded [[uploaded/2025-12-09]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Samuel Gregory walks through running Claude Code entirely against local models instead of paying for a subscription: download a model in LM Studio (or Ollama), install Claude Code Router to redirect Claude Code's API calls to your local server, configure a coding model and a thinking model, then run `ccr code` to drive Claude Code with GPT-OSS-20B and Qwen Coder running on your own GPU.

**Watch this if:** you want Claude Code's UX (memory, skills, MCPs) without a subscription and have a machine with enough VRAM to load large local coding models.

## Key Takeaways
- LM Studio (or Ollama) downloads and serves local models over a local HTTP server; note the server's URL/port (LM Studio defaults to `127.0.0.1:1234`, Ollama to `11434`).
- Qwen Coder 3 (30B) is recommended for its large context window (~236K tokens), important for working across larger codebases; Devstral is another option with a 120K context window.
- Set each model's context size to its maximum in LM Studio's config screen so it loads with full context available.
- Claude Code Router lets you keep all of Claude Code's quality-of-life features (memory, skills, MCPs) while rerouting the underlying model calls to any provider — OpenRouter, GLM/MiniMax/GPT-Codex coding plans, or a local model.
- To point Claude Code Router at a local model, add a new provider with the API URL appended with `/v1/chat/completions`, any placeholder API key, and the model name matching what's loaded (e.g. `openai/gpt-oss-20b`).
- You can run a fast "background" model (GPT-OSS-20B) alongside a bigger "thinking" model (Qwen Coder) simultaneously if you have enough VRAM (64GB used here) — Claude Code Router auto-loads whichever model a request targets.
- Local inference is noticeably slower than hosted Claude Code (the demo waits ~5+ minutes per prompt on suitable hardware), so it's currently more of a hobbyist/future-proofing exercise than a production replacement.

## 🛠 Tools & Software
- [[topics/LM Studio]] — used to download, configure (context size), and serve local models via a local API server.
- [[topics/Ollama]] — mentioned as an alternative to LM Studio for downloading and serving local models.
- [[topics/Claude Code]] — the CLI being run against local models instead of Anthropic's hosted API.
- [[topics/Claude Code Router]] — installed via npm and configured (via `ccr ui`/`ccr model`/`ccr code`) to redirect Claude Code's requests to a local LM Studio server.

## 🤖 LLMs Mentioned
- [[topics/Qwen Coder]] — recommended local coding model for its large (~236K) context window; used as the "thinking" model in the demo.
- [[topics/Devstral]] — mentioned as another local coding model option with a 120K context window.
- [[topics/GPT-OSS-20B]] — loaded as the default/background model and demoed answering a "tell me about this file" prompt.

## 📡 Protocols & Standards
- [[topics/REST]] — Claude Code Router talks to LM Studio over an OpenAI-compatible REST endpoint (`/v1/chat/completions`).

## ✅ Action Items
- Install LM Studio or Ollama and download a coding-focused model with a context window that matches your codebase size (Qwen Coder or Devstral).
- Set each local model's context size to its maximum in LM Studio before loading it.
- Install Claude Code Router (`npm install` per the repo), add a local provider pointing at your LM Studio/Ollama server URL, and run `ccr code` to launch Claude Code against it.
- Check your machine's available VRAM before trying to run two models (a fast background model plus a larger thinking model) side by side.

## 🔗 Related Videos
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, GPT-OSS-20B, Ollama
- [[videos/I Tried the Open Source ElevenLabs Alternative (Voicebox)]] — shared: Claude Code, Ollama, REST
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Code, GPT-OSS-20B, Ollama
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Claude Code, REST
- [[videos/Pick the Wrong Gemma 4 and You'll Think It's Broken FOUR Models Compared]] — shared: LM Studio, Ollama
- [[videos/Qwen Coder Next Locally Can It Replace Paid AI Models]] — shared: LM Studio, Ollama
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, GPT-OSS-20B
- [[videos/The HTTP Header Trick That Cuts AI Agent Costs in Half!]] — shared: Claude Code, REST

## Timeline
- `0:00` — Intro: running Claude Code with local models to skip the subscription fee.
- `0:13` — Setting up LM Studio and downloading a local model.
- `1:02` — Why Qwen Coder 3's large context window matters for bigger codebases.
- `1:53` — Devstral as an alternative model with a 120K context window.
- `2:09` — Checking model size vs. available VRAM before downloading.
- `2:54` — Setting max context size per model in LM Studio's config screen.
- `3:43` — Setting up Claude Code Router and what it preserves from Claude Code (memory, skills, MCPs).
- `4:36` — Configuring a new local provider in Claude Code Router (API URL, chat completions endpoint, model names).
- `6:23` — Running `ccr code`, querying GPT-OSS-20B, then triggering Qwen Coder's thinking mode.
- `7:44` — Summary: local hardware limitations today vs. future potential.

## Transcript
<details>
<summary>Full transcript</summary>

What if you could write code with Claude Code without paying that pesky subscription fee? Well, that's exactly what we're going to do today. But we're going to use models running on your local machine. So, if you're excited, give us a like and subscribe if you want to see more content like this. With that, let's get on with it. I've gone through this in some of my previous videos, so feel free to skip ahead. But the first thing you're going to want to download is LM Studio. That's my personal favorite just because it gives you a little bit more fine grain control. You can do it with Ollama as well, which both of these software all they do is enable you to download local models and run basic inference on them. They both support local server settings. So with Ollama and with LM Studio, they'll broadcast the local model across the computer and we just need to take note of what that URL is.

Once you've downloaded LM Studio, we go over here into the search mode. What you're going to really want to consider here is a couple of things. The first of all is obviously the model itself, what you want to do with it, whether you have heard good things or bad things — I can't tell you what model you should choose. Personally, the latest Qwen Coder 3 is a great model for a couple of reasons: you've got 30 billion parameters from Qwen Coder 3, 14 billion on Qwen Coder 2.5, 32 billion Qwen Coder 2.5, and a bunch of community models. Now, because I'm on a Mac, I'm going to untick GGUF — it's not that they don't work, but these are just more performant for Mac uses. So the reason why I like Qwen Coder is because it has quite a large context window. Some of the other models don't quite have a great context window for working on larger code bases — for me, they're just kind of out of the question. Qwen Code actually has, I think, like a 236,000 context window. Another great model is Devstral, which has a 120,000 context window size. So, something with a big context size.

The other thing you want to pay attention to is the size of the model — one, the actual space on your hard drive to download the model, which in this case is 13.28GB, but secondly, the amount of VRAM you have in your machine. I've got 64 gig, so this one will be quite easy for me to load into my VRAM. And again, you've got some community versions here, but once again, go and download models — Ollama have their own set of models to download as well, in my opinion a little bit nicer to pick through. Regardless, you can download GPT-OSS — this is totally fine on LM Studio as well. But you want to download the model of your choice, and then once that's downloaded, you can click load model here or go over to model selector and download them there.

What I like to do is on each of these models, on the config screen, let's take GPT-OSS as an example — I always set the context size to the maximum allowed, so 131072. And then that way when I load it over in this area, let's do GPT-OSS, it will load with the maximum context size window. I've done another video, or will be doing another video, on KV cache quantization — it reduces the context size just a little bit, but not noticeable in terms of speed or anything like that. It's worth just trying to see what sort of luck you get with the quantization on. So, this is now loaded in, and what I'm taking note of, I've got my server running, and I'm taking note of the URL here — so it's 127.0.0.1 port 1234. If you're on Ollama, the port is 11434.

So with the LM Studio side of things set up, let's get on to Claude Code. Now the tool we're going to use is Claude Code Router. I'm only scratching the surface here on what Claude Code Router is capable of — ultimately it allows you to use all of the quality-of-life benefits from Claude Code, such as memory, skills, MCPs, all of that good stuff, but reroute it to OpenRouter, your own choice of model whether that's a closed-source or an open-source model. You can also take advantage of your other subscriptions like the GLM coding plan, the MiniMax coding plan, or indeed GPT Codex, but in our case we're going to route it to our local model.

You're obviously going to want to download Claude Code — I'm assuming you've already done that. But then you want to npm install Claude Code Router. So in my terminal here, copy and paste that will install Claude Code Router. Now the other thing I'm taking note of is that LM Studio will tell us the paths that it's capable of supporting, and it's registering that it's OpenAI-like, which kind of makes sense because we're using an OpenAI-style model. But this is just something to take note of in case it uses something different. One thing I will say is that I've had issues in the past where my claude wasn't set correctly in my paths — all I did was go `which claude` and it will tell me my path. I can then copy this, and then the easiest thing I recommend doing is just going `ccr ui`, and this will open an interface. Go into the UI and set my path — as you can see it's already set there, you just might need to do that, you might get an error.

You can see I've got a bunch of providers set up where I can point it to Ollama — I actually have Ollama already set up here, I've got some OpenRouter ones and I've got Anthropic here. So if we add a new provider here, we're going to name this "local LM" just so we can differentiate it, and for our API URL we have 127.0.0.1:1234 — we're going to append `/v1/chat/completions` at the end of that, and the API key can be anything. The models, of course, is going to be `openai/gpt-oss-20b` or whatever models you want to use. We want to also use the Qwen 3 model because it has a bigger context window. Default we're going to set GPT-OSS as our background — we're going to set GPT-OSS as well, I think, just so we can demonstrate it really quickly. It's going to be Qwen Coder, but our also-long-context is also going to be Qwen Coder.

So, if we save and restart that, head back into our terminal in a new tab, we can also go `ccr model` here and just verify that all of the models are selected. You can select a new model if you want — so default here, we're just going to reselect the same one, and you can just do it all through the CLI. But if we go `ccr code`, it should spin up Claude Code with Claude Code Router wrapping around it. And if I go to sort of default mode, let's keep context size down and go "readme, tell me about this file," and that should do its thing. If we head into LM Studio, back into here, we should see prompt process report spinning up there, and we open up our GPU history — you can see our GPU is being fully utilized, and we wait for a response. And there we go, we've got a response from GPT-OSS.

Now, what we're going to do to trigger Qwen Coder is go into thinking mode and say, "Tell me more." And what you'll notice is that I haven't actually loaded the model in LM Studio, but what will happen is it will register that that's the model I'm trying to query, and it's going to load it in automatically for us. So, you can see that everything's starting up — my GPU, I don't know if you can hear that, it is going off. And we can see that it's using Qwen Coder as the thinking model. Obviously, to have these two loaded side by side you need adequate VRAM, which I do have fortunately. And there we go, we got a response from Qwen Coder using thinking mode.

Now that took a while, and as I've been saying with all of these local coding things, you really need very very good hardware to be able to run these. It becomes debatable whether it's even worth running a local model, but it's really enjoyable exploring how this is done, because I do believe in the future consumer hardware will be able to run these models — these models will become more efficient, potentially even leveraging the CPU a little bit more. But ultimately, we have Claude Code running local models. So again, if you have any questions for me, leave them down below. If you have any advice on how we can squeeze more out of these local models so I'm not waiting around for 5 minutes per prompt, join me over on my Patreon for early access to videos just like this. Links for everything will be down below in the description. Until next time, keep on vibing.

</details>
