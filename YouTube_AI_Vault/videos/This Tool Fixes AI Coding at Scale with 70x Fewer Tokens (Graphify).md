---
title: "This Tool Fixes AI Coding at Scale with 70x Fewer Tokens (Graphify)"
video_id: WNru_PFycT8
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-29
processed: 2026-07-05
duration: "5:16"
url: https://www.youtube.com/watch?v=WNru_PFycT8
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [ai-codebase-context-management, token-cost-reduction]
tools: [Graphify, Claude Code, Cursor, Tree-sitter]
llms: []
protocols: [RAG]
transcript: true
tags: [youtube, ai-automation]
---

# This Tool Fixes AI Coding at Scale with 70x Fewer Tokens (Graphify)

![thumbnail](https://i.ytimg.com/vi_webp/WNru_PFycT8/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=WNru_PFycT8) | 📅 Uploaded [[uploaded/2026-04-29]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Graphify turns a codebase into a queryable knowledge graph instead of a pile of raw files, using tree-sitter for structure and an LLM to extract meaning, clustering code, docs, diagrams, audio, and video together locally. In a live demo, the same cross-file question drops from ~14,000 tokens to a couple hundred after running one `graphify` command, because the AI answers from real extracted relationships instead of re-reading everything from scratch.

**Watch this if:** you use Claude Code or Cursor on a real, multi-file project and keep hitting slow, expensive, half-wrong answers because the AI has no persistent map of your repo.

## Key Takeaways
- Coding AIs normally see a project as an unconnected pile of files and relearn it from scratch on every question — Graphify instead runs once (`graphify`) to generate a persistent graph plus a written markdown report the AI can reference going forward.
- In the demo, the same "what connects to the API layer?" question cost ~14,000 tokens before running Graphify and only a couple hundred tokens after, because the AI answers from generated relationships instead of reprocessing raw files.
- Under the hood: tree-sitter parses code structure, an LLM extracts meaning from it, and everything gets clustered into a graph — and it isn't code-only, it also reads PDFs, diagrams, audio, and video, all processed locally with nothing leaving the machine.
- Unlike RAG-based tools that just retrieve "similar" text chunks, Graphify builds explicit relationships (this function calls that one, this module depends on that one, this idea came from this document) and labels each one by confidence: extracted, inferred, or ambiguous.
- It's incremental — after the first run it's cached and only updates what's changed, so context persists across sessions instead of starting from zero each time.
- Pros: token costs compound down over time, and connecting code with docs/diagrams surfaces relationships useful for onboarding into messy, unfamiliar projects.
- Cons: the first run can be slow and token-expensive (especially with lots of documents), it's an early-stage tool with unknown long-term support, relationships aren't always perfect (hence the confidence labels), and it's overkill for small/simple repos.

## 🛠 Tools & Software
- [[topics/Graphify]] — turns a repo (plus docs, diagrams, audio, video) into a queryable, persistent knowledge graph and markdown report, cutting repeat-query token usage by up to ~70x
- [[topics/Claude Code]] — one of the coding agents used against real projects that Graphify is built to give persistent context to
- [[topics/Cursor]] — the other coding tool named as hitting the same token/context problem Graphify addresses
- [[topics/Tree-sitter]] — parses the codebase's structure as the first step in building Graphify's knowledge graph

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/RAG]] — the standard approach (similarity search over text chunks) that Graphify is explicitly contrasted against, since it builds real labeled relationships instead

## ✅ Action Items
- Run `graphify` (two Y's) once on a real, multi-file project to generate a persistent knowledge graph before relying on repeated raw-context AI queries.
- Check the confidence label (extracted/inferred/ambiguous) on any relationship Graphify surfaces before trusting it fully.
- Skip it for small or simple scripts — the setup cost isn't worth it below a certain project size.
- Budget for a slower, more token-expensive first run, especially on repos with a lot of accompanying documentation.

## 🔗 Related Videos
- [[videos/OpenCode Graphify Stop Wasting Tokens in Opencode, Every Developer Use this]] — shared: Claude Code, Graphify, Tree-sitter
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, Cursor
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude Code, RAG
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, RAG
- [[videos/Claude Code 'Interview' Mode in 6 Minutes]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Drawbridge Builds Websites By Sight (NEW Plugin)]] — shared: Claude Code, Cursor
- [[videos/Claude Code + Paperclip Just Destroyed OpenClaw]] — shared: Claude Code, Cursor
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor

## Timeline
- `0:00` — Why AI coding tools break on real projects: the token problem
- `0:40` — The hidden cost of AI coding: tokens, context, and hallucinations
- `1:11` — Live demo: turning a small repo into a knowledge graph with one command
- `2:17` — What Graphify actually is: a persistent map instead of raw files
- `2:43` — How it works: tree-sitter for structure, an LLM for meaning, graph clustering
- `3:25` — Graphify vs. RAG: why similarity search fails for code relationships
- `3:40` — Pros: compounding token savings, multi-modal support, better reasoning
- `4:00` — Cons: costly first run, early-stage maturity, accuracy limits
- `4:30` — Is Graphify worth it for developers?
- `4:55` — Final thoughts

## Transcript
<details>
<summary>Full transcript</summary>

If you're using Claude Code or Cursor on a real project, you'd think the hard part is writing code. It's not — the hard part is understanding your own repo. Ask one question and your AI burns through tokens just to figure out what's going on. It's slow, expensive, and half the time still wrong. What if instead of sending your whole project every time, you gave the AI a map of it? That's what Graphify does, and it can cut token usage by over 70%.

Right now, an AI sees a project as just a pile of files — no real connections, no structure, no memory. Every question means relearning everything from scratch, which is why answers feel close but not quite right. This is the "raw folder problem" that's been pointed out before, and Graphify showed up right after that observation, as more of a memory layer.

Demo: a small repo with code, docs, and a diagram. Normally you'd have to explain all of this to the AI every time. Instead, run one command, `graphify`. After it finishes, this isn't just files anymore — it's an actual graph. Everything is connected, and you can click through and dissect what's linked together within the generated HTML file. Instead of asking the AI to read everything again, you can ask "what connects to the API layer?" and it answers using relationships from the generated markdown file — not guesses, relationships. Before this, the same question cost around 14,000 tokens; after running Graphify once, the same question costs maybe a couple hundred. Same question, completely different cost, all because of the generated map.

So what is this actually doing? Graphify is basically like Google Maps for your codebase — instead of raw text, you get nodes and connections. Under it all, it uses tree-sitter to understand structure, then an LLM to extract meaning, then groups everything into clusters. It's not just code either — it reads PDFs, diagrams, even audio and video, all locally, nothing leaves the machine. What you get out: a visual graph, a written report, and an explorable knowledge base. The visual graph alone is huge for seeing how things connect.

This changes how AI coding usually works. Most tools use RAG — finding similar chunks of text. Graphify doesn't do that; it builds real relationships: this function calls that one, this module depends on that one, this idea came from this document — and it tells you how confident it is in each relationship, rather than just "this looks related." The biggest difference is that it remembers, since it generated that markdown file to look back on — you're not starting from zero every time. It updates only what's changed, so your AI finally has context that sticks.

Good and bad: the efficiency compounds — every question gets cheaper, and because it connects code, docs, and diagrams, you start finding relationships you didn't know existed, which is huge for onboarding into messy projects. The drawbacks: the first run can be slow and cost tokens, especially with a lot of documents — after that it's cached, but that first hit is real. It's also early-stage, so long-term support is unknown. Small note: it's spelled "Graphify" with two Y's — check your spelling. The relationships aren't always perfect, but they're labeled clearly as extracted, inferred, or ambiguous, so you know what to trust. And if your repo is tiny, this is overkill.

Is it worth it? If you're using AI on anything real, yes. Your biggest problem isn't running the code, it's understanding it across files, across time, across context — and that's exactly what this fixes. The token savings alone make it worth trying, but the bigger win is that your AI stops guessing and starts reasoning. If you're working solo, doing research, or managing big systems, this is a serious upgrade. If you're just working on smaller scripts, it's probably overkill and you don't need it. But for most people, this is going to be an awesome tool to try.

</details>
