---
title: "The cure for AI slop is a 1986 aircraft manual"
video_id: uJblcC4lKYw
channel: "[[channels/Ege Vusal Chelebi]]"
uploaded: 2026-07-24
processed: 2026-09-11
duration: "16:41"
url: https://www.youtube.com/watch?v=uJblcC4lKYw
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [ai-writing-quality]
tools: [Agent Skills, Caveman]
llms: [Claude, GPT-5.5]
protocols: [ASD-STE100]
transcript: true
tags: [youtube, ai-automation]
---

# The cure for AI slop is a 1986 aircraft manual

![thumbnail](https://i.ytimg.com/vi_webp/uJblcC4lKYw/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=uJblcC4lKYw) | 📅 Uploaded [[uploaded/2026-07-24]] | 🗓️ Processed [[created/2026-09-11]]

## TL;DR
> A viral thread claimed the fix for AI slop isn't banning words like "delve" but ASD-STE100 — Simplified Technical English, the 53-rule, 900-word aerospace writing standard from 1986. The creator distilled the 434-page spec into an agent skill and a linter, then ran 6 real developer writing tasks across 4 conditions on 2 models. Result: banned-word lists barely moved slop on Claude (-3%), Orwell's rules cut it 43%, and STE cut it 74% (and 50% on GPT-5.5). The durable lesson: give the model a checkable writing system, not a blacklist.

**Watch this if:** you're fighting AI-sounding docs, READMEs, or agent output with banned-word lists and want a measured, testable alternative.

## Key Takeaways
- Slop reduces to six machine-checkable habits: synonym rotation, hedging stacks, nominalized verbs, marketing adjectives, run-on sentences, and chatty phrasal verbs — each one nameable, so each one bannable.
- [[topics/ASD-STE100]] kills each habit by design: one meaning per word (900-word dictionary), no complex verb constructions, verbs not nouns, 20-25 word sentence caps, semicolons banned outright.
- The standard was built so non-native-speaker aircraft mechanics never misread a manual — a 1996 study showed comprehension jumping from 69% to 87% for non-native readers, up to native level.
- Measured on a custom linter (violations per 100 words, Claude): baseline 4.36, banned-words list 4.21 (-3%), Orwell's six rules 2.48 (-43%), STE 1.12 (-74%). On [[topics/GPT-5.5]] STE still cut slop 50%, though banned words also worked there (-40%) — the 3% flop was a [[topics/Claude]] quirk.
- The damning data point: banning em dashes killed em dashes (6 → 1) while overall slop barely moved — you get a slop paragraph with no em dash in it.
- In practice: a distilled skill file (via [[topics/Agent Skills]]) with strict mode for procedures/error messages and a looser STE-flavored mode for prose; the [[topics/Caveman]] rule set already implements the short-checkable-rules idea.
- Caveat: STE fixes the form of slop, not the substance — and keep it away from anything that needs a voice; use it for docs, PRs, error messages, and agent output only.

## 🛠 Tools & Software
- [[topics/Agent Skills]] — the 434-page standard is distilled into an agent skill file with strict and STE-flavored modes rather than pasted into context.
- [[topics/Caveman]] — cited as an already-adopted product built on the same "short checkable rule set" idea.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — primary test model; its slop is flashy (em dashes, "seamless", run-ons), and banned-word lists barely helped it (-3%).
- [[topics/GPT-5.5]] — replication model; STE cut slop 50% there, and its slop is quieter — clean-looking sentences that are too long and too passive.

## 📡 Protocols & Standards
- [[topics/ASD-STE100]] — the Simplified Technical English specification (issue 9, Jan 2025, free download): 53 rules plus a ~900-word one-meaning dictionary, and the best-performing anti-slop condition in the test.

## ✅ Action Items
- Stop playing banned-word whack-a-mole; adopt a writing system the model can check itself against (STE, Orwell, or a small Vale-style config).
- Grab the skill and linter linked from the video and score your AI output as violations per 100 words.
- Use strict STE mode where a wrong reading has a cost (procedures, error messages); use the looser flavored mode for prose.
- Make the rule set a test the output must pass in your pipeline — and don't apply it to marketing copy or anything needing a voice.

## 🔗 Related Videos
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Caveman, Claude
- [[videos/Never hit Claudes Usage Limit Again]] — shared: Caveman, Claude
- [[videos/This Claude Skill Cuts Your Token Costs In HALF]] — shared: Caveman, Claude
- [[videos/Why OpenAI Built Symphony and Gave It Away for Free]] — shared: Claude, GPT-5.5

## Timeline
- `0:06` — The claim: same prompt, two answers, one is slop
- `0:51` — How it started: a 2M-view thread on making AI docs not sound like AI
- `1:28` — Banning words is whack-a-mole; the model defaults to the average of the internet
- `1:40` — The better answer: ASD-STE100, built so mechanics never misread a manual
- `2:14` — Defining slop mechanically: the six habits
- `3:56` — What STE is: 1986 spec, issue 9 (Jan 2025), 434 pages, free
- `5:02` — The 900-word dictionary: one meaning, one grammatical job per word
- `5:53` — Rule-by-rule execution of the slop list (word caps, semicolon ban, verbs not nouns)
- `7:16` — Before/after: a caching library README with and without the standard
- `8:07` — Error message result: 41% fewer words, perfect linter score
- `8:47` — Human evidence: 1996 technician study and Microsoft's 2007 translation study
- `10:28` — The test: 6 writing tasks x 4 conditions, scored by a custom linter
- `11:10` — Results: baseline 4.36 vs STE 1.12 (-74%); banned words only -3%
- `11:57` — GPT-5.5 rerun: STE -50%, banned words -40%; models slop differently
- `13:55` — How to use it: distilled skill with strict and STE-flavored modes
- `15:11` — Verdict: cures the form of slop, not the substance

## Transcript
<details>
<summary>Full transcript</summary>

The same prompt, same model, two answers. Answer one says designed to slot into your existing stack with minimal friction and no vendor lock-in. And the answer two says a normal cache matches requests by exact text. A small change in wording then causes a cache miss. And one of these is slop. And two million people just watched a thread claim that the cure is a writing standard built for aircraft mechanics in 1986. And that sounded just absurd enough that I had to shake in myself, too. So, I got the real standard, all 434 pages of it. I got the rules, gave them to my model, and ran the test nobody had actually run before. And here's the output. But first, the story, because the story is the reason this video exists, too. A few days ago, a post went viral and an account called Joe Briscoe asking in plain words, "How do I make AI write technical documentation that doesn't sound like AI?" And it got over two million views. And then a writer called Vox picked it up and made the sharper point. He said, "Stop telling Cloudy no em dashes. Stop banning the word delve." And this is whack-a-mole and you lose because the model was never choosing those words on purpose. You never gave it a writing system, so it defaults to the average of the internet. And the average of the internet is slop.

His fix was George Orwell's six rules for clear writing from 1946. And then Mike Hostetler, a man whose biological says chief agent officer, quote tweeted the better answer. Just tell the model to always use ASD-STE100, simplified technical English. A real published international standard. A 53-rule and 900-word dictionary built so that an aircraft mechanic never misreads a repair manual. Because a misread repair manual kills people. And that was the moment I fell down the rabbit hole. A mum property decides the whole thing. So, keep it in mind the entire way. The rules that matter are machine checkable. A dumb script can verify them, and no taste is required. Before the fix, we have to be precise about the disease. Sounds like AI is a feeling, not a definition. And you cannot fix a feeling. So, the first thing I did was to try to pinch slope down mechanically. And everything I kept running into collapses into six habits. You already know every one of them. One, synonym rotation. The text calls the same thing three names in one paragraph. The user, the customer, and the client. You are never sure they are the same one person.

Two, hedging. Literal help of verbs stack until nothing happens. It's important to note that this may potentially help to improve. Five verbs and zero verb. Three, verbs frozen into nouns. A perform an analysis of instead of analyze. And provides assistance instead of help. The grammar people call it nominalization. All you need to know is that it makes sentences longer and weaker. Four, marketing adjectives. Seamless, robust, powerful, cutting edge. Words that claim quality instead of showing it. Five, run-on sentences. Four ideas stitched together with m dashes and semicolons when they should be four sentences. Six, overly chatty phrasal verbs. A spin up, reach out, dive into. And here's why this list matters. Every one of these is a specific, nameable move. And anything you can name, you can ban, too.

Now, hold that list. We are about to check it out off rule by rule. So, what is this aircraft standard? Now, I was obviously not around in the late 1970s. So, this is a story the way my research tells it. Back then, European airspace had a deadly problem. Maintenance manuals were written in English. But, most of the mechanics reading them around the world were not native English speakers. And one misread instruction on an aircraft is a funeral. So, industry built a controlled version of English. Not a style guide, a specification. And first released in 1986. The current version, issue nine, came out in January 2025. And you can download it for free from the official site. The full document is 434 pages. And I'll be honest with you, I didn't sit down and read every single page. I dug through it and mined out the parts that matter. The rules, the dictionary, and the logic behind them. That took a while, but you will never have to open it.

It has two parts. Part one is procedures. Part two is the part that genuinely surprised me. A dictionary of roughly 900 approved words. Where every word gets the exact one meaning and one grammatical job. Now, in AST, fall only means to move down by gravity. You are not allowed to use it to mean decrease. And where English gives five words for one idea, AST keeps one and deletes the rest. You get start. You do not get begin, commence, initiate, or originate. Notice what that just did. Synonym rotation. Slope habit number one is dead by design already. And one more number I found that tells you this thing escaped its cage. Today, 64% of the people are requesting the standard or outside aerospace and defense entirely.

Now, watch the slop list get executed rule by rule. This mapping is the part of the research that made me sit up. A synonym rotation killed by rule 1.11. One name per thing plus the one meaning dictionary. Heging stacks killed by rule 3.4. No complicated verb constructions. Frozen verbs killed by rule 3.7. Use a verb for an action, not a noun. Performant analysis is illegal. Analyze is the law. Marketing adjectives. They are simply not in a dictionary. Seamless is not an approved word. You cannot say it. Run-ons killed by hard caps. Rule 5.1. An instruction gets at most 20 words. Rule 6.3. A descriptive sentence gets 25. And the semicolon is banned outright. Phrasal verbs killed by rule 9.3. You remove the panel. You do not take it off. And here's the punchline. A style was never designed for AI. It was designed 40 years ago to remove ambiguity for a stressed human reader. AI slop is just ambiguity with good posture. The aerospace industry has spent four decades engineering the cure but for a different patient.

Let me read you the real thing, not a toy example. Same model, same job. Write the intro for a caching library's readme. Here's a default with no writing system. Traditional caches miss constantly in LLM workloads because users rarely phrase the same question identically. This is 1/3 of word breath with an em dash coming and it closes with design to slot into your existing stack with minimal friction and no vendor lock-in. For marketing phrases, wearing a trench coat. Now, the same model with a standard loaded. A normal cache matches a request by exact text. A small change in wording then calls a cache miss. Flux cache compares the meaning of a new prompt with the prompts already in the cache. Short sentences, active voice, one idea each, nothing to decode at all. And my favorite result was an error message. The default version hedges on pads. You have exceeded the limit. This ensures fair access for all users. The ST version said the same thing in 41% fewer words and scored a perfect zero on my checker. Everything it deleted was slop. Nothing it deleted was information. The gap between what you caught and what you lose is the entire game.

Now, does controlled English actually work on human readers or is it just an aesthetic I happen to like? I went to digging for studies and there's a real evidence. I will give it to you straight including the parts that weaken it. The strongest study I found is from 1996 by Sherback, Dury, and Volets. They gave 175 aircraft technicians real maintenance work cards. Some in regular English, some in simplified. Comprehension went from 76% to 86. And for the non-native speakers, the people the standard was built for, it went from 69 to 87. Now, listen to that. The constraint pulled the struggling readers up to the native speaker level. Microsoft research ran a bigger one in 2007. 520 sentences translated into Chinese, French, Dutch, and Arabic. The controlled versions beat the normal ones in every single language and the odds of that being luck are below one a thousand. And the single most effective rule in their data was cutting flowery and formal phrasing, which is almost literally the definition of anti-slop.

Now, the honesty. Those translations gains were real, but small. About a tenth of a point on a four-point scale. An Airbus study found that oversimplifying can even backfire and slow readers down. Shorter is not always clearer, and every study here measures understanding, not memory. Nobody has shown a STE text is remembered better, only understood better. So, use it for clarity, do not expect magic, too. And here's the gap in everything I just told you. All of that evidence is about aircraft manuals and human writers. Nobody had ever tested this standard on AI output. The Wired claim was a guess by analogy, so I ran it. The setup in plain words. Six real writing jobs a developer actually does. A readme, a pull request description, API docs, an error message, a getting started guide, and a depreciation notice. Each one generated four ways. A plain baseline. The band words list everyone is using right now. Orwell's six rules, and my STE score. Then I wrote a linter, a small script that counts the mechanical stuff. Words per sentence, semicolons, passive voice, phrasal verbs, marketing adjectives.

The score is violations per hundred words. And lower is cleaner. The results aren't cloudy. The baseline scored 4.36. The band words list 4.21. This is a 3% improvement. Three. Orwell's rules 2.48. Down 43%. And simplified technical English 1.12. Down 74%. Less than a third of the baseline slope. And buried in that data is the most damning number of the whole experiment. The banned words list did kill em dashes, six down to one, because that's the one thing you told it to do. And the overall slope barely moved. You banned the em dashes and you got a slope paragraph with no em dash in it. That's the entire mistake in one data point.

But a result on one model is not a result, so I ran the whole thing again on GPT 5.5. And here's the honest part. ST still cut slope in half, minus 50%. So the core finding holds, but on GPT the banned words list actually worked, minus 40%. And the overall tied ST there. So that brutal 3% number was a Claude quirk, not a law of nature. The two models even sloped differently. Claude's slope is flashy, em dashes, seamless long run-ons, but GPT slope is quiet, clean-looking sentences that are simply too long and too passive. Same disease, but with the different symptoms. The finding that survives both models is narrower and truer. Give the model a real writing system and slope drops by half or more. Every time on every model I tried. ST was the best or tied for best. Banning words one at a time is just a less reliable version of the right idea.

One caveat because it matters, my linter is not the full standard. The people who maintains ST say plainly that no software can certify full compliance. Some rules need a human to judge whether a sentence makes sense or not, and they are right actually. But the judgement rules are not the slope rules. Slope is the mechanical stuff, and the mechanical stuff is 100% checkable by a script. And that idea is not even new. From what I found, Boeing has shipped a simple fighter English checker with a 350 rule parser since about 1990. Mission checked writing is a solved, boring, battle-tested category. We just pointed it at a new problem. So, how do I actually use this? Not by pasting 434 pages into the model. The standard is copyrighted and 900 dictionary words would burn your context for nothing. You distill it. I built a small-scale file with two modes. Strict mode is for procedures and error messages, anywhere a wrong reading has a cost. It gets the full rules and the hard lines caps. AST flavored mode is for normal prose. It gives a sentence discipline, the paragraph discipline, and the no phrasal verbs habit, but drops a dictionary lockdown because a blog post needs range, not personality transplants.

And some smart people think even that is too much. One engineer replied to the thread, "AST AST 100 is a bit too much. I wrote a tiny well rule set instead. 90% of the benefit." And he's not wrong, and that's the real takeaway. The standard is one option. A short checkable rule set is a product. And this product is actually Caveman, which has been already implemented a couple of months ago, and people have adopted using it, too. But burn this caveat in. AST fixes the form of slop, not the substance. A linter can turn a whole of paragraph into a clean, confident, well-punctuated whole paragraph. It cannot make it true. Slop is two problems wearing one coat, bad writing and nothing to say. This fixes the first one only. So, the verdict. Does a 1986 aircraft maintenance standard cure a slop? One form, yes, better than anything else I tested, and for a reason that is not an accident. Slop is ambiguity, and STE is 40 years of engineering aimed directly at ambiguity. But it will not make your writing good. Only unsloppy.

And keep it away from anything that needs a voice. Running your marketing copy through STE is a torque wrench spec applied to a poem. Use it where invisible clarity is the entire job. Docs, pull requests, error messages, agent output, and nowhere else. And honestly, this standard is not even the lesson. The lesson is the thing Box pointed at and my numbers back up. You will not fix AI writing by banning dull of one word at a time forever. You fix it by giving the model a system it can check itself against instead of a blacklist it will always root around. Orwell is a system. STE is a stricter one you can test as well. A 10-line well config is a smaller one. Pick one, make it a test the output has to pass, and stop playing whack-a-mole. Constrain the writer and you free the reader. The aerospace industry figured that out before most of us were born. The skill, the linter, and every number from this video are linked below. This is the first video on this channel, too. If this is the kind of the test you want more of, you know what to do. See you in the next one.

</details>
