---
title: "Antigravity 3.0 (New Upgrades): These New Updates make ANTIGRAVITY REALLY GOOD!"
video_id: m8gnIieakL8
channel: "[[channels/AICodeKing]]"
uploaded: 2026-01-14
processed: 2026-07-06
duration: "10:47"
url: https://www.youtube.com/watch?v=m8gnIieakL8
playlist: "[[Agents skills n8n]]"
type: news
difficulty: beginner
use_case: [ai-coding-tool-selection]
tools: [Antigravity, Claude Code, Gemini CLI, Google Drive]
llms: [Claude Opus, Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Antigravity 3.0 (New Upgrades): These New Updates make ANTIGRAVITY REALLY GOOD!

![thumbnail](https://i.ytimg.com/vi/m8gnIieakL8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=m8gnIieakL8) | 📅 Uploaded [[uploaded/2026-01-14]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> AICodeKing walks through three major Antigravity updates: a new Skills feature (triggerable custom workflows, similar to Claude Code custom commands), a controversial switch from 5-hour to weekly rate-limit refreshes for Pro users, and a new Secure Mode adding terminal permission levels and command allow/deny lists. He concludes the free tier is still the best free AI-editor option available, and Pro remains decent value despite tighter limits.

**Watch this if:** you use (or are considering) Antigravity and want to know how its Skills, rate limits, and new security controls actually work before you hit them.

## Key Takeaways
- Skills are saved, on-demand-triggerable workflows (via slash command) — similar to Claude Code custom commands — as opposed to Rules, which are always-active system instructions (e.g. "always add docstrings"). Skills can be created globally or per-workspace and shared across a team for consistent results.
- Google is introducing weekly rate limits (replacing the previous 5-hour refresh cycle) for Google AI Pro ($20/mo) users; Google AI Ultra ($200/mo) users are unaffected and remain the recommended tier for power developers.
- Usage is now calculated by "work done" (including hidden thinking tokens Gemini 3 generates during reasoning) rather than raw request counts, so complex planning/debugging tasks consume quota faster than simple ones.
- Even with tighter Pro limits, all tiers retain unlimited Gemini 3 Pro tab completions and full product features (agent manager, browser integration), plus access to top-tier models like Opus 4.5, Gemini 3 Pro, and Gemini 3 Flash.
- Secure Mode adds three Terminal Permission levels: Turbo (auto-executes everything, fastest/riskiest), Auto (agent decides when to ask for approval), and Off (every command needs explicit approval, recommended for production/sensitive projects).
- Secure Mode also adds Allow Lists (deny-by-default, most secure) and Deny Lists (allow-by-default except blocked commands) for controlling exactly which terminal commands the agent can run.
- For enterprise use, Google recommends running Antigravity in a sandbox/VM, setting command allow lists, and using strict version control to audit all agent changes.
- The host's overall take: Skills and Secure Mode are genuinely good additions; the rate-limit change is disappointing for Pro users but not disqualifying; the agent manager is still a bit buggy, so he still recommends the side-panel agent for most tasks; the free tier remains the best free AI-editor option available.

## 🛠 Tools & Software
- [[topics/Antigravity]] — Google's AI coding editor, the entire subject of the video: its new Skills feature, rate-limit changes, and Secure Mode.
- [[topics/Claude Code]] — referenced as the comparison point for how Antigravity's new Skills/slash-command triggering works.
- [[topics/Gemini CLI]] — mentioned as one of the tools where Pro-tier subscribers get better usage limits.
- [[topics/Google Drive]] — mentioned as one of the bundled perks (2TB storage) included with the Antigravity/Google AI Pro subscription.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — cited (as Opus 4.5) as one of the top-tier models still accessible to Pro users despite the new weekly limits.
- [[topics/Gemini]] — Gemini 3 Pro and Gemini 3 Flash are the models whose hidden "thinking tokens" now count toward usage, and remain available across tiers.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- If you rely on repeatable workflows (tests, code review, refactor style), create an Antigravity Skill for it instead of re-prompting each time, and share it with your team for consistent results.
- If you're on the Pro tier, monitor weekly usage more carefully than before, since complex reasoning tasks now consume quota faster via thinking tokens.
- Enable Secure Mode and set terminal permissions to "Off" (or use an allow list) for any production branch or sensitive project.
- For enterprise/team use, run Antigravity in a sandbox or VM with command allow lists and strict version control for auditability.

## 🔗 Related Videos
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Claude Opus, Gemini CLI
- [[videos/Can Claude Code Fix an Engineer's Terrible Taste]] — shared: Antigravity, Claude Code, Gemini
- [[videos/Google Stitch 20 Antigravity Free Design-to-Code Workflow Nobody Talks About]] — shared: Antigravity, Gemini, Gemini CLI
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Claude Code, Gemini, Gemini CLI
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Code, Claude Opus, Gemini CLI
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, Gemini CLI
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude Code, Claude Opus, Gemini
- [[videos/The greatest Claude Code workflow ever (10x your speed)]] — shared: Antigravity, Claude Code, Claude Opus

## Timeline
- `0:00` — Intro: Antigravity's recent updates address prior criticisms (buggy agent manager, confusing rate limits).
- `0:39` — Skills feature: on-demand triggerable custom workflows vs. always-active Rules, global/per-workspace, team sharing.
- `2:53` — Rate limit changes: weekly limits replace 5-hour refresh for Pro users; Ultra users unaffected.
- `4:44` — Usage now calculated by "work done"/thinking tokens rather than request count.
- `5:35` — What Pro/Free users still get: Opus 4.5, Gemini 3 Pro/Flash, unlimited tab completions, full product features.
- `6:03` — Secure Mode: Terminal Permission modes (Turbo, Auto, Off) and Allow/Deny command lists.
- `8:15` — Enterprise recommendations: sandboxes/VMs, command allow lists, version control auditing.
- `8:37` — Summary of the three updates and overall verdict.
- `9:58` — Recommendation: try the free tier first, Ultra only if you need unlimited power-user access.

## Transcript
<details>
<summary>Full transcript</summary>

Hi, welcome to another video. So, Antigravity has been getting some major updates lately, and I thought I'd tell you about them because they actually make the tool a lot more usable. Now, if you remember my previous videos, I was critical of some things in Antigravity, especially the agent manager, which was buggy, and the rate limits, which were a bit confusing. But Google has been listening to feedback and has fixed a lot of stuff here and there. So, let's talk about what's new — the major updates are the new Skills feature, the updated rate-limit structure, and the new Secure Mode. All of these are actually pretty useful, and I think they make Antigravity a much better option.

First, let's talk about Skills. Skills are basically like saved workflows or custom agents that you can trigger on demand — if you've used Claude Code commands or similar custom commands, this is similar to that. You can create custom skills that guide the agent's behavior for specific tasks. The way it works: you create skills either globally or per workspace, save them in specific locations, and then trigger them with a slash command whenever you want. So let's say you have a specific way you want the agent to write tests, or you want it to follow a certain code style when refactoring — you create a skill for that and trigger it whenever needed. This is different from Rules, which are always active — Rules are more like system instructions the agent always follows, like always adding docstrings or following a specific naming convention. Skills, on the other hand, are triggered on demand by you. I think this is a great addition because it lets you customize the agent for your specific workflows — you can create skills for code reviews, documentation generation, test writing, or even deployment workflows. It's similar to what was shown in a previous "self-spawning AI coder" video with custom commands, but this is built directly into Antigravity. The nice thing is you can share these skills across your team as well, so if your team has a specific workflow, everyone can use the same skills and get consistent results. Pretty cool for sure.

Now let's talk about the rate-limits update — this one is a bit of a mixed bag, honestly. Google has announced they're establishing weekly limits for all models, and this applies to Google AI Pro users as well; they say this is to balance giving the best possible quotas while maintaining fairness between users given incredible demand. This is not great news for Pro users — previously, limits refreshed every 5 hours, which was pretty generous, but now with weekly limits, if you burn through your quota in a day or two, you're stuck for the rest of the week. Google says this will only affect a minority of Pro users, but if you're a heavy user, you'll probably feel it. The good news is these limits do not apply to Google AI Ultra users — if you have the $200 Ultra subscription, you're still good, and Google says Ultra continues to be the best plan for power developers. But honestly, $200 is a lot, and most people won't want to pay that. So for the $20 Pro users, the limits are going to be relatively worse now. It's a bit disappointing, since the host was praising the Pro tier's value in previous videos, but hey, it's still usable — you can still use models like Opus 4.5, Gemini 3 Pro, and Gemini 3 Flash, which is great nonetheless; you just need to be a bit more careful about how you use your quota throughout the week.

One thing worth mentioning: Antigravity calculates usage based on work done rather than the number of requests. This means simple tasks use less of your quota while complex reasoning tasks use more — because of the thinking tokens Gemini 3 generates during its internal reasoning process, and these hidden tokens count against your usage. So if you're doing a lot of complex planning or debugging, you'll use up your limit faster — keep this in mind when managing your weekly quota. But regardless of tier, all users still get access to Gemini 3 Pro unlimited tab completions and all the product features like the agent manager and browser integration. So even with the new limits, it's still better than most alternatives, in the host's opinion. The free tier is still pretty solid, and even the Pro tier, despite the new weekly limits, gives you access to models like Opus 4.5 for free, which would cost a lot if you were paying for Claude's API directly. So it's still good value, just not as generous as before.

Now, let's talk about Secure Mode. This is actually a pretty important update because security has been a concern with Antigravity since it launched — within 24 hours of launch, security researchers found vulnerabilities where the agent could potentially leak data or execute unauthorized commands, and Google even has a disclaimer in their terms of use about Antigravity's security limitations. Secure Mode is their answer to this. When enabled, several security measures are enforced: first, different Terminal Permission modes. Turbo mode lets the agent automatically execute all terminal commands without asking — fastest, but also riskiest, since it can run anything. Auto mode is a balance, where the agent analyzes each command and decides when it needs your approval, giving oversight while staying fast. Off mode requires explicit human approval for every terminal command — slowest but safest, recommended for production branches and sensitive projects. Apart from this, you also have Allow Lists and Deny Lists: an Allow List is a positive security model where everything is forbidden unless you specifically allow it (the most secure configuration); a Deny List is the opposite, where everything is allowed unless you specifically block it — useful if you want speed but need to block specific dangerous commands. The host recommends using Secure Mode if you're working on anything sensitive or in a team environment — configure allow lists for commonly used commands and block everything else, so even if the agent tries something unexpected, it won't be able to. For enterprise users, Google also recommends running Antigravity inside a sandbox or VM, setting command allow lists, and using version control to audit all changes — pretty standard stuff, but good that Google is being transparent about the security considerations.

So, to recap the major updates: Skills give you custom workflows; the new rate limits are a bit worse for Pro users but still usable; and Secure Mode gives you better control over what the agent can do. The host thinks the Skills and Secure Mode updates are genuinely good additions; the rate-limit change is disappointing for Pro users but not the end of the world — you still get access to Opus 4.5, Gemini 3 Pro, and Gemini 3 Flash, which is great, you just need to be mindful of weekly usage. The free tier is still the best free tier available anywhere for an AI editor — you get access to all these models for free, which is insane — and even the Pro tier, despite the new weekly limits, is still decent value because you also get 2TB of Google Drive storage, a Gemini Pro plan for mobile, and better limits in Gemini CLI and Jules. The agent manager is still a bit buggy, and the host still recommends using the side-panel agent for most tasks because it's more stable, but overall Antigravity is still a solid option, and Skills and Secure Mode make it even more customizable and secure. If you haven't tried it yet, give it a shot — start with the free tier, and if you don't hit the rate limits, just keep using it; if you're a power user who needs unlimited access, the $200 Ultra tier is the only option now, which is a bummer, but for most people the free or Pro tier should still work fine.

That's majorly about it — overall, it's pretty cool. Share your thoughts below and subscribe to the channel; you can also donate via the Super Thanks option or join the channel for some perks. I'll see you in the next video. Bye.

</details>
