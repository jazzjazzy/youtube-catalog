---
title: "This is The Most Powerful Tool to Give to Claude Code"
video_id: YHk45NEpspE
channel: "[[channels/Nate Herk - AI Automation]]"
uploaded: 2026-05-09
processed: 2026-07-05
duration: "14:45"
url: https://www.youtube.com/watch?v=YHk45NEpspE
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [cli-tool-creation-for-agents, reducing-agent-token-usage]
tools: [Printing Press, Claude Code, Skool, Go, Gemini CLI, Codex, GitHub CLI, Playwright, Higgsfield, HeyGen, ESPN, Hacker News, Tally]
llms: []
protocols: [MCP, OAuth]
transcript: true
tags: [youtube, ai-automation]
---

# This is The Most Powerful Tool to Give to Claude Code

![thumbnail](https://i.ytimg.com/vi_webp/YHk45NEpspE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=YHk45NEpspE) | 📅 Uploaded [[uploaded/2026-05-09]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Printing Press is a CLI factory-and-library tool that turns almost any website or API (even ones with no public API, like Skool) into a fast, token-efficient command-line interface for Claude Code. The video argues CLIs beat both raw APIs and MCP servers for agent use, walks through installing Printing Press's starter pack, and demos building a working Hacker News CLI live from a single natural-language request.

**Watch this if:** your agent setups are burning tokens on bloated MCP servers or raw API JSON, and you want a faster, cleaner way for Claude Code to talk to tools and sites that don't have good official APIs.

## Key Takeaways
- CLIs beat MCP and raw APIs for agents: one cited benchmark shows MCP using 35x more tokens than a CLI for the same task, with reliability dropping from 100% (CLI) to 72% (MCP) as tasks get harder.
- Printing Press is both a "factory" (a skill/tool that helps build new CLIs from scratch) and a "library" of roughly 50 pre-built CLIs (ESPN, ~~Recipe/Movie/Flight~~ "Goat" tools, Amazon, Craigslist, eBay, TikTok Shop, Shopify, Airbnb, and more).
- In a live example, asking Claude Code to pull Skool community posts used a custom-built Skool CLI: it sent ~260 tokens out and got ~132,000 tokens back from Skool, but only ~2,000 tokens of clean summary ever hit the agent's context window.
- The presenter's tiering rule of thumb: prefer a CLI first; if no CLI exists but there's an API, build a CLI around the API; only fall back to MCP if a site truly offers no API and no CLI is buildable.
- Setup requires installing Go (a free, Google-built language for CLI tools) alongside Printing Press's starter pack and factory skill, all doable by just handing Claude Code the three relevant links and asking it to set everything up.
- Live demo: giving Claude Code a single natural-language request ("use Printing Press to build me a Hacker News CLI") triggered autonomous research, reverse-engineering, a full Go CLI build, and a working skill in well under the tool's own estimated 30-60 minutes.
- Built CLIs can be packaged into a private GitHub repo and shared with a team (as done with a Tally CLI), with the same caveat as APIs: never hardcode auth keys directly into CLI scripts — keep them in `.env`.

## 🛠 Tools & Software
- [[topics/Printing Press]] — the CLI factory-and-library tool that is the entire subject of the video, used to build Skool, Tally, and Hacker News CLIs live
- [[topics/Claude Code]] — the coding agent driving every demo: installing Printing Press, invoking CLIs via natural language, and building the Hacker News CLI
- [[topics/Skool]] — the community platform with no public API; a custom CLI built with Printing Press pulls posts/wins from it in both demos
- [[topics/Go]] — the programming language Printing Press requires and uses to compile the CLIs it builds (including the live Hacker News CLI)
- [[topics/Gemini CLI]] — named as an example of an existing official CLI agents already use
- [[topics/Codex]] — named alongside Claude and Gemini as an existing CLI-based coding agent
- [[topics/GitHub CLI]] — named as an example of an official vendor CLI already used by agents
- [[topics/Playwright]] — named as another tool that ships its own CLI
- [[topics/Higgsfield]] — named as a tool that recently shipped a CLI
- [[topics/HeyGen]] — named as another tool that recently dropped a CLI
- [[topics/ESPN]] — has no public API; its Printing Press CLI is demoed live to fetch tonight's NBA schedule
- [[topics/Hacker News]] — built live via Printing Press's CLI factory from a single natural-language prompt, then demoed pulling top stories
- [[topics/Tally]] — an existing API the presenter converted into a CLI and packaged into a shareable GitHub repo for his team

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — directly compared against CLIs and APIs; cited as far more token-hungry and less reliable for agent tool use
- [[topics/OAuth]] — mentioned as one of the auth types (alongside cookies/API keys) a Printing Press-built CLI may need to store in `.env`

## ✅ Action Items
- Run `/context` in a fresh Claude Code session to see how many tokens your loaded MCP servers are consuming, even unused.
- Install Printing Press's starter pack plus the factory skill (and Go) by pasting the three linked URLs into Claude Code and asking it to set everything up.
- Before reaching for an MCP server, ask Claude Code to build a CLI around the tool's existing API or reverse-engineer one for sites with none.
- Package any custom CLI you build into its own GitHub repo (with secrets left out) so your team can clone and reuse it.

## 🔗 Related Videos
- [[videos/7 Tools That Make Claude Code + Codex Dangerous]] — shared: Claude Code, Codex, GitHub CLI, OAuth
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude Code, MCP, OAuth, Playwright
- [[videos/OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)]] — shared: Claude Code, Codex, MCP, Playwright
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Claude Code, Codex, Gemini CLI, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Codex, MCP
- [[videos/AGENT THREADS How to SHIP like Boris Cherny Ralph Wiggum in Claude Code]] — shared: Claude Code, Codex, Gemini CLI
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude Code, Hacker News, MCP
- [[videos/Anthropic Just Killed All Your Agent Harnesses]] — shared: Claude Code, MCP, Playwright

## Timeline
- `0:00` — Intro: Claude Code pulling Skool community posts through a custom CLI
- `1:10` — What is Printing Press: a CLI factory and a library of ~50 pre-built CLIs
- `1:35` — CLI vs. API vs. MCP: token efficiency and reliability compared
- `5:03` — Printing Press walkthrough: browsing the catalog and starter packs
- `6:53` — Setup and install: Go, the starter pack, and the factory skill
- `7:48` — Why CLIs win for sites without APIs: ESPN, Craigslist, Allrecipes, Domino's, Skool
- `9:48` — Building your own CLI live: the Hacker News example
- `11:45` — Sharing CLIs with your team via a private GitHub repo
- `13:40` — Final thoughts and the CLI > API > MCP tiering rule

## Transcript
<details>
<summary>Full transcript</summary>

All right, so what would you think if I told you that I just said to Claude code, "Hey, go to my school community and grab me some posts." And keep in mind, school does not have an API and it was able to use the CLI, it was able to find nine wins, and it made sure that they were in the wins category, and then it gave me the three strongest ones. And I got a link to all of them so we can see if they actually exist. But anyways, the way that we're doing this is we're using a CLI and the tool I'm going to show you guys today actually helped me build the school CLI. So if you've never heard of the term CLI before, don't worry, I'm going to explain it. I'm going to compare it to APIs and compare it to MCPs. But before we get into all that, let me show you one more example. So here I said, "Hey, can you just go pull 10 of the most recent posts in my community?" It goes ahead and it uses the school PP CLI. PP stands for Printing Press, which is the tool I'm going to show you guys today. It comes back, it grabs all of these 10 posts, and then I also asked like, "How many tokens did you actually consume to make the CLI request?" And it said, "Okay, here's what happened. I sent about 260 tokens to school. It sent me back about 132,000 tokens." But what's important is that none of that hit my context window because we were basically able to point all of that routing through the CLI so that none of it actually pollutes your session or your context. So that is super cool and I built the school CLI and it literally took me about 10 minutes.

All right, so here is the tool that we are using. Introducing Printing Press, a CLI factory and a CLI library. The whole idea is that APIs suck for agents, MCPs also suck for agents and a lot of times official CLIs suck for agents because they waste tokens or they're not efficient. So Printing Press has a library of like 50 pre-built CLIs that you can use right away and it also gives you a factory so that you can turn anything into a CLI. So let's just start off with the basics real quick. Why CLIs beat MCPs and APIs and what even is a CLI? So CLI stands for command line interface and it's a way to use a tool by typing a command instead of clicking buttons. So it's not a new concept, it's been around for a long time. You know, like Gemini's got a CLI, Claude CLI, Codex CLI. And you might have been seeing a lot of tools recently create CLIs like Google have their official GWS CLI, which is probably the most used thing in my cloud code. GitHub has a CLI. Playwright has a CLI. Higgsfield just created a CLI. Hay gen just dropped a CLI. It's really just the best and most efficient way to have agents talk to other tools.

Now, what are the other ways? API and MCP. And when MCP came out and it kind of broke the internet, everyone just assumed that MCPs were the answer and we're just going to shove MCPs into all of our agent setups and they all just have different pros and cons. APIs are very raw. You're going to get back a huge JSON snippet from the API endpoint and sometimes you need all that information and it's really, really nice. They're also more token efficient than an MCP server because MCP servers have to have all the different tools and descriptions and the ability for the agent to look through everything, which is cool because they're way more flexible than an API endpoint. But, as you can see, they add overhead, extra context bloat and you have to keep a server running. So, if you go into Cloud Code right now, brand new session and do slash context, if you've got a bunch of MCP servers loaded in, you'll see how many tokens they're using every single time. And you may not even be invoking that MCP server, so it might just be a waste of tokens. And then we have CLIs, which are local, they're fast, they're composable, they have a SQLite backend, they're agent native. And you can start to build some skills around these CLIs, just like you can with APIs and MCPs as well, to chain them together and make some really cool, fast workflows. And the cool thing is the output you get is super short and super clean.

Okay, so real quick to hit on each of those individually, why do APIs lose? Because they were built for code, not for all of these autonomous agents that pay per token. Because when you get back an API response, you just get this massive JSON body. You also might run into issues with pagination or auth and it just can get a little bit funky sometimes. And what about MCP? MCP solved discovery because like I said, you could quickly glance at 50 tools that are available from a certain server, but because you're loading all 50 tools, now you have tokens and descriptions for all of those 50 tools. Here's a real benchmark. MCP used 35 times more tokens than the CLI on the same task and reliability drops from 100% with the CLI to 72% with MCP as tasks get harder. So really, if you can just shift to every single time you want Cloud Code to talk to something, just try to find a CLI or build your own CLI now. Because they were built for exactly how agents actually think. They have lazy discovery, they have pre-formatted outputs where you're basically just getting 200 tokens of clean text rather than raw JSON. You can compound commands together, you have a local SQLite mirror, which means no round trips and it means no rate limits. It's obviously native to the agent and the auth is pretty much solved one time because the CLI holds the token and then you are all set. So the bottom line, APIs are built for code, MCPs built for tools, and CLIs are built for agents, especially when you're paying per token or managing your session limit.

Okay, so what is Printing Press? What are we looking at today? So if you go to printingpress.dev, this is what it will look like. It's a very new tool just dropped like yesterday and I've been playing with it all day today. This kind of was inspired by Peter Steinberger, the creator of Open Claw, needing to make his own CLIs because the official ones were bad. So he built like Gog CLI, which is for Google, and people are saying that it's even better than the GWS CLI that is Google's official CLI. So that's the whole idea. You have a factory, so basically a skill and a tool to help you build CLIs, but also if you come down here, there's a library. So you've got a Flight Goat CLI, ESPN, Movie Goat, Recipe stuff, Linear. And if we keep scrolling down, you can see there's different ones, Amazon, Craigslist, eBay, TikTok Shops, Shopify. There's so many different CLIs on here that you can use. What I would recommend if you want to get in here and get started is just start off with a starter pack. This has like four or five CLIs, ESPN, Flight Goat, Movie Goat, and Recipe Goat.

So, basically what I did is I took all three of those URLs, and I went into my Cloud Code, and I said, "Hey, read all three of these. This is a new tool I'm seeing that has a bunch of preloaded CLIs, and it also helps you build CLIs, and just install everything I need." It's super super easy. You basically install it, and then you can do natural language requests to use all this stuff. The one pre-rec is that you're going to need to get Go, and it's basically as simple as asking Cloud Code to do it. It's a free open-source programming language made by Google. It's designed to be simple, fast, and it's great for building command line tools, so CLI tools, web servers, cloud apps, and other AI-related stuff. So, that'll take you maybe 1 minute. You tell Cloud Code, "Okay, download that for me." And then you just follow the prompts.

And why is this a big deal? Because most websites your agents want don't have a clean API, but Printing Press just lets you basically build your own with the CLI. So, ESPN, for example, no public API. Craigslist, no public API. Allrecipes has anti-scrape protection, but the CLI uses a real Chrome session. Domino's has no public API. School, as you guys saw, no public API. So, if I come into Cloud Code, now that I've got this all installed, I can ask, "Can you take a look at our Printing Press library of CLIs and tell me what we have access to?" Here you can see it's using the Printing Press catalog skill. Here is what we have. These are the three local ones that I just built. We have School, we have Tally, and we have YouTube. So, now if I just say, "What NBA games are on tonight?" it's going to use the ESPN skill, and it's going to pull back that data for us. So, it says, "Okay, there are two NBA games on tonight, Eastern Time, Knicks and Sixers at 7:00, and Spurs and Timberwolves at 9:30." And you can see, that is exactly correct.

The last thing I want to do now is just show you what it actually looks like to build your own. So, let's say I did want to build my own and we're going to take Hacker News as just an example. I basically would just say, "Hey, can you please use Printing Press? Can you use the CLI factory to help me create my own CLI? I want to be able to pull in articles from Hacker News and just get insights every day from that site." Now, Hacker News doesn't actually take any authentication, so we should be able to just pull it in. The point is that you can just ask in natural language and it will start doing all the research and investigating and reverse engineering things and then help you build it out. But, if it does take like authentication cookies, or OAuth, or an API key, then you still basically treat it the same way you would like an API. You would be putting those in your .env and storing them in there. So, anyways, this comes back and it says, "I'm going to research Hacker News. I'm going to catalog every feature that exists in any tool. I'm going to present what I found and then I will generate you a Go CLI, build every feature, and then we will verify quality through dog food, runtime verification, and scoring." It says it is going to take 30 minutes to 60 minutes, but it's always bad at those estimations.

I'll talk about something else real quick, which is what can you do with those CLIs? Because you could publish them back to the library, and then other people could publicly pull them in and use those CLIs as well. And you can also just share them with your team internally. So for example, this Tally one that I just built, I have been able to push this to a private repo, and now I can just invite some of my team to actually be a contributor to this, so they can clone it, and then they can use the Tally CLI as well, and maybe just swap out their own API key in their .env file. All I did was I said, "Okay, cool. So you built me this Tally CLI, and you built me this skill. Can you just package just that into a GitHub repo so I can share that across my team?" And a couple seconds later, I had this new GitHub repo. So of course you don't want to be putting any of your API keys or your authentication stuff inside of the CLI scripts. That would still be treated the same way as you treat your API endpoints.

So once again, this isn't exactly that "Hey, this CLI is going to give you so much more functionality than if you just use the API." But it's the ability to first of all be able to turn anything into a CLI, and start natively working through just CLIs rather than APIs and MCPs. So maybe think of an example of something that you use a lot that doesn't have a great API, or it only has an MCP server, and just think about the fact that you could now tell Cloud Code, "Hey, I use this software for X, Y, and Z. Do you think you could help me build a CLI around that right here in Cloud Code?" So it's kind of just like the checklist of thinking about how you talk to tools. I would say like CLI would be tier one. If there's no CLI option or you just can't do it, then the API would be next. If there's an API, you're pretty much 100% going to be able to make a CLI. But then, if there's no API and you can only use an MCP, then that would be the final option.

All right, so all of that has finished up now. We can see this is exactly where the binary actually lives. It's giving some examples here where you could actually invoke this command basically in the CLI. Or, it should have built kind of like a skill around this and we're able to just invoke it with natural language. So, I'm just going to go ahead and see what happens if I say, "Can you test this out using the actual skill and just go ahead and see which sites are dominating Hacker News today?" It came back super fast. It said, "Okay, last 24 hours, stories with 100 plus points ranked by total score." And we get these 10 stories right here. So, anyways, this demo wasn't about the fact that we're doing this with Hacker News. It was just to show you guys how easy it is to set up these CLIs. And from here, you can build skills around them and you can chain them together. And of course, you can access the catalog on printingpress.dev. And I'm assuming that this is just going to continue to grow and grow. So, anyways, wanted to keep this one quick, but I hope that you guys learned something new or enjoyed the video.

</details>
