---
title: "The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing"
video_id: EH8Mdx948Kw
channel: "[[channels/Dylan Davis]]"
uploaded: 2026-01-31
processed: 2026-07-06
duration: "10:54"
url: https://www.youtube.com/watch?v=EH8Mdx948Kw
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [document-hallucination-prevention]
tools: [NotebookLM]
llms: [ChatGPT, GPT-5, Claude, Claude Opus, Gemini]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing

![thumbnail](https://i.ytimg.com/vi_webp/EH8Mdx948Kw/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=EH8Mdx948Kw) | 📅 Uploaded [[uploaded/2026-01-31]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> AI chatbots would rather confidently guess than admit they can't find something in an uploaded document, causing frequent hallucinations in document-extraction workflows. This video shows a right-model choice plus a three-part grounding prompt (only use the document, allow "not found," require citations), then three escalating verification methods (self-check, cross-model check, NotebookLM) to catch what still slips through.

**Watch this if:** you extract data from invoices, contracts, or policies with ChatGPT, Claude, or Gemini and need to trust the answers instead of fact-checking everything by hand.

## Key Takeaways
- AI hallucinates on document extraction because models are trained to be "helpful" — when information isn't found, they guess confidently rather than say "I don't know."
- Step 1: pick the highest-reasoning model available (at time of recording: GPT-5.2 with extended reasoning, Claude Opus 4.5 with extended reasoning, or Gemini 3 Pro) — this alone reduces hallucination rate.
- Step 2, grounding prompt part 1: "Base your answer only on the uploaded documents and nothing else" — stops the model from filling gaps with internet/training knowledge.
- Step 2, grounding prompt part 2: "If information isn't found, say not found in the documents, don't guess" — explicitly permits uncertainty, which a leading AI research lab cites as its #1 hallucination-reduction recommendation.
- Step 2, grounding prompt part 3: require a citation (document name, page/section, exact quote) for every claim — this both reduces hallucination rate and makes claims fast to human-verify.
- Bonus prompts: a "middle ground / unverified" flag for claims the model isn't fully confident about, and a strict "only respond if 100% confident" mode for high-stakes work (contracts, legal, financial) — with an explicit precision-vs-recall trade-off.
- Three verification tiers, increasing in rigor: (1) self-check — ask the same AI to rescan the document and re-justify each claim or retract it; (2) cross-model check — feed the output and source doc to a *different* model and ask it to flag unsupported claims; (3) NotebookLM — purpose-built for grounded search, checks claim-by-claim and returns clickable source links.

## 🛠 Tools & Software
- [[topics/NotebookLM]] — used as the third and most rigorous verification method, checking each claim against the source document and returning clickable citations; note it's powered by Gemini 3, so the presenter recommends using ChatGPT or Claude as the first-pass model when pairing with it.

## 🤖 LLMs Mentioned
- [[topics/ChatGPT]] — recommended extraction model for document work when using OpenAI's product; also demoed hallucinating a confident but fabricated answer.
- [[topics/GPT-5]] — specific high-reasoning model recommended (GPT-5.2 with extended reasoning) for document extraction to minimize hallucinations.
- [[topics/Claude]] — recommended as one of the three chatbot families to apply the grounding prompts to.
- [[topics/Claude Opus]] — specific high-reasoning model recommended (Opus 4.5 with extended reasoning) for document extraction.
- [[topics/Gemini]] — recommended model family (Gemini 3 Pro) for document extraction; also powers NotebookLM under the hood.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Switch to the highest-reasoning-mode model your provider offers before doing any document extraction task.
- Add the three grounding lines to your extraction prompt: document-only scope, permission to say "not found," and mandatory citations with quotes.
- For high-stakes documents, add the "only respond if 100% confident" clause and accept the precision/recall trade-off deliberately.
- Add a self-check pass that asks the model to rescan the document and re-verify or retract each claim.
- For anything important, cross-check with a second, different model, or run the source + analysis through NotebookLM for claim-by-claim verification with clickable citations.

## 🔗 Related Videos
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: ChatGPT, Claude, GPT-5, Gemini
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, GPT-5, Gemini
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, Claude Opus
- [[videos/Claude Code Skills Just Got Even Better]] — shared: ChatGPT, Claude, Claude Opus
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Claude, Gemini
- [[videos/How I Watch ANY Video with AI in Seconds]] — shared: ChatGPT, Claude, Gemini
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: ChatGPT, Claude, Gemini
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Claude Opus, Gemini

## Timeline
- `0:00` — Intro: ChatGPT confidently fabricates an answer about an uploaded document.
- `0:25` — The problem: AI would rather guess than say "I don't know," especially in document extraction (invoices, insurance policies, etc.).
- `1:43` — Fix #1 — choosing the right model: use the highest-reasoning option (GPT-5.2, Claude Opus 4.5, or Gemini 3 Pro) with extended reasoning enabled.
- `3:01` — Grounding prompt part 1: restrict answers to the uploaded document only.
- `3:46` — Grounding prompt part 2: explicitly allow "not found, don't guess."
- `4:30` — Grounding prompt part 3: require citations (document, page/section, quote) for every claim.
- `5:10` — Bonus prompts: "unverified" middle-ground flag, and a strict 100%-confidence mode for high-stakes documents.
- `6:34` — Verification method 1: self-check — have the AI rescan and re-justify or retract each claim.
- `7:40` — Verification method 2: cross-model check — a different AI reviews the first AI's analysis against the source document.
- `8:40` — Verification method 3: NotebookLM checks claims against sources and returns clickable citation links.
- `9:18` — Recap of the three-step process: right model, grounding prompts, verification.
- `10:18` — Outro and teaser for a related video on forcing brutal honesty from AI feedback.

## Transcript
<details>
<summary>Full transcript</summary>

I asked ChatGPT about a document that I uploaded and it gave me a confident answer. Sadly, that answer was completely made up. This happens way more than you think. It's not because AI is bad at reading documents — it's because AI would rather guess than say "I don't know." This video covers a simple three-rule prompt that fixes this, plus three ways to verify anything AI tells you.

Extracting data from documents is one of the lowest-hanging-fruit AI use cases in business, and it's also where hallucination shows up constantly — extracting invoice line items, checking an insurance policy for coverage, and endless similar tasks. AI fails here because it's trained to be a helpful assistant: if it can't find something in a document, it will guess, and guess confidently, to seem satisfying. When a model is trained, all its knowledge gets baked in; during extraction, if it can't see or skips a piece of information, it starts hallucinating to fill the gap.

Tactic one — the easiest — is choosing the right model. Most people accept whatever model is defaulted in ChatGPT, Gemini, or Claude, but for document processing you want the highest-reasoning model available to minimize hallucinations. As of recording: GPT-5.2 with extended reasoning for ChatGPT, Claude Opus 4.5 with extended reasoning, and Gemini 3 Pro for Gemini — names will likely change over time, but the principle (choose the top reasoning tier) stays the same.

After choosing the model, add grounding prompts. Grounding means the AI bases its answer only on the provided document, not the internet or its training data — the first prompt is literally "base your answer only on the uploaded documents and nothing else." The second prompt gives the AI explicit permission to say it doesn't know: "if information isn't found, say not found in the documents, don't guess." One leading AI research lab states this is their #1 recommendation for reducing hallucinations in document extraction. The third prompt requires citations for every claim — document name, page/section, and a relevant quote — which both reduces hallucination rate and makes the claim fast for a human to validate.

Two bonuses: a "middle ground" prompt for claims the AI thinks are valid but isn't fully sure about — "if you find something related but aren't fully confident it answers the question, mark it as unverified" — which helps you prioritize what to check first. And for high-stakes work like contract review, financial analysis, or legal documentation, a strict prompt: "only respond with information if you're 100% confident it came from the file" — trading off less data for higher confidence in what you do get.

Next comes verification, and AI itself can help. Method one, the lowest intensity: self-check — ask the same AI, in the same thread, to rescan the document, give the exact quote supporting each claim, and retract any claim it can't find a quote for; forcing a rescan makes it actually re-check rather than just rubber-stamp its prior output. Method two, more intense: a cross-model check, where a *different* AI reviews the first AI's output against the source document — e.g., ChatGPT extracts, then Claude Opus 4.5 or Gemini 3 Pro reviews the analysis and flags unsupported claims. Method three, the final and most rigorous: NotebookLM, purpose-built for grounded search and citation matching — feed it the source document and the prior AI's analysis, ask which claims aren't supported by the sources, and it checks claim by claim while returning clickable source links (note: NotebookLM itself runs on Gemini 3, so pair it with ChatGPT or Claude as the first-pass model for a genuinely independent check).

Recap: choose the right (highest-reasoning) model, ground it with the three prompts (document-only, permission to say unsure, mandatory citations), then verify — first with AI (self-check, then cross-model), then as a human.

</details>
