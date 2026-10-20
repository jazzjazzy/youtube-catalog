---
title: "OpenCode + Graphify: Stop Wasting Tokens in Opencode, Every Developer Use this"
video_id: -L_faOE-H5g
channel: "[[channels/AI Stack Engineer]]"
uploaded: 2026-04-21
processed: 2026-07-05
duration: "10:11"
url: https://www.youtube.com/watch?v=-L_faOE-H5g
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [token-efficient-codebase-context, knowledge-graph-indexing]
tools: [Graphify, OpenCode, Python, Tree-sitter, Whisper, Git, Claude Code]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# OpenCode + Graphify: Stop Wasting Tokens in Opencode, Every Developer Use this

![thumbnail](https://i.ytimg.com/vi/-L_faOE-H5g/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=-L_faOE-H5g) | 📅 Uploaded [[uploaded/2026-04-21]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Every new OpenCode session re-reads a codebase from scratch, burning tokens rebuilding the same mental model. Graphify fixes this by parsing a project once into a knowledge graph — using Tree-sitter for code (free, local), Faster Whisper for audio/video (free, local), and paid sub-agent calls only for markdown/PDF/docs — then wires into OpenCode via a plugin and an agents.md entry so every future session reads the cached graph instead of re-scanning files.

**Watch this if:** your OpenCode (or Claude Code) sessions keep re-reading the same README, config, and source files at the start of every conversation and you want that context cached instead of rebuilt each time.

## Key Takeaways
- Without Graphify, a fresh OpenCode session on a simple question (e.g. "what does this payment module do?") reads the README, a config file, and source files one by one from zero — and starts over completely the next day with no memory of what it already read.
- Graphify runs three passes: pass one uses Tree-sitter to statically parse ~23 languages (Python, JS, TS, Go, Rust, Java, C/C++, Ruby, Swift, Kotlin, etc.) at zero API cost; pass two transcribes audio/video locally via Faster Whisper at zero API cost; pass three fires parallel sub-agents through your model provider to extract concepts from markdown/PDFs/docs — the only pass that costs money, and it's cached so re-runs only reprocess changed files.
- Setup for OpenCode: `pip install graphify` (needs Python 3.10+), `graphify install --platform opencode` to copy the skill file, then `graphify opencode install`, which writes a section into `agents.md` and installs a plugin hook that injects a "check the knowledge graph first" reminder before every bash tool call — no manual per-session prompting needed.
- Building the graph itself is `/graphify .` inside OpenCode (or a specific subfolder), optionally excluding paths via a `.graphifyignore` file; a medium project (a few hundred files) takes roughly 5-10 minutes and outputs a `graphify-out` folder with `graph.html`, `graphreport.md`, `graph.json`, and a cache.
- The `graph.html` visualization shows concepts/functions/classes/docs as nodes, with "god nodes" marking the most-connected, most-central pieces of the codebase; nodes are clickable and filterable by community (e.g. isolate just the auth-related subgraph).
- Keeping the graph current matters: run `graphify update` manually, or `graphify hook install` to wire git hooks so the graph rebuilds automatically on every commit and branch switch.
- Honest limitation: for small projects (under ~10 files) the graph isn't worth building — the value is structural/compounding on codebases with lots of mixed content (docs, PDFs, meeting recordings), not raw token savings on tiny repos.

## 🛠 Tools & Software
- [[topics/Graphify]] — the knowledge-graph tool under demo: three-pass indexing (code, audio/video, docs), OpenCode plugin integration, and the graph.html visualization walkthrough
- [[topics/OpenCode]] — the agent harness Graphify is installed into via a plugin and an agents.md entry so every session reads the cached graph automatically
- [[topics/Python]] — Graphify is installed via pip and requires Python 3.10+
- [[topics/Tree-sitter]] — powers Graphify's first, free, fully local parsing pass across ~23 programming languages
- [[topics/Whisper]] — Faster Whisper transcribes audio/video content in the corpus locally, at no API cost, as Graphify's second pass
- [[topics/Git]] — `graphify hook install` wires into git hooks so the graph automatically rebuilds on every commit and branch switch
- [[topics/Claude Code]] — noted as Graphify's default install target; the video explicitly switches the install flag to target OpenCode instead

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Run `pip install graphify` and `graphify install --platform opencode` on a real project with mixed content (code + docs + PDFs) rather than a tiny repo.
- Set up `graphify hook install` immediately so the graph rebuilds on every commit instead of going stale.
- Use `.graphifyignore` to exclude `node_modules`/`vendor`/`dist` before running the first full graph build to save time and cost.
- Try the terminal-only `graphify query`, `graphify path`, and `graphify explain` commands for quick answers without opening a full OpenCode session.

## 🔗 Related Videos
- [[videos/This Tool Fixes AI Coding at Scale with 70x Fewer Tokens (Graphify)]] — shared: Claude Code, Graphify, Tree-sitter
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Git
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, OpenCode
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Python
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, Git
- [[videos/Anthropic Released A New Way To Vibe Code]] — shared: Claude Code, Git
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, Git
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Claude Code, OpenCode

## Timeline
- `0:00` — The problem: OpenCode re-reads a codebase from scratch every new session
- `1:03` — Graphify's premise: build the "internal wiki" once, every session gets it automatically
- `3:44` — Graphify's three-pass architecture: code (free), audio/video (free), docs (paid, cached)
- `5:05` — Install: checking Python 3.10+, `pip install graphify`
- `5:20` — `graphify install --platform opencode` and `graphify opencode install`
- `6:04` — How the OpenCode plugin hook injects the "read the graph first" reminder
- `7:04` — Building the graph: `/graphify .`, subfolders, `.graphifyignore`
- `7:44` — Exploring `graph.html`: nodes, god nodes, community filtering
- `8:41` — Keeping the graph in sync: manual update vs. git hook install
- `9:08` — When to skip Graphify, and terminal-only query/path/explain commands

## Transcript
<details>
<summary>Full transcript</summary>

Let's say you're working on a project in OpenCode. You've just opened a new session and want to understand the codebase before making any changes, so you ask a simple question: what does this payment module do, give me a quick summary of each file. Pretty basic question — now watch what happens. Before it answers anything, it opens the readme to figure out what kind of project this even is, then reads a config file, then starts going through source files one by one, building a mental picture from scratch. Reading file after file, and every single read burns tokens. The answer you eventually get is only as good as whatever OpenCode managed to pick up along the way. Here's the part that actually hurts: if you close that session and come back tomorrow, OpenCode starts from zero all over again — no memory of what it read, no idea how your files connect, no clue which modules are important. Every new session, same tokens burned, same files reread, same grepping around in the dark.

There's a tool called Graphify that fixes this. It reads your project once, builds a knowledge graph of how everything connects, and then OpenCode just reads that graph at the start of every session instead of scanning files over and over. This tool actually came out of something Andrej Karpathy mentioned publicly — one of the co-founders of OpenAI, and a lot of developers follow him for his takes on AI and tooling. The problem he described is exactly what Graphify solves: a pile of mixed content you can never fully reconstruct when you need it.

The idea is simple: think of a regular OpenCode session as a contractor who walks in on day one with no context — they have to skim everything before answering even a basic architecture question. Graphify is like handing them the internal wiki before they start; they already know which files are the core of the system, which modules talk to which, and where the important decisions live. You build that wiki once, and every future session gets it automatically.

This doesn't only work for code — you can point it at a folder of research papers, PDFs, meeting notes, screenshots, even video files, and it handles all of that in the same graph. But sticking to a code project for the demo: under the hood, Graphify runs in three passes, and it's worth understanding them because it tells you where your money actually goes. The first pass parses your code using tree-sitter, supporting around 23 languages including Python, JavaScript, TypeScript, Go, Rust, Java, C, C++, Ruby, Swift, and Kotlin. This pass is fully local — it reads every class, function, import, and call, and costs nothing in API tokens because no model is called, it's just static analysis. The second pass handles audio and video: if you have meeting recordings, tutorial videos, or YouTube links in your corpus, Graphify transcribes them locally using Faster Whisper — again no API tokens, no network calls, everything stays on your machine. The third pass is the one that actually costs money: for markdown files, PDFs, images, readmes, and docs, it fires off parallel sub-agents through your model provider to pull out concepts and relationships. This is the only pass that hits the API, and it only runs once per corpus — after that the result is cached, so when you change files later and run an update, it only reprocesses what actually changed.

Install: check your Python version first, Graphify needs 3.10 or newer. Open your project folder in a terminal — the install is two commands. First, `pip install graphify` (package name ends in double y, graphify with a y, not graphify). If you're on WSL or Linux, you might want a virtual environment since newer Python setups block global pip installs. After the package installs, run `graphify install` — by default this sets up the skill for Claude Code. Since we want OpenCode specifically, run `graphify install --platform opencode`, which copies the skill file into the right place for OpenCode to pick it up.

The next step actually makes Graphify always-on: run `graphify opencode install`. This does two things under the hood: it writes a section into agents.md in your project root telling the assistant to check the knowledge graph before doing anything else, and it installs a plugin file at `.opencode/plugins/graphify.js`, which hooks into OpenCode's tool-execute-before plugin system. That plugin fires right before any bash tool call and injects a reminder into the output saying the knowledge graph exists, read the graph report first before grepping around. It registers itself in opencode.json automatically. Without the plugin, you'd have to remember to tell OpenCode about the graph every session; with it installed, every new conversation just has the graph context available without typing anything.

Now you're ready to build the graph. Open OpenCode in your project and type `/graphify .` — the dot means current directory; you can also point it at a specific folder like `/graphify ./src` if you only want to graph a subfolder. If your project has a ton of files, add a `.graphifyignore` file at the root, same syntax as `.gitignore` — node_modules, vendor, dist, whatever you want skipped. The run takes a while depending on corpus size; for a medium project with a few hundred files, expect 5 to 10 minutes, with progress shown as it goes. When done, you get a `graphify-out` folder with four things: `graph.html` you can open in your browser, `graphreport.md` (the summary), `graph.json` (the full machine-readable graph), and a cache folder. Opening graph.html shows something like a star map — colored dots with lines between them, each dot a concept, function, class, document, or image from your corpus. The bigger dots are "god nodes," the pieces everything else connects to — if 40 files touch a specific module, that module becomes a big node. On the side panel you can click any node to see which files it lives in, and filter by community — e.g. only show the authentication stuff.

Keeping the graph in sync matters too, since an unrefreshed graph goes stale fast. Two options: run `graphify update` manually whenever you feel like it (only reprocesses changed files), or run `graphify hook install` to wire up git hooks so the graph rebuilds automatically on every commit and branch switch — recommended, since you'll forget otherwise. One honest callout: if your project is small, under 10 files, don't bother — the graph's value is structural for large, mixed-content projects (a docs folder full of markdown, a research vault, PDFs and meeting recordings), not token savings on tiny codebases that OpenCode can already handle unaided. You can also query the graph directly from the terminal without opening OpenCode: `graphify query "<question>"` traverses the graph and answers with source file references, `graphify path` finds the shortest connection between two concepts, and `graphify explain` gives a plain-language summary of any node — useful for a quick answer without spinning up a full session.

</details>
