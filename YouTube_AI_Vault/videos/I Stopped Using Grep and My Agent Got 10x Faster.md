---
title: "I Stopped Using Grep and My Agent Got 10x Faster"
video_id: gPeWb4_DMok
channel: "[[channels/Better Stack]]"
uploaded: 2026-04-25
processed: 2026-07-05
duration: "8:06"
url: https://www.youtube.com/watch?v=gPeWb4_DMok
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [codebase-search, semantic-code-search]
tools: [Claude Context, Zilliz Cloud, Milvus, Tree-sitter, OpenCode, OpenAI]
llms: [GLM, Claude Opus]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# I Stopped Using Grep and My Agent Got 10x Faster

![thumbnail](https://i.ytimg.com/vi_webp/gPeWb4_DMok/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=gPeWb4_DMok) | 📅 Uploaded [[uploaded/2026-04-25]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Claude Context is an MCP server by Zilliz that indexes an entire codebase into a Milvus vector database using Tree-sitter AST parsing, Merkle DAG change hashing, and hybrid semantic + BM25 search, claiming up to 40% context reduction over raw grep/glob. The video sets it up against VS Code's 1.5M-line codebase and a smaller 23K-line codebase, comparing it head-to-head with plain grep/glob search in OpenCode to see whether the setup effort and cloud/embedding costs are worth it.

**Watch this if:** your coding agent burns huge chunks of context grepping around large or unfamiliar codebases and you want to know if a vector-indexed MCP search tool actually helps.

## Key Takeaways
- Claude Context (by Zilliz, the team behind Milvus) connects to any MCP-compatible agent, not just Claude Code, and does three things: Tree-sitter AST parsing into function/class chunks across 9+ languages, Merkle DAG file hashing so only changed files get re-indexed, and dual vector + BM25 search at query time.
- It requires a Zilliz Cloud account and an OpenAI API key for embeddings even when the agent itself is running a different model — the free Zilliz tier caused timeouts, so a paid serverless cluster was needed.
- Indexing a 23K-line codebase cost about 1 cent in OpenAI embeddings and took under a minute; indexing VS Code's ~1.5M-line codebase produced 223,000+ entries, took about 50 minutes, and cost roughly $1.06.
- Head-to-head against grep/glob search in OpenCode (running GLM-5 Turbo) on the VS Code repo: results were mixed on raw speed — sometimes grep/glob was faster — but Claude Context consistently returned more detailed, better-organized answers (e.g. layered architecture, specific file/line references) for the same or fewer tokens on complex prompts.
- On a broad "explain how this project works" prompt, Claude Context answered in 49 seconds with rich architectural detail including the Electron process breakdown, while plain grep/glob search took about 5 minutes and produced less detail even with sub-agents doing the digging.
- Verdict: Claude Context shines most on average-size codebases (20-30K lines) where indexing is fast and the answer-quality gap is obvious; on very large codebases the long indexing time makes the tradeoff less clear-cut.
- The presenter calls it "a great sales tool for Zilliz" (introduced them to a vector-DB vendor they'd never used) but says they'll keep using it for regularly exploring open-source codebases since the embedding/serverless costs stay low for average-size repos.

## 🛠 Tools & Software
- [[topics/Claude Context]] — the MCP server under test: indexes codebases into a vector DB and is benchmarked against plain grep/glob search
- [[topics/Zilliz Cloud]] — the hosted cluster Claude Context indexes into; free tier timed out, so a paid serverless cluster was used instead
- [[topics/Milvus]] — the vector database engine underlying Zilliz Cloud, made by the same team that built Claude Context
- [[topics/Tree-sitter]] — parses the codebase into AST-based function/class chunks across 9+ supported languages
- [[topics/OpenCode]] — the agent harness used to run both the Claude Context MCP server and the plain grep/glob comparison instance
- [[topics/OpenAI]] — provides the embeddings API that Claude Context calls during indexing, billed separately from whatever model the agent uses

## 🤖 LLMs Mentioned
- [[topics/GLM]] — GLM-5 Turbo is the model actually running inside OpenCode for the comparison, chosen to avoid burning Claude Pro weekly limits
- [[topics/Claude Opus]] — Opus 4.7 with high effort is mentioned as a smarter but slower/more expensive model that might extract more detail without Claude Context

## 📡 Protocols & Standards
- [[topics/MCP]] — Claude Context is delivered as an MCP server exposing index/search/clear/status tools, making it usable from any MCP-compatible agent

## ✅ Action Items
- Set up Claude Context's MCP server against a mid-size (20-30K line) codebase before trying it on something huge, since indexing time scales badly.
- Budget for both a Zilliz Cloud serverless cluster and OpenAI embedding costs — the free Zilliz tier isn't reliable enough.
- Compare answer detail, not just speed, when judging whether a vector-indexed search tool is worth it — token/time parity can hide a large quality gap.

## 🔗 Related Videos
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: GLM, MCP, OpenCode
- [[videos/How Hermes Agent Can Save You 85 (Or More) in BG Task Token Cost]] — shared: Claude Opus, GLM, MCP
- [[videos/How to Never Hit Your Claude Session Limit Again]] — shared: Claude Context, Claude Opus, MCP
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Opus, GLM, MCP
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Opus, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Opus, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Opus, MCP
- [[videos/9 NEW Claude Mods that can truly change how you work]] — shared: Claude Opus, MCP

## Timeline
- `0:00` — Intro: Claude Context indexes a codebase into a vector DB for 40% less context use
- `0:39` — What Claude Context is and who built it (Zilliz, makers of Milvus)
- `0:53` — The three techniques: Tree-sitter AST chunking, Merkle DAG hashing, hybrid vector+BM25 search
- `1:39` — Setup: testing against the VS Code codebase using OpenCode with GLM-5 Turbo
- `2:03` — Zilliz Cloud cluster setup and the free-tier timeout problem
- `2:25` — MCP server setup and the four exposed tools
- `2:40` — Indexing costs: 1 cent for 23K lines vs $1.06 for 1.5M lines (~50 min)
- `3:43` — First head-to-head search comparison: entry point lookup
- `4:24` — Second comparison: finding a specific function, token/time/detail differences
- `5:30` — Broad "explain the project" prompt comparison and Electron process follow-up
- `6:34` — Verdict: best fit is average-size codebases, not huge ones

## Transcript
<details>
<summary>Full transcript</summary>

So there's this MCP plugin called Claude Context that indexes your entire codebase into a vector database, meaning your coding agent can get the exact code it needs quickly without guessing using grep or glob and hoping it finds the right file. It even parses your code with ASTs and uses a hybrid search approach combining semantic vectors with keyword matching, which ends up using 40% less context. But it does need a Zilliz Cloud account and an OpenAI key for embeddings even if you use Claude Code. So is the extra effort and cost worth the token savings?

Claude Context is made by Zilliz, a company created by the founders of Milvus, a very performant vector database. It connects to your agent by MCP, so it can work with any agent harness, not just Claude Code. It does three pretty complex things to make your code easily findable. First, it uses Tree-sitter to parse through all of the code, creating chunks of functions and classes, supporting nine languages including TypeScript, Python, Rust, and Go. Then it uses a custom Merkle DAG to hash each file with JSON snapshots, meaning it only re-indexes files that have changed, not the whole codebase. And when you actually search, it does two searches at the same time: a vector search for semantic meaning and a BM25 index search for exact keyword matching. This results in up to 40% context reduction, which is a lot for large codebases.

Let's see it in action testing against the VS Code codebase, which has around 1.5 million lines of code. Inside the VS Code repo, using OpenCode with GLM-5 Turbo to avoid burning Claude Pro weekly limits, the MCP server is already configured in the OpenCode JSON file. You could run Milvus locally, but I used Zilliz Cloud — got an API key, created an AWS cluster, got the public endpoint. I tried the free cluster first but kept getting timeout issues, so I had to get a serverless one, which costs money but worked a lot better. Once the MCP server is set up (Node below 24, above or equal to 20), you get access to four MCP tools: index code, search code, clear index, and get index status.

First you have to index the codebase. Before hitting enter, a look at OpenAI embedding spend so far: just 1 cent, for testing a 23,000-line codebase. The cluster already has information from that indexed codebase. Now indexing the VS Code codebase takes a while and starts in the background — I don't recommend searching while it's running. After about 50 minutes, indexing is complete: over 223,000 loaded entries in the cluster. For reference, the 23,000-line codebase had about 1,000 lines of entries and took less than a minute to index. OpenAI usage went from 1 cent to $1.06 — a lot, but not something people will do regularly for 1.5 million lines of code.

Now, how fast is a search? One instance of OpenCode uses the Claude Context MCP server, another uses no MCP server — just regular grep and glob tools. Prompt: use Claude Context to find the entry point of when this project starts up. It uses the index tool, then the search tool, taking about 19 seconds to find main.ts. The plain-grep instance finds a response in 14 seconds — for this query, regular GLM is faster. New session, new prompt: what function opens a new untitled document. This one took 40 seconds and found the main function with a line number, using about 23K tokens. The other instance did it in 12 seconds using 18K tokens, but found a different file — Claude Context gave way more information, showing code and related files. Asking both to show the exact code: Claude Context responds in 23 seconds, the non-Claude-Context instance in 49 seconds, almost double, giving the same code Claude Context did.

A more broad prompt: look through the code and tell me how this project works. Claude Context finishes in 49 seconds using 41K tokens; the other instance finishes faster and uses fewer tokens, but its output has much less detail. Claude Context gives layered architecture and information about the Electron app and its processes; the other option gives some architectural info but far less detailed. A follow-up prompt asking for more detail on the main process in the Electron app took about 1 minute 47 seconds with Claude Context but returned huge detail — boot sequence, phase one service creation and initialization, phase two code application with references to specific files and line numbers like app.ts line 185. Without Claude Context, OpenCode is still going through files using multiple sub-agents — deceiving because you can't see exactly how many tokens each sub-agent uses — and after about 5 minutes it responds with information about the Electron process, but less than Claude Context provided, taking five times longer. Maybe a smarter model like Opus 4.7 with high effort would get more information, but it would still take a long time and use a lot of tokens. These are the kinds of differences — 5 minutes versus 1 minute — seen testing before recording with the 23K-line codebase.

In the end it's difficult to say who the clear winner is. Claude Context always provided more detail but wasn't always the fastest or most token-efficient, and for large codebases it took a very long time to index. However, for average-size codebases — 20 to 30,000 lines — indexing is really quick and the difference in result detail is very apparent. I'd much rather use Claude Context for average-size codebases than large ones. To be honest, this is more of a great sales tool for Zilliz — before this I'd never heard of them, and now they have a new paying customer. But even though setup and indexing large codebases took a while, as someone who regularly goes through open-source codebases and asks questions, this is a tool I'll be using a lot more — for an average-size codebase the serverless plan isn't too expensive since OpenAI embeddings don't cost much either.

</details>
