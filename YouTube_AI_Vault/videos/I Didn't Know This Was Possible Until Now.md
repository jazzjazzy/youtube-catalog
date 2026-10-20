---
title: "I Didn't Know This Was Possible Until Now"
video_id: LqN_ItMqovA
channel: "[[channels/AI LABS]]"
uploaded: 2026-03-13
processed: 2026-07-05
duration: "11:43"
url: https://www.youtube.com/watch?v=LqN_ItMqovA
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [mcp-context-window-optimization, ai-coding-agent-tooling]
tools: [Claude Code, MCP2CLI, Docker, Supabase, GitHub, Puppeteer, Context7, Cursor, Next.js, TOON]
llms: []
protocols: [MCP, REST, OpenAPI]
transcript: true
tags: [youtube, ai-automation]
---

# I Didn't Know This Was Possible Until Now

![thumbnail](https://i.ytimg.com/vi_webp/LqN_ItMqovA/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=LqN_ItMqovA) | 📅 Uploaded [[uploaded/2026-03-13]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Connecting many MCP servers bloats a coding agent's context window with unused tool descriptions and large raw outputs. MCP2CLI converts MCP servers (and OpenAPI/REST APIs) into bash-callable CLI commands at runtime, keeping tool schemas and outputs out of context until explicitly needed, with 1-hour caching for speed. The host walks through connecting Supabase, GitHub, Puppeteer, and Context7 (78 tools total) to Claude Code, building an app incrementally, and shows why Skills beat claude.md for teaching an agent to actually use the tools — plus a genuinely new capability: piping large MCP output to a file and using grep instead of dumping it into context.

**Watch this if:** you connect more than a couple of MCP servers to a coding agent and are tired of context bloat, slow responses, or the agent ignoring tools it doesn't remember it has.

## Key Takeaways
- The MCP context problem has two parts: (1) every connected MCP's tool schemas sit in the context window whether used or not, and (2) MCP tool *outputs* also land directly in context, even when huge.
- Prior attempted fixes each had gaps: Docker's "code mode" (agents write JS that calls MCP tools directly) solved schema bloat but locked users into Docker-configured MCPs with local/remote limits and no way to save custom tools as functions; Anthropic's own paper-driven approach (convert every tool to a TypeScript file) requires manually converting and validating each tool; Claude Code's native CLI flag for on-demand tool loading still leaves large outputs sitting in context; other CLI-conversion tools (e.g. CLI Hub) convert at build time, so they don't auto-reflect upstream MCP changes.
- MCP2CLI converts MCP servers into bash commands at *runtime* (built on the same MCP Python SDK every MCP server uses), so any change to the underlying MCP is automatically reflected — with a 1-hour TTL cache so repeated calls stay fast without sacrificing that runtime flexibility.
- It also exposes any OpenAPI/REST API through the same CLI interface, so tools without an MCP server at all can still be used the same way — and it handles secrets safely by referencing environment variables, file paths, or a secret manager instead of putting tokens in command-line arguments.
- In the demo, connecting Supabase, GitHub, Puppeteer, and Context7 via MCP2CLI yielded 78 tools total, verified by asking Claude to confirm the connections.
- Skills beat claude.md for guiding an agent: a Skill's description loads directly into the agent's context so it already knows what's available and when to use it, versus claude.md instructions the agent may or may not read/follow — the team had Claude generate one skill per connected MCP describing its tools and usage.
- A real bug found during the build: Claude used a deprecated Next.js middleware pattern for session refresh (should use the newer proxy pattern) — fixed only after explicitly pointing it out and telling the agent (via claude.md) to check Context7 documentation before writing code.
- Puppeteer MCP testing worked for catching real UI bugs an agent's own click/scroll interaction surfaces that static review can't, but it couldn't maintain session/browser state across tool calls (each call spins up a fresh browser instance) — Claude's own browser extension retained session state better for that kind of end-to-end testing, because MCPs run as persistent processes that maintain state across a session.
- The output-format options (JSON, raw, and TOON — a compact indentation/CSV-style format that beats JSON/YAML on token count) plus a claude.md instruction to redirect large MCP outputs (e.g. Context7 docs) to a file and grep it instead of loading it into context — mirrors Cursor's context-editing workflow (treating MCP results as files), but only became possible for other agents because MCP2CLI treats MCP results as bash output rather than native tool-call context.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent the whole workflow is built around; configured via claude.md and Skills to use MCP2CLI-converted tools correctly.
- [[topics/MCP2CLI]] — the tool at the center of the video: converts MCP servers (and OpenAPI/REST APIs) into runtime-cached bash CLI commands, keeping schemas and outputs out of context until needed.
- [[topics/Docker]] — Docker's "code mode" is discussed as the prior best solution (agents write JS calling MCP tools directly) and contrasted with MCP2CLI's flexibility.
- [[topics/Supabase]] — connected via MCP2CLI as the backend for the demo app; Claude used it to create the project, set up auth, and add tables.
- [[topics/GitHub]] — connected via MCP2CLI for version control.
- [[topics/Puppeteer]] — connected via MCP2CLI for automated browser testing of the demo app's chat UI; found to lose session state across tool calls.
- [[topics/Context7]] — connected via MCP2CLI to ground the agent in up-to-date documentation; used to fix the deprecated Next.js middleware bug.
- [[topics/Cursor]] — cited as the origin of the context-editing workflow (treating MCP results as files, using grep) that inspired MCP2CLI's file-piping approach.
- [[topics/Next.js]] — the demo app's framework; Claude initially used a deprecated middleware pattern for session refresh instead of the current proxy pattern.
- [[topics/TOON]] — the token-efficient output format MCP2CLI supports, used for Context7 responses to avoid dumping large docs into context.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — the core protocol whose context-bloat problems (tool schema and output bloat) this entire video addresses.
- [[topics/REST]] — MCP2CLI also exposes plain REST APIs through the same CLI interface as MCP servers.
- [[topics/OpenAPI]] — cited alongside REST as another API type MCP2CLI can wrap without a native MCP server.

## ✅ Action Items
- If connecting more than a couple of MCP servers to Claude Code, try MCP2CLI instead of relying on native MCP tool loading to cut context bloat.
- Ask your agent to generate a Skill (not just a claude.md note) for each connected MCP, describing its tools and when to use them.
- Add a claude.md instruction to redirect large MCP tool outputs to a file and use grep for extraction instead of loading everything into context.
- Get access tokens generated and configured via environment variables or a secrets file before connecting an MCP, to avoid the tool erroring out.

## 🔗 Related Videos
- [[videos/The Best MCP Servers of 2025]] — shared: Claude Code, Context7, Cursor, Docker
- [[videos/I Tried the Open Source ElevenLabs Alternative (Voicebox)]] — shared: Claude Code, Cursor, Docker, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Cursor, GitHub, MCP
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Cursor, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude Code, Docker, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude Code, GitHub, MCP, Supabase
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Claude Code, Docker, GitHub, MCP
- [[videos/Suna The FREE Open Source Alternative to Manus AI]] — shared: Docker, Next.js, REST, Supabase

## Timeline
- `0:00` — Intro: the MCP context bloat problem and prior attempted fixes (Docker code mode, Anthropic's TypeScript-conversion approach).
- `1:29` — MCP2CLI introduced: converts MCP servers into bash CLI commands.
- `2:22` — Why runtime conversion beats build-time conversion (auto-reflects upstream MCP updates); 1-hour TTL caching for speed.
- `3:11` — Also wraps OpenAPI/REST APIs through the same CLI interface; secure secret handling via env vars/file paths/secret managers.
- `3:46` — Token-efficiency benchmark using tiktoken backing up the tool's claims.
- `5:19` — Demo setup: connecting Supabase, GitHub, Puppeteer, and Context7 via MCP2CLI, 78 tools total.
- `7:00` — Real bug: deprecated Next.js middleware pattern, fixed via Context7 lookup after being flagged.
- `8:07` — Skills vs. claude.md: why Skills' loaded descriptions beat hoping the agent reads instructions.
- `8:38` — Puppeteer MCP testing catches a UI bug but can't maintain session state across tool calls; Claude's browser extension preferred for that.
- `9:35` — Output formats (JSON/raw/TOON) and redirecting large MCP output to files with grep, inspired by Cursor's context-editing workflow.

## Transcript
<details>
<summary>Full transcript</summary>

These past two months, the AI community has already realized that MCPs have a huge problem. And due to this, the community has actually come up with some solutions. But all of the solutions have huge gaps. A while back, we made a video on Docker's solution, which we considered the best solution to the MCP problem until now. Docker released code mode, which lets agents write JavaScript code that calls MCP tools directly. And this solved the problem where MCP tools consume a lot of context by having the tool and description exposed in the context window. So, if you are working with a lot of MCPs, your context window will be bloated with unnecessary tools, out of which most of them aren't even needed most of the time. But with the Docker MCP gateway, you were locked into the MCPs Docker had configured, and there were limits on local and remote MCPs. Also, you weren't able to save those custom tools as functions.

All of this was triggered when Cloudflare identified this issue and proposed a solution to have these tools exist as executable code, rather than having them sit in the context window. Anthropic, who were the original architects of this protocol, acknowledged this gap in their product and followed up by releasing a paper highlighting this exact issue. After this, people started taking this problem seriously and started exploring solutions. But their solution of converting every tool into a TypeScript file also has gaps. With a lot of MCPs connected, you have to convert each one to code individually, and you also need to spend a lot of time to make sure that none of them fail in the process. But since this became an acknowledged problem, people are still trying to bring out better solutions. And this is when we found this new tool called MCP2CLI.

MCP2CLI solves the context bloat problem that MCPs have by actually turning all of the MCP servers into CLI tools that you can run through bash commands. Now, we primarily use Claude Code in our team, and it actually has a CLI flag that aims to solve a part of this problem. That tool solves the initial MCP context bloat problem by not exposing all of the tools up front in the context window. But it allows Claude Code to dynamically load each tool as needed. But that still leaves out the other issue in cloud code. As you probably know, MCPs return their outputs directly in the context window. And in case there is a large output returned by the MCP tool, it remains in the context window anyway, leading to unnecessary context window bloat.

Now, you might also have heard about other open-source tools such as CLI hub that target the same problem, but they are inefficient because they convert them at build time and not at run time. So, what does run time conversion actually mean? It means the tool gets converted into a bash command at the moment it's actually called. Now, this might seem all right, but what happens when the original MCP itself gets updated? Because this tool builds up its MCP tools at run time, any change in the actual MCP is automatically reflected in the converted tool. This wouldn't have been possible if we were building tools at build time. In that case, we would have had to manually fetch and update the tool ourselves every single time. But, you might think that converting the same tool every time it's called would make repeated calls slow. That's where the caching mechanism comes in, which they've built into the tool. It saves all of the MCP tools in a cache with a 1-hour time to live by default. So, all of the frequently used MCP tools go right into a cache and stay there for 1 hour. And from there, the agent can get the tools with faster retrieval without sacrificing the run time flexibility.

Now, this tool is built right on top of the MCP Python SDK, the same one every MCP server actually uses underneath. So, with all of the MCP tool calls it runs, it simply executes them as bash commands and only injects the response into the agent's context window when it's asked to. It also handles open API and REST APIs through the same CLI interface, meaning any existing API that doesn't have an MCP server can still be used the exact same way. Without this tool, you're limited in what type of MCPs you can actually connect to. Other similar solutions don't usually give you flexibility to work with all types of MCPs all in one place. To back up their claims on token efficiency, they ran an automated test suite using tiktoken, the Python library for counting tokens. When they tested it, the tool was much cheaper and had much faster execution. So, you don't just have to take our word for this one. This one actually had the numbers behind it.

You can either install it on your system using pip or run it without installing. We chose to run it without installing because it keeps the working environment clean. And they've also provided a skill that helps agents work with this tool better. It lays out the core workflow and gives examples of the bash commands for different tasks like authentication and caching that your agent doesn't have the context for.

Just like you, we also want to get rich, and one way is to notice a gap in the market, and that's when we came across this golden idea. Grinder, but for horses. But, jokes aside, building large-scale products requires a lot of MCP tools because they have a lot of dependencies and they bloat the context window fast. We connected the agent to the Superbase MCP using MCP to CLI because that was the back-end infrastructure we were using. Now, you don't have to configure anything manually because of the skill we installed earlier. That skill handles everything on its own and configures the MCPs for you. But, before installing it headfirst, you need to get the access tokens of whichever MCP you are using. Because, if you don't do so, you'll run into errors like we did, after which we got our access token generated and gave it to Claude to add it. Once configured correctly, you should be seeing the tools available for use.

Now, you might think that if this tool runs as a bash command, it's not safe to have sensitive data like API keys and access tokens in it, because they could be exposed when processes are listed. But, this tool adds a protection layer. It doesn't put sensitive data in the command line arguments. Instead, it handles them through environment variables, or it references a file path where the access tokens are saved, or it uses a secret manager that injects them at runtime. So, it's secure to run.

Similar to the Superbase connection, we connected the GitHub MCP for version control, the Puppeteer MCP for browser testing, and the Context 7 MCP for grounding the agent with proper documentation, so that it works with updated docs. Once all the MCPs were connected, we asked Claude to verify everything. It confirmed that we had all four MCPs connected, 78 tools in total in our case.

Now, once we were actually connected, it was time to start implementing the app incrementally. We started with connecting the client-side code to the Superbase backend. When Claude ran the MCP to CLI command to create the project, we noticed that did not put the access token directly into the tool call. Instead, it referred to our .env.local at the project level for the token. It created the project, set everything up, and added in the logic for connecting in the code. But, we noticed that it used the middleware file for the session refresh logic, and it shouldn't have been using that because it's deprecated. The new version of Next.js used the proxy, and we knew this would give us an error when we actually ran the app. This just shows that connecting tools is not enough to make the agent listen to the tools and actually use them when needed. So, we created a Claude.md and told it to use the Context 7 MCP before writing any code, so this wouldn't happen again. That way it knows it should refer to the context 7 MCP before implementation. Once it had finished adding tables and setting up authentication on Superbase, we pointed out the deprecated middleware warning to Claude so that it could correct it. After we told it to, it finally used the context 7 MCP to pull in the documentation and resolve the issue properly.

But when we were exploring this tool further, we found out that there was a better way to handle these issues than creating a Claude.md file. Skills are better because their descriptions are loaded directly into the agent's context, so it already knows what tools are available and when to use them, rather than us just dumping instructions into Claude.md and hoping it reads them. So we asked it to create a skill for all of the MCPs we had connected. Claude then created skills for each MCP. Each one detailed what tools it had, how to use them, and when to use them. With that in place, we moved to the next problem.

But what we had was purely far from functional. The feedback from the horses told us that they were getting impatient because they were unable to chat directly on the platform. So we asked Claude to make the chat functional for the project on top of the UI. When we tested it ourselves, the messages didn't load and only showed a loading screen. So we asked it to use the Puppeteer MCP to test the message flow. We had it check itself because an agent that can click and scroll and interact with its own UI catches things that static code review never can. For testing purposes, it created two users, but it couldn't maintain session data across tool calls since each one spun up a new browser instance. The number of tools it used and the time it took to work in a headless browser made us realize something. A better option would be to just let the MCP handle it. It was much faster and took far less time than the 7 minutes we wasted on such a simple task. We prefer using Claude's own browser extension that works better with more capabilities and is able to retain sessions better for end-to-end testings like these. And MCPs run as persistent processes, which is why they're able to maintain state across the entire session.

This tool also provides control over the output format like JSON and raw output. It also supports tune, the token efficient coding format for LLM consumption. When we work with MCPs like context 7, they usually return a huge chunk of output directly into the context window. To prevent that, we added in the cloud.md file that whenever it uses the context 7 MCP, it should use the tune format for output. It's an efficient format because it combines indentation and CSV style lists compacting large information into much smaller chunks as compared to JSON and YAML. This way you don't waste any tokens unnecessarily.

But the biggest unlock came from something that wasn't even possible when MCPs were handled natively by agents. If you remember, Cursor released a context editing workflow inside its product. They treated MCP results as files and let the agent use bash scripts like grep for pattern matching to extract data. We covered that in our previous video. We tried to implement this idea in other coding agents, but since MCPs are handled natively by agents, we weren't able to get much out of it. But now with this CLI, it's possible because MCPs are treated as bash command tools. So we added an instruction in the cloud.md file that whenever any MCP tool produces a large output, instead of loading it into the context window, it should redirect it to a file at the path we specified. We were tracking this project's progress through a progress.json file. After adding the instruction, we asked Claude to implement one feature from the list. It then used the context 7 MCP for tool calls, but instead of dumping the output to the context window, it piped it to a file and used grep to extract the data and complete the implementation.

The cloud.md file with all the best practices to use this tool is available in AI labs pro. For those who don't know, it's our recently launched community where you get ready-to-use templates that you can plug directly into your projects for this video and all previous ones. If you found value in what we do and want to support the channel, this is the best way to do it. The link's in the description. That brings us to the end of this video. If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below. As always, thank you for watching and I'll see you in the next one.

</details>
