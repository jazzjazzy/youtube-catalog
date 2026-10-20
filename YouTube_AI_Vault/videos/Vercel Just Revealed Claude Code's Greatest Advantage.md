---
title: "Vercel Just Revealed Claude Code's Greatest Advantage"
video_id: gZr5VmsXmXQ
channel: "[[channels/AI LABS]]"
uploaded: 2026-01-22
processed: 2026-07-06
duration: "9:40"
url: https://www.youtube.com/watch?v=gZr5VmsXmXQ
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: intermediate
use_case: [cost-efficient-retrieval]
tools: [Claude Code, Vercel Sandbox]
llms: [Gemini]
protocols: [RAG]
transcript: true
tags: [youtube, ai-automation]
---

# Vercel Just Revealed Claude Code's Greatest Advantage

![thumbnail](https://i.ytimg.com/vi_webp/gZr5VmsXmXQ/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=gZr5VmsXmXQ) | 📅 Uploaded [[uploaded/2026-01-22]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A Vercel engineer's write-up reveals that for a lot of agent workloads, the fix for runaway token costs isn't a bigger RAG pipeline — it's treating your data as plain files and letting the agent use `ls`/`find`/`grep`/`cat` directly, the same way CLI coding agents already do. The presenter rebuilds a company-policy Q&A agent on this pattern with Gemini and lays out exactly when file-based retrieval beats a vector database, and when it doesn't.

**Watch this if:** you're deciding between a vector database and a simpler file-system-plus-bash-tool approach for an agent that answers questions from structured data.

## Key Takeaways
- Models are already good at navigating files and running bash commands because they're trained on huge amounts of code — an agent using `grep`/`ls` isn't doing anything new, just something more controlled.
- Agents can find the exact file with `ls`/`find`, then pull only the relevant slice with `grep`/`cat`, so irrelevant data never enters the context window — unlike vector search, which returns loosely related chunks and leaves the model to sort them out.
- Because folder structure mirrors real domain relationships, the file-system approach preserves hierarchical context that gets flattened away (and often lost) when data is chunked into vector embeddings.
- Vercel open-sourced a bash tool built on this pattern, offering two isolation modes: a lightweight in-memory sandbox restricted to a single directory, or full VM isolation (Vercel Sandbox) for stronger security guarantees.
- The presenter rebuilt his own company-policy project (JSON/markdown/txt files per department) using this architecture with Gemini 2.5 Flash instead of a vector database like Chroma, and matched RAG-level answer accuracy.
- The trade-off is exactness versus meaning: bash-tool retrieval is great for structured data and clear queries, but RAG still wins when queries are messy or when you need semantic (meaning-based) matching rather than exact matching.

## 🛠 Tools & Software
- [[topics/Claude Code]] — cited as an existing example of a CLI agent that already relies on bash/grep-based file navigation instead of vector search for research and codebase work.
- [[topics/Vercel Sandbox]] — Vercel's open-sourced bash tool that lets an agent browse a directory with `ls`/`find`/`grep`/`cat`; the presenter wires it up (in-memory mode) to build a company-policy Q&A agent, and also describes its full-VM isolation mode.

## 🤖 LLMs Mentioned
- [[topics/Gemini]] — Gemini 2.5 Flash is the model the presenter connects to Vercel's bash tool to answer questions from company handbook/leave-policy files.

## 📡 Protocols & Standards
- [[topics/RAG]] — used throughout as the baseline being challenged; the video argues file-system-plus-bash-tools beats RAG for structured data and exact-match queries, while RAG remains better for messy or semantic queries.

## ✅ Action Items
- Try swapping a small RAG/vector-DB pipeline for a sandboxed bash tool (`ls`/`find`/`grep`/`cat`) when your source data is well-structured and your queries are precise.
- If you give an agent shell access, restrict it to an isolated directory or sandbox — never the production filesystem.
- Benchmark token/cost overhead of your current vector-DB retrieval against a file-system approach on the same dataset before committing to either.

## 🔗 Related Videos
- [[videos/7 new open source AI tools you need right now]] — shared: Claude Code, Gemini
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude Code, RAG
- [[videos/Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to Build Instead]] — shared: Claude Code, Gemini
- [[videos/Antigravity 3.0 (New Upgrades) These New Updates make ANTIGRAVITY REALLY GOOD]] — shared: Claude Code, Gemini
- [[videos/Auto Claude This Opensource Tool converts CLAUDE CODE into a PROJECT MANAGER]] — shared: Claude Code, RAG
- [[videos/Can Claude Code Fix an Engineer's Terrible Taste]] — shared: Claude Code, Gemini
- [[videos/Claude Code + Karpathy's Autoresearch = GOD MODE!]] — shared: Claude Code, Gemini
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Claude Code, Gemini

## Timeline
- `0:00` — Framing: LLM apps burn tokens fast; a Vercel engineer's "everything is a file" idea is the fix.
- `0:38` — Why models are naturally good at bash/file navigation (trained on massive amounts of code).
- `1:15` — Agent workflow: `ls`/`find` to locate the file, `grep`/`cat` to extract just the relevant slice.
- `1:42` — Vercel open-sources a bash tool built specifically around this pattern.
- `2:33` — File-system structure mirrors domain relationships instead of flattening them into vector chunks.
- `3:01` — Grep/bash return exact matches vs. vector search's loose, chunk-based results.
- `5:59` — Presenter wires up Gemini 2.5 Flash with Vercel's bash tool and a per-command usage guide.
- `6:22` — Verifies via logs: the agent runs `ls` then `grep` and answers a leave-policy question with RAG-level accuracy.
- `6:46` — Safety question: is letting agents execute server-side commands safe? (cites the Dec. React RSC CVE scoring 10.0).
- `7:09` — Two isolation modes: lightweight in-memory bash-only vs. full VM isolation (Vercel Sandbox).
- `8:23` — Rule of thumb: bash tool for structured data with clear queries, RAG for meaning-based or messy queries.

## Transcript
<details>
<summary>Full transcript</summary>

Ever since models started getting powerful, many people have started building really cool products, integrating models into them, and solving lots of problems for us. But these systems consume a lot of tokens, especially if you're actually integrating a model using an API. The solution to this is much simpler than you think. The best architecture is not some extreme pipeline or highly scaled tuning, but actually an old philosophy that forms the basis of a Unix-based system that everything is a file. Now, I know they weren't talking about model costs and we're talking about devices and files, but surprisingly enough, the solution to this high-cost issue is the exact same principle. And this is exactly what a software engineer at Vercel talks about. Before we explore why files are the solution, let's understand a few things about how these models actually work. Models have been trained on massive amounts of code. This is the exact reason why they're better at understanding code, directory structures, and native bash scripts that developers use to navigate files and find what they need. When an agent uses grep and ls, it's not doing something new. It's simply doing something it already knows how to do, just in a more controlled way. This approach isn't limited to code. Agents can navigate any directory containing anything, be it code or not, because they're already comfortable with commands and understand file systems. Whenever an agent needs

something, it looks around the file system using native bash commands like ls and find. Once the agent finds the exact file using find, it searches for relevant content within that file using pattern matching with grep and cat. Only a small relevant slice of information is sent to the model while the rest stays out of memory, keeping the context window clean. This means we're not burning through tokens on irrelevant data that the model doesn't need. Using this approach, the agent returns a structured output. This pattern worked so well that Vercel ended up open sourcing a bash tool built specifically around it, giving agents the ability to explore file systems the same way a developer would. When building large language model systems, there are two ways of providing the right information to the model. Either through a detailed system prompt, hoping the agent actually follows it, or by feeding a lot of data into a vector database and using semantic search to extract it. But each approach has limitations. System prompts have a limited token window which limits how much information we can send to the model at a time. To handle larger data sets, we use semantic search which finds information based on matching meanings to the query. But vector search is used for semantic similarity rather than exact searches. It returns chunks of data that match the general context of the query, not necessarily the specific value we're looking for. This leaves extracting the right content from all

the chunks to the model itself. File systems, however, offer a different approach. With file systems, the structure actually maps to your domain. You often have relationships between files in the folder structure that mirror the relationships between parent folders. With file systems, you don't have to flatten these relationships into model understandable vector chunks, which helps avoid missing relationships that are usually lost in semantic search. These hierarchical connections are preserved naturally, maintaining the organizational logic that already exists in your data. Another advantage is that retrieval is precise because grep and bash tools return exact matches. Unlike vector search, which returns all chunks that loosely match the query and then leaves it to the model to decide which one to use, you get only the required value. The context is minimal when agents use bash tools because they receive the specific chunk they need and many other chunks don't go into memory. This allows them to stay aligned and focused on the exact piece of information without getting lost in unrelated data. Now, this idea isn't something you are unfamiliar with. This idea has already been used inside Claude Code and all CLI agents where they use bash functions to narrow down findings using pattern matching. We've already been using the file system and Claude Code's capabilities for research purposes for any idea that we evaluate. We usually pass the software tool we come

across through this pipeline which contains multiple phases with our evaluation criteria that the research must pass through. All of this is defined in a markdown file containing the requirements and objectives of the tool we're testing, how to write the final document, and all the information required for each phase. We also provide Claude with certain documents as samples, which act as a guide for style matching, and the final document is saved in a research results folder. To guide the research, we have a claude.md file explaining how to pass the idea through each phase one by one, ultimately giving us a research document that meets all our checks. Whenever we have anything to research, I just go to Claude and tell it the idea or the tool to research. It then runs it through the six-phase validation process first by understanding the tool or idea and then passing it through each phase one by one. Once the idea has gone through all the phases, Claude generates a final report which we can read to verify whether the idea has potential or not. This file system approach saves us a lot of time by automating a research process that we would otherwise have to do step by step. If you want to try out this pipeline for yourself for your own use case, you can get a ready-to-use template for creating your own research pipeline similar to ours in our recently launched community called AI Labs Pro. For this and for all the previous videos, you get

ready-to-use templates, prompts, all the commands and skills that you can plug directly into your projects. If you found value in what we do and want to support the channel, this is the best way to do it. Links in the description. I was going through Vercel's case study in which they explained how to build a sales summary agent using this architecture. They've also open-sourced it, but it gave me a really interesting idea that I wanted to try out on my own. I was actually building a company policy project where I had a lot of company data in the form of JSON, markdown, and txt files, all separated by department. Normally, I would have implemented this system using a vector database like Chroma, but I decided to give this tool a shot. I went ahead and implemented this architecture. On the back end, I included the path to the document folder containing the company's data and gave the agent access to the ls, cat, grep, and find commands along with a guide on how to use the tool and when to use each command. I used the Gemini 2.5 flash model, provided it with Vercel's bash tool, and gave it the path to the documents inside the tool. And so when I tested the agent by asking it any question related to the data, it basically answered based on the exact content from the company's policies, including the handbook and leave policy documents. To verify how it was working,

I logged its tool usage on the terminal. The agent first used the ls command to see what documents were available and then used grep with pattern matching to look for off days or any similar terms. This set of commands handled our query and gave us results with the same level of accuracy as a RAG system would. If you want the source code for this project, you can find it on our community from where you can download and try out for yourself. Now, the first question that came to my mind while going through this tool was, is it really safe to equip agents to execute commands on the server? We literally saw a vulnerability in React server components this past December, which scored a 10.0, the highest on the scale, and it involved code being executed on the server. So this is a really powerful and potentially dangerous capability to give agents. So why did I actually trust this tool? It's because it runs in a sandbox and has isolation. It only accesses the specific directory we provide. It doesn't modify anything else. In the article, they also mentioned that the agent explores the files without access to the production system. So your production code remains safe even if the agent tries to run harmful commands on the server. It provides two types of isolation. The first is an in-memory environment. In this setup, it uses just the bash tool which runs bash scripts only on the files it

has access to, just like we did when creating our agent. The second type is a fully compatible sandbox environment offering full virtual machine isolation using the Vercel Sandbox. We can choose either based on our needs. The in-memory approach is lighter and faster for simple use cases while the full VM isolation is better when you need stronger security guarantees. Even though this approach is really good for saving costs per model call, it's not the right approach for all kinds of problems. It's definitely not ideal if you need to match the meaning of words because bash tools are for exact matching. As we saw when we called our agent, it used specific keywords to locate the required data. It's also not suitable for unorganized file structures where the agent would have to struggle with multiple tool calls. A structure that the agent can easily navigate is much better. My personal suggestion is to use the bash tool when you have highly structured data and your requests are mostly clear in terms of what you want. Use RAG when you care more about the meaning of what's written in the files or when your queries are likely to be messy. Before we wrap up, here's a word from our sponsor, Brilliant. The best engineers don't just know syntax. They break down problems from first principles. That is why we've partnered with Brilliant. Their philosophy is that you learn best by doing. They prioritize active problem solving. So you get hands-on with concepts instead of just memorizing. For example, in their course named How AI Works, you don't just read, you manipulate the actual logic. You'll get hands-on with technicalities like calculating loss in the loss space and visualizing interpolation, building a deep intuition you just can't get from a video lecture. Through their interactive technical courses, you get the most effective way to truly master the concepts we talk about. You'll also get 20% off on an annual premium subscription, unlocking their entire catalog of math, data, and CS courses, giving you a complete road map to upskill. Click the link in the description or scan the QR code on your screen to claim your free 30-day trial.

That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
