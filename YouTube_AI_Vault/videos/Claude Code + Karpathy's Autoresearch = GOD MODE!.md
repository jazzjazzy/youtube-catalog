---
title: "Claude Code + Karpathy's Autoresearch = GOD MODE!"
video_id: vjJwgXsMfjM
channel: "[[channels/AI Andy]]"
uploaded: 2026-03-18
processed: 2026-07-05
duration: "11:16"
url: https://www.youtube.com/watch?v=vjJwgXsMfjM
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [self-improving-content-pipeline, social-media-analytics]
tools: [Claude Code, Autoresearch, Meta Graph API, n8n, Airtable, ContentMate, launchd]
llms: [Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code + Karpathy's Autoresearch = GOD MODE!

![thumbnail](https://i.ytimg.com/vi/vjJwgXsMfjM/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=vjJwgXsMfjM) | 📅 Uploaded [[uploaded/2026-03-18]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> The host adapts Andrej Karpathy's open-source "Autoresearch" framework — originally built for optimizing ML training scripts — to self-improve a daily short-form content pipeline. Real Instagram/Facebook view data (pulled via Meta Graph API into Airtable) feeds a 10-question binary eval scored by Gemini, and a 24-hour loop rewrites the n8n content-generation prompt automatically based on what actually got views.

**Watch this if:** you publish content on a schedule and want a data-driven, self-improving feedback loop instead of manually guessing why some posts flop.

## Key Takeaways
- Karpathy's Autoresearch repo needs three inputs: a file to change (the prompt), instructions on what to optimize, and a measurable way to score whether it got better — then you let it run in a loop.
- The host mapped his content pipeline onto that same structure: the prompt is his generation script, the loop instructions are a program.md file, and the eval is real Instagram/Facebook view counts.
- Meta Graph API (free) pulled his last 30, then 200, Instagram reels sorted by views to surface performance patterns — separating what actually drives views from surface-level assumptions.
- The biggest mistake people make with autoresearch-style evals is using vague/subjective criteria ("is this engaging?"); the fix is strict yes/no binary criteria (10 questions covering hook framing, result vs. feature framing, avoiding press-release tone, etc.) that a model like Gemini can score consistently.
- The wired loop: pull yesterday's views → match to Airtable production records → pre-score new ideas against a 5-point threshold before they enter the creation queue → score published scripts with the 10-question eval → correlate high-eval/high-views (validated winners) vs. high-eval/low-views (false positives, meaning the eval itself needs fixing) → generate an improved prompt and push it to the n8n workflow via API.
- The whole loop runs once every 24 hours via a single Python script triggered by macOS's launchd, fully hands-off besides a human spot-checking finished videos before scheduling.
- Framing, not topic, was the pattern that separated 100K-view videos from ~56-view flops — the prompt evolved over five revisions across two days, from an announcement-style hook toward a curiosity-trigger, secrets-about-to-be-revealed framing.
- Every prompt change is logged with the data that caused it, so when a stronger model becomes available later, it can pick up the research log and continue optimizing from where it left off — Karpathy himself has called the research log potentially the most valuable asset of the whole system.

## 🛠 Tools & Software
- [[topics/Claude Code]] — used to adapt Karpathy's Autoresearch repo, replacing the ML-training eval loop with a social-media-views eval loop, and to write the ~1,000-line Python autoresearch loop script.
- [[topics/Autoresearch]] — Andrej Karpathy's open-source self-improvement framework (originally for ML training scripts); repurposed here as the core loop structure.
- [[topics/Meta Graph API]] — free API used to pull real Instagram and Facebook view counts and reel data for analysis.
- [[topics/n8n]] — runs the actual content-generation pipeline whose prompt gets automatically rewritten and pushed via API each cycle.
- [[topics/Airtable]] — production database matching content posts to their view counts, eval scores, and performance tier.
- [[topics/ContentMate]] — the host's content pipeline product; a team member uses the manual version (2.0.3) while the newer version (2.1) has the auto-improvement loop built in.
- [[topics/launchd]] — macOS's task scheduler, used to trigger the daily autoresearch script every morning at 8am.

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — reads each published script and answers the 10 binary eval questions, producing a machine-readable score used to correlate against real view counts.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Turn any subjective "does this sound good?" content eval into a strict list of 10 yes/no binary questions a model can score consistently.
- Pull your own platform's historical post performance (top and bottom performers) before guessing at what patterns drive engagement.
- Log every prompt change alongside the data that triggered it, so future model upgrades can resume optimization from the existing research log instead of starting over.

## 🔗 Related Videos
- [[videos/7 new open source AI tools you need right now]] — shared: Claude Code, Gemini
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Gemini
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Claude Code, Gemini
- [[videos/Can Claude Code Fix an Engineer's Terrible Taste]] — shared: Claude Code, Gemini
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Claude Code, Gemini
- [[videos/JEV Breakdown The First AI Model Built For Code]] — shared: Claude Code, Gemini
- [[videos/My Claude Code Can INSTANTLY Watch Any Video (Here's How)]] — shared: Claude Code, Gemini
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: Claude Code, Gemini

## Timeline
- `0:00` — Intro: an automatically improving content machine that publishes 5 videos/day and rewrites its own prompts.
- `0:28` — What is Autoresearch: Karpathy's repo, the three required inputs, his original ML-training experiment (11% improvement overnight).
- `1:44` — Pulling the data: adapting the repo to use social view counts instead of ML metrics; Meta Graph API setup and initial pattern-finding.
- `3:57` — Build the eval: why vague criteria fail; the 10 binary yes/no eval questions.
- `5:22` — Wiring the loop: full pipeline from pulling views to pushing an updated prompt to n8n via API.
- `7:37` — How it evolves: five prompt revisions across two days, from announcement framing to curiosity-trigger framing.
- `8:26` — How to run it daily: launchd scheduling, human approval step, ContentMate 2.0 vs 2.1.
- `9:40` — Why the research log matters for future model upgrades; generalizing autoresearch to any measurable prompt.

## Transcript
<details>
<summary>Full transcript</summary>

I used Andre Karpathy's auto research to build an automatically improving content machine. It makes five videos per day, publishes them, gathers real data, figures out what worked and what didn't, then rewrites its own prompts to get better every single day automatically. Let me show you how I built it, and I'll give you the entire template for free. But, before that, just let me show you how it works. So, what is auto research? So, a couple weeks ago, Andrej Karpathy, one of the founding members of OpenAI and former head of AI at Tesla, released this repo that is called auto research. And the idea is dead simple. You give an AI agent three things: a file to change, instructions on what to optimize, and a way to measure whether it got better. Then, you just let it run. And in his case, he was optimizing for machine learning training script. So, his experiment right here, the agent would tweak the code, run it, check if the results improved, then kept the changes if they did, throw them out if they didn't, and repeat. He ran hundreds of experiments overnight and got an 11% improvement. But, here's what most people miss. This isn't just for machine learning. You can apply this to literally anything that has a measurable output. I looked at this and thought, "My content pipeline has all three of these. The prompt is my train.py, the loop instructions are my program.md, and the eval is real views from Instagram and Facebook. I built it, and here's how you can do it, too.

Pulling the data. So, it all started when I posted this repo into Claude code and asked if it was actually possible to use this repo with a feedback of views taken from social media instead, because I kind of wanted to self-optimize based on views. After a quick confirmation that it wouldn't be exactly the same, cuz this has a slow loop using 24 hours as the time base, I kind of started getting obsessed and just had to figure out if I could do it. So, the actual work was to pull Instagram data and Facebook data to analyze it and start creating my E Val basically what to optimize for based on real data. I have fully unleashed my AI avatar to Instagram and Facebook using my AI clone. And as you can see, most of the views are 1,000, but some actually get over 100,000 views without me having to film anything. And the real question was, what are the criteria that are basically 198 views, right? So, I set this all up through a meta graph API, which is completely free. I made a new app, and then I went to the tools, the graph API explorer, added some Instagram basic permissions, and read pages, and just like that, he found our 30 last reels sorted by views as top performers and the bottom performers as well. It said, "A clear pattern already jumping out. The wow factor, visual demos crush it, where Claude code or productivity content underperforms." And I was like, "That doesn't really make sense. Can you actually pull a lot more data?" And just like that, it pulled 200 Instagram reels and started getting even more key patterns of what was working and what was underperforming. But, because Instagram is a bit different than Facebook, we had to pull from there as well, so we can actually sandbox it based on just Instagram and Facebook, no other social media platforms.

Now that it had all the data, but we had to build the eval. So, this is where most people screw up auto research. They make the eval criteria something like, "Is this engaging?" or "Does it sound good?" That's just vibes, and what we need is a clear yes-no question, no gray area. And please roast me in the comments. I would love for this to improve by you guys improving it as well. But, here are the evals that we ended up with. This is no vibes, it's just a yes-no. Does the hook describe a result or transformation, not just a feature? Does the hook feature a person or story, not just a company? Those are for the hook quality, and the content framing is the short framed around what you can do, not what it is. Does the script avoid sounding like a press release or change log, right? So, you can see these are yes-no questions that can be answered easily. Would the first frame of this video make someone stop scrolling? These were the 10 questions that we ended up with. And the key is that binary criteria are machine readable. You can feed a script into Gemini and ask it these 10 questions, and you get a score out of 10. No subjectivity, no rate this on a scale of 1 to 10 just on vibes. It's just yes-no.

But, now that we had all of these, we started on wiring the loop. Here is the actual system, I'll show you in a minute. Here is the actual code that it wrote, 1,000 lines. A auto research loop that is working exactly like this. The first thing is that we pull our views from Facebook and Instagram. This is really important cuz every morning, maybe we got views, maybe we didn't. Then we match an update with views to our air table. This is kind of our production system. It looks like this right now, and this is essentially where we make all the videos, and here is where the videos are stored as well. As you can see, "Stop everything. Robots are now mastering your favorite sports just by watching our messy YouTube clips." Pretty cool, and as you can see, we have the database here for the eval score, performance tier, etc. And the automation in the back end, just to show you, looks a bit like this, and AI can improve this by itself over time. But, I'm getting ahead of myself. Next we pre-score new ideas. So, we scrape social media every single morning. We have an eval that is actually based on just the sources as well, even before creating. So, there's two sets of evals here, and if it gets above a five score, it enters the creation queue. Next, we score published script. So, Gemini reads each script and answers 10 yes/no eval questions, that's the one you just saw, and outputs a score for every published short. Next, we correlate with high eval plus high views equal validated winners. High eval plus low views false positives. That means we have to fix the eval plus handle rankings plus approval rate tracking. As you can see, it's getting smarter. Then we generate and push. We write an improved prompt from correlation data, winners, failures, push new prompt to N&N workflow via API, and this self-improvement loop is going every 24 hours starting at 8:00 a.m. my time. All fully automated with one Python script.

But, you might be wondering how it evolved. As you can see, we started with the original prompt that had a hook detail tone close word budget and etc. Then it started reframing it from announcement to a curiosity trigger. It pushed it to be broader, more dramatic. Then it tried to deepen the personalization with life-altering language added. The hook scoped away from events more into universal and timeless discoveries. And we ended up at hook framing sharpened with secrets about to be revealed. So it went through five meaningful revisions across two days. And we can see it all here in this auto research prompt JSON that get updated every single day based on the criteria. But the last part I had to figure out was how to run it daily. The last piece is making it hands-off. So the script runs every morning at 8:00 a.m. via launchd. So that's macOS's task launcher. Every day it pulls yesterday's views count and it does all these things, right? And at the end it actually gives me a summary or auto auto research daily report. Here it has the top performers that we have done, the prompt updates with a bunch of changes that it's done, with top handles and human approval as well. Currently I have a team member that is using Content Made 2.0.3 where he is using it himself manually. And we got Content Made V2.1 now that has this auto improvement feature built into it. And literally every single day five videos get made and my coworker, what he does is watch the video and if it's good, he puts this one on schedule. If it's not good, he just says no. And AI learns from this as well, making it almost 100% fully automated besides quality inspection and the beautiful thing is that it never stops getting better.

Every day the pipeline publishes five shorts. 24 hours later the loop checks back in what happened. The prompts get slightly better. After a week and seven iterations, after a month, 30. Unlike manual tweaking, every single change is a logged with the data that caused it. So, when a smarter model comes out next month, I hand it that research log and it picks up exactly where it last left off. And Karpathy said this himself, the research log might be the most valuable asset. And you can apply this to anything, your thumbnail prompts, your email sequences, your landing pages. If a prompt has a measurable output, auto research can improve it. This is the coolest thing that I found in a long while and I'm giving it all the way for free. If you want Content Mate, if you want the NAN template, and you want the auto improvement loop, head to our free school community where I give away all the resources here inside of the AI Clone Automation. But I can understand that it is maybe a little bit technical for some people. So, if you want to implement this way easier, customize it for your business, head into the AI Made Plus community where I will help you more hands-on. Now, I guess all we need to do is wait. I want to make a video in a month from now showing the exact results and what ended up happening. So, subscribe. Maybe it's gotten better or it's posting corn. Who knows? But it's going to be fun anyways. Thanks for watching and I'll see you tomorrow at lunch.

</details>
