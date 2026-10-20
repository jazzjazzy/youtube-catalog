---
title: "Andrej Karpathy Just Fixed Claude Code's Biggest Weakness..."
video_id: jI4ZVB_MPhU
channel: "[[channels/Dream Labs AI]]"
uploaded: 2026-08-03
processed: 2026-09-11
duration: "9:00"
url: https://www.youtube.com/watch?v=jI4ZVB_MPhU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [agent-memory-management]
tools: [Claude Code, Claude Skills]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Andrej Karpathy Just Fixed Claude Code's Biggest Weakness...

![thumbnail](https://i.ytimg.com/vi_webp/jI4ZVB_MPhU/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=jI4ZVB_MPhU) | 📅 Uploaded [[uploaded/2026-08-03]] | 🗓️ Processed [[created/2026-09-11]]

## TL;DR
> Karpathy's "dreaming" idea — an LLM equivalent of sleep that distills the day's sessions into lasting memory — has now shipped as an official Anthropic feature, but it's enterprise-only and burns API credits. This video explains the three problems it fixes with in-band agent memory (split focus, missed cross-session patterns, stale/duplicated memories), then walks through a free prompt that recreates dreaming in Claude Code: a "foresight dream" skill that reads the last 24 hours of session transcripts nightly at 3 a.m., proposes memory changes with transcript evidence, and waits for your approval via a dream report.

**Watch this if:** you use Claude Code daily and want it to consolidate memory across sessions overnight without paying for the enterprise dreaming feature.

## Key Takeaways
- Karpathy's flaw: LLMs boot with zero tokens and restart from scratch — there's no sleep-like distillation of experience into weights, so [[topics/Claude Code]] only learns while you're actively prompting it.
- In-band memory has three problems per Anthropic: agents split focus between the task and memory upkeep; single-session writes miss patterns across sessions and agents; and memory files accumulate stale, duplicated, confidently-wrong notes.
- Anthropic's official dreaming feature scans recent session transcripts and produces organized, up-to-date memory content; early-access customers Harvey and Rakuten reportedly saw ~6x task completion rates.
- The catch: dreaming is enterprise-only and consumes API credits — so the video ships a free prompt that builds the same loop locally.
- The prompt creates a "foresight dream" skill (via [[topics/Claude Skills]]) that reads 24 hours of transcripts, diffs them against stored memory, and proposes numbered changes with short transcript quotes as evidence.
- Only tiny safe fixes (typos, index repairs) auto-apply; everything else waits in a "dream gate" HTML report you approve or reject each morning.
- Real results shown live: a new fact about his editor added, a 105-day-stale CLAUDE.md flagged for deletion, and an iCloud asset folder location learned — [[topics/Claude]] gets smarter while you sleep.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent being upgraded: the dreaming routine is pasted into Claude Code and runs nightly against its session transcripts and memory files.
- [[topics/Claude Skills]] — the mechanism used: the setup creates a "foresight dream" skill invoked by a scheduled routine each night at 3 a.m.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model doing the dreaming; you need to have used Claude or Claude Code in the last 24 hours for a dream run to have new context.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Copy the free dreaming prompt and paste it into Claude Code to set up the nightly routine (it works around any existing memory system).
- Schedule the dream skill to run at 3 a.m. nightly, then run it once immediately as a test to see what it proposes.
- Review the dream report each morning: approve genuine facts, reject noise, and let it delete stale memory files that are steering work the wrong way.
- Keep the default approval gate on — auto-approving everything is possible but "fast and loose."

## 🔗 Related Videos
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills
- [[videos/How to Use Claude Code Skills Like the 1 (its easy actually)]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude, Claude Code, Claude Skills
- [[videos/Understand the FULL Claude Ecosystem in One Video]] — shared: Claude, Claude Code, Claude Skills
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code

## Timeline
- `0:00` — Intro: Karpathy on the biggest flaw in current AI setups
- `0:11` — Karpathy clip: sleep distills the day into brain weights; LLMs restart from zero tokens
- `0:35` — What "dreaming" means: reconcile sessions, spot patterns, self-improve overnight
- `1:29` — Problem 1: split focus — the chef writing his recipe book mid-dinner-service
- `1:53` — Problem 2: patterns obscured — the NBA coach judging a season from one game
- `2:26` — Problem 3: memories go stale — duplicates, outdated notes, confidently wrong files
- `3:06` — Anthropic clip: the official dreaming feature explained
- `3:34` — Harvey and Rakuten's early access: ~6x task completion rate
- `3:50` — The catch: enterprise-only and burns API credits
- `4:05` — The free dreaming prompt: paste it into Claude Code
- `4:47` — The "foresight dream" skill: read 24h of transcripts, propose evidenced changes
- `5:41` — Schedule at 3 a.m. nightly, then run once as a test
- `6:46` — The dream gate report: approving and rejecting real memory updates
- `7:21` — Live wins: 105-day-stale CLAUDE.md removed, asset folder location learned

## Transcript
<details>
<summary>Full transcript</summary>

Andrei Kapathy might be the brightest mind in AI. And 9 months ago, in this interview with Dwarkesh, he revealed what he thought was the biggest current flaw with AI and Claude setups. Roll the clip. I feel like when I'm awake, I'm building up a context window of stuff that's happening during the day. But I feel like when I go to sleep, something magical happens where there's some process of distillation into weights of my brain. And this happens during sleep. We don't have an equivalent of that in large language models. These models, when you boot them up, they have zero tokens in the window. They're always like restarting from scratch. So, I almost feel like we are redoing a lot of the cognitive tricks that evolution came up with through a very different process. But we're going to converge on a similar architecture cognitively. See, Kapathy says the problem with your Claude code setup is it can only learn while you're actively prompting it. But, if there was some form of magical dream-like state that it could enter, where it could distill and reconcile all your sessions, see the patterns between them, and update and improve himself based on your goals even when you're not actively prompting it, he calls this dreaming, your Claude code could become 10, 100 times more powerful.

Well, fun fact for all of us, since Kapathy's interview with Dwarkesh, Anthropic, which Kapathy now works at, has actually dropped this exact feature, which now allows your Claude code to dream. And according to Kapathy, this is so powerful because it fixes the three biggest problems that you currently have with your Claude memory, even if you're using Boris's cutting-edge self-learning MD file. And so, Anthropic say, if you're not currently using dreaming, you have three big problems with your in-band memory. Firstly, you have a split focus. So, your agent, while you're prompting it, is trying to split its attention between finishing the task you're giving it and maintaining and updating your memory file. It's sort of like a chef with a dinner service who's trying to get everyone their chickens, but at the same time he has to write his chicken recipe book. He's just dividing his energy and dividing his focus. Anthropic say the second biggest problem is something called patterns obfuscated. So, it's agents writing to your memory file in-band miss patterns from across the sessions and across different agents. So, if you have every single agent you're asking to do a task writing to that memory file, it doesn't have a wider context window about the patterns through all of your sessions. Kind of like an NBA coach out there looking at one game out of the season of 84 games and trying to rearrange rosters and orders and who's shooting what shot based on just that one performance.

And then thirdly, Anthropic say that memories go stale. So, duplicates that disagree, notes gone stale, and your memory file being confidently wrong. So, this is basically your memory file is written by these individual agents who don't have this context. They could be adding duplicates that disagree with each other, or there could be stuff in your memory file that's from 6 months ago that is no longer true and therefore guiding your work in the wrong direction. This one's like Google Maps giving you directions based on the roads 10 years ago. And this is why Karpathy was harping on we needed something like dreaming for our Claude code agents to actually reach their maximum power. And like I said, Anthropic have recently dropped this official dreaming feature. Let's hear it from them directly. We've been experimenting with a couple of different types of processes and we landed on one. We call this process dreaming. Dreaming is a process that looks for patterns and mistakes across your recent agent sessions and their transcripts and automatically produces organized and up-to-date memory content. The ultimate goal of dreaming is continuous self-learning and self-improvement where the next day's agents automatically get better based on the learnings and the work of the previous days.

And apparently, the businesses Harvey and Rakuten who actually got first access to this dreaming feature saw massive upside, something like a 6x times task completion rate compared to before they let their agents dream. And so, I have good and bad news for you. Firstly, dreaming is here and it's really effective. However, it's currently only limited to enterprise customers and it also uses API credits, which means you're paying every time your Claude is dreaming and we want it to dream often. So, we don't want that. Onto the good news, I have for you this prompt right here, which is in full Andrej Karpathy alignment, a way to set up a routine for your Claude code to dream every night and reconcile all your sessions, see the overall patterns, remove duplicates, and make your Claude way more powerful. So, to set this up, copy the prompt, come into your Claude code, and simply just paste it in. So, the prompt says that we're going to set up a dreaming routine for your Claude code modeled on Anthropic's dreaming feature, so that Claude code can learn from your sessions while you are snoozing. It's first going to set up the memory. If it already has a memory system, it's going to work around that and then set up an alignment with how Karpathy wants an AI to dream.

The second thing is it's going to create a skill called foresight dream. And this skill, what it does is it's going to read your session transcripts from the last 24 hours across different sessions. This is the real breakthrough about it. Compare them against the memory file and what's currently stored, and find corrections. I gave you preferences, I repeated new facts worth keeping, memories that are now stale or wrong, and duplicates. Propose each change in a numbered list. You're going to get a report in a numbered list with a short quote from the transcript as evidence. Then auto apply only tiny safe fixes such as typos and index repairs. You don't have to approve those. You can also set it so that you auto approve everything if you prefer to be a little more fast and loose, but by default we've set it at everything else will wait for you. You can do it inside the console here or I've actually got a report in a HTML format where you can click approve. I'll show you that in just a second. If you run overnight with nobody here, write the proposals to the dream report so I can review them in the morning. The schedule, make dream run at 3:00 a.m. every night using whatever the computer supports, which at the moment we are using a routine. When you're done, run dream once right now as a test and show me what it proposes.

Now, if you are running this as a test, you are going to need to have used Claude or Claude Code in the last 24 hours for it to have new context to actually use to update your memory files. So, you can see in my routines, I've actually been running this for a couple of weeks. We have the nightly dream feature right here. Now, you can see it started on July 19th, July 20th, July 21st. I did I actually went and had hair surgery, if you can't tell. My hair is currently missing uh for 9 days, so I didn't actually use Claude Code over those 9 days, which means there was nothing to actually dream about. But now, since I'm back active, mine's working again, and you can see it's been doing it over the last 4 days since. And you can see what happens. It says, "Invoke the dream skill with no arguments. Use the skill tool, the skill dream," which we just read through, and basically this is the context that you need in order to actually do the dream. So, it went and did that while I slept every night at 3:00 a.m. when I used Claude Code the day before. And this is the report. This is what I call dream gate, which it will constantly add to until I approve or don't approve. So, you can see I can reject or approve the changes that the dream state has made. And if I scroll down, you can see other things. So, this is an addition. Uh this was an update.

So, the addition, "Benji isn't Solly, who has a dedicated video editor who is a she." This is true. Great she, by the way. Thanks for cutting this. "Who cuts the Dream Labs videos from the B-roll." Okay, great. So, it's learning more about me. It's learning more about my business, my workflows, my setups, so I can approve that, and it's going to add it into my Claude memory files. You can see this one right here, Claude Code MD is now 105 days stale, and its TBDs are already answered in memory. Okay, so we can get rid of that, which has been a memory file that's been slowing down my Claude for 105 days and not actually being used. You can see here it's identified where I save my video and thumbnail sources and assets in an iCloud Drive folder, which is fantastic, cuz now I can get Claude to actually access that directly and help me with the saving and opening and changing of those files. So, I can approve something like that. And now it feels like I really do have a co-founder working beside me scanning all of my conversations with it for these minute details. And the biggest thing, that's what dreaming really does, is it opens up patterns between sessions to be recognized where if you're just using an agent to write to the MD file, you don't get that opportunity.

And if you want to learn more tips from the greatest minds in AI, we have the world's best AI community, which we're just getting started. And we want to grow this to be a massive place. Well, I personally will take 95% of the work out of your hands, break down the top people like Kapathy, like Boris Cherney, literally the creator of Claude code, even business minds like Alex Hormozi to see what they're implementing in their businesses. Literally, you can't get more cutting edge than someone like Andre Kapathy, and bring those strategies back for you to implement in your routines and your business. So, if you'd like to be on the cutting edge, come and join us inside this community. I'm personally in there, as is our top AI researcher. And together, we can conquer this AI revolution using the best tools, playing with an unfair advantage in the business marketplace. Looking forward to seeing you in there. Thanks so much. I'll see you in the next video.

</details>
