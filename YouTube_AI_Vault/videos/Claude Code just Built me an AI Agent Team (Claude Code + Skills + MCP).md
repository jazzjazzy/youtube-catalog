---
title: "Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)"
video_id: 0J2_YGuNrDo
channel: "[[channels/Grace Leung]]"
uploaded: 2025-12-16
processed: 2026-07-06
duration: "17:23"
url: https://www.youtube.com/watch?v=0J2_YGuNrDo
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [ai-agent-team-orchestration]
tools: [Claude Code, Claude Skills, VS Code, Cursor, GitHub, Notion, Ahrefs, Google Analytics]
llms: [Claude, Nano Banana]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)

![thumbnail](https://i.ytimg.com/vi_webp/0J2_YGuNrDo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=0J2_YGuNrDo) | 📅 Uploaded [[uploaded/2025-12-16]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Grace Leung builds a five-agent marketing team inside Claude Code for a fictional agency: a content strategist (plain context file), a presentation specialist (official document-creation Skills), a data analyst (MCP-connected to GA4), a social media specialist (custom brand-specific Skills plus Notion MCP), and an SEO content specialist — then wires up routing rules in CLAUDE.md so Claude itself acts as team lead, delegating a multi-step content-research-to-blog-to-deck workflow across all of them automatically.

**Watch this if:** you keep copy-pasting between separate Claude Projects/ChatGPT chats and want a single Claude Code workspace where multiple purpose-built agents share context and hand off work to each other.

## Key Takeaways
- Claude Projects-style agents are siloed — you manually copy-paste between them and act as coordinator. Claude Code agents instead share the same workspace/context files, can hand off work to each other, and each get their own token context window, with Claude itself acting as team lead.
- Every Claude Code agent needs three core components defined in one markdown file: its role/responsibilities, its knowledge (workflow details, reusable Skills), and the MCP tools it has access to — give each agent specific, non-overlapping roles to minimize conflicts.
- Four ways to access Claude Code: local terminal (most complete experience, now via Anthropic's native installer), an IDE extension (VS Code/Cursor), the Claude web app (requires a linked GitHub repo), or the Claude Desktop app (used throughout this video, though agent creation still requires dropping into the embedded terminal via `/agents`).
- Setup always starts with a dedicated project folder plus business context, then asking Claude to generate a CLAUDE.md project system prompt and folder structure before creating any agents.
- Agent 1 (content strategist) uses only a context file — created via `/agents` → create new agent → project-level → generate with Claude — and is asked to build its own reusable templates (campaign plan, content brief, content strategy) directly into the right folders.
- Agent 2 (presentation specialist) adds official Anthropic Skills, installed via `/plugin` to register the official skills GitHub repo and install the document-creation and example skills, then builds branded slide decks from a data folder with consistent brand colors.
- Agent 3 (data analyst) adds MCP: import existing Claude Desktop MCP servers into Claude Code via `mcp add-from-claude-desktop` from a local terminal (the embedded terminal doesn't support this), then connect to GA4 to build interactive branded HTML dashboards, exportable to PDF.
- Agent 4 (social media specialist) uses a custom-built Skill (extending Anthropic's official canvas-design skill with brand colors/logo/style) plus a Notion MCP connection to generate on-brand social visuals and schedule posts directly to a Notion content calendar.
- The full team only becomes an orchestrated system once CLAUDE.md is updated with agent-routing rules (which agent handles which trigger phrases, plus multi-agent workflow instructions) — demoed with one prompt that chains content research → SEO blog post → presentation deck across three different agents automatically.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the platform the entire five-agent team is built in, including project setup, `/agents` configuration, `/plugin` skill installation, and MCP import.
- [[topics/Claude Skills]] — official document-creation and canvas-design skills are installed and later extended into custom branded skills (branded social visuals, keyword research, blog writer, brand voice).
- [[topics/VS Code]] — used as the IDE to inspect the generated folder structure, CLAUDE.md, and agent files side by side with Claude Code.
- [[topics/Cursor]] — mentioned as an alternative IDE for running the Claude Code extension.
- [[topics/GitHub]] — hosts Anthropic's official Skills repository and MCP servers repository referenced for installation, and is required to use the Claude web app's code tab.
- [[topics/Notion]] — connected via MCP so the social media agent can schedule branded posts directly to a Notion content calendar.
- [[topics/Ahrefs]] — connected via MCP and used by a custom keyword-research skill for the SEO content specialist.
- [[topics/Google Analytics]] — connected via a GA4 MCP server so the data analyst agent can pull live website performance data into a dashboard.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model powering every agent in the team and acting as the overall team-lead orchestrator.
- [[topics/Nano Banana]] — suggested as an alternative image-generation model Claude could call for more polished social visuals than its own image output.

## 📡 Protocols & Standards
- [[topics/MCP]] — used to connect agents to Notion, Ahrefs, and GA4 for live external data and actions, imported via `mcp add-from-claude-desktop`.

## ✅ Action Items
- Start every Claude Code agent project with a CLAUDE.md file generated from your real business/brand context, before creating any agents.
- Give each agent a narrow, non-overlapping role (content strategist, presentation specialist, data analyst, etc.) to avoid conflicting outputs.
- Install official Anthropic Skills via `/plugin` rather than hand-building common capabilities like document or slide creation from scratch.
- Import your existing Claude Desktop MCP servers into Claude Code with `mcp add-from-claude-desktop` run from your computer's local terminal.
- Extend an official skill (e.g. canvas design) into a custom brand-specific skill by feeding Claude your brand colors, logo, and visual examples.
- Once you have multiple agents, explicitly update CLAUDE.md with routing rules and trigger phrases so Claude can delegate multi-step workflows across agents automatically.

## 🔗 Related Videos
- [[videos/Claude Code Clay Makes Lead Generation Actually Fun]] — shared: Claude, Claude Code, Claude Skills, MCP
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Cursor, GitHub, MCP
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Googles New Tool Just 10xd Claude Code]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude, Claude Code, Cursor, GitHub

## Timeline
- `0:00` — Intro: why Claude Code beats siloed Claude Projects for building an AI work team.
- `0:33` — What makes Claude Code different: shared workspace, agent hand-offs, Claude as team lead.
- `1:44` — Four ways to access Claude Code: terminal, IDE extension, web app, desktop app.
- `2:33` — Setting up Claude Code for Desktop: project folder, business context, CLAUDE.md generation.
- `3:36` — Agent 1 build: content strategist using only a context file, plus self-generated templates.
- `7:15` — Agent 2 build: presentation specialist using official document-creation Skills via `/plugin`.
- `9:23` — Agent 3 build: data analyst connected to GA4 via MCP for branded interactive dashboards.
- `11:30` — Agent 4 build: social media specialist using a custom brand-visuals Skill plus Notion MCP.
- `13:45` — Setting up agent routing rules in CLAUDE.md so Claude knows who to delegate to.
- `14:34` — AI team orchestration demo: a single prompt chaining research → blog post → presentation deck across agents.

## Transcript
<details>
<summary>Full transcript</summary>

I use Claude more than any other AI, but even I dismissed Claude Code as just for developers, and I was wrong. After using it myself, I am completely sold, and this is too powerful to ignore if you want to use AI to build a system and do work for you end to end, not just chatting and copy-pasting. So in this video I'll share how to get started with Claude Code, even if you don't use it for coding, and most importantly, how to use it to build an AI work team and system that you can actually use.

So why is Claude Code even needed if Claude is already so powerful? Most people use Claude Projects with custom instructions to turn Claude into AI agents, but they are siloed — you end up copy-pasting between them, you are the coordinator. With Claude Code it's different: these agents share the same workspace, access to the same context file, they can talk to each other and hand off work automatically, each with their own token context window. Claude now becomes the team lead — you give direction, they execute together, and that's what we're building today.

Each Claude Code agent you create needs at least three core components, all defined in one single markdown file: their role and responsibilities, their knowledge (workflow details, reusable Claude agent skills), and the MCP tools they have access to. For this demo, we'll build a five-agent work team, with Claude as our main agent acting as team lead to coordinate between them. A bonus tip: when designing your AI teammates, give them specific, non-overlapping roles to minimize potential conflicts.

There are four main ways to access Claude Code. First, the local terminal — the raw method, giving the best experience; Anthropic just launched a native installer making this easy. Second, an IDE extension — add Claude Code to VS Code or Cursor and run it alongside your project file structure. Third, the Claude web app, where you click the code tab and run Claude Code in the cloud, but it requires linking a GitHub repository. Fourth, the Claude Desktop app, which has Claude Code built in — this is what we'll use today. Whatever way you choose, I still recommend installing Claude Code through the terminal first, since it gives the most complete experience with all commands and features fully working.

Since we're running Claude locally, the first thing is to set up a local project folder — think of it as a dedicated workspace. Let's say I run a marketing agency and I'm setting up the team system: create a folder called "marketing team," and include all useful business context about the agency and brand. Then access Claude Code — for our case, the Claude Desktop app, navigating to Claude Code, picking local as the environment and the folder we just created. Before creating any agents, the very first step is to initiate the project by creating a CLAUDE.md file — like a project system prompt giving Claude all the important context about what it should know. Ask Claude to read the business context file, create a CLAUDE.md file, and build the necessary folder structure. Immediately, Claude creates all the folders for this agency brand, and we can open an IDE to double-check all the folders and the CLAUDE.md file.

Now let's build our first teammate, the content strategist — the simplest version, no Claude Skills, no MCP tools, just the basic context file. A key feature of Claude Code is the slash command — type slash to trigger built-in shortcuts, mostly for coding purposes. For agent creation, we need the CLI terminal because agent commands aren't fully supported in the chat interface yet. Type `claude` to initiate a session (the chat interface is just a wrapper around this raw session), then type `/agents` to trigger the built-in agent configuration. Select create new agent, pick project-level agent, then generate with Claude — describe what this agent will do (a content strategist agent that does web search and prepares content research documents in markdown files), select the tools and default Claude model, and we're done. Whenever you want to call this agent, just tag its name in any Claude Code session. Checking in VS Code, you'll see the agent created under the `/agents` folder — just a markdown file containing the system prompt defining its role and capabilities, which you can always edit.

Since this agent will use different strategy templates, we can ask it to create all the necessary templates it will use — and Claude not only creates the files but puts them in the right folder according to the team system structure, no copy-paste needed. Immediately, templates like campaign plan, content brief, and content strategy templates are created under the templates folder, in great detail. To use this agent in chat, tag it or use plain language specifying the agent name and ask it to research the latest SEO challenges and prepare a content brief — it triggers web searches and reads the content brief template it just created, and after a few minutes the content brief is ready, comprehensive and following everything stated in the template. So don't just create an agent — always give it context, templates, resources, and standard rules to follow, so it consistently produces quality output like this.

[Sponsor section: HubSpot/SurveyMonkey "In AI We Trust" report on consumer trust in AI-generated content.]

Let's create our second agent, a presentation specialist, this time adding Claude Agent Skills — reusable instruction manuals that tell Claude how to execute tasks. For this agent we'll use the official document-creation skills. Anthropic provides a list of official skills, but they're not prebuilt inside Claude Code, so go to the official skills GitHub repository, and the easiest way is the built-in `/plugin` command inside Claude Code: type `/plugin`, register the official skill repository, and install the document skills (I also recommend installing the example skills to enable all other official skills). Use a prompt to confirm the skills are successfully installed. Then, using the embedded terminal in Claude Desktop and agent configuration mode, create the presentation specialist agent, which transforms data into polished slide decks — I also specified the brand color palette here so it always follows this color tone. With a performance dataset in a data folder, tag this agent and ask it to create a presentation deck for that file (or, in the terminal, simply tag the file path). It triggers the document-creation skills we installed, and after a few minutes creates a 10-slide performance report presentation — quite decent, using our defined color scheme, call-out boxes, charts, and graphs for storytelling. Not the most sophisticated graphics, but ready to present with minimal adjustment. You can drop different datasets/documents/reports into the folder and let Claude scan and load them without uploading manually.

Our third agent is a data analyst, this time adding MCP tools — MCP lets Claude connect to external systems and retrieve live data or context, which is where your AI team becomes truly powerful. First, install the necessary MCP servers and make them available in Claude Code. If you've used Claude Desktop, you probably already have MCP servers connected — the easiest way is to import them through the local terminal (the embedded terminal in Claude Desktop doesn't support the import command). Open the terminal app, `cd` into the project folder, then use `mcp add-from-claude-desktop` to import the servers you want — in this case Notion, Ahrefs, and GA4 (some may require further authentication). Confirm installation by going back to Claude Desktop, opening the terminal, and typing `/mcp` to see all three servers available. Repeat the same agent-creation process for the data analyst, connecting to GA4 through the MCP tool to create polished interactive HTML dashboards, again using the same brand color palette. Testing it to analyze website performance and build a dashboard: it calls the GA4 MCP server to retrieve data and quickly builds a dashboard in the brand color scheme with an executive summary, key metrics boxes, interactive charts, and trend lines — this is where Claude really excels, at strategic storytelling and insights. We can even export this directly as a PDF ready to send to the team.

Let's level up further: create custom skills to make agents even more brand-specific, and build a fourth agent, a social media specialist using a custom skill. Create a custom skill called "branded social visuals" for creating branded social graphics — upload visual examples for Claude, then ask it to read the official canvas design skill and extend it for visual creation with the specified brand colors, layout, and style. This triggers the official skills-creator we enabled, studies the canvas design skill, extends it, and creates a new custom skill following the official structure — a new skill.md file appears in the IDE explorer. Using the same method, you can create more custom skills: a keyword-research skill that calls the Ahrefs MCP, an LLM-optimized blog-writer skill that generates AI-search-friendly blog posts, and a custom brand-voice skill.

The social media specialist agent uses this custom skill plus a Notion MCP: give it topic ideas and ask it to draft post copy with visuals and schedule them on the Notion calendar. It calls the branded social visuals skill for visual creation, then calls the Notion MCP to upload post details to the calendar. All visuals get created under the folder — not super fancy (not Claude's strength), but clearly on-brand using the brand color palette and text/logo. This workflow is 100% working, and you could let Claude use other image-generation models, perhaps Gemini's Nano Banana, for more stunning visuals. Claude also successfully scheduled all posts on the Notion content calendar following the posting schedule, with platform details, posting status, post copy, and hashtags — this is what makes Claude Code so powerful, everything done in about 30 minutes.

We've now built our AI team: four agents shown here plus an SEO content specialist built the same way. Now for the exciting part — watching them work together. But first, Claude needs to know when and who to delegate to, so back to the CLAUDE.md file from the very first step: ask Claude to review all the agents in the workspace and update CLAUDE.md with agent routing rules — instructions telling Claude which agent to call for different tasks and what the trigger phrases are. It adds these routing rules and even a section for multi-agent workflows.

Testing a multi-agent workflow: ask it to do content research about a topic, then create a blog post and a presentation deck based on the research findings — meaning both the blog and the deck depend on the first research task. It starts with content research, calling the content strategist agent to do web search; once that's complete, it moves to blog post creation, delegating to the SEO content specialist, which triggers the keyword-research skill (calling Ahrefs MCP) and then the blog-writing and document skills. Then it moves to the client presentation task, calling the presentation agent, which uses the PowerPoint creation skills. All tasks complete, and Claude, as team lead, gives a summary of all deliverables and the agents used: a detailed content brief backed by research following the predefined format; an impressive blog post following required formats (bullet points, FAQ sections, and a section on common pricing mistakes great for AI search engines) that follows the content brief's structure and talking points at almost 5,000 words; and a presentation deck also using the brand theme and the same research findings — all deliverables coherent and aligned to the same story. This is true AI orchestration in action, using different agents to achieve a bigger task through agentic workflows.

There are still so many possibilities and use cases with Claude Code — let me know in the comments if there are other topics I should cover.

</details>
