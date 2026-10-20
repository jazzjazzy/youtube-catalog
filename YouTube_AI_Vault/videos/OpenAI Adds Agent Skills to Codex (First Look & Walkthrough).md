---
title: "OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)"
video_id: MsJzacfjzp8
channel: "[[channels/JeredBlu]]"
uploaded: 2025-12-22
processed: 2026-07-06
duration: "6:41"
url: https://www.youtube.com/watch?v=MsJzacfjzp8
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [agent-skill-installation, skill-portability]
tools: [Codex, Claude Code, Claude Desktop, Claude Skills, Playwright, GitHub, Bright Data]
llms: []
protocols: [MCP, Agent Skills]
transcript: true
tags: [youtube, ai-automation]
---

# OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)

![thumbnail](https://i.ytimg.com/vi/MsJzacfjzp8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=MsJzacfjzp8) | 📅 Uploaded [[uploaded/2025-12-22]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> OpenAI adopted Anthropic's open Agent Skills spec into Codex just two months after it launched, so most existing Claude skills work in Codex with zero config changes. The video walks through updating Codex, using the built-in `$skill-installer` to pull a GitHub-hosted skill, copying an existing Claude skill folder straight into a `.codex/skills/` directory, and running a real skill (a Playwright skill evaluator) that self-corrects when it hits a Claude-specific file path.

**Watch this if:** you've already built or installed Claude Agent Skills and want to know exactly how portable they are to Codex, and why skills beat MCP for avoiding context bloat and config friction.

## Key Takeaways
- Codex added Agent Skills support by following Anthropic's open Agent Skills spec closely enough that most existing Claude/Claude Code skills work in Codex out of the box, no config changes needed — just update Codex.
- Skills solve context bloat (from MCP servers, long AGENTS.md/CLAUDE.md files) via progressive disclosure: only each skill's name and short description load at startup; full instructions/scripts/reference files load only when the skill is actually invoked.
- A skill package is simple: a required SKILL.md file plus optional scripts, reference files, and assets; Codex can load a skill either when explicitly told to or implicitly when it matches the task (the presenter prefers explicitly invoking skills in both Claude and Codex).
- Codex ships its own skill-creator and skill-installer skills; installing a third-party skill from GitHub is as simple as invoking `$skill-installer` and pasting a URL — arguably easier than adding skills in Claude Code or Claude Desktop.
- Because installed skills add custom prompts/commands to your agent, the presenter built and demoed his own "agent skill evaluator" skill specifically to vet third-party skills for shady commands before trusting them.
- Transferring an existing Claude skill to Codex is as easy as copying its folder into a project's `.codex/skills/` directory (mirroring the existing `.claude/skills/` structure) — no reformatting required.
- Skill portability beats MCP portability: switching an MCP config between Claude and Codex requires converting JSON to TOML, while skills need no config translation at all.
- Live demo payoff: a third-party Playwright skill (built with Claude in mind, expecting a Claude-specific output directory) ran successfully in Codex — when it hit a read-only path mismatch, Codex self-corrected by creating its own output directory instead of failing.

## 🛠 Tools & Software
- [[topics/Codex]] — the video's central subject: OpenAI's coding agent, newly updated to support the open Agent Skills spec via `/skills` and `$skill-installer`.
- [[topics/Claude Code]] — the origin ecosystem for the skills being transferred; compared throughout as the tool Codex's skill installation process is now competing with (and arguably beating on ease of install).
- [[topics/Claude Desktop]] — cited alongside Claude Code as another place skills are normally installed, contrasted with Codex's simpler installer flow.
- [[topics/Claude Skills]] — the Anthropic feature/format (skills, progressive disclosure, SKILL.md) that Codex's new support is built on and that the demoed Playwright skill and evaluator skill originate from.
- [[topics/Playwright]] — the subject of the demoed third-party skill: a community-built Playwright skill that nearly replaces the Playwright MCP server, shown running successfully in Codex after being copied over from a Claude project.
- [[topics/GitHub]] — where the presenter's own "agent skill evaluator" skill and the third-party Playwright skill are hosted and installed from via URL.
- [[topics/Bright Data]] — one of the MCP servers the agent-skill-evaluator skill invokes as part of its automated safety evaluation of a third-party skill.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/MCP]] — contrasted with skills throughout as the older approach to giving agents capabilities; skills are framed as a simpler fix for the context bloat MCP servers can cause, and MCP config (JSON vs. TOML) is cited as a portability pain point skills avoid.
- [[topics/Agent Skills]] — the open specification (originated by Anthropic, adopted by OpenAI for Codex within about two months) that makes skill packages — instructions, scripts, and resources — portable across agents with no reconfiguration.

## ✅ Action Items
- Update Codex to the latest version to get Agent Skills support (`/skills` to list installed skills).
- Use `$skill-installer` with a GitHub URL to install a third-party skill directly in Codex.
- Copy an existing `.claude/skills/` folder into a project's `.codex/skills/` directory to reuse Claude skills in Codex with no changes.
- Build or install a skill-evaluator-style skill to vet third-party skills for unsafe commands before trusting them.

## 🔗 Related Videos
- [[videos/Continual Learning in Claude Code]] — shared: Claude Code, Claude Skills, GitHub, MCP
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude Code, Claude Skills, GitHub, MCP
- [[videos/Claude Just Introduced a New Way To Fix Your UI]] — shared: Claude Code, Claude Desktop, Claude Skills, MCP
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Claude Code, Codex, GitHub, MCP
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude Code, GitHub, MCP, Playwright
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude Code, GitHub, MCP, Playwright
- [[videos/I Open-Sourced My Own AFK Software Factory]] — shared: Claude Code, Claude Skills, Codex, GitHub
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude Code, Claude Skills, GitHub, MCP

## Timeline
- `0:00` — Codex gets Agent Skills support; just update Codex to enable it.
- `0:20` — Quick recap of what skills are and how progressive disclosure avoids context bloat.
- `1:22` — Skill structure overview: SKILL.md plus optional scripts/references/assets.
- `2:23` — OpenAI's currently available skills (GitHub and Notion skills).
- `2:41` — Installing the presenter's own Skill Evaluator skill from GitHub via `$skill-installer`.
- `4:01` — Transferring existing Claude skills to Codex.
- `4:27` — Creating a `.codex/skills/` folder and copying a Claude Playwright skill into it.
- `4:48` — Confirming both Claude Code and Codex now see the same skill.
- `5:40` — Running the agent skill evaluator against the third-party Playwright skill, including its self-correction when hitting a Claude-specific path.
- `6:12` — Final thoughts: open standards let a two-month-old spec get adopted across companies.

## Transcript
<details>
<summary>Full transcript</summary>

Codeex just got agent skill support. And the good news is you don't have to do anything crazy to get it working. All you have to do is update your codeex installation. It's really easy. And the even better news is that it follows the skills spec almost word for word. Meaning if you created skills for claude or claude code, 99% of the time it will work out of the box. So in this quick video we're going to go over agent skills for codecs. I did a video on skills about 2 months ago when Anthropic just released it. I'll link to that above.

Essentially what it is is a way to pass skills to your agent. Be it custom instructions, be it executable scripts, you could put reference files in there. And this is a very simple solution for fixing context bloat. Be it MCB servers, be it long agents.mmd files or claw.mmd files. All these tools and rules and files that essentially get put into context and bloat our context window even before we start working. And skills uses this thing called progressive disclosure which essentially just gives the skill name and a short description. And if the agent either chooses to use it or you tell it to use it, it will then look at the subsequent files if it needs to instead of it all getting added to your context at the get-go. And I've used this to improve MCB servers. I've used this instead of MCP.

And what's great about this is OpenAI took the agent skill standard spec and just applied it to Codex. So if we look at the documentation, the skill packages its instructions, resources, and optional scripts to codeex to perform a specific workflow reliably. You can share them across teams or the community, and they build upon the open agent skills standard. Skills are available in codec cli and the ID extensions.

The structure of skills are very simple. All you really need is a skill.mmd file, but you can also put in scripts and reference files and assets. These are all optional. Skills use progressive disclosure to manage the context efficiently. At startup, Codex loads the name and description of each available skill and then Codex can load the skill in two ways. Either you tell it to do it or Codex can decide to use it implicitly when it matches the user's task. But in my experience of skills both in Claude and now in Codex, I prefer to just tell the agent use the skill.

With Codex, you can put skills on multiple places. Codex has its own skill creator skill and its own skill installer skill, which is actually even easier than adding skills via cloud code or cloud desktop. But let me just show you. First things first, you have to update your version of Codex. If you installed via npm, I'm pretty sure it will auto update for you. If you installed via bun, you just have to run the installer again.

Once you're on the latest version of Codex, you just open it up. If you do /kills, you can list the skills that are already in there. And all we see here are the skill creator and the skill installer. And then if you go to the skill installer and you just press enter, it will tell you what skills are available via open AI right now. So let's just go through that. They have two GitHub skills and four notion skills. That's cool and not really relevant. So we're not going to install any of those right now.

But one thing I want to show you right now to invoke a skill directly, you just do dollar sign and you can choose whatever skill you want. If you do skill creator, you can now have Codeex help you build your own skills. But I want to show you how to install already created skills. In a different video I did about skills, I showed how to build, evaluate, and install skills. And in that video, I showed my skill evaluator skill. Because when you install skills, you're adding custom prompts and custom commands to your agents. And therefore, you're potentially opening yourself up to shady business. If you're installing other people's skills, you never know what they put in there. So, I created a skill evaluator skill to check other people's skills.

And I'm just going to show you how to install that one right now because it will show you how easy it is to install other people's skills. And it's actually even easier to install third-party skills than it is for Claude Code or Claude Desktop. So in that video, which I'll link to above, I shared my eval marketplace where I have an MCP evaluator and a skills evaluator. And by the way, this is built with Claude for Claude and Claude Code, but Codeex doesn't support plugins or marketplaces yet, but that doesn't really matter.

So if we go into evaluator tools and then we go into skills and then we go into the agent skill evaluator and all we're going to do is take the URL. And now I'm going to invoke the skill installer, dollar sign skill installer, and just paste the URL in here. Press enter. And now it's asking permission. So, we're just going to give it permission and that's it. So, it installed the agent skill evaluator to my user level skills and all I have to do to get it working is to quit codeex and go back into it. So, let's do /quit and open up codex again. And now, if we do /kills, we see three skills. The skill creator, the skill installer, and the one we just installed, the agent skill evaluator skill. It was that simple and I'll show you it working in 1 second.

But let's say you already have skills installed for Claude in your project. Let me show you how easy it is to get it working in Codex. This is a project I used in a previous video just testing skills versus MCP and in it we have a playright skill. In that video I also showed how certain skills can replace MCP servers. In this case we talked about playright because playright could also be called from the CLI and somebody created a playright skill that almost completely replaces the need for the playright MCP server which takes up a lot of context. So this is a third party skill that somebody created. He's still updating it and it's already working for Claude code.

So to get it to work in codeex in this project all I have to do is create a codeex folder. Inside that, create a skills folder. And now we're just going to paste it in here. So check this out. Here's a claude skills folder with a playright skill. And here we have the Codex folder with a skill folder with a playright skill as well. So now if we quit Codex again, and then we reopen it up and then do /kills. We now see the new playright browser skill. It was that easy. It just works.

So let's just clear it up, make it clean. Open up Codex again. So what we're going to do is we're going to use the agent skill evaluator skill that we imported from GitHub to look at the Playright skill and make sure it's safe. And I just want to show you how portable our clot skills are with codeex skills. And by the way, this is unlike MCP where with codeex you have to change the JSON config to Toml. This doesn't need any different configurations right now. And more than that, I've tested skills I made for claudex and by definition it shouldn't have worked and codeex just selfcorrected. Let me just show you.

So we're going to press the agent skill evaluator. And now we're going to go back to the GitHub, copy the URL, and put it in here. So we're doing agent skill evaluator and putting in the URL of this third party playright skill. And by the way, this skill tells the agent to use various MCP servers like Bright Data, like GitHub, and do a whole evaluation of the skill to make sure there's no shady commands or code and then give us a full report to know if this is a good skill to install or not. So, let's see what happens.

Okay, so it finished running and it worked almost perfectly. It used the bright data MCP. You can see all the tool calls here and then it looked at the reference files, the attack patterns.mmd file, and then it asked me to create the output. And this is actually really interesting because this skill was built with Claude in mind and it want to output it to this directory. But this directory is very specific to claude and claude code. So here it sees it was read only. So in the end it created its own outputs directory in the project and then gave us the markdown file just like I told it to do in the skill itself. Very detailed, very good. And the bottom line here is it just selfcorrected.

So that's really cool. I think it's great that only after 2 months Openai has adopted the full spec, implemented it into codeex. I'm hoping that it will also come to chatbt very soon. I think it's really cool that Anthropic is coming out with these novel ideas to solve limitations of LLMs. And they're not perfect and they're still being improved upon, but they're simple enough that other companies are able to adopt them and ship them in a matter of months.

So, let me know what you guys think. I hope you found this video helpful or insightful. If you have any questions or feedback, drop it in the comments below. If you haven't done so already, subscribe to the channel. It really helps me grow. Thank you guys for watching and have a great

</details>
