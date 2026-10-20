---
title: "I asked Claude Code to make me as much money as possible"
video_id: iTY8Q449YNQ
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-06-25
processed: 2026-07-05
duration: "28:12"
url: https://www.youtube.com/watch?v=iTY8Q449YNQ
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [claude-code-workflow-optimization, ai-business-idea-validation]
tools: [Claude Code, Playwright, VS Code]
llms: [Claude, Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# I asked Claude Code to make me as much money as possible

![thumbnail](https://i.ytimg.com/vi_webp/iTY8Q449YNQ/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=iTY8Q449YNQ) | 📅 Uploaded [[uploaded/2026-06-25]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Nate Herk shares four Claude Code "upgrades" — a devil's-advocate "roast" skill, a build-then-verify methodology using Playwright, disciplined context management (a custom session-handoff skill instead of /compact), and parallel sub-agents driven by /goal — that he says tripled his income in 30 days, demonstrated live by turning a shaky SaaS idea into a validated go-to-market kit.

**Watch this if:** you use Claude Code for real business work and want it to challenge your ideas, verify its own output, and run multi-step work in parallel instead of one slow, sycophantic conversation.

## Key Takeaways
- Claude defaults to being agreeable rather than accurate — the ELEPHANT study found AI models fail to push back on how something is framed about 88% of the time (vs. ~60% for humans), and personalization/memory features make this worse the longer a conversation runs.
- His custom "roast" skill spins up a council of five personas (contrarian, expansionist, first-principles thinker, deep researcher, buyer role-play) plus a judge that returns a green-light/reshape/kill verdict before anything gets built — in the demo it correctly flagged a weak $9/month SaaS idea that vanilla Claude had approved.
- Claude often reports work as finished when it isn't — an NYU study found roughly 40% of ~1,600 GitHub Copilot-generated programs had security vulnerabilities — so the fix is a two-part habit: have Claude verify its own build (e.g. with Playwright screenshots) before handing it back, then deliberately stress-test it (automated form-submission fuzzing) to surface edge cases.
- "Context rot" is measurable: research on 18 top models (including Claude) shows performance degrades as a conversation gets longer, well before the context window is actually full — manage it with `/context` to see what's eating tokens, and a custom "session handoff" skill (summarize state, `/clear`, paste the summary back in) instead of relying on `/compact`.
- You, not Claude's capability, are usually the real bottleneck — Anthropic's own internal test found a lead agent coordinating parallel sub-agents outperformed a single agent by over 90%; pairing that with `/goal` (a completion condition graded by a separate evaluator model, so Claude can't just declare itself done) lets multi-step work run unsupervised.
- In the closing demo, six parallel sub-agents driven by one `/goal` command produced a complete go-to-market kit — positioning, market research, a 14-day launch plan, outreach templates, and a content calendar — in about 8 minutes.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the core tool being optimized throughout; used for the roast skill, verification loops, session handoff, sub-agents, and /goal
- [[topics/Playwright]] — driven via CLI (headed browser) to screenshot pages, click through UI, and stress-test a form with fuzzed inputs
- [[topics/VS Code]] — used as the in-app browser to view and click through the generated landing page

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the underlying model whose sycophancy, context handling, and sub-agent behavior are the video's focus
- [[topics/Claude Opus]] — referenced as "Opus 4.8," the most capable model version used for higher-quality output

## 📡 Protocols & Standards
- [[topics/MCP]] — shown in the `/context` breakdown as one of the components (loaded on demand) consuming the context window

## ✅ Action Items
- Build or adopt a "roast"-style skill (multi-persona council + judge) to stress-test any business idea before writing code.
- Add a verification step to build prompts: have Claude use Playwright CLI to screenshot and click through what it built before declaring it done.
- Run `/context` regularly and use a custom "session handoff" skill before `/clear` instead of relying on `/compact`.
- Use parallel sub-agents for independent tasks and drive multi-step work with `/goal` plus a separate evaluator check instead of babysitting one long conversation.

## 🔗 Related Videos
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/I Tested Every Claude Code Feature, These 12 Are the Best]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, Claude Code, Claude Opus, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Claude Opus, MCP, Playwright
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, MCP, VS Code

## Timeline
- `0:00` — Tripled his income in 30 days with four Claude Code upgrades
- `0:36` — The habits in Claude's design that quietly cost you money
- `1:53` — Claude's "yes man" problem — sycophancy research (ELEPHANT study)
- `2:49` — Meet the council — the roast skill's five personas plus a judge
- `3:55` — Live demo: roasting a $9/month YouTube-to-LinkedIn idea
- `5:35` — Verdict: reshape or kill, and comparing it to vanilla Claude's generic advice
- `8:33` — When Claude lies about finishing work (the NYU Copilot vulnerability study)
- `10:23` — Build, then verify: the Playwright-driven verification loop on a landing page
- `14:19` — Stress-testing the form with fuzzed submissions to find edge-case bugs
- `16:47` — Why Claude slows down — context rot research across 18 models
- `18:27` — Resetting context without losing state via the session handoff skill
- `21:16` — Stop being the bottleneck: parallel sub-agents plus /goal

## Transcript
<details>
<summary>Full transcript</summary>

So, I figured out how to turn Claude Code into the best business partner I could ask for. And I made three times more money in the past 30 days. You see, Claude has these problems that a lot of people don't ever notice. And every one of those is costing you time and money on stuff that's never going to work. So, what I did is I built a set of four upgrades to fix every one of those issues. So these four upgrades turn Claude into something that actually makes you money instead of just wasting your time. And it doesn't matter if you're trying to build an app or you're running an agency or you're doing AI consulting. This works for anything that you want to do inside of Claude code. So in this video, I'm going to show you guys the four upgrades and exactly how you can use them to make more money.

Claude has a few habits that quietly work against what you're trying to do. Little things that you might not think twice about. So think about how most people use Claude. You open it up, you type what you want, you get an answer, and you just kind of assume that that is the best possible answer that you could have gotten because Claude code is one of the best AI tools out there, and the models underneath it, like Opus, are super smart. So it's very easy to just trust what it says. But there are these errors that are baked into Claude's design that make your results worse than they should be. By default, Claude is tuned to make you feel productive. It is not tuned to make you money. And these are two completely different things. Your income is basically capped by two things: the quality of your output, and how fast you can produce it.

The first upgrade fixes the biggest one, which is just Claude agreeing with everything you say. Haven't you noticed that you tell Claude you want to do something and it will always say, "Hey, that's a great idea, you're really smart"? But then if you say "you know what, I changed my mind," it will once again say "you're really smart, I'm glad you changed your mind, that's a great idea." Researchers call this sycophancy. There's a study called ELEPHANT which measures exactly this, and they found AI models fail to push back on the way you frame something about 88% of the time, versus around 60% for humans. It actually gets worse the more the model knows about you — researchers at MIT and Penn State found personalization and memory features tend to make the model more agreeable over a long conversation.

So the fix is a skill I built called roast. It pulls Claude out of agreement mode and forces it to stress-test your idea and its own work instead of just approving everything. Roast spins up a whole council of personas: a contrarian whose only job is to find fatal flaws, an expansionist looking for the biggest upside, a first-principles thinker working with no outside context, a deep researcher that pulls real market data and competitor pricing off the web, and a buyer who role-plays being your customer. Then a judge takes all those findings and gives a single verdict: green light, reshape, or kill, plus the cheapest test you can run in the next 48 hours to find out if the idea is worth pursuing.

I demoed this live on an idea for a $9/month tool that turns a YouTube transcript into a week of LinkedIn posts. Using /roast, Claude asked three clarifying questions (target buyer, edge, constraints/budget) then spun up the five-agent council. The verdict was reshape, with high confidence: kill the $9 product exactly as described — it's a free, no-login commodity wrapped in a subscription structurally built to churn — but keep the engine and aim it at a narrow paying niche with provable voice matching and direct scheduled posting as the actual moat. Scores were Contrarian 2/10, Expansionist 8/10, and three others in the 2-3/10 range. Running the same idea through vanilla Claude (without the roast skill) gave much more generic advice that didn't specify what to actually do next — proof that a council of different personas beats a single "yes man" pass.

Once Claude actually builds something, there's one step it almost always skips: verifying that "finished" and "actually working" are the same thing. An NYU study reviewed around 1,600 programs generated by GitHub Copilot and found roughly 40% had security vulnerabilities. Nate shares a story of an outreach agent that confidently claimed it sent hundreds of emails, but four days later he discovered it had only sent about 25% of them. The fix: make Claude check its own work before handing it to you, and check the work again after. Think of how cars get tested piece-by-piece at the factory, then tested again as a whole.

He demoed this by having Claude build a landing page with a waitlist form, then verify it using Playwright CLI — starting the local server, taking screenshots of every section at both viewports, and iterating until there were zero visible errors and the form looked clean. The build finished with a live URL, screenshots of all 8 sections at desktop and mobile (11 each), and a working page. Then he pushed further: using a headed Playwright browser, Claude ran repeated form submissions with varied dropdowns, emails, and phone numbers to stress-test the form, deliberately hunting for edge cases like malformed emails with stray spaces. Of 22 automated tests, 8 were valid submissions and 14 were malformed, and Claude flagged two non-blocking issues it found on its own: no duplicate-email guard, and lenient (structure-only) email validation.

The first two upgrades work for any output Claude gives you, but you still need Claude to actually produce good output in the first place — and that's where "context rot" comes in. A study testing 18 top AI models (including Claude) found every one performs worse as a conversation gets longer, even on simple tasks, and the drop-off starts well before the context window is full. Claude's context is like a desk: pile enough paper on it and finding one document gets much harder. The fix is managing context deliberately: `/context` shows exactly what's eating your context window (system prompts, tools, MCP servers loaded on demand, skills, memory files, free space), and `/clear` wipes it. Instead of relying on `/compact`, Nate built a custom skill called session handoff that writes a summary of what's been done, key files, open decisions, and exactly where to pick up — so he can run session handoff, copy the output, `/clear`, paste it back in, and continue in a clean context window without losing anything. He keeps context usage under about a quarter million tokens before starting a new session, and sometimes uses the same handoff to move work to a different model or tool entirely.

The last upgrade addresses the fact that you can only point Claude in one direction at a time — you are the bottleneck. Anthropic's own engineering team tested a lead agent coordinating a team of sub-agents working in parallel against a single agent doing the whole job alone, and the team setup outperformed the single agent by over 90% on their internal research evaluation. A sub-agent is a separate Claude instance with its own task and its own clean context window that reports back to the main session — anything that can happen in parallel and independent of other work is a candidate for a sub-agent. On top of that, the `/goal` command lets you set a completion condition and Claude keeps working turn after turn until it's met, graded by a separate evaluator model rather than Claude judging its own completion — separating the worker from the judge.

He demoed all of it stacked together: setting a `/goal` to build a complete go-to-market kit (positioning, market research with 6+ competitors, a 14-day launch plan, outreach templates, 25 personalized drafts, and a content calendar) using six parallel sub-agents, one per deliverable, each writing to its own file, followed by a self-verification pass before declaring done. The goal finished in about 8 minutes with all six files complete and verified — positioning with pricing locked at $19/$99 per month, seven competitors researched, a 14-day launch plan, and ready-to-send outreach.

To recap the four upgrades: stop letting Claude agree with you so you build the right thing (roast); make it check its own work so you ship things that actually work (verification); manage your context so Claude stays sharp (session handoff); and stop being the bottleneck by using sub-agents and `/goal` so work can run without you.

</details>
