---
title: "This Claude Skill Cuts Your Token Costs In HALF"
video_id: RuH3uiJy84A
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-12
processed: 2026-07-05
duration: "5:05"
url: https://www.youtube.com/watch?v=RuH3uiJy84A
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [token-cost-reduction, llm-output-optimization]
tools: [Claude Code, Caveman, Codex]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This Claude Skill Cuts Your Token Costs In HALF

![thumbnail](https://i.ytimg.com/vi/RuH3uiJy84A/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=RuH3uiJy84A) | 📅 Uploaded [[uploaded/2026-04-12]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Better Stack tests the trending "Caveman" Claude Code skill, which strips filler words, hedging, and pleasantries from LLM responses. Output tokens drop by up to 45% without losing technical accuracy, but the skill's own instructions add input tokens that can offset the savings on single one-off prompts.

**Watch this if:** you want to cut Claude Code costs but wonder whether skill-based prompt compression actually saves money end-to-end.

## Key Takeaways
- Caveman is a Claude Code (also works with Codex) skill that strips filler words, hedging, pleasantries, and articles from responses.
- In a live demo, a normal Claude Code answer about a fake auth system was full of filler; the Caveman version delivered the same technical facts in terse note form.
- Across 10 test prompts, Caveman cut output tokens by 45% vs baseline and 39% vs simply telling Claude Code to "be concise."
- Loading Caveman's markdown instruction file adds input token cost, which can make single, one-off prompts about 10% more expensive overall than baseline.
- The savings return once follow-up questions trigger prompt caching, netting an average 39% cost reduction in multi-turn sessions.
- A cited 2026 study found constraining model responses to be brief improved accuracy by up to 26% on certain benchmarks.
- Caveman ships bonus skills: Caveman Commit (terse conventional commits), Caveman Review (one-line code review comments), and a Compress skill for shrinking natural-language files; it also has a Wenyan mode using classical Chinese for maximum token efficiency.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent used to demo the Caveman skill's before/after outputs.
- [[topics/Caveman]] — the token-compression skill under review; installed as a package and invoked to strip filler from responses.
- [[topics/Codex]] — mentioned as another agent the Caveman skill also works on.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model whose verbose default responses are compared against Caveman-compressed ones.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install the Caveman skill and compare token usage on your own recurring Claude Code prompts.
- Check whether your workflow benefits more from single-shot prompts (where Caveman may cost slightly more) or multi-turn sessions with prompt caching (where it saves more).
- Try Caveman Commit and Caveman Review for terser commit messages and code review comments.

## 🔗 Related Videos
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Codex
- [[videos/Agent memory resolved]] — shared: Claude, Claude Code, Codex
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Caveman, Claude, Claude Code
- [[videos/Never hit Claudes Usage Limit Again]] — shared: Caveman, Claude, Claude Code
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: Claude, Claude Code, Codex
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Code, Codex
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude, Claude Code, Codex
- [[videos/Turn Claude Code and OpenCode into Your Marketing Department (Free Skills)]] — shared: Claude, Claude Code, Codex

## Timeline
- `0:00` — Intro to the Caveman skill and its token-saving claim
- `0:40` — Demo: normal vs Caveman-skill Claude Code response on a fake auth system
- `1:44` — Test results: 45% output token reduction vs baseline, 39% vs "be concise"
- `2:26` — Baseline costs ~8 cents vs Caveman ~4 cents for output tokens
- `3:19` — Input token cost of loading the skill nearly offsets savings on single prompts
- `3:38` — Follow-up questions hit prompt caching, swinging savings back to a 39% net gain
- `3:48` — Study cited: constraining responses to brief answers improves accuracy up to 26%
- `4:14` — How to install: Vercel skill package command, and the skill's actual instruction rules
- `4:30` — Bonus skills: Caveman Commit, Caveman Review, Compress, and Wenyan mode

## Transcript
<details>
<summary>Full transcript</summary>

If you like saving money or just hate the way the LLM's talk, this one might be for you. It's a new trending skill called Caveman and it promises to cut up to 75% of output tokens while keeping full technical accuracy, all thanks to the wise words of Kevin. "Why waste time say lot word when few word do trick?" This works on Claude, Codex, and wherever and it takes your outputs from filler word to long not reading responses to a nice TLDR with the same technical accuracy and it's even customizable and has extras like Wenyan mode, terse commits, one-line code reviews, and an input compression tool. It may seem a little crazy at first, but there's even some science behind this. So, let's jump in and take a look.

So, I was testing this out in Claude Code earlier with a demo Next.js app I have that actually has a fake authentication system. I was simply asking, "Can you explain how auth is implemented in this app?" Now, this is normal Claude Code without the skill installed. You see right away it gets into sort of filler words saying, "This is a simulated authentication system." We have a m-dash. It says, "No backend, no passwords, no real security. Exist to demonstrate Better Stack RUM user tracking." After this, it then goes on to explain the core files and how it works. Everything's just sort of in readable English. If we then ask the same question but this time use the Caveman skill, you can see it just gets straight to the point and is a lot more concise. The first sentence is demo only, client-side auth, no real security, built for Better Stack RUM tracking demos. Doesn't have any of those filler words, the m-dashes, or anything like that. It doesn't need to make a proper sentence. You can just tell you the technical information straight away.

The same thing goes for the how it works section, the flow, and the integration points. You can see here instead of saying how this works sort of in a plain English sentence, just says app load then has an arrow to check local storage for the saved user. So, it's just way more concise and that's what I care about to be honest. I don't really care about it being in plain English. I just wanted the technical information from it. That conciseness is actually the main reason that I like this skill, but its other selling point is that this means it should reduce output tokens and therefore theoretically you can get more out of your Claude Code subscription or even save money on your API tokens.

But, I do think there's a small catch here. This is the results of a comparison test I was running earlier where I was comparing the baseline Claude Code response versus a terse one, which is where I literally say to Claude Code, "Be concise." versus using our Caveman skill. This was on 10 prompts and it's things as simple as, "How does Git rebase differ from a Git merge?" And you see the results are very positive. When we use the Caveman skill versus the baseline, we actually have a 45% reduction in our output tokens and a 39% one against just saying, "Be concise." to Claude Code. Now, that's obviously going to relate to cost as well. There's going to be a 45% saving there in the output tokens. So, the baseline cost around 8 cents for them and Caveman costs around 4 cents. So, everything looks quite good initially.

Where things start to get a little more interesting though is when we factor in the cost of input tokens. Obviously now that we're using the Caveman skill, we're loading in a markdown file which has a lot more text in it than our single sentence prompts. So, for the baseline where we were just sending that sentence, it's fractions of a cent, but when we use our skill, you can see it's now around 4 cents. If we then combine our input and output token costs, you can see that on average Caveman is actually 10% more expensive than the baseline because the savings that we made on those output tokens have been lost to our input tokens.

But, this doesn't mean it's a loss for Caveman. That's because this is only true in very specific scenarios. It's only true if we're sending a single small prompt and we're not asking any follow-up questions. If you start to ask follow-up questions, you can hit the prompt cache pricing and when we do that, you can see things swing back in favor of Caveman. We're actually making a 39% cost saving. You can see I went down a bit of a rabbit hole there, but it does prove there is some logic to using Caveman. That's before we even factored in another possible advantage, which is that a study this year showed that constraining large models to brief responses improves accuracy by 26% on certain benchmarks. So, maybe Kevin was the smart one after all and you'd be smart for subscribing.

You can try out this skill for yourself by using the Vercel skill package and running a command like this. And in here we can also see what it's asking the agent to do. We have some rules like drop articles like a, an, and the. Drop any filler words, drop pleasantries, drop hedging. Then we also have use short synonyms, so use big instead of extensive and say fix instead of implement a solution for. And we also have what we want to keep, which is technical terms, code blocks, and errors. After this, we then have the pattern of how it should be structured, so we should have a thing, an action, a reason, and then a next step. So, nice and concise. There's even intensity modes in here to change just how Caveman it gets. You see it ranges all the way from light up to ultra. I was using full since that is the default. You can see in ultra it abbreviates everything, it strips conjunctions, it uses arrows for causality, and it uses one word when one word enough.

There's also a Wenyan mode, which is using classical Chinese characters because they're actually the most token efficient. Unfortunately, I can't read them, so it's not much use to me. That's not even all that Caveman has to offer. There's actually a few more skills for specific scenarios. We have Caveman commit to write terse and exact messages in a conventional commits format. We have Caveman review to write code review comments that are one concise line per finding. And we also have a compressed skill to take your natural language files and Cavemanify them so you can reuse them with slightly less input tokens. Let me know in the comments if you like the sound of any of these and while you're down there subscribe and as always, see you in the next one.

</details>
