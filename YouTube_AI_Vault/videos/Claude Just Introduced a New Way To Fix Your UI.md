---
title: "Claude Just Introduced a New Way To Fix Your UI"
video_id: eLDq5TfIHys
channel: "[[channels/AI LABS]]"
uploaded: 2025-11-23
processed: 2026-07-06
duration: "10:50"
url: https://www.youtube.com/watch?v=eLDq5TfIHys
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [ui-design-with-ai]
tools: [Claude Code, Claude Skills, Claude Desktop]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Just Introduced a New Way To Fix Your UI

![thumbnail](https://i.ytimg.com/vi_webp/eLDq5TfIHys/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=eLDq5TfIHys) | 📅 Uploaded [[uploaded/2025-11-23]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Anthropic published an article on why AI-generated UIs default to generic "AI slop" (distributional convergence) and how Claude Skills can steer front-end output toward more creative, aesthetic designs without bloating the context window. The host walks through Anthropic's typography, theme, and general-purpose front-end prompts, turns them into Claude Skills, and tests them inside Claude Code against real landing page, dashboard, and Apple Notes-clone prompts.

**Watch this if:** you're tired of Claude Code producing the same generic Shadcn-looking UI every time and want to know whether Anthropic's new front-end skills actually fix it.

## Key Takeaways
- Distributional convergence explains why AI models default to the "safest," most probable design — Claude's blog names this as the root cause of generic AI-generated UIs.
- Claude is "highly steerable" with the right targeted instructions, but writing all that front-end guidance into a system prompt would bloat context for unrelated work — Claude Skills solve this by loading UI-specific context only when needed.
- Anthropic's stated split: Skills = specialized expertise loaded on demand, sub-agents = specialized tasks run by a separate Claude instance, MCP = external data/network access (skills themselves can't make network requests).
- Best results come from targeted, general-direction language (e.g. "use solid colors or geometric patterns instead of gradients") rather than hyper-specific technical instructions like exact hex codes.
- Testing a typography-only skill improved font choices on a basic admin dashboard, but Claude Code repeatedly failed to auto-load the installed skill unless explicitly told to "use the front-end skill" — a reliability gap the host says doesn't happen in the Claude Desktop app.
- Anthropic's 400K-token general-purpose front-end prompt (combining typography, themes, and aesthetics guidance) produced noticeably better landing pages and blog layouts, but overcorrected on an admin dashboard, making it "too colorful" and less usable than the basic version.
- A separate Web Artifacts Builder skill breaks generated UI into components and uses the file system, but on an Apple Notes clone it only produced minor icon/hover-state improvements over the no-skill baseline.
- Even with fonts specified as "avoid these" rather than "use these," Claude Code kept converging on similar fonts and layouts across different landing page prompts — suggesting manual font curation (e.g. via Google Fonts) is still needed.

## 🛠 Tools & Software
- [[topics/Claude Code]] — where all the front-end skill testing happens; shown repeatedly failing to auto-invoke installed skills unless explicitly told to use them.
- [[topics/Claude Skills]] — the core subject: Anthropic's typography, theme, general-purpose front-end, and Web Artifacts Builder skills are built and tested throughout.
- [[topics/Claude Desktop]] — mentioned as not having the same skill-invocation reliability problem seen in Claude Code.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model whose default "AI slop" UI output and distributional-convergence tendency the whole video is built around, tested via Claude Code and Claude Desktop.

## 📡 Protocols & Standards
- [[topics/MCP]] — described per Anthropic's framing as the layer for external data access, distinct from skills (expertise) and sub-agents (tasks).

## ✅ Action Items
- Read Anthropic's "Improving Front-End Design Through Skills" article and turn its typography/theme/general-purpose prompts into your own Claude Skills.
- When building a front-end skill, use targeted directional language ("avoid gradients, use solid colors") instead of exact technical specs like hex codes.
- If Claude Code isn't picking up an installed skill automatically, explicitly tell it to use the skill by name rather than assuming auto-invocation.
- Pick your own fonts from Google Fonts rather than relying on the model to pick something distinctive on its own.
- Try the Web Artifacts Builder skill when you need Claude to break generated UI into properly organized components.

## 🔗 Related Videos
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Code, Claude Desktop, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)]] — shared: Claude Code, Claude Desktop, Claude Skills, MCP
- [[videos/Understand the FULL Claude Ecosystem in One Video]] — shared: Claude, Claude Code, Claude Desktop, Claude Skills
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, MCP

## Timeline
- `0:00` — Intro: AI agents default to the most basic, generic UI design possible.
- `0:18` — Claude's explanation: distributional convergence, models predicting the highest-probability (safest) output.
- `0:34` — Anthropic's article "Improving Front-End Design Through Skills" introduced.
- `1:27` — Why skills over system prompts: avoids bloating context for non-UI work.
- `2:00` — Skills vs. sub-agents vs. MCP: specialized expertise vs. specialized tasks vs. external data access.
- `2:32` — Sponsor break (Scribba).
- `3:36` — Front-end design principle: map subjective taste to concrete implementation guidance, use targeted not hyper-specific language.
- `4:27` — Zen browser aside (viewer question, unrelated to main topic).
- `6:14` — RPG-themed UI example using the themes/aesthetics prompt.
- `6:24` — The 400K-token general-purpose front-end prompt introduced.
- `9:35` — Web Artifacts Builder skill: component breakdown tested on an Apple Notes clone.
- `10:24` — Closing thoughts: front-end design cookbook and upcoming Claude Code design plug-in to test in a future video.

## Transcript
<details>
<summary>Full transcript</summary>

Have you ever noticed that when you ask your AI agent to make something, for example, a landing page for a TV website, it starts up and presents you with the most basic design you've ever seen? Well, we weren't the only ones. And Claude also noticed how their models always generate that AI look. And they actually told us the main issue behind it, which is distributional convergence. It just means that models predict their next words based on probability in their training data. So the website you just saw had the highest probability of being built and was the safest option. This basically means that these AI models are not creative at all. But that's why Claude released this article on improving front-end design through skills outlining the main problem and actually giving the solution for this.

This is where Claude gives us the good news saying that creativity can be injected because the models are highly steerable with the right specific instructions. But this introduces a big challenge. The more specialized the task becomes, the more bloated the context window gets as you need to offer more context. For front-end design especially, there are many dimensions such as typography, colors, animations, and more. And you need to specify all these things so that it doesn't default back to its basic nature and give you the most basic designs.

Now, this is where Claude tries to bring in their skills feature, saying that you could put this all in a system prompt, but then the rest of your work that you need to do would be hindered by this extra information about UI that you don't need because you're not only going to be working with UI in a project. So, Claude skills help by loading the effective UI context when the model actually needs it. In this section, they explain what their skills are used for and why they are applying them to this UI problem. I'm not going to go over the basics of skills again as I already made a video on this. But there is one other thing for those of you who've been really confused in the comments section as to why we need skills. I'll leave this in the description below, but it's basically Claude telling you which is the right tool to choose.

I don't want to look through all of this, but the best four section pretty much sums it up with skills being for specialized expertise, which we're loading for UI right now. And sub agents are for specialized tasks, so they're a whole instance of Claude with other tools. and MCP is for external data access since we all know skills can't do network requests. But coming back to the topic, they say that with these front-end skills when you're building a landing page, Claude will automatically load the skill in and use those instructions. And this allows you to basically keep your context window clean because too many tokens, as you know, can result in the degradation of its performance. So, keeping the context window clean is really important.

But before we dive deeper into the findings, here's a word from our sponsor, Scribba. Ever felt stuck watching coding tutorials but never actually learning? Scribba fixes that. Every lesson lets you pause, jump in, edit the code, experiment, and see instant results. It turns passive watching into hands-on practice, making learning stick. One of the most powerful paths is the back-end developer path. You start with command line basics, then move through NodeJS, express databases, architecture fundamentals, and building full back-end projects. Take control of your learning and master backend development with Scribba. Click the link in the pinned comment below.

Claude actually dives a little deeper into the prompt that we need to provide in our skills, saying that the main thing is to think about front-end design in the way a front-end engineer would. This basically means that you need to map what you think looks good to actual implementations. For example, you know that this gradient doesn't look good and the aesthetic implementation would be specifying what to replace it with like solid colors or geometric patterns. They also say that you shouldn't really write detailed technical instructions, but instead just use targeted language that helps the model. For example, you shouldn't actually go ahead and specify the exact hex code of the color that you want implemented. Giving a general direction to induce creativity is much more helpful.

I've also noticed in the comments that a lot of you ask me which browser I use. Right now I'm actually using Zen browser. Previously I was on Arc browser but ever since they discontinued support for it, I've switched to Zen because Arc was becoming too unstable.

But coming back to the video, they start with the first dimension which is typography and they've given a system prompt that applies the principles they discussed above. In this example, we've got a pretty basic looking admin dashboard. And when the typography prompt is applied, we get this dashboard with fonts that look a little bit better. So to actually test this out, I copied the prompt, opened up Claude, told it to make a Claude skill for this prompt, downloaded the skill, put it inside the skill folder in my project, started up Claude code, and gave it the landing page prompt again. And this time, it came up with something like this, which is certainly improved over the previous version that we saw it build. Now, I don't like the fonts that it used here, but it was nudged towards these by the prompt itself. However, you can also go to Google Fonts yourself and get a bunch of fonts that you think would look cool and let Claude be creative with them.

Another big flaw with Claude skills is that when I first prompted it with the skills already inside the project, it didn't recognize them and built it just like before. But when I asked it to manually use them, only then did it start running those skills and apply the typography prompt. This is a really huge flaw in the runtime that Claude is providing. I don't know if I'm doing something wrong, but if you do know something about this, then do let me know.

The next aspect they talk about is themes and aesthetics. Because Claude has been trained on massive amounts of data, you can actually make it focus on some popular themes that you want to implement. And with it, they made it implement this RPG themed UI, which does look more creative.

Next, they lead us into this general-purpose prompt by saying, "What if we could combine all these smaller improvements into one giant and reusable prompt?" And they developed a 400K token prompt. Here they specify that they're giving it a general overview of the problem it causes where they tell it that it tends to converge towards these generic outputs. They scold the model for its basic nature which is producing AI slop and then give it a general guide to surprise the users. At the end, they also ask it to think outside the box.

Then they start showing us these examples. At first, we have our simple landing page and with the skill, it makes this landing page which actually does look good. Other than that, the use of gradients is actually really good this time. After that, they show us how it's improved a blog layout and made it kind of like Claude's own website. And then we have the admin dashboard example again where this time it just completely went overboard with the colors and made it too colorful. I think there are probably some places where the basic output is better because this just looks unusable to me.

So again, I copied the front-end prompt, had Claude make the skill, put it inside my skills folder, and then prompted Claude code with the same prompt to make the landing page. The previous skill was named typography skill and I thought that maybe that was why Claude didn't use it. But this time it was named the front-end aesthetic skill and it still didn't use it. I then made a new prompt explicitly saying that I wanted to make the front end of a landing page but it still didn't use it. And only when I mentioned that it should use the front-end skill did it go ahead and run the skill. Now this issue is only in cloud code. I don't encounter this problem when working in the cloud desktop app.

Anyway, this is what it actually came up with. And I must say it does look really beautiful. The fonts do actually make a lot of difference, but this glow looks really, really bad. I did notice another thing here. It was also asked to make a landing page and both of these examples do look kind of similar and even the fonts look the same. So I looked in the prompt and found out that this time they didn't actually specify which fonts to use. They just told it which ones it should stay away from. But still the model kind of went in the same design direction with landing pages and use the same fonts as well.

Next up, they do have a section in which they say that they want to improve artifact quality with skills. They still made this web artifacts builder skill which basically shows it how to break things into components and allows it to use the file system. I asked it to make an Apple Notes clone and this is what it made without the skill. You can see it's fully functional and it's the Shad CN looking UI that Claude normally produces. But when I did use the skill, it produced something really similar with just small improvements like slightly better icons and hover states on the icons. This allows it to divide everything into different components and it pays more attention to components. But other than that, I don't think there's any significant improvement.

So to conclude, they just dive a little bit into skills saying that it's a tool that brings constant guidance and domain expertise to every task by providing these special instructions and you shouldn't only look at design but also at things that are really repeatable to actually turn them into skills. Other than that, they also have a front-end design cookbook and a new plug-in for Claude Code that helps with front-end design. I will be testing it out and I'll feature this in a future video as well to see how this new design plug-in actually works.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next.

</details>
