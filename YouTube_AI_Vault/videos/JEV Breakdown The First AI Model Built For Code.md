---
title: "JEV Breakdown: The First AI Model Built For Code"
video_id: 2Bs0Ink_-Uo
channel: "[[channels/Rob Shocks]]"
uploaded: 2026-09-17
processed: 2026-09-18
duration: "10:36"
url: https://www.youtube.com/watch?v=2Bs0Ink_-Uo
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [llm-classification, agent-guardrails, model-routing]
tools: [TypeSafe, OpenCode, Claude Code]
llms: [Jev, Gemini]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# JEV Breakdown: The First AI Model Built For Code

![thumbnail](https://i.ytimg.com/vi_webp/2Bs0Ink_-Uo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=2Bs0Ink_-Uo) | 📅 Uploaded [[uploaded/2026-09-17]] | 🗓️ Processed [[created/2026-09-18]]

## TL;DR
> TypeSafe has launched Jev, a "System One" AI model that returns typed decisions and calibrated probabilities instead of text — in roughly 100 milliseconds and at $42 per billion tokens. Rob breaks down how reinforcement learning with calibrated decisions works, shows the playground's Choice, Score, and Noul primitives live, and covers real-world results like Vercel replacing Gemini 2.5 Flash Lite and getting 6x faster classification. The pitch: frontier-level judgment is now fast and cheap enough to bake directly into deterministic code paths.

**Watch this if:** you build agents or AI-powered software and want classification, routing, guardrails, or triage decisions that are orders of magnitude faster and cheaper than calling a chat LLM.

## Key Takeaways
- Jev generates no tokens and has no autoregressive loop: you send a state (text or JSON) plus typed questions, and it evaluates them all in parallel, returning typed JSON with calibrated confidence values.
- It exposes three question primitives — Choice (pick from options), Score (rate on a scale), and Noul (yes/no probability) — each with a confidence value your code can branch on.
- The economics are the story: 20-200x cheaper than LLMs used for the same tasks, ~100 ms responses, and an hour of realtime Doom-playing cost about $7 in calls.
- Vercel swapped Gemini 2.5 Flash Lite for Jev in a classification workload and saw 6x faster results while saturating their eval.
- Sweet spots: guardrails and security review instead of a subagent, model routing, ticket/email triage, fraud scoring, and tool-call selection for agents — including rapidly picking from an MCP tool list.
- It is deliberately not a chat model: TypeSafe is picking a lane — hybrid AI-powered software where deterministic code delegates individual judgment calls to a fast calibrated model.
- Access came fast off the waitlist: you get a playground, usage dashboard, and API keys, and it can be installed directly into Claude Code.

## 🛠 Tools & Software
- [[topics/TypeSafe]] — the company behind Jev; its console playground, sample requests (sky color, help desk triage), API keys and smart-home demo are shown live.
- [[topics/OpenCode]] — the OpenCode team tested Jev with browser automation and Rob highlights how blazingly fast the results were.
- [[topics/Claude Code]] — named as a direct integration target: Jev can be installed straight into Claude Code alongside using the raw API.

## 🤖 LLMs Mentioned
- [[topics/Jev]] — the subject of the video: TypeSafe's decision-only model, demoed in the playground and via Doom, Wikipedia-hop, and smart-home examples.
- [[topics/Gemini]] — Gemini 2.5 Flash Lite was Vercel's previous cheap classifier; swapping it for Jev was 6x faster and saturated the eval.

## 📡 Protocols & Standards
- [[topics/MCP]] — flagged as a major beneficiary: Jev's millisecond typed decisions could let coding agents jump through an MCP tool list or skill calls far more efficiently.

## ✅ Action Items
- Join the TypeSafe waitlist (turnaround was a couple of hours) and explore the docs and playground at typesafe.ai.
- Run the playground sample requests to learn the three primitives: a Choice request (sky color), a Score, and a Noul probability question.
- Rebuild a triage flow with Jev: pass ticket text plus context (user role, location, channel, time) and ask for priority Choice, deadline Noul, and tool-call Choice with confidence values.
- Audit your own AI-powered software for expensive decision flows — classification, verification, routing — that could become typed yes/no or multiple-choice calls.
- Try Jev as a guardrail or security-review step in a coding agent instead of a slower subagent, or as a model router that classifies tasks before dispatch.

## 🔗 Related Videos
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Claude Code, MCP, OpenCode
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, MCP, OpenCode
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Gemini, MCP
- [[videos/The Last Claude Code Tutorial You'll Ever Need]] — shared: Claude Code, Gemini, MCP
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude Code, MCP, OpenCode
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude Code, Gemini, OpenCode
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, MCP

## Timeline
- `0:00` — A new paradigm: a model that can't write a sentence but big companies call extraordinary
- `0:20` — TypeSafe launch and founder credentials (Diego Almeida)
- `0:51` — Reinforcement learning with calibrated decisions explained: decisions for code, not text for humans
- `1:38` — Use cases: guardrails, security review, model routing, ticket triage
- `2:26` — Vercel case study: replacing Gemini 2.5 Flash Lite, 6x faster, saturated eval
- `3:28` — The three question types: Choice, Score, Noul, each with confidence values
- `4:02` — Email classification example: hundreds of emails categorized and prioritized in seconds
- `4:24` — Deterministic software vs non-deterministic agents; Jev powers the hybrid middle
- `4:59` — Jev playing Doom in realtime — an hour of calls for about $7
- `5:21` — System One naming: Kahneman's fast/slow thinking; no tokens, parallel evaluation
- `6:07` — Getting access: playground, API keys, and installing into Claude Code
- `8:06` — Playground walkthrough: sky-color Choice request, then full help desk triage with priority, deadline Noul, and tool-call selection

## Transcript
<details>
<summary>Full transcript</summary>

So this huge new model can't write a single sentence. It can't explain itself, but it is a very interesting model and big production companies like Forcel are saying they're seeing extraordinary results from it. So it's called Jev. >> My name is Jeff. >> So it literally came out yesterday from a company with some serious credentials. This is Diego Almeida and he was one of the co-founders of Chat GPT. So Tface and Jev are something completely different. So this is a different kind of model. We're used to most frontier models producing text. It's designed for humans and instruction following. So the problem is these models are trained for human preferences and that doesn't make them ideal for machine usage. We get no dropping over confidence and lack of reliability. So the team at Typespace has spent the last 2 years reinventing the process and have come up with reinforced learning with calibrated decisions. Now what the heck is that?

So the big difference here is Jev is trained to produce decisions for your code to act on. So every model that we're used to is basically creating text for humans to read and consequently agents can read that text as well. But Jev does something very different and very useful. In just milliseconds and between 20 and 200 times cheaper than existing models you might use for the same task. You can get it to categorize things and even decide whether something is true or false. There are a lot of really good use cases for something like this that is super fast and very cheap. If you're building coding agents or you're building agents in production, this is going to make you a lot more accurate and efficient. Instead of using a sub agent as a guardrail or a security review, you could have Jev do that at lightning speed. Let's say you want to classify a task to see what model should be used. Jev could be used as a great model router. One great example is ticket triage. So what's the big deal here? We could have done this before with a large language model. The big difference here is the difference between the speed and the cost. If you want chat, this is not the model for you.

If you want lightning fast, cheap with high levels of confidence, then this is what you want. So you can imagine that thousands of companies out there including companies like Verscell that do any kind of classification or verification. It's going to be incredibly expensive to do that at scale particularly because all these models are non-deterministic and they tend to veer off or hallucinate or get things wrong. The guys at Verscell were using a cheap model like Gemini 2.5 flashlight to do some of their classifying. They swapped it out with types and it was 6x faster and it basically saturated the eval meaning it just performed way above. This can actually be a really big deal particularly when you just don't need all that text coming back. Already people are doing some really cool things with it like wiring it up to Starcraft and having it win missions. Now what Typesape and Jev are doing here is really picking a lane. They're not saying they're the all model. They're a very specific focus model and they do that thing very well.

So, it's not going to be the smartest model in terms of what you need. But look at what it does in terms of cost per workflow. This means it can be used at huge scale and it can unlock completely new types of companies and workflows. Another great example here, the guys over at Open Code tested it with browser use and it is blazingly fast. This is why I'm excited for what really cool workflows this could start to unlock. There's a lot to play with here. So when you're submitting a question to Jeff, you've got three different question types, choice, score, or new. So you give it the options, which would either be billing, technical, or sales. It reads the ticket and decides that it's going to be technical. And it's going to give you this confidence value here as well. You can also give it to give you a score. So maybe with that issue or ticket that comes from a customer, you want to score it on a scale of how frustrated the user might be. Is it calm, civil, or angry? So you get that score there as well. And then a new gives you a kind of yes no probability on your ask. Is this true? Is this urgent with a probability number.

So one cool application I saw from YouTuber Vogle was basically classifying all of his emails. So literally in just a couple of seconds, he got it to read through hundreds of emails, uh, categorize them, and drop priorities on them. If you were to do that via a regular LLM, it would take you so much longer. So here's a good breakdown from the docs that I posted on Twitter. So traditional software is deterministic. It's all about yes, no, gate, if, then else. Agents, on the other hand, are very non-deterministic. It makes them super flexible and super useful, but it also means that they're not always correct. They don't always follow the plan, and they're not guaranteed to do the same thing 100% of the time. Where Jeb comes in really powerful is in the hybrid world of AI powered software. That's where we're using some levels of determinism, but then we bake in a model like Jeff to help us with those decisions that we previously couldn't manage via completely deterministic methods. So this is Jev playing Doom. And you can actually see the realtime rate. And running this whole thing for 1 hour, the amount of calls was crazy. Only cost around $7. So system one is getting a structured description of what's happening in real time. And the model is feeding back instructions also in a structured format. So there's some cool Easter eggs baked into some of the naming conventions here. So system one is actually the name of the company and that comes from the two systems of thinking from Daniel Canaman, thinking fast and slow.

So system one is the fast intuitive gut check and then system two is the slow deliberate reasoning. Every LLM we've been using is trying to be system two. Think it true, write it out and do it one token at a time. However, Jev doesn't generate tokens. There's no auto reggressive loop. You just send it a state, some text, a JSON object, and a set of type questions. It evaluates them all in parallel. So, that's the other cool thing. This is all done in parallel, which makes it super fast. You're not sending requests in a blocked fashion, one at a time. So, you should be able to get access to this pretty quick. I was on the wait list for just a couple of hours and I got in. So, in there, you'll get a playground, your usage, API keys, etc. This is an API you can set up. You can also install it directly into claw code, but the playground is well worth investigating. So, you can look at some of the demos here. So, this is a fun test. It's like six degrees of separation. How many hops can you get from a Wikipedia page like DNA to something like Manny Pury Pony? How fast can a model do that by negotiating its way through the page and finding the next link? Let's check it out. >> Uh, and we're going to press go. >> And types it got there in 1.7 seconds.

So, it went through. If we're working with a smart home device and we give it some natural language like turn on the living room lights that would have to go to an LLM, get processed, read through the available list of devices, pick a state, send that back and then hope it's accurate enough so that the system can actually run it. Let's take a look at how that might work with the typing that we can do with type safe. So we can do turn off all of the lights and over here in our mock smart home we can see that all the lights turned off. We can say turn on the living room lights and those turned on. We can say shut off all the music in the house and the smart speaker turned off. Get the coffee boiling. >> Now you can see how fast that is. It's super fast in its return. Look, 185 milliseconds. What we're doing there is sending in the command. It's doing some very quick classification. It doesn't have to go through reams of text and tokens. It's reinforced learning is designed to shoot us back an answer really fast and really cheap. So, I hope you're starting to get the picture. This is about decisions and not about text.

We're sending in a state which might be a mixture of an email, user, some transaction details and then the context of what we want the model to do. It's going to process that and then we get back set typed JSON that we're able to process with some kind of function on the other side. Fraud level, confidence and risk scores. I think this has big implications for the speed and predictability of our coding agents and particularly MCP usage and CLI usage. Imagine being able to rapidly jump through an MCP2 list or a skill call really efficiently. So let's check out some sample requests in the Typespace console playground. So we've got three different example requests. Let's look at choice. So we have our question here. What color is the sky? So our request is titled sky color. Then we pick a primitive. So in this case we're asking a multiplechoice question. The instructions are what color is the sky? And our criteria are the list of possible selections or answers that we want the model to choose from based on its probability. So we'll just run that request. And in just a few milliseconds, we get our response. It's an 81% likelihood to be baby blue and a confidence level of 78%.

So another great example is a help desk triage. So here we have the state. So the request is it's been over a week. Nobody's responded to my report about the Wi-Fi. And then you can pass in things like user role, location, channel, location, and time. And then the main question here is what priority are we setting this? So we're giving this a choice. So the model has to decide which priority we're going to assign this. We're giving it a instruction of what priority and then criteria of low, medium, high, critical. Some examples, and then also some nested options. So then running this, we get a percentage likelihood on a medium priority. So a triage. So it's decided as a choice where this should go. Is it the help desk, the finance ops, etc. Our new question is, does this mention a deadline of any type? And there is a 5% chance that that is true. And this is a really cool area when it comes to agents. Which tool call should we use? Is it ticket status, Wi-Fi troubleshooting, and what confidence level? So, in this case, it's saying it should be ticket status.

So, you can imagine tool calling is a huge part of how we use agents. If we've got a model like this, and probably more models like this to come that are super cheap and super fast, it's going to be a big deal. So if you're building AI powered software, you need to ask yourself, what are the big decision flows within your system that are costing you lots of time and real money to make those decisions? Can those simply be changed into a yes or no structured input and output that is way faster and way cheaper? Imagine the difference that is going to make to your app. And also, what are the really cool things you can start to build with this now? Like some of the examples that I showed you in the video, I stayed up really late to make this video. So, if this was useful, please subscribe. This is going to move really fast and I'll be covering it as it does. If you're new to the channel and you're a software developer and builder, I cover all things got to do with building AI. Check out my last video on Pstack, which is a really cool skills library, and also my breakdown on the new SDLC from Antropic.

</details>
