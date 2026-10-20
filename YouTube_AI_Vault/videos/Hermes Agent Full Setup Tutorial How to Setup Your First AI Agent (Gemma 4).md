---
title: "Hermes Agent Full Setup Tutorial: How to Setup Your First AI Agent (Gemma 4)"
video_id: THA8Fov44QY
channel: "[[channels/Bart Slodyczka]]"
uploaded: 2026-04-08
processed: 2026-07-05
duration: "14:14"
url: https://www.youtube.com/watch?v=THA8Fov44QY
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [local-ai-agent-setup, self-hosted-web-search]
tools: [Hermes, Ollama, Firecrawl, Docker, Telegram, NeuTTS, Open Claw, GitHub]
llms: [Gemma]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Hermes Agent Full Setup Tutorial: How to Setup Your First AI Agent (Gemma 4)

![thumbnail](https://i.ytimg.com/vi_webp/THA8Fov44QY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=THA8Fov44QY) | 📅 Uploaded [[uploaded/2026-04-08]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A full walkthrough of installing Hermes Agent from GitHub and wiring it up to a fully local, fully private stack: a Gemma 4 model served through Ollama, self-hosted Firecrawl (via Docker) for web search, local text-to-speech, and a Telegram bot as the chat interface. By the end the agent runs with no paid APIs.

**Watch this if:** you want a step-by-step reference for standing up a private, local-first AI agent with web search and a chat channel, without touching cloud AI APIs.

## Key Takeaways
- Run Hermes Agent on a separate, non-primary device — since it can access files, passwords, and logged-in accounts, isolating it limits the blast radius if it's ever compromised.
- Ollama is used to download and serve local models; Hermes Agent connects to it via a custom endpoint at `http://localhost:11434/v1`.
- Model choice matters: the smaller Gemma 4 E2B (7GB) failed basic tool-calling/web-search tasks, while the larger Gemma 4 E4B (9.6GB) handled them correctly — expect to test multiple model sizes for your hardware and use case.
- Agent settings worth tuning include max tool-calling iterations (default 60), tool progress display verbosity, context compression ratio (0.5 default, useful for small models with ~128k context), and session reset mode (daily or by inactivity) to keep long-running Telegram conversations from bloating context.
- Telegram setup goes through BotFather to create a bot token, and restricting the allowed Telegram user ID is important — leaving it blank lets anyone who finds the bot chat with it.
- Web search runs through a self-hosted Firecrawl instance in Docker rather than Firecrawl Cloud, keeping search fully local and free.
- Hermes Agent ships terminal commands (via its GitHub repo) for reconfiguring models/tools after initial setup, and for full uninstall.

## 🛠 Tools & Software
- [[topics/Hermes]] — the AI agent framework being installed and configured end-to-end in this tutorial.
- [[topics/Ollama]] — used to download, list, and locally serve the Gemma 4 model, then plugged into Hermes as a custom endpoint.
- [[topics/Firecrawl]] — self-hosted (via Docker) as the private web search provider for the agent, instead of the paid cloud tier.
- [[topics/Docker]] — required to run the self-hosted Firecrawl container.
- [[topics/Telegram]] — configured as the chat channel for the agent, via a BotFather-issued bot token and a restricted allowed user ID.
- [[topics/NeuTTS]] — selected as the local, self-hosted text-to-speech provider for the agent (as opposed to a cloud TTS service).
- [[topics/Open Claw]] — mentioned as another tool the presenter used to test Gemma 4 models, where they "worked very well."
- [[topics/GitHub]] — source of the Hermes Agent install command and repo documentation (including the Firecrawl self-host guide).

## 🤖 LLMs Mentioned
- [[topics/Gemma]] — Gemma 4 is the local model powering the agent; the smaller E2B variant failed tool-calling tests while the larger E4B variant succeeded, illustrating a real model-size/capability tradeoff for local agents.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Set up Hermes Agent on a spare/secondary device rather than your main machine before granting it broad tool access.
- Test at least two model sizes (e.g., Gemma 4 E2B vs E4B) against your actual agent tasks before committing to one for local hosting.
- Self-host Firecrawl in Docker if you want private web search instead of paying for the cloud tier.
- Lock down your Telegram bot to your own user ID before leaving it running unattended.

## 🔗 Related Videos
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: GitHub, Open Claw, Telegram
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: GitHub, Open Claw, Telegram
- [[videos/Hermes The Self-Improving Agent That Gets Smarter Every Day]] — shared: Gemma, Hermes, Open Claw
- [[videos/OpenClaw is the most powerful AI tool Ive ever used in my life Heres how to set it up]] — shared: GitHub, Open Claw, Telegram
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: Docker, Gemma, Ollama
- [[videos/Self-Host Openclaw (Clawdbot) in a Proxmox VM (The Secure Way)]] — shared: Ollama, Open Claw, Telegram
- [[videos/The Chinese OpenClaw is Here(PicoClaw)]] — shared: GitHub, Open Claw, Telegram
- [[videos/You NEED to try these open-source AI projects right now]] — shared: GitHub, Hermes, Open Claw

## Timeline
- `0:00` — Intro: full Hermes Agent setup plugging into Telegram, a local model, and local web search
- `0:28` — Recommendation to run Hermes on a separate device for security isolation
- `1:18` — Installing Hermes via the GitHub install command; full setup flow chosen
- `1:26` — Choosing a custom endpoint (no paid models) and installing Ollama
- `2:06` — Downloading Gemma 4 in Ollama; E2B fails web-search tool calls, E4B succeeds
- `3:41` — Connecting Hermes to Ollama's local API base URL and selecting the model
- `4:57` — Configuring agent behavior: max tool iterations, tool progress display, context compression, session reset mode
- `7:19` — Setting up the Telegram bot via BotFather and restricting allowed user ID
- `9:14` — Choosing tools and skipping browser/vision features for this setup
- `9:52` — Self-hosting Firecrawl in Docker for private web search
- `12:11` — Testing the agent: successful local web search and a working Telegram chat with Gemma 4
- `13:20` — Reconfiguration commands and a demo of the Hermes uninstall command

## Transcript
<details>
<summary>Full transcript</summary>

Hello legends. In this video, I'm going to show you how to set up Hermes agent for the very first time. We'll start off by going across to GitHub and then downloading and setting up Hermes agent step-by-step. We'll plug it into Telegram, we'll plug it into a free local AI model that's running on your computer, and we'll also plug it into a free local web search that's running on your computer. Now, both of these two things will need to download some different tools, and I'll cover all that in this video, so that by the end of this video, you'll be able to chat with a Hermes agent that is 100% private.

So, the first thing we need to do is go across to the Hermes agent GitHub and then copy this install command. Now, before we set this up, I don't recommend running this on your main computer. Best thing to do is get a separate device and then install Hermes agent on that device. The reason being is that on your main computer, you most likely have very private files, passwords, you're probably logged into your like banking applications. So, depending on the settings you give Hermes agent, if it ever gets hacked, it can possibly access all that stuff. So, you want to separate this, give it its own device, and then run it on that. So, assuming you have that separate device, open up a terminal and then paste in that install command. Now, Hermes agent's going to go away and look at all the packages and libraries you have on your computer. It'll then determine any missing packages that you have and then automatically install them.

Once it's done installing, we have two options, one for a quick setup and then one for a full setup. We'll be going through the full setup step-by-step together. Now, for models, I don't want to use any paid models, so I'm going to go to more providers and then go all the way down until I get to custom endpoint. So, at this stage, we want to figure out how to get a local model onto our computer and then plug it into Hermes agent. And to do that, we're going to be downloading and using something called Ollama. Ollama's going to give us the ability to download and manage models local AI models on our device and then also plug them into tools like Hermes agent.

So, let's go ahead and copy this install command, open up a brand new terminal, and then hit enter. So, this command's going to go ahead and install Ollama on your computer. Once it's done, let's go back into Ollama and start browsing some local models. We'll click on models, and over here we can see a bunch of free open-source models that we can download and install into our computer. I'm going to go ahead with Gemma 4. I've actually been doing a lot of testing with Gemma 4 recently. I've been doing a lot of this actually using OpenClaw, and these models are super small and work very well with OpenClaw. Now, unfortunately, I did try the E2B, which is a 7 gig model with Hermes agent, and it wasn't able to do like basic tasks. I asked it to do some web searching, and it wasn't able to follow those instructions, which is pretty disappointing. In OpenClaw, it actually worked perfectly fine, but I then upgraded to the E4B, which is a 9.6 gig model, and it was able to do those basic requests. So, what I recommend is just finding a model, you can even browse different models on Ollama, find one that fits on your device, and actually works for your use case. So, you might need to go away and do some testing.

Now, if the device that you're using doesn't actually have the ability to download a model onto it, like if you're using a VPS or a really like a not very powerful computer, you can still use Ollama and use the cloud version. They've got a $20 a month tier. It has really good API limits, so you can also use that with Hermes agent. But, for this video, we're just going to go ahead and download this local model. So, I'm just going to copy this model name, and now I'm going to start downloading the model to my computer. So, I'm just going to go type in Ollama pull and then paste in the model name and then hit enter. And then Ollama will download and install that model onto your computer. And if you ever want to see all the models you have installed on your device, you can just go Ollama list, hit enter, and then you'll be able to see all the models that you have on your device.

And back in the Hermes agent settings, we're asked to enter an API base URL. This base URL just needs to point across to Ollama, and then whenever we download a new model, we can just select that model using this setting. So, the base URL for Ollama is always this. So, you can just copy this down as it is, http localhost 11434-v1. We're going to go ahead and hit enter. And for the API key, I'm not going to set one now, so I'm just going to hit enter. And over here, we can see all the models that we have available to us. And these are the exact same models that we had over here when we used the Ollama list command. So, the cool thing is that whenever you go off and you download a new model, it's always going to appear under the Ollama list.

I'm going to be using the Gemma 4 E4B. I'm just going to press one and then hit enter. For the context length, I'm just going to hit enter, and it's going to automatically detect what it needs to set. Now, we have the option for text-to-speech. So, for text-to-speech, I don't want to use any cloud versions. I actually prefer, when I'm running these AI agents, to always use locally hosted stuff. So, for this instance, I'm going to go with this NEUTTS, which is local on a device. I'm going to hit enter, and it's asking me if I want to download and install all the dependencies. I'm going to go capital Y and hit enter for yes. For the terminal backend, we're just going to keep the recommended local. So, we're going to hit enter.

And then on the bottom here, we have some specialized agent questions. So, the first one is, what is the maximum tool calling iterations that you want for your conversation? So, if your agent ever has to go away and do complex tool calling for you, like multiple times, execute a tool, get a response, execute the next tool, things like deep research or actually creating documents and sending them across to different places and managing files, all that kind of stuff has many, many iterations. So, over here, you can set your limits. I think really this is going to come down to a bunch of trial and error, depending on what model you're using, what task you're performing. So, all this stuff you can change later on. I'm going to go with the default of max iteration 60. I'm going to hit enter. And same thing for the tool progress display. So, every time we have a conversation with the Hermes agent, we can either choose to display all the different micro steps that it's doing in the background before it actually comes to us with a response. I'm going to choose this as all because I like to see, if I'm ever doing web research, what are the actual tools that it's executing.

Same thing with context compression. As the context gets really long, then your agent gets a little bit dumber because there's just so many tokens floating in the balance. So, by compressing that, not only does your agent retain some of the smartness across a really long conversation, but also you manage the context window. So, for the smaller models that we're using, we have like a 128,000 token context window, so you might want to set a lower compression. So, we're just going to go with the default of 0.5. And for session reset mode, another important thing to note here is that if you never reset your session and you're constantly chatting with your agent through Telegram, and you're accumulating three to four messages per day, after 7 days, you've got 28 different messages that you've accumulated. You don't really realize that all those actually stay within the agent context. So, for these smaller models, it's actually very important to constantly flush that context as you work on a new task. So, over here, we have the recommended, which is either by inactivity or by daily reset, which means either every 24 hours is going to reset your conversation, or if you're inactive for a period of time, like if you don't message it for 5 hours, then you want the conversation to be reset. So, let's go with the recommended setting. The inactivity timeout is 1440 minutes by default, and the daily reset hour default is 4, which is 4:00 a.m. local time.

Now we have the option of setting up some different channels. So, to set up Telegram, you have to hit the space bar to then select it and then hit enter. And now we're asked for the bot token, so let's go across to Telegram, go to the Bot Father, and then type in /newbot. Hit enter, and we're asked to choose a name for our bot. So, I'm just going to go Hermes demo. And now for the username, this has to end in bot, so I'm going to go Hermes demo bot. Now that we have the bot created, let's copy this bot token and paste it into here and hit enter. And now over here, we're asked to import our Telegram user ID. Whatever you put into here is going to be allowed to message your Hermes agent. If you leave it blank and you just hit enter, that means if anyone finds your Hermes agent on Telegram, they can have conversations with it. So, really you want to be very restrictive over here. I recommend just starting off with your own Telegram bot token. To find your Telegram user ID, you can search for raw_data_bot, press start, and you'll be able to see your Telegram ID. Let's paste that in and hit enter, and set our Telegram user ID as the home channel. We're going to install the gateway as a launch service and start the service now.

And now we've got a list of tools that we can give to our Hermes agent. You can go through these one by one, pressing space bar to select or deselect. For now, I don't want to do any vision or image analysis, image generation. This setting is about giving our agent access to a browser — for now I'm just going to skip this and keep the defaults. For our text-to-speech provider, we're just going to keep the default. And for our search provider for web search, we're not going to go to Firecrawl Cloud, we're going to go down and go to Firecrawl self-hosted.

So, at this stage, we have to set up Firecrawl. Firecrawl has an option to use a paid cloud service, where you pay per use, or you could also use their self-hosted version. Let's go across to the self-host.md file — it was a little bit tricky getting this set up for the very first time, so I've just got a bunch of commands to give you. Before we can install Firecrawl on our computer, we first have to download and install Docker. Docker is a container, and we're going to be installing Firecrawl within that container. Go across to docker.com and choose the correct version for yourself. After you download and install Docker, go to a brand new terminal and copy these commands — before you do, put them into your ChatGPT or Claude, explain what you're doing, that you're setting up Hermes agent with locally hosted Firecrawl with default configuration, and it might give you some tips on what to change for your personal setup.

Once Docker is installed and turned on, I've pasted in the commands, and it looks like it's installed and started up in Docker — you can confirm by opening the Docker application and seeing the Firecrawl container running. Back with Hermes agent, the default URL they list is the actual URL we need for the Firecrawl instance, so I'm copying that in. It looks like we've just gone back a couple of settings — this is a little bit strange, I've done the Hermes setup process three or four times and each time something kind of bugs out here and there, so if this happens to you just play nice with it. I'm skipping the browser setting, skipping text-to-speech since we already set it, and Firecrawl for self-hosted is already active, so I'm keeping the defaults for now.

It looks like we're ready to launch the Hermes chat. Actually, what happens here is that the system crashes — if you see this, it's completely normal, I think. I'm going to type in Hermes and hit enter, and now we're opening up our chat with the Hermes agent using our locally hosted model. Let's test this out and say "Hi there." It might take about 10 or 20 seconds to first load the model into RAM to get a response. Since I'm recording a video at the same time, my computer is going to be lagging a little bit — took about 30 seconds there.

But let's see if we can use the web search tool: research the latest AI news. What we see happening over here is that the agent is dropping down all the tool calls it's making as it gets our response — that was one of the settings we set earlier. That was actually pretty quick, even though my computer is under some load from recording. We have a successful web search, which means our Firecrawl is working successfully locally — completely private for us. And we're using the Gemma 4 E4B model, which is local and private to us.

The final thing I want to do is test that my Telegram bot works. I'll click the Telegram bot name, open up a new session, click start, and send "Hi there." And there we go — we have the response from our Gemma 4B model directly into Telegram as well. So, at this stage we've done our initial configuration with Hermes. If you ever want to go back and make changes, there's a bunch of terminal commands available on the Hermes GitHub that let you change the model you're using, add new models, give your agent access to different tools, or change the configuration settings. For example, to finish off the video, I'm going to run Hermes uninstall and hit enter — this is one of the commands to actually remove Hermes from our computer. I've got the option to uninstall but keep the data, or do a full uninstall — I'm going to choose full uninstall and confirm yes, which removes Hermes agent completely from my device.

All right, guys. Thank you very much for watching. If you want to see more Hermes agent content, please subscribe to my channel and drop a comment below. See you in the next one.

</details>
