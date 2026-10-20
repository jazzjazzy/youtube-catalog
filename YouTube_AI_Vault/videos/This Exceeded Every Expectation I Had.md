---
title: "This Exceeded Every Expectation I Had"
video_id: iC9loBJjduM
channel: "[[channels/AI LABS]]"
uploaded: 2026-01-15
processed: 2026-07-06
duration: "11:04"
url: https://www.youtube.com/watch?v=iC9loBJjduM
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [ai-context-window-management]
tools: [Cursor, Claude Code, Claude Skills, Claude Browser Extension, ZenRows]
llms: []
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# This Exceeded Every Expectation I Had

![thumbnail](https://i.ytimg.com/vi_webp/iC9loBJjduM/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=iC9loBJjduM) | 📅 Uploaded [[uploaded/2026-01-15]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> AI LABS breaks down Cursor's five new native "dynamic context discovery" methods for managing AI coding context, then shows how to replicate each one in Claude Code today using CLAUDE.md instructions, a context folder, Claude Skills, and a hidden `--enable-experimental-mcp-cli` flag. The goal in every case is the same: keep only what's relevant in the context window, offload everything else to files the agent can search on demand.

**Watch this if:** you're hitting context-window exhaustion or degraded output quality in Cursor or Claude Code from large MCP tool responses, repeated auto-compaction, bloated MCP tool lists, or noisy terminal output.

## Key Takeaways
- Cursor's core principle: providing fewer, more relevant details in context produces better model output than dumping everything in — this is "dynamic context discovery," essentially structured note-taking that excludes information not needed right now.
- Method 1 — long MCP tool responses to files: instead of truncating (and losing) large MCP responses, save them to files (e.g. a CLAUDE.md rule to save any MCP response over 50 lines to a file via an echo command) so the agent can re-read them as many times as needed without repeated tool calls.
- Method 2 — chat history as retrieval: rather than relying purely on auto-compaction summaries (which lose detail with repeated compression), save full session transcripts to history files per session, giving the model a reference to recover details a summary might have dropped.
- Method 3 — Agent Skills for context-efficient capability access: only a skill's name and description sit in static context; the full scripts/instructions are pulled in on demand (progressive disclosure). In the host's project, 5 configured Claude Skills consumed only ~0.2% of total context. Claude Skills can also be manually triggered via slash commands.
- Method 4 — dynamic MCP tool discovery: Cursor's tested approach (sync tool descriptions into per-MCP folders so only tool names sit in context, looked up on demand) reduced MCP-related context usage by 46.9% in their testing, and also lets the agent notice and report an MCP that's disconnected/needs reauthentication instead of silently forgetting it.
- Claude Code has an equivalent for this: an experimental, currently hidden `enable-experimental-mcp-cli` flag that removes all MCP tool schemas from the context window up front — Claude instead uses a middle "MCP CLI" bash layer to search, inspect, and invoke MCP tools on demand (the MCP servers stay connected; they're just not pre-loaded into context).
- Method 5 — terminal sessions as files: instead of letting raw command output flood context, a CLAUDE.md rule logs both stdout and stderr from commands (e.g. npm scripts) to timestamped files in a terminal folder, then greps the last ~20 relevant lines out instead of re-running commands to see errors again — saving time like avoiding a 2-minute test re-run just to see an error you already saw.

## 🛠 Tools & Software
- [[topics/Cursor]] — the coding tool whose newly published article on native dynamic context management methods is the basis for the whole video.
- [[topics/Claude Code]] — where the host reimplements each of Cursor's five context methods via CLAUDE.md instructions, a context folder, and an experimental MCP CLI flag.
- [[topics/Claude Skills]] — demoed as Claude's progressive-disclosure mechanism for exposing capabilities (name/description only in context) without bloating the window, and its slash-command trigger option.
- [[topics/Claude Browser Extension]] — the tool-heavy Chrome extension whose "read page" tool responses were bloating context until the host added a rule to save large MCP responses to a file instead.
- [[topics/ZenRows]] — sponsor; a web-data-extraction and anti-bot-bypass tool that returns structured JSON/Markdown output for AI pipelines.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — the Model Context Protocol whose large tool responses and tool-schema bloat is the problem all five context-management methods are designed to solve.

## ✅ Action Items
- Add a CLAUDE.md rule that saves any MCP tool response over ~50 lines to a file in a dedicated context/MCP folder instead of letting it sit in context.
- Have Claude log a running chat/session history to per-session files so a compacted summary isn't your only source of truth for past decisions.
- Move any repeated capability into a Claude Skill so only its name/description sit in static context, and consider exposing it as a slash command too.
- Try Claude Code's experimental `enable-experimental-mcp-cli` flag if MCP tool schemas are consuming too much of your context window.
- Add a CLAUDE.md rule to redirect terminal/command output (stdout+stderr, timestamped) into log files, then have Claude grep them instead of re-running long commands to see an error again.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Claude Skills, Cursor, MCP
- [[videos/Claude Code Can Now Control Your Browser (Thanks to Vercel)]] — shared: Claude Code, Cursor, MCP
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: Claude Code, Cursor, MCP
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude Code, Claude Skills, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Browser Extension, Claude Code, MCP
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude Code, Claude Skills, MCP
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude Browser Extension, Claude Code, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude Code, Claude Skills, MCP

## Timeline
- `0:00` — Intro: good models alone don't determine code quality — how you manage context matters just as much.
- `1:19` — Cursor's core principle: dynamic context discovery, i.e. structured note-taking that excludes irrelevant/confusing information.
- `1:45` — Method 1: saving long MCP tool responses to files instead of truncating them, demoed via the Claude Chrome extension.
- `3:01` — Sponsor: ZenRows web data extraction and anti-bot bypass.
- `3:55` — Method 2: saving chat history/session transcripts to files as a backstop against lossy auto-compaction summaries.
- `5:19` — Method 3: Agent Skills and progressive disclosure — only name/description in static context; Claude Skills' slash-command triggering.
- `7:00` — Method 4: dynamic MCP tool discovery via per-MCP folders, cutting MCP context usage by 46.9% in Cursor's tests.
- `8:10` — Replicating this in Claude Code via the hidden `enable-experimental-mcp-cli` flag and the MCP CLI middle layer.
- `9:04` — Method 5: routing terminal session output (stdout/stderr) to timestamped log files and using grep instead of re-running commands.
- `10:51` — Closing.

## Transcript
<details>
<summary>Full transcript</summary>

With the advancement of AI and the increasing power of each new model being released, the way we produce code has been completely transformed. There are now many tools specialized for coding like Claude Code, Cursor, Antigravity, and others, each with its own unique capabilities. But good models alone don't determine the quality of the code you produce — how you use the tool and manage context matters just as much. All of these tools have some inherent mechanism for context engineering, but Cursor just made a major push for a new approach, building it natively into the app itself. As I went through their article, I realized these principles are genuinely strong — these ideas can be applied broadly to any platform you use to build applications.

Context management has always been critical when working with AI agents because good context management determines output quality. Cursor implemented context-management features directly into their product and released an article about it — their observation is that to get good results from models, it's better to provide as few details as possible in the context window. The less information the model receives at once, the less it has to process, meaning less confusion and more focus on the task at hand, because only relevant information is included. This is what they call dynamic context discovery: structured note-taking, where information not needed right now should not be in the context window. Excluding potentially confusing or contradictory details significantly improves the quality of an agent's responses. Cursor's release adds five dynamic context-management methods rolling out soon — and even though Cursor is shipping this as a product update, these principles are widely transferable to all AI agents.

The first method: long tool responses should go into files. MCPs often return large responses that stay in the context window, and not all of that information is always needed. Cursor noted that most coding tools' common approach — truncating long MCP responses — leads to data loss, potentially removing information that's actually necessary. Claude's Chrome extension is a very tool-heavy extension, and just a few prompts can fill up context by loading a huge chunk into the window. So I added an instruction in the CLAUDE.md file: any MCP tool response greater than 50 lines must be saved to an MCP folder within the context folder by running an echo command in the terminal. When I ran the Chrome extension to analyze the UI of a landing page, whenever Claude hit a tool like "read page" that would significantly bloat context, it saved the MCP response to a file for further reading, using it to analyze the whole page and give me a report. This workaround improved the accuracy of the tool-response analysis by letting Claude re-read the file as many times as needed, eliminating repetitive tool calls — when data from previous MCP calls is needed, Claude reads it directly from the context folder instead of making new tool calls, saving significant time.

(Sponsor break: ZenRows — a web-data-extraction tool that handles anti-bot bypass and returns clean, structured JSON/Markdown output, aimed at AI startups, data teams, and automation builders who don't want to babysit scraping infrastructure.)

We know the summarization step that fires when context fills up is messy and loses a lot of information. Most tools, including Cursor and Claude Code, trigger a summarization/compaction step and start the session fresh with the summary as a starting point — but hit "compact" again and again, and the summary starts forgetting details that might matter to you even though the model's summary missed them. There's only so much control you have over auto-compaction, and repeated compression loses crucial information over time. Cursor's solution (method 2) is to save all previous chat history as a file for the agent to reference later — when a specific prompt can't be answered from the summary alone, the previous transcript serves as a knowledge base the model can pull from to recover lost detail, until Cursor's own implementation rolls out fully. The host implemented this in Claude Code by adding a CLAUDE.md instruction to update chat history after each turn, documenting key decisions and steps into a history folder inside the context folder, with each file named after its session — so at the end of every task, Claude documents the session into its corresponding history file, giving the context folder a detailed record of everything done across all sessions.

Method 3: Agents were given skills to manage the context problems MCPs cause. The whole purpose of skills is to give agents a better ability to use their own capabilities by guiding them through scripts and instruction files, reducing context bloat via progressive disclosure. Anthropic was first with this idea — giving agents a set of instructions, scripts, and resources they can discover and use to perform better at specific tasks — and open-sourced Agent Skills as a standard others could implement; Codex, Gemini, and others followed, and eventually Cursor did the same. Cursor Skills bundle the same kind of executables/scripts into a single skill the agent can use; only the skill's name and description sit in static context, and once discovered the agent pulls the skill's contents on its own using grep and Cursor's semantic search (its own embedding model and indexing pipeline, rather than plain regex-based grep). Claude Skills work similarly — only name and description are exposed in context regardless of how many files the script uses, preventing context bloat. In the host's project, 5 configured skills consumed only about 0.2% of total context, leaving much more room for actual work. What's different with Claude is that skills can also be triggered manually via slash commands, addressing complaints that skills weren't always loading on demand properly.

Method 4: MCPs contain a lot of tools, all exposed in the context window, bloating it unnecessarily. Cursor emphasized that it's the coding agent's responsibility, not the MCP server's, to fix this bloat — their solution was dynamic context discovery by syncing tool descriptions into per-MCP-named folders, so the agent only receives tool names up front and looks up any specific tool's details from the folders when needed. In Cursor's own testing, this dynamic discovery of MCP tools reduced usage by 46.9% — a huge difference for long-running systems — and it also helps when an MCP server accidentally disconnects or needs reauthentication: instead of the system silently forgetting those tools, the agent can now notify the user that reauthentication is required. Claude also has an advanced search tool addressing this exact problem via flags telling Claude whether to load a tool or not — implementing Cursor's exact dynamic-discovery idea, but limited to the developer platform for those building directly with the API; you can't modify how MCPs are exposed inside Claude Code itself since Anthropic built that in. While looking for a way to replicate this in Claude Code, the host found a hidden flag: without it, all connected MCP tools were exposed in Claude Code's context; setting `enable-experimental-mcp-cli` removed all those tools from the context window, freeing up the space they'd occupied — without actually disconnecting the MCPs. The only difference is they're no longer exposed up front; instead of putting all tool schemas into context, Claude uses a middle bash layer called MCP CLI that handles all MCP-related tasks — searching, getting information, and invoking tools — so whenever a task needs an MCP tool call, Claude goes through MCP CLI instead of the usual method, executing tasks as normal just through this middle layer.

Method 5: reporting terminal errors is hard in Cursor because of its limited terminal access — if the terminal showed an error, you had to manually add it to chat to get it fixed. Cursor's solution is, again, moving terminal sessions to files: whenever you ask a question, it references history files and uses grep to extract the relevant output. Since server logs are usually long-running and noisy, using a grep-based task is more efficient, letting the agent pattern-match — an idea borrowed from CLI-based coding agents, which normally inject full command output into context by default just like Claude Code and others do. Even though Claude already handles this reasonably intelligently on its own, you can manage it further with CLAUDE.md instructions telling it to write all terminal logs into a file in a terminal folder inside the context folder. So whenever Claude runs, say, an npm command, it runs a special command that logs both the output stream and input stream to document files — "2" representing stderr and "1" representing stdout — written to the terminal folder with a timestamp. Whenever it needs to search through them, it uses a grep command with a specific pattern and loads the last ~20 lines to extract only what matters. When the host tested a development server this way, Claude kept writing terminal runs to files per the CLAUDE.md rule, then after running the server, referred back to the log files to figure out what was causing an issue and fixed it. Even though this add-on might seem insignificant for immediate work, it's very useful for referring back to your app's behavior later — for instance, when the host needed to identify which service was crashing his app, he simply told Claude to refer to the existing test logs instead of rerunning the tests, saving a 2-minute test-suite rerun just to reproduce an error he'd already seen.

That brings us to the end of this video. If you'd like to support the channel, you can do so with the Super Thanks button below. Thanks for watching, and I'll see you in the next one.

</details>
