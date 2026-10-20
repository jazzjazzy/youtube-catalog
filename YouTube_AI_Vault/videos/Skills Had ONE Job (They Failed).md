---
title: "Skills Had ONE Job (They Failed)"
video_id: i0W90tlKfYg
channel: "[[channels/Better Stack]]"
uploaded: 2026-01-29
processed: 2026-07-06
duration: "5:50"
url: https://www.youtube.com/watch?v=i0W90tlKfYg
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [skill-invocation-reliability]
tools: [Claude Code]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Skills Had ONE Job (They Failed)

![thumbnail](https://i.ytimg.com/vi_webp/i0W90tlKfYg/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=i0W90tlKfYg) | 📅 Uploaded [[uploaded/2026-01-29]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Breaking down Vercel's own eval results: giving a coding agent a "skill" containing Next.js documentation was never invoked 56% of the time and provided zero improvement over no skill at all — sometimes even performing worse. Putting a compressed documentation index directly into agents.md instead scored 100% on Vercel's evals, because it removes the agent's decision point entirely.

**Watch this if:** you're deciding between packaging framework docs as a Claude Skill/agent skill versus baking them into agents.md (or claude.md) and want the actual eval numbers behind that choice.

## Key Takeaways
- Vercel's goal was giving a coding agent version-matched Next.js documentation so it uses current APIs instead of outdated training-data knowledge.
- Skills are an open standard from Anthropic — modular bundles of instructions/scripts/context an agent loads on demand — but the agent itself decides when to load them, which turned out to be the core weakness.
- In Vercel's evals, the skill was never invoked 56% of the time, and having the skill available produced zero measurable improvement over having no skill at all — sometimes performing worse than baseline, suggesting an unused skill can introduce noise/distraction.
- Explicitly instructing the agent in the prompt to "use this skill" raised the trigger rate to 95% and the eval pass rate to 79%, but wording proved brittle — e.g. "you must use the skill" caused it to skip project context, requiring careful combined phrasing ("use both the skill and the project context").
- Switching to agents.md (the same mechanism as Claude Code's claude.md) removes the agent's decision point because instructions are always in the system prompt rather than fetched on demand — but naive use risks context bloat from dumping entire documentation sets in.
- Vercel's fix: put a documentation index (file paths, not full content) in agents.md, plus an instruction to "prefer retrieval reasoning over pre-training reasoning" for Next.js tasks — this scored 100% on Vercel's evals, including perfect build/lint/test scores.
- Vercel's theory for why agents.md wins: it eliminates the decision point — knowledge becomes persistent system-prompt context instead of something the model must choose to fetch.
- Skills aren't useless: Vercel found they complement agents.md — skills work better for explicit, user-triggered workflows (e.g. "upgrade my Next.js version," "migrate to the app router"), while agents.md wins for general, passive framework knowledge with today's models.
- Recommendations for anyone authoring skills or agents.md files: don't wait for skill-triggering to improve, compress context aggressively, design for retrieval rather than memory, and always validate with evals rather than assumptions.

## 🛠 Tools & Software
- [[topics/Claude Code]] — referenced by name as using the equivalent convention (claude.md) to Vercel's agents.md approach.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Before shipping a skill for your framework/tool, run an eval measuring actual invocation rate rather than assuming the description alone will trigger it.
- If you must rely on a skill, test explicit "use this skill AND the project context" prompt wording rather than a single terse instruction.
- For general, always-relevant framework knowledge, put a compressed documentation index (file paths, not full text) into agents.md/claude.md instead of a skill.
- Add an explicit "prefer retrieval reasoning over pre-training reasoning" instruction when you want the agent to look up current docs instead of relying on stale training knowledge.
- Reserve skills for explicit, user-triggered workflows (e.g., "migrate to X," "upgrade to version Y") rather than passive background context.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: Vercel's surprising finding that agents.md beats skills for providing Next.js docs.
- `0:40` — The goal: version-matched documentation so the agent doesn't rely on stale training data.
- `1:10` — What skills are, and why on-demand loading is their core weakness.
- `2:00` — Eval results: skill never invoked 56% of the time, zero improvement, sometimes worse than baseline.
- `2:40` — Explicit "use this skill" prompting raises trigger rate to 95%/79% pass rate but proves wording-brittle.
- `3:20` — Switching to agents.md: removes the agent's decision point, but risks context bloat.
- `3:50` — Vercel's fix: a documentation index plus a "prefer retrieval reasoning" instruction scores 100% on evals.
- `4:30` — Why agents.md wins: no decision point, persistent context instead of on-demand retrieval.
- `5:00` — Skills and agents.md actually complement each other — skills for explicit triggered workflows, agents.md for passive framework knowledge.
- `5:30` — Recommendations: compress context, design for retrieval, always validate with evals.

## Transcript
<details>
<summary>Full transcript</summary>

Skills might not be the best approach to give additional context to your agents — you might have more luck going back to the agents.md file. This was the surprising result Vercel found testing the best method to provide coding agents with Next.js documentation.

Vercel's goal was giving a coding agent additional context — Next.js documentation — so it uses current APIs not yet in training data, or stays restricted to methods available in an older version, via version-matched documentation. They tested two approaches. First, skills: an open standard from Anthropic, modular bundles of instructions, scripts, and context an agent loads on demand to perform tasks more accurately. The crucial detail: it's entirely up to the agent to decide when to load this information — and that's the current downfall. In Vercel's evals, the skill was never invoked 56% of the time; the agent just decided not to use it. Providing the skill gave zero improvement over an agent without it, and surprisingly sometimes performed worse than baseline, suggesting an unused skill introduces noise or distraction.

To fix this, Vercel tried explicitly prompting "please use this skill," which raised the trigger rate to 95% and the eval pass rate to 79%. But different wordings produced drastically different results — saying "you must use the skill" caused it to skip project context, requiring phrasing that covered both the skill and the project context. Vercel didn't like this fragility, noting that if small wording tweaks cause large behavioral swings, the approach feels too brittle for production.

So they tried agents.md — an open format (the same mechanism as Claude Code's claude.md) used to give coding agents instructions that are always included in the system prompt. Unlike skills, the agent isn't in charge of deciding to fetch the information — it's already there. But this risks context bloat, where growing context degrades output, so you can't just dump the entire Next.js documentation into agents.md. Vercel's solution: a documentation index — a list of file paths to individual documentation files — plus an instruction to "prefer retrieval reasoning over pre-training reasoning" for Next.js tasks. Testing this on their evals, the agent scored 100%, including perfect build, lint, and test scores — significantly more reliable and accurate than skills. Classic software engineering: the simpler approach turns out to be the best one.

Why does agents.md outperform skills? Hard to say definitively since AI is something of a black box, but Vercel speculates it comes down to decision-making: with agents.md there's no decision point — the agent is told at the start, in the system prompt, exactly where each documentation file is, making the knowledge persistent context instead of something the model must decide whether to use on demand.

This doesn't make skills useless — Vercel found they complement each other. Skills work better for explicit, user-triggered workflows ("upgrade my Next.js version," "migrate to the app router," "apply framework best practices"), while agents.md outperforms for general, passive framework knowledge, at least with today's models. Future models may be optimized for skill-based retrieval, but not yet. Vercel's recommendation for framework authors and skill/agents.md writers: don't wait for skill triggering to improve — compress context as much as possible, design for retrieval rather than memory, and always test with evals. For end users, Vercel provides a tool to download documentation and a pre-built agents.md file matched to your specific Next.js version.

</details>
