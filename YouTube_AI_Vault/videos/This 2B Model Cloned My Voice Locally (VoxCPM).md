---
title: "This 2B Model Cloned My Voice Locally (VoxCPM)"
video_id: O4TMwZlUJvQ
channel: "[[channels/Better Stack]]"
uploaded: 2026-09-01
processed: 2026-10-20
duration: "10:14"
url: https://www.youtube.com/watch?v=O4TMwZlUJvQ
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [local-text-to-speech, voice-cloning]
tools: [VoxCPM, vLLM, Python, PyTorch, Hugging Face, ElevenLabs, Chatterbox TTS, Qwen3-TTS]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This 2B Model Cloned My Voice Locally (VoxCPM)

![thumbnail](https://i.ytimg.com/vi_webp/O4TMwZlUJvQ/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=O4TMwZlUJvQ) | 📅 Uploaded [[uploaded/2026-09-01]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> VoxCPM2 is OpenBMB's open-source, Apache 2.0, 2B-parameter local text-to-speech model that combines three normally separate capabilities in one checkpoint: speech generation, designing a brand-new voice from a text description, and cloning a voice from ~8 seconds of reference audio, across roughly 30 languages at 48 kHz. The video installs it via pip, generates speech from a Python script on a Mac M4 Pro, serves it behind an OpenAI-style `/v1/audio/speech` endpoint with vLLM, and weighs it against ElevenLabs, Chatterbox, and Qwen3-TTS as a way to remove a hosted TTS dependency.

**Watch this if:** you're paying a hosted TTS API like ElevenLabs and want to know whether a self-hosted, commercially licensed model can replace most of that traffic without wrecking your stack.

## Key Takeaways
- VoxCPM2 works on continuous audio representations instead of discrete code tokens, which helps preserve breathing, pacing, and mid-sentence emotion shifts that make speech feel human.
- Hosted TTS APIs bring three inherited problems: latency you don't control, a bill that scales with usage, and text (sometimes reference audio) leaving your network — a local model sitting next to the app removes all three.
- Setup is `pip install` of PyTorch + torchaudio + the `voxcpm` package; the checkpoint is `openbmb/VoxCPM2`, needing about 8 GB of VRAM on the NVIDIA path (a 24 GB card is more realistic for production concurrency with KV cache and multiple requests).
- Test your actual sentences in the Hugging Face demo before touching infrastructure — if the voice fails there, you've saved yourself a pointless deployment project.
- Served with vLLM, the model exposes an OpenAI-shaped `/v1/audio/speech` endpoint, so an app already talking to that route only needs a base-URL change, not an audio-layer rebuild.
- Voice design from plain text ("hyped American on caffeine") turns the voice into configuration instead of a recorded asset — a bad persona can be thrown away in 10 seconds.
- Cloning applies a reference voice to brand-new text (it isn't replaying the clip), and supplying the reference clip's transcript gives the model performance information, not just speaker timbre.
- Quality isn't uniformly state of the art: Arabic output was rough while French was much better, and people still bounce between VoxCPM, Chatterbox, Qwen3-TTS, and ElevenLabs — the right goal is replacing ~80% of hosted generation, not beating ElevenLabs on every sentence.

## 🛠 Tools & Software
- [[topics/VoxCPM]] — the star of the video: installed locally, used for generation, voice design, cloning, and multilingual speech, then evaluated for production use.
- [[topics/vLLM]] — the serving path that turns the local model into a service exposing an OpenAI-style `/v1/audio/speech` endpoint on a GPU host.
- [[topics/Python]] — the demo script (imports, model init, prompt text, generate call) that produces the first local 48 kHz output.
- [[topics/PyTorch]] — installed alongside torchaudio as the runtime dependency for the model.
- [[topics/Hugging Face]] — the hosted demo space recommended for validating your actual sentences before self-hosting.
- [[topics/ElevenLabs]] — the hosted incumbent VoxCPM2 is positioned against throughout: great quality, but you pay for convenience and your text leaves the network.
- [[topics/Chatterbox TTS]] — compared as an easier/lighter alternative whose emotional range the presenter found weaker.
- [[topics/Qwen3-TTS]] — named as the other model he'd evaluate directly if text-based voice design matters.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try your real product sentences in the VoxCPM Hugging Face demo before provisioning any GPU infrastructure.
- `pip install` PyTorch + torchaudio + `voxcpm` in a fresh virtual environment and generate a 48 kHz sample from a short Python script.
- If you have an NVIDIA box, stand up the vLLM server and point an existing OpenAI `/v1/audio/speech` client at it by swapping the base URL.
- Prototype a persona with a one-line text voice description before recording or licensing any reference audio.
- Budget VRAM honestly: 8 GB runs the model, but plan on ~24 GB for concurrent production traffic.
- Audit which share of your current hosted TTS spend could move local (the ~80% question) rather than demanding per-sentence parity with ElevenLabs.

## 🔗 Related Videos
- [[videos/Best 120b Model for Offline Use Nemotron 3 Super Out Now]] — shared: Hugging Face, vLLM
- [[videos/I Tried the Open Source ElevenLabs Alternative (Voicebox)]] — shared: Chatterbox TTS, ElevenLabs
- [[videos/The Most Powerful Free TTS Model You've Never Heard Of]] — shared: ElevenLabs, Hugging Face
- [[videos/This Speech Model Went From 12GB to 178MB (Parakeet Redux)]] — shared: PyTorch, Python

## Timeline
- `0:00` — Cold open: two AI-generated clips, both fake, from a 2B model running locally with no audio upload
- `0:33` — What VoxCPM2 is: generation, text-based voice design, and cloning in one OpenBMB checkpoint using continuous audio representations
- `2:06` — Installing locally: pip install PyTorch/torchaudio + voxcpm, `openbmb/VoxCPM2` checkpoint, ~8 GB VRAM on the NVIDIA path
- `3:15` — First local generation from a simple Python script, played back with afplay ("Deploy failed on US East 1. No problem.")
- `4:24` — Serving with vLLM on a GPU host: the OpenAI-shaped `/v1/audio/speech` endpoint means only a base-URL change for existing apps
- `5:35` — Voice design from text: "hyped American on caffeine" persona generated with no reference recording
- `6:22` — Cloning his own voice from ~8 seconds of reference audio and applying it to a brand-new sentence
- `7:00` — Multilingual cloning: Arabic comes out rough, French much better, ~30 languages supported
- `7:33` — Head-to-head framing vs ElevenLabs, Qwen3-TTS, and Chatterbox
- `8:15` — Pros and costs: Apache 2.0 license, 48 kHz quality, ComfyUI/GGUF/MLX community paths, but 24 GB VRAM for real concurrency
- `9:20` — Verdict: use it if you have a GPU box and speech is a real product feature needing local, multilingual, or persona-driven voices

## Transcript
<details>
<summary>Full transcript</summary>

I shipped it. I actually shipped it. Don't touch anything. This will crush 11 Labs. >> I need you to say that again, slower, please. Did you say this will crush 11 Labs? How is that possible? >> Could you tell which audio was fake? News flash, they both were fake. They came from a 2 billion parameter model running locally on this machine. No 11 Labs, no audio upload. And the weird part is voice cloning might not even be the most useful thing this does. Let's get into it. >> [music] >> This is Vax CPM-2 from Open BMB. And instead of solving one tiny part of text to speech, it combines three things we normally end up stitching together. It can generate speech, it can create a completely new voice from a written description, and it can clone a voice you actually have permission to use. And the emotions here are actually really good. There's a lot going on, but the useful version is simple. Instead of turning speech into code tokens first, it works with continuous audio representations. That gives it a better shot at keeping the small things that make speech feel human, breathing, pacing, and changes in emotion halfway through a sentence. But none of that matters if you're just looking for better audio.

If your app talks today, you're probably sending text to somebody else's API, hence 11 Labs. And the second you do that, you inherit three problems. Latency you don't fully control, a bill that grows with usage, and text sometimes reference audio too that actually leaves the network. Vax CPM-2 changes all this for us. The voice model can sit next to the app, so now we don't have to ask ourselves, does this sound cool? It's more along the lines of, can this remove a hosted dependency without making my stack worse? Now, we're going to install it and generate something useful, talk about turning into a service, and design a voice from text. I'm even going to clone my own voice, and then we'll get to the part that actually decides whether you should use it, where it breaks down, and all the stuff in between. Let's run it. If you enjoy coding tools that speed up your workflow, be sure to subscribe. We have videos coming out all the time. Now, setup is easy, but you do need a few gigabytes of space. In your virtual environment, you can pip install PyTorch with torch audio along with vox cpm. The package is just vox cpm. The main checkpoint is open bmb/vox cpm 2. You'll want a newer version of Python and a reasonably recent PyTorch build.

But, here's the first catch. On the normal path, this is a GPU model. I'm on a Mac M4 Pro. If you go on Nvidia's path, that's about 8 gigs of VRAM. And that number still matters because if your only machine is a small laptop GPU, trying to self-host this first is backwards. I'm on a Mac, so that's enough to answer the first question, or the question that I want to know. Does the voice actually sound good? It's not the machine that I'd use in production, but to work here. So, before you touch infrastructure, use the hugging face demo, test your actual sentence. If the voice fails there, you just saved yourself from solving a deployment problem you never needed to have. So, let me answer this. Does the basic thing actually work? And I'm not going to give it just "Hello" or "Hello world." We're going to give it some actual phrases here. Here you can see the Python script I wrote to handle all this. It's rather straightforward. I have my imports, then I built out a model with vox cpm. I set up some initial text here. This is where I can describe a lot of the detail how I want the voice to sound and what I want to output, but we'll touch on that in a second. Then finally, I generate everything down here with this method.

Now, in a little bit, I'll give it some sample audio where I can actually clone myself, but let's just run the initial version. I'm going to run the Python script. You can see it's compiling. It's doing its thing here. Then all we have to do is run it via I can run AFplay, type the name of the file. >> Deploy failed on US East 1. No problem. >> All right, so it does pretty good, right? We heard the output there. It can be better, but that was the boring path to all this. And sometimes boring is good. The text goes in, 48 kHz wave comes out. There's no speaker ID, there's no language parameter I dropped in, there's no external API. So, the first question is kind of closed here. Yes, it does work. If this is going to be in a real product, I'm obviously not importing a giant model inside some random Django route. You want a service. You want to see how you can actually use this. And this is where Voxia PM2 starts to become much more interesting. The local script that proved the voice. This is how you turn that into something your app could actually handle. You could run this command right here on a GPU, that Nvidia GPU I talked about. Now, I'm not running that here. That is a GPU host command. So, Linux or Nvidia. Enough VRAM to keep the model going. Not on this laptop here.

But once it is running, your application can call the route. Right, V1 audio speech. That endpoint is OpenAI shape. So, if your app already talks to V1 audio speech, you're not rebuilding your entire audio layer. You change the base URL, maybe a couple parameters here and there, and you're done. What I just ran, that just proves the voice. This endpoint is what actually extends it. So, now we have normal TTS behind a normal service. Okay, pretty useful. But hosted APIs already do that extremely well. The real reason Voxia PM2 is interesting is what happens when you stop asking it for a normal voice. Now, first is the voice design. No reference recording, there's no speaker file here. You just describe the person you want. The emotions here are actually insanely good compared to something like Chatterbox that I had issues with. Let's just say some text right here, just right here. Hyped American on caffeine. Okay, good enough. And then we can drop in text after that. Let's say the migration is reversible. We are not running it on Friday. And this is probably the feature I underestimated the most. Normally, if you want a new voice, you go find one. Here we just describe one. The voice becomes the configuration, not an asset you have to record first. You can throw away a bad persona in literally 10 seconds instead of rebuilding an entire voice pipeline.

>> The migration is reversible. We are not running it on Friday. >> Really good. All right. Then there's cloning. Here was about 8 seconds of my real voice. Now, Vax CPM 2 gets a completely different sentence. And this is the key difference. It isn't replaying the reference. It's taking the voice and applying it to new text. This is a clone of me talking through this thing. That was actually really good on the cloning part of it. But cloning is only half the problem. A voice can sound like the right person and still perform the line completely wrong. That's where a more complete cloning path comes in. If you also provide the transcript of the reference audio, the model gets more information about the actual performance, not just the sound of the speaker. And then the same pipeline can move across languages. Now, it can't translate, but you can give it a language and an output. So, take Arabic for example. Okay, that wasn't the best. Maybe it was cuz it was Arabic, but it did work. Then if we take French for example, That hat was a lot better. It handles around 30 languages including multiple Chinese dialects. So, this is the point where I stopped asking what it can do and started asking what I'm actually giving up.

Cuz picking a TTS model is still an engineering trade-off. Vax CPM 2 is interesting because it lands in a pretty unusual middle ground. It runs locally, the license is commercially friendly, it's multi-lingual, it clones, and it can design a new voice from scratch, from text, all from one checkpoint. But that does not automatically mean it wins. Chatterbox can be easier and lighter depending on the job, though emotions are tough. Quan 3 TTS is probably the other model I'd look at directly if voice design matters. And 11 Labs, well, it's great, but again, this is a really good alternative. I don't want to send my text somewhere, I don't want to pay someone to use that. That convenience is what you're paying for, sure. With Voch Cpm 2, you're choosing to own the voice stack, and in return, three things change. Your data can stay inside your infrastructure, and one model can potentially replace separate systems for voice design, cloning, and multi-lingual speech. That sounds great until you start treating it like a production infrastructure.

Now, this stuff was pretty easy to use, as you saw. 48 kHz output sounds good, text-based voice design is useful for prototyping personas. Apache 2.0 makes the commercial conversation easier, and the VLLM path means this can look like a normal service. There's also community paths around comfy UI, GGUF, and MLX if you're outside normal Nvidia setup. But now, the costs. First, VRAM. If we're doing this on Nvidia, 8 gigs might be enough to get the model running. That's different from saying 8 gigs is what I'd want in production. Once you add KB cache, multiple requests, and concurrency, a 24 gig card gives you a lot more room. Then, the quality is not automatically state of the art for every prompt. Depending on the language, as you heard with Arabic, your reference audio, and what you ask for, people are still bouncing between Voch Cpm, Chatterbox, Quan, maybe 11 Labs. So, the wrong question is, does Voch Cpm 2 beat 11 Labs on every English sentence? Did really good. The better question is, can this replace the hosted API for about 80% of what we generate, and maybe keep a little bit that stays hosted. Now, that can actually help reduce costs and it makes a lot more sense. So, should you actually use this? Well, use it if you already have a GPU box. I did it on my Mac. It did really good, so it can still do certain things. If speech is a real product feature, not a one-off voice-over, if you need local speech, multiple languages, or custom personas, this is really good. But, remember, it depends on your setup. I dropped the repo down below so you guys can check it out. I'm Josh from Better Stack. If you enjoy coding tips and tricks like this, be sure to subscribe. We have videos coming out all the time.

</details>
