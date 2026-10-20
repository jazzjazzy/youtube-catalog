---
title: "I Let Strix Attack My App... Here's What It Found"
video_id: vRTliPb8fjg
channel: "[[channels/Better Stack]]"
uploaded: 2026-07-09
processed: 2026-07-13
duration: "5:41"
url: https://www.youtube.com/watch?v=vRTliPb8fjg
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [ai-pentesting, security-testing]
tools: [Strix, FastAPI, Docker, GitHub Actions]
llms: [Claude, Gemini, Llama]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# I Let Strix Attack My App... Here's What It Found

![thumbnail](https://i.ytimg.com/vi_webp/vRTliPb8fjg/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=vRTliPb8fjg) | 📅 Uploaded [[uploaded/2026-07-09]] | 🗓️ Processed [[created/2026-07-13]]

## TL;DR
> Strix is a free, open-source (Apache 2.0, ~38k GitHub stars) AI pentesting tool that spins up a crew of AI agents — one does recon, others attack OWASP Top 10 issues like SQL injection, XSS, and broken access control — inside a Docker sandbox. Tested against a FastAPI expense app with auth and a database, a ~10-minute quick scan found a real endpoint, wrote a working exploit, ran it, pulled data out, and delivered the fix — validated findings instead of a pile of "might be exploitable" scanner noise. Limits: quality depends entirely on the model you bring, quick scans cost ~$3–5 in tokens, deep scans take hours, and complex chained logic attacks aren't there yet.

**Watch this if:** you ship web apps without a security team and want automated, validated pre-merge security checks rather than scanner what-ifs.

## Key Takeaways
- Strix uses a multi-agent architecture: agents map the app, attack it, and talk to each other to chain attacks — not one model guessing.
- Findings are validated: it breaks in, proves exploitability with a working exploit, and closes the loop with auto-fix pull requests — eliminating false-positive triage.
- One-line curl install; run with `strix target <code path + live UI> --scan-mode quick` plus your model API key. Bring your own model: Claude, Gemini, or a local Llama (no lock-in).
- Requires Docker — agents act inside a sandbox on first run so exploit attempts never hit your real systems. Only run against apps you have permission to test.
- Benchmark: ~96% solve rate on the XBEN exploitation benchmark at ~19 minutes per challenge — real break-in tasks, not detection quizzes.
- CI-friendly: command-line tool with native GitHub Actions support; exits with an error code on findings, so it can block a bad merge pre-land.
- Costs and limits: weak local model → weak findings; strong model → real token spend (~$3–5 per quick scan); deep scans take hours; complex long-chain logic attacks still beyond it.
- Positioning: one strong layer in a layered security posture — validated CI feedback next to existing scanners plus human review for hard calls, not a replacement for human pentesting on critical systems.

## 🛠 Tools & Software
- [[topics/Strix]] — the subject: open-source multi-agent AI pentesting tool, demoed end-to-end against a live app
- [[topics/FastAPI]] — the demo target: an expense-tracking app with auth and a database
- [[topics/Docker]] — required runtime; Strix pulls a sandbox image so agent exploits stay contained
- [[topics/GitHub Actions]] — native CI integration; error exit codes let Strix block bad merges

## 🤖 LLMs Mentioned
- [[topics/Claude]] — model used in the demo (via Anthropic API key)
- [[topics/Gemini]] — supported alternative backend
- [[topics/Llama]] — supported local option for keeping scans off cloud APIs

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Strix via the one-line curl command; make sure Docker is running for the sandbox pull.
- Point it at a staging/side-project app you own with `--scan-mode quick` and your Anthropic API key; budget ~$3–5.
- Wire it into GitHub Actions as a pre-merge gate — the non-zero exit code on findings can block merges.
- Treat it as one security layer: keep existing scanners and human review for complex logic and critical systems.

## 🔗 Related Videos
- [[videos/Someone open-sourced a hedge fund (53k stars on GitHub)]] — shared: Claude, Docker, Gemini
- [[videos/Suna The FREE Open Source Alternative to Manus AI]] — shared: Claude, Docker, FastAPI
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Gemini
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: Claude, Gemini
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Docker
- [[videos/How I Watch ANY Video with AI in Seconds]] — shared: Claude, Gemini
- [[videos/I Tried Every Skill These Best Claude Skills Are Bizarre]] — shared: Claude, Gemini
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Claude, Gemini

## Timeline
- `0:00` — Passing tests ≠ secure: the break-in your tests never see
- `0:28` — What Strix is: a crew of AI agents doing recon + OWASP Top 10 attacks
- `0:50` — Why it matters: no security team, no pentest budget, scanners bury you in what-ifs
- `1:11` — One-line curl install; demo FastAPI expense app with auth + database
- `1:42` — Running `strix target` with code path, live UI, quick mode, Anthropic API key
- `2:03` — Docker sandbox requirement; only test apps you have permission to test
- `2:39` — Results: found endpoint, wrote working exploit, ran it, pulled data, delivered fix
- `3:04` — vs manual pentest / static scanners / other AI tools: chained agents, sandbox, auto-fix PRs
- `3:29` — 96% solve rate on XBEN exploitation benchmark (~19 min/challenge)
- `3:39` — CI usage: GitHub Actions support, error exit codes block bad merges
- `4:14` — Limits: model-dependent quality, $3–5 quick scans, hours-long deep scans, weak on complex chained logic
- `4:51` — Verdict: pre-merge checks and staging, one layer of a layered defense — not a human replacement

## Transcript
<details>
<summary>Full transcript</summary>

Your tests pass, the code is clean, you ship, and you're done. Then something happens to your database through a bug you were never going to see in the first place. This thing that just shows me exactly how that break-in happened, and it isn't some hack. It's open source, it's free, it's sitting at almost 38,000 stars on GitHub, and this thing has a name. This is Strix. Let me show you what it does and where it falls apart.

So, what is this thing? Strix spins up a team of AI agents that behave as hackers, similar to some pen test tools, but not one model is taking a guess, it's a crew of them. One agent does recon and maps your app, another goes after the OWASP top 10 and your APIs, SQL injection, cross-site scripting, broken access control, the stuff that actually gets shipped. Here's why this matters to us, because a lot of us don't have a team and we don't have a bunch of money laying around for a pen test. So, we either ignore the problem or you run a scanner that buries you in a ton of what-ifs. Strix doesn't do that. It doesn't say this might be exploitable. It breaks in, proves it, and hands you it as a pull request.

Now, let me show you all this in action. All right, now you'd expect setting up would be a lot, but in reality, this is one line. I fired up with a curl command to install it, that is what installs this. Now, here is a FastAPI app for expenses just built out, and it's running on this UI, which you can see here. I added one expense, which is subscribe to the Better Stack channel. I put one cent, but in reality, subscribing is always free, and you learn a ton from our countless videos coming out all the time. Now that we have Strix, I can run this one command here. Strix target. I'm going to put my code path in the live UI, then I'll add the scan mode quick. I'm just giving Strix a model to use here. I'm using my Anthropic API here, but it takes Claude, Gemini, or even a stronger Llama model if you want to keep it local. This command targets my live site and my project together. One catch here, it pulls a docker sandbox on the first run, so docker does need running. The sandbox lets the agents actually act without the blast hitting your systems. Then I pointed at a small app, my app that I built. I wrapped some auth and a database to it, and that's the one rule. You only ever run this on something that you have permission to test. Now, you think it fires back results instantly, it doesn't. Does any pen test tool do that? A quick scan here took about 10 minutes. All right, so but I'll speed that up for you. Let me cook this and let me grab a coffee in the meantime.

All right, with that coffee in hand, we can take a look at this now. Now, most tools tell you your door might be unlocked. Strix found the endpoint, wrote a working exploit, ran it, pulled data out, and gave me the exact steps here. Plus the fix, it told me what's wrong. This is everything I got back from Strix. After a little bit of time running on the quick mode. You could change quick mode, but that's going to take a lot longer, and it's going to rack up more tokens. So, how is this different from many of the others already out there? Manual pen test is accurate, but it's slow and it's pricey. A static scanner is fast and cheap, but it never really runs our code, and other AI tools exist. They do, right? Here's where Strix kind of pulls ahead or changes it a little bit. The agents talk to each other in chain attacks. It's all sandboxed, and it closes the loop with auto fix pull requests. On the XBEN exploitation benchmark, it hits a 96% solve rate around 19 minutes per challenge. And those are real break-in tasks, not multiple-choice detection.

How would you actually use this? Well, it's a command-line tool with native GitHub actions support, and it works on open-source code and a live app. Shipped Python drops right in. Now, the best part by a mile is validated findings. Every real bug here comes with working proof. So, that 400 maybes pile just disappears. The CI hook is clean. It exits with an error code when it finds something. So, you can straight-up block a bad merge before it even lands. So, open source Apache 2.0, bring your own model with no lock-in, and it's strong on APIs and web apps. And it mostly held up, but it's got real limits as well. It leans hard on the model you give it. You're basically renting a hacker for a minute or two or however long this takes. A weak local model gives weak findings. A strong one, it costs a lot of tokens. Budget three, maybe $5 for a quick scan. It depends on how big your project is. Deep scans are slow. They're hours. They're not minutes. And Docker adds friction. And on the really messed-up stuff, complex logic, long chain attacks, it's not quite there yet. It's pretty cool for routine repeatable checks, but maybe not a stand-in for a human on your actual systems, depending on how big they are.

So, do you actually run this? I mean, yeah, you could. Where I'd reach for it maybe is pre-merge checks, side project staging, catching the obvious stuff before production. Wired in your pipeline, let it run on real changes and see what happens. As your only defense on a critical system with a bit of setup, maybe not. Think of security as layers, not a single wall. Strix is one strong layer. Validated feedback in CI sitting next to your existing scanners for coverage and a human review for the hard calls. That's just an idea. If you care about shipping secure code faster, this is a pretty sweet open source tool and it's free to try with your own keys. If you enjoy coding tips and tricks like this, be sure to subscribe to the Better Stack channel. We'll see you in another video.

</details>
