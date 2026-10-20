---
title: "Every app on Earth is now open source... whether it likes it or not"
video_id: wajoP_5Cpw8
channel: "[[channels/Fireship]]"
uploaded: 2026-10-12
processed: 2026-10-20
duration: "5:55"
url: https://www.youtube.com/watch?v=wajoP_5Cpw8
playlist: "[[Agents skills n8n]]"
type: news
difficulty: beginner
use_case: [reverse-engineering, open-source-alternatives]
tools: [ArtCraft, REA, Ghidra, Adobe Premiere, Rust, Supabase]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Every app on Earth is now open source... whether it likes it or not

![thumbnail](https://i.ytimg.com/vi/wajoP_5Cpw8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=wajoP_5Cpw8) | 📅 Uploaded [[uploaded/2026-10-12]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> Code Report episode on two colliding stories: developer Brandon Thomas, burned by Adobe's cancellation fees, used Claude to rebuild seven Creative Cloud apps in Rust as the free, open-source, Linux-friendly ArtCraft suite — and the viral reverse-engineer-anything (REA) project that can decompile virtually any binary (stripped ELF/PE/Mach-O, JVM bytecode, .NET assemblies, firmware, OCI layers). Fireship's hands-on verdict: ArtCraft's FilmCraft clones Premiere's UI but is "nearly unusable vibe-coded" software today — yet REA + Ghidra genuinely let him extract C-like pseudo-code from Premiere's timeline feature and hand it to a coding agent to rebuild a stripped-down "Premiere Light" in Rust, and even analyze Supabase's API traffic to vibe-build a tailored backend.

**Watch this if:** you want the entertaining five-minute version of why compiled binaries no longer hide how software works — and a reality check on AI-rewritten Adobe clones.

## Key Takeaways
- [[topics/ArtCraft]]: one developer plus [[topics/Claude]] reverse-engineered Adobe's 30-plus-year codebase and shipped free [[topics/Rust]] rewrites of Photoshop, Illustrator, Premiere and more — running even on Linux, which Adobe never supported.
- Reality check: the apps are currently "a nearly unusable pile of vibe-coded" software — FilmCraft's one-to-one Premiere UI clone lags on a single stock clip and its transitions fall far short, despite Rust's blazingly-fast reputation.
- [[topics/REA]] (reverse-engineer-anything) decompiles stripped ELF, PE, and Mach-O executables, obfuscated JVM bytecode, ECMA-335 .NET assemblies, bare-metal firmware, and OCI container layers — "virtually every app in the world is now open source, whether it wants to be or not."
- Compilation destroys source but not structure: REA maps binaries back into C-like pseudo-code, assembly, strings, symbols, calls, and references — with [[topics/Ghidra]] (the integration Fireship says deserves most of the credit) doing read-only analysis of EXEs and DLLs.
- The practical workflow: inspect one feature of a locally installed app (Premiere's timeline), take the pseudo-code output, and hand it to your favorite coding agent to re-implement just the features you actually use — a personal "Premiere Light".
- REA's networking feature also analyzes API interactions and UI changes of running services — demoed on [[topics/Supabase]] to vibe-build a tailored backend ("Studbase"), complete with self-aware made-up benchmarks.

## 🛠 Tools & Software
- [[topics/ArtCraft]] — Brandon Thomas's open-source Rust rewrites of seven Adobe Creative Cloud apps, including the FilmCraft Premiere clone tested here.
- [[topics/REA]] — the viral reverse-engineer-anything project: set up via npx, then used like any AI agent to inspect local binaries.
- [[topics/Ghidra]] — REA's decompilation backbone on Windows, doing the read-only analysis of native EXEs and DLLs.
- [[topics/Adobe Premiere]] — both the $69/month incumbent being cloned and the reverse-engineering target for the timeline-feature inspection.
- [[topics/Rust]] — the language of the ArtCraft rewrites and of the planned "Premiere Light" re-implementation.
- [[topics/Supabase]] — the backend whose API interactions REA's networking feature analyzed for the Studbase experiment.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model Brandon Thomas "opened up" to reverse-engineer Adobe's codebase; the episode's framing question is whether one person plus Claude made Adobe obsolete.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Try the ArtCraft apps (free downloads) but calibrate expectations — treat them as early vibe-coded previews, not Premiere replacements.
- Set up REA with Node.js/npx and configure the Ghidra integration if you're on Windows.
- Pick one feature of an app you legally can inspect and ask the agent for its pseudo-code, strings, and call graph.
- Pipe REA's output into your coding agent to rebuild only the features you actually use, rather than cloning a whole product.
- Use REA's networking analysis to understand a service's API surface before building a tailored replacement.
- Be skeptical of "orders of magnitude faster" benchmarks — including the ones in this video.

## 🔗 Related Videos
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, Supabase
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Supabase
- [[videos/Suna The FREE Open Source Alternative to Manus AI]] — shared: Claude, Supabase
- [[videos/The Best MCP Servers of 2025]] — shared: Claude, Supabase
- [[videos/The Fastest-Rising Repo on GitHub Is a Little Scary REA]] — shared: Ghidra, REA

## Timeline
- `0:00` — ArtCraft: a developer rebuilds seven Adobe Creative Cloud apps in Rust with Claude and gives them away, Linux included
- `0:32` — reverse-engineer-anything goes viral: stripped ELF/PE/Mach-O, JVM bytecode, .NET assemblies, firmware, OCI layers
- `1:10` — The Code Report, October 12, 2026: did one person plus Claude obsolete the Adobe suite overnight?
- `1:29` — Hands-on with FilmCraft: a one-to-one Premiere UI clone that lags on a single stock clip
- `2:14` — Transitions side-by-side: nowhere near Premiere quality — "not good enough yet"
- `2:35` — Plan B: reverse engineer Premiere into a simpler personal editor
- `2:49` — Binary basics: compiled ones and zeros mapped back to something resembling source
- `3:20` — Setup: npx install, Ghidra integration for read-only EXE/DLL analysis — "the tool that deserves the most credit"
- `3:37` — Inspecting Premiere's timeline feature returns C-like pseudo-code, assembly, strings, symbols, and calls
- `3:58` — Handing the output to a coding agent to re-implement the feature in Rust: Premiere Light
- `4:15` — Studbase: REA's networking feature analyzes Supabase API interactions to build a tailored backend with trust-me-bro benchmarks
- `4:58` — Sponsor segment and sign-off

## Transcript
<details>
<summary>Full transcript</summary>

Last week, a developer got so tired of Adobe's predatory business model that he decided to rebuild seven of its Creative Cloud apps with Rust, like Photoshop, Illustrator, and Premiere, then open-sourced them, and gave them away for free. The project is called ArtCraft, and the developer's name is Brandon Thomas, who, after being hit with Adobe's cancellation fee more than once, opened up Claude, then reverse-engineered Adobe's 30-plus-year code base from scratch. And the apps even run on Linux, a platform Adobe has never officially supported. What's crazy, though, is that you, the human being watching this video, can do the same thing thanks to an unrelated project called reverse-engineer-anything. It's been going viral on the internet lately because it can easily decompile any native binaries you can get your hands on. We're talking stripped ELF, PE, and Mach-O executables, JVM bytecode with obfuscated constant pools, ECMA-335-compliant .NET assemblies, bare-metal firmware with architecture-specific instruction sets, and even OCI container layers entangled in declarative infrastructure manifests. In layman's terms, that means virtually every app in the world is now open-source, whether it wants to be or not. In today's video, we'll attempt to reverse-engineer anything and everything and find out if this is the final nail in the coffin for software as we know it. It is October 12th, 2026, and you're watching The Code Report.

So, is it really true that one person plus Claude made the entire Adobe suite obsolete overnight? Well, on the surface, yes. As you can see on the website, you can download a Rust-based version of any Adobe program for free right now. That's awesome, but after trying it out myself, I realized there's one small catch. The software is a nearly unusable pile of vibe-coded horse Now, I begrudgingly pay Adobe a $69 tribute every month to use Premiere to edit these videos for you guys, and I was thrilled to finally see an open-source alternative. And let's just ignore the fact that DaVinci Resolve has been an open-source alternative for over 20 years now. And when I first opened FilmCraft, I was thrilled to see that the UI was nearly a one-to-one clone of Premiere. So, I could get to work immediately without any learning curve. My plan was to edit this video with it, but the cracks became visible immediately. Like after dragging a clip of some lame stock video onto the timeline and hitting play, there was a massive lag in the audio bars and just overall slowness and laziness despite being vibe coded in rust, which I've been told is a blazingly fast programming language.

So then, I tried implementing some transitions between clips and they were just nowhere near the quality of Premiere, which you can clearly see with this glitch transition side-by-side. And for someone like me who's a once-in-a-generation cinematic visionary who many have called the Stanley Kubrick of sponsored posts, the sad reality is that Film Craft is just not good enough yet. But I sincerely hope it gets there someday because Adobe. But then that got me thinking, what if instead of trying to use off-brand Premiere, I just reverse engineer it myself and make it simpler because Premiere has hundreds of features that I don't use that just get in the way. Luckily, there's a new project in town that can help us do that called reverse engineer anything. Adobe Premiere is primarily written in C and C++, and crazy smart Asians on H-1B visas have been writing its code for decades. Now, its actual source code is top secret Adobe intellectual property, but in order to actually run it on your machine, they need to compile that code into a native binary of ones and zeros. This stuff is almost unreadable to humans, but with a lot of painstaking work, it is technically possible to map these ones and zeros back into something that resembles human readable source code.

And the REA project can do that for people who can't even count to three in binary. First, we set it up by running it with Node.js and the NPX command. And then because I'm a loser on Microsoft Windows, we'll configure REA's Ghidra integration, which is actually the tool that deserves the most credit here and can do a read-only analysis of native EXEs and DLLs. Then from there, we can just use it like any other AI agent and tell it to inspect the locally installed version of Adobe Premiere. In this case, I'll have it inspect Adobe's timeline integration and try to figure out how it does this one specific feature. A while later, we get back a bunch of C-like pseudo code along with assembly, strings, symbols, calls, and references, which to an obsolete HTML programmer is all pretty useless. However, we can now take this garbage code and pass it off to our favorite coding agent to re-implement the exact same feature in Rust. And thanks to reverse engineering, I'll eventually be able to build my own version of Premiere Light that's not only free, but only has the actual features I want to use.

But as a cheapskate developer, I'm not stopping there. I think it's crazy that any real vibe developer in 2026 is still paying money for developer tools when that money should be spent burning tokens. For example, let's take a look at an ancient technology called Supabase, which is basically a wrapper on top of AWS that provides a UI for your database. Even though it's mostly open source, it has a ton of features I don't want. So what I'm doing instead is using the networking feature in REA to analyze API interactions and UI changes, which has allowed me to build a better back-end that I'm calling Studbase, which is not only perfectly tailored to the needs of Horse Tender and Donker, but is also orders of magnitude and faster according to this benchmark I just made up. Trust me, bro. You can trust these trust me, bro benchmarks.

And another thing you can trust is Appify, the sponsor of today's video. Their MCP server lets you connect your agent to thousands of tools called actors. They can do things like scrape live data from YouTube or monitor your competitors' prices on Amazon. But right now, I'm using it to track the most liked posts on the Donkeys of Instagram hashtag so I can invite the most desirable assets to sign up on Donker. It only takes one line to connect to the server, and I could explain what I wanted it to do in natural language. From there, my agent started using the relevant Appify tools to return to the structured data I needed in order to help these gay donkeys find love. But the most impressive part was how few tokens it took. But because Appify's MCP server only exposes a handful of core tools, it then finds the best one for your job and runs it in the background to avoid token bloat. You get $25 in free credits to try it out by using the code fireship25 at the link below. This has been the code report. Thanks for watching and I will see you in the next one.

</details>
