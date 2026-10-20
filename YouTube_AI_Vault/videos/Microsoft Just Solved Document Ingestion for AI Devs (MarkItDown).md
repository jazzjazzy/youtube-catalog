---
title: "Microsoft Just Solved Document Ingestion for AI Devs (MarkItDown)"
video_id: 9ZaiZzp4XcY
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-22
processed: 2026-07-05
duration: "6:17"
url: https://www.youtube.com/watch?v=9ZaiZzp4XcY
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [document-ingestion, rag-pipeline]
tools: [MarkItDown, Python, OpenAI, Claude Desktop, Pandoc, Unstructured, Docling]
llms: [GPT-4o, Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Microsoft Just Solved Document Ingestion for AI Devs (MarkItDown)

![thumbnail](https://i.ytimg.com/vi_webp/9ZaiZzp4XcY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=9ZaiZzp4XcY) | 📅 Uploaded [[uploaded/2026-04-22]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> MarkItDown is Microsoft Research's open-source, MIT-licensed Python tool (110,000+ GitHub stars) that converts messy Word docs, PDFs, Excel sheets, images, and audio into clean, structured, token-efficient Markdown in one command or one line of code — fixing the actual root cause of bad RAG answers, which is usually messy document ingestion, not a bad model. The video runs a live PDF-to-Markdown conversion and a chart-image-to-Markdown conversion, then compares MarkItDown against Pandoc, Unstructured, and Docling.

**Watch this if:** your RAG pipeline or agent is giving bad answers and you suspect the problem is messy document ingestion rather than the model itself.

## Key Takeaways
- Stacking separate libraries for PDFs, Excel, Word, etc. tends to break: tables lose structure, headings disappear, token usage balloons, and RAG pipelines end up feeding the LLM garbage input.
- MarkItDown fixes this with one command (`markitdown doc.pdf output.md`) or a few lines of Python, producing clean Markdown with intact headings and table structure.
- It supports far more than PDFs — Word, PowerPoint, Excel, PDF, audio, images, and links — and can even convert a PNG chart into a Markdown summary of its data by piping the image through an LLM.
- It now ships an MCP server, so it can be plugged directly into tools like Claude Desktop or a custom agent instead of being called only as a CLI/library.
- Compared to Pandoc: Pandoc is built for humans (publishing, formatting, LaTeX) while MarkItDown is built for machines (LLMs, pipelines, automation) — different goals despite surface similarity.
- Compared to Unstructured and Docling: those use heavier ML models, need more setup, and handle complex documents better, while MarkItDown trades some extraction accuracy for speed, simplicity, and "good enough" results on most files.
- Honest limitation: complex PDFs with dense tables or unusual layouts still break MarkItDown — for messy scanned documents handled daily, Unstructured or Docling are the better choice; image descriptions also require plugging in an LLM.

## 🛠 Tools & Software
- [[topics/MarkItDown]] — Microsoft's open-source document-to-Markdown converter, demoed converting a PDF and a PNG chart via CLI and Python
- [[topics/Python]] — used to write the MarkItDown client code, including the OpenAI-backed image-to-Markdown conversion
- [[topics/OpenAI]] — the API client instantiated in the Python demo to power MarkItDown's image/chart description step
- [[topics/Claude Desktop]] — mentioned as one of the tools MarkItDown's new MCP server can plug directly into
- [[topics/Pandoc]] — compared against MarkItDown as the human-facing publishing/formatting alternative, solving a different problem
- [[topics/Unstructured]] — compared against MarkItDown as a heavier, ML-based ingestion tool better suited to complex documents
- [[topics/Docling]] — compared alongside Unstructured as a more accurate but heavier and slower-to-set-up ingestion alternative

## 🤖 LLMs Mentioned
- [[topics/GPT-4o]] — referenced as one of the LLMs developers feed MarkItDown's cleaned output into for RAG pipelines
- [[topics/Claude]] — referenced via Claude Desktop as a client that can connect to MarkItDown's MCP server

## 📡 Protocols & Standards
- [[topics/MCP]] — MarkItDown now ships an MCP server, letting it be plugged directly into Claude Desktop or a custom agent instead of only being called as a library

## ✅ Action Items
- Swap a fragile multi-library document ingestion pipeline for a single `markitdown` call and compare table/heading structure before and after.
- Try MarkItDown's MCP server with Claude Desktop or your own agent to convert documents inline without leaving the tool.
- If you deal with dense tables or scanned documents daily, evaluate Unstructured or Docling instead of forcing MarkItDown to handle them.

## 🔗 Related Videos
- [[videos/Claude Code Loop The Feature Everyone Misunderstands]] — shared: Claude, Claude Desktop, MCP
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude, Claude Desktop, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, MCP
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, MCP
- [[videos/Anthropic Just Shipped 10 Wall Street AI Agents, GitHub 1]] — shared: Claude, MCP

## Timeline
- `0:00` — Intro: RAG pipelines fail because of messy ingestion, not bad models
- `0:33` — The real problem: stacking separate libraries for PDFs, Excel, images
- `1:40` — Live demo: converting a PDF to clean Markdown in one command
- `2:34` — Python demo: converting a PNG chart into a Markdown summary
- `3:06` — What MarkItDown actually is: Microsoft Research, MIT license, supported formats
- `3:32` — MarkItDown's MCP server and Claude Desktop integration
- `4:26` — MarkItDown vs. Pandoc: publishing vs. LLM workflows
- `4:53` — MarkItDown vs. Unstructured and Docling: speed vs. accuracy
- `5:22` — Cons: complex PDF and dense table limitations
- `5:40` — Verdict: when to use MarkItDown vs. when to skip it

## Transcript
<details>
<summary>Full transcript</summary>

We spend way more time processing documents than actually building our AI apps. We connect multiple libraries, finally get a PDF into the pipeline, and the LLM still gives bad answers — not because the model is bad, because the input is. This is MarkItDown, a tool by Microsoft that's blown up with over 110,000 stars on GitHub, and it fixes the whole pipeline in basically one line of code.

Every AI project starts the same: files everywhere, Word docs, slides, spreadsheets, PDFs, screenshots, maybe audio files. Then comes stacking tools — one for PDFs, one for Excel, one for Word, all linked together to build the pipeline. At first it feels fine, but then things start to break: tables lose structure, headings disappear, token usage blows up, the RAG pipeline is pulling garbage, and the agent gives bad answers. You end up debugging ingestion instead of shipping — wasting hours every week. Instead of fixing your model, you need to fix your input.

Running through it: it's all Python, pretty simple. Pip install it in a virtual environment, take a PDF (doc.pdf), and run `markitdown doc.pdf output.md` in the terminal — that's it, it makes the file automatically. Opening that file, headings are clean, tables actually look like tables, structure is preserved. Writing some Python code for it: with the imports and using OpenAI, make a client and a MarkItDown object, pass in an API key and the model to run. Running the code generates clean output in the terminal. Better yet, you can feed it a PNG image — here, a chart from Nvidia — and let MarkItDown convert the chart into Markdown using the same convert function, this time given the image. The result is a summary of what the chart is and what could be extracted and used for RAG. This lets you extract what you need faster, right in your code, without jumping between tabs.

So what is MarkItDown really? An open-source Python tool from Microsoft Research, MIT licensed, built specifically for LLM workflows. Its job is to take messy files and turn them into clean Markdown so models can actually understand them. It supports Word, PowerPoint, Excel, PDF, audio, images, and links — really anything. It even has an MCP server now, so you can plug it directly into tools like Claude Desktop or your own agent, plus plugins. Instead of building ingestion pipelines, you're now basically calling one tool. Devs weren't struggling with models, they were struggling with inputs — the expectation was "just use better models," but the reality is better inputs equal better outputs. Now instead of writing scripts that break, people use one tool for everything: RAG pipelines, agents, fine-tuning datasets, knowledge bases, document analysis. The key detail most people miss is it produces structured, token-efficient Markdown, so there's less noise going in and better answers coming out. But that doesn't mean it's perfect.

Comparing it to what you're probably already using: Pandoc would seem like the obvious rival, but it's solving a different problem — Pandoc is for humans (publishing, formatting, LaTeX), MarkItDown is for machines (LLMs, pipelines, automation). Same idea, different goal. Then there's Unstructured or Docling — these use ML models, take more setup, and are better for really complex documents. MarkItDown takes the opposite approach: less setup, super easy, faster results, good enough for most files. The real tradeoff is perfect extraction versus something that works fast and reliably — for most people, speed wins. Of course there are downsides: complex PDFs still break it, especially dense tables or weird layouts. If you deal with messy scanned documents every day, tools like Docling or Unstructured do way better. If you want image descriptions, you'll need to plug in an LLM. It's not perfect, but it's a pretty cool tool solving a real problem.

Is it worth using? For most people, yeah, absolutely. If you're building AI apps right now, this is probably what your ingestion layer should look like. Try MarkItDown if you want clean input for RAG or agents, deal with mixed file types, and don't want to maintain a bunch of fragile scripts that could break. Skip it or combine it with other tools if you're working with extremely complex PDFs every single day.

</details>
