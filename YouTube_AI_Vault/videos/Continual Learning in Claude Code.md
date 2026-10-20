---
title: "Continual Learning in Claude Code"
video_id: sWbsD-cP4rI
channel: "[[channels/Developers Digest]]"
uploaded: 2025-12-30
processed: 2026-07-06
duration: "8:55"
url: https://www.youtube.com/watch?v=sWbsD-cP4rI
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [continual-learning-agents, skill-based-memory]
tools: [Claude Code, Claude Skills, GitHub, Playwright, Chrome DevTools MCP, Open Lovable]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Continual Learning in Claude Code

![thumbnail](https://i.ytimg.com/vi_webp/sWbsD-cP4rI/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=sWbsD-cP4rI) | 📅 Uploaded [[uploaded/2025-12-30]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Traditional agent development means manually rewriting system prompts every time you find an edge case — the agent itself never learns. This video argues Claude Code's "skills" solve that because Claude can read and write its own skill files, turning them into persistent, git-shareable team memory that compounds every session, echoing Robert Nishihara's (Anyscale CEO) point about storing knowledge outside model weights.

**Watch this if:** you keep hand-tuning system prompts after every failure and want a way for the agent to encode its own lessons (successes and failures) into reusable, human-readable skill files instead.

## Key Takeaways
- The standard agent-building loop — write a system prompt, add rules/constraints, test, find edge cases, repeat — requires manually encoding every insight; the agent never learns on its own.
- Claude Code skills are efficient with context, composable, portable, and discoverable; the key underused unlock is that Claude can read AND write to its own skill files, improving them every session.
- A skill is just a directory with a required `skill.md` (name + description) plus optional scripts/references that load progressively — only the description sits in the main context window until the skill is actually triggered.
- Skills can live at the user/root level, the project level, or be packaged in a shareable plugin (which can also bundle MCP servers and hooks).
- A "learning loop" pattern: query the skill registry before a task to surface past experiments and known failures, run the task, then have Claude do a retrospective that updates the skill file (or opens a PR) with what worked and what didn't.
- Deliberately documenting failures (not just successes) matters because a new session has no memory of what went wrong before — capturing failure examples helps a non-deterministic model avoid repeating mistakes.
- Robert Nishihara's (Anyscale CEO) tweet is quoted: storing knowledge outside model weights via skills is interpretable, editable in plain text, and data-efficient like in-context learning, versus retraining/post-training a model.
- Anthropic's public skills repo includes examples like a front-end design skill and a web-app testing skill (which can invoke tools like Playwright or Chrome DevTools MCP).

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent environment where skills live and where the continual-learning loop (retrospective slash command, skill updates) is set up.
- [[topics/Claude Skills]] — the central subject: directory-based, progressively-disclosed markdown skill files that Claude can both read and write to build persistent memory over time.
- [[topics/GitHub]] — where skills/skill registries can be hosted, shared, and updated via pull requests generated from a session's retrospective.
- [[topics/Playwright]] — cited as one of the tools a web-app testing skill can invoke to test an application.
- [[topics/Chrome DevTools MCP]] — cited alongside Playwright as a tool a web-app testing skill can leverage.
- [[topics/Open Lovable]] — the presenter's own project, used as an example of the painful manual system-prompt iteration cycle that motivates skills-based continual learning.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model discussed throughout as the one reading, writing, and improving its own skill files across sessions.

## 📡 Protocols & Standards
- [[topics/MCP]] — mentioned as something a Claude Code plugin can bundle alongside skills and hooks, and as the protocol behind tools like Chrome DevTools MCP.

## ✅ Action Items
- Set up a retrospective slash command (or a CLAUDE.md instruction) that has Claude update the skill files it used at the end of a session.
- Write skill descriptions carefully since that's what the orchestrator model sees in context to decide when to invoke a skill.
- Deliberately log failures, not just successes, inside skill files so future sessions know what to avoid.
- Try Anthropic's public skills repo examples (front-end design, web-app testing) as a starting point.
- Consider sharing project-level skills via a Git repo or plugin so teammates inherit the same accumulated knowledge.

## 🔗 Related Videos
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Katelyn Lesse Evolving Claude APIs for Agents, Anthropic]] — shared: Claude, Claude Code, Claude Skills, GitHub
- [[videos/OpenAI Adds Agent Skills to Codex (First Look & Walkthrough)]] — shared: Claude Code, Claude Skills, GitHub, MCP
- [[videos/Anthropic just open-sourced Wall Street (114k stars)]] — shared: Claude, Claude Code, GitHub, MCP
- [[videos/Chrome Just Became the Ultimate Agent Browser (Finally)]] — shared: Chrome DevTools MCP, Claude Code, MCP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Playwright

## Timeline
- `0:03` — The problem: manually encoding insights into system prompts means the agent never learns on its own.
- `0:34` — Introduction to Claude Code skills: efficient, composable, portable, discoverable — and readable/writable by Claude itself.
- `1:19` — Setting up skills: directory structure, required skill.md, where skills can live (root, project, plugin).
- `2:39` — Progressive disclosure explained: only the description loads into context until the skill is triggered.
- `3:45` — Documenting failures as well as successes to inform a non-deterministic model what to skip.
- `4:42` — Robert Nishihara's tweet on continual learning and storing knowledge outside model weights.
- `6:27` — Getting started with Anthropic's public skills repo examples.
- `6:48` — Leveraging skills personally, at the project level, and via shareable plugins/registries.
- `7:59` — Extending the same learning-loop idea to system prompts generally, via PRs from captured failures/successes.

## Transcript
<details>
<summary>Full transcript</summary>

In this video, I'm going to be going over continual learning within cloud code. One of the big problems today is if you were to write an AI agent, generally speaking, the process will go something like this. You'll write a system prompt. You'll add rules, constraints, test, find edge cases, and you will repeat this process until something actually works. But one of the issues with this is every insight as you're going through and actually building this out is going to be manually encoded, when you actually add to your system prompt, whether you're doing that with AI tools or a combination of writing things manually. One of the problems with this is the agent never actually learns on its own.

What is the solution to this? Now, if you've used cloud code before, you've probably heard of skills. Now, a lot of people were excited about these for a number of different reasons. They're efficient with context. They're composable. They're portable. They're efficient. They're discoverable. You can just put them on GitHub and you can download this markdown file, potentially some scripts, and it's really easy to actually have these be invoked. But one of the big unlocks with skills that I don't see enough people talking about, Claude can read and write to these. And what this means is that the model can actually improve them with every session. So you can set up a slash command to have a retrospective at the end of your coding session where it can go through whatever happened and actually update the particular skills that you were using. Additionally, what you could do is you could actually just encode this within something like your cloud.md and have that happen automatically.

In terms of skills, if you're not familiar, what you'll have is you'll have a directory. And within the directory, you'll have all of your different skills. In each directory, the one thing that you do need is a skill.md. Now, within that skill, you can include other things that it could progressively disclose, like say if there's scripts or references or other helpful assets that you do want to leverage. In terms of how you can actually set these up within cloud code, there are a number of places where you can put them. So, you can put them at the root of your computer. So, you're going to be able to access them whenever you want. And additionally, you can have them at the project level or you can actually have it within a plug-in that you can share with others to be able to easily install.

Now, in terms of the format for skills, they're super straightforward. So, you can come up with a name, a description. Now, the description is really important because this is going to be what actually is within the context of the orchestrator model or the main thread to know when to actually invoke that. So, make sure you have a good description. Now, additionally within skills, you can give it particular tools and you can also reference within the file if there are other helpful things that could potentially be useful. You can put them all within here and it doesn't necessarily load up all of that context within the skill.md file. It can go and reach for those things progressively. The cool thing with this is you're only going to be using a number of tokens within the description to actually have it within the main context window. And then all of the other aspects below this is only going to be loaded once that skill is actually triggered.

Now, in terms of how skills work, one of the really cool things with this is called progressive disclosure. So, Claude will load up the skills names and the descriptions. And what it will do is it will request matches for a skills descriptions and it will ask for confirmation before loading. Now, I'm not going to go through and actually show you how to set this up. It's really straightforward to set up slash commands. You can do a little bit of Googling or you can actually just ask Claude Code itself to set up these slash commands.

Now, in terms of setting up a learning loop, it's really quite straightforward. I'm not going to be going through and showing you step by step in terms of how you can actually set up these triggers, how you can set up these slash commands, but effectively what you can do is you can query for your skill registry prior to different learnings. It can surface the relevant past experiments, show known failures as well as provide the working configuration and additionally at the end of it, you can provide a retrospective. So once all of that is within context, you can go ahead and run an update process where Claude will read through the entire conversation, extract the relevant pieces of what worked as well as what failed. You could set it up so it actually opens a PR if it's within a registry. Or you can actually have it just write to that skills MD file or all of the different files that you have within the skill directory.

Now, another helpful thing with this is you can actually document failures. One of the things that I did when I was setting up a project open lovable is I spent an awful lot of time with the system prompt and it was basically a lot of do this don't do that and me just going through the cycle like I mentioned earlier where you're writing out a system prompt you're trying different things you're finding edge cases and you're repeating that within a cycle. Now, one of the things with failures that I don't think a lot of people are capturing is you can actually use these failures to inform which things to skip because when you start up a new session with the model, it's not going to have the context of all the things that it does bad. It isn't necessarily as intuitive to actually encode failures or put failures within a place. That's something that we don't typically want to do within software. But because large language models are non-deterministic, actually having some examples of where it can go off the rails can be very helpful. And this goes both ways, having examples for failures as well as successes. These can help improve these skills over time.

Now, I want to pull up a tweet from Robert Nishihara. This is the CEO of any skill, an inference provider. And one of the things that he said when skills came out, I'm just going to read through this is the thing that excites me about anthropics agent skills announcement is that it provides a step towards continual learning. Rather than continuously updating model weights, agents interacting with the world can continuously add new skills. Compute spent on reasoning can serve dual purposes for generating new skills. Right now, the work that goes into reasoning is largely discarded after a task is performed. I imagine vast amounts of knowledge and skills will be stored outside of a model's weights. It seems natural to distill some of the knowledge into the model's weights over time, but that part seems less fundamental to me. Now, some of the key aspects that he mentioned is there are many nice things with storing knowledge outside the model. It's interpretable. You can just read through the skills. You can correct mistakes. The skills and knowledge are just plain text, so they're easy to update and they should be highly data efficient in the same way that in context learning is data efficient.

And I think some of the key aspects of this is you can just read through this. You can just edit it. If there's something within natural language, you can just see that is not what I want to do and I'm just going to go ahead and update that. It makes it much much easier than actually having to go and retrain or post-train a model where you don't necessarily know exactly what's happening under the hood. With skills, you're going to know exactly what it's doing because it's written in English. One of the key insights with this is that the knowledge stored outside the model's weights in skills we can read, edit, and share. And not to mention, every session's reasoning can compound into future skills. What you can do with continual learning is create effectively a flywheel where this will just get better over time and learn from mistakes or as things change or as the environment updates and it needs to leverage different libraries or leverage whatever the skill is actually using.

Now, in terms of getting started with skills, if you haven't tried them, there are a number of really great examples on Anthropics repo on this and I'll also put this within a link within the description of the video and what you can do with skills. What it is is just effectively another way that you can actually leverage different tools as well as pass in different contexts at progressive disclosure and then like I mentioned you can actually leverage it for continual learning.

Now, in terms of how you can leverage skills, so you can do this for personal things. So, if there are things within your day-to-day job or things that you do personally and create custom skills very easily, just write out natural language, equip it with particular tools, and have it learn over time whatever you're actually wanting that skill to do. Now, the other benefit of this is you can actually have them at the project level. And what's nice with this is you can have repos. And where that can be helpful in a team setting is when you share that and someone else is leveraging a system that can leverage skills, they're going to be able to inherit all of those particular skills that are specific to the project.

Now, additionally, you can set this up where you can share it via a plug-in or a registry. If you do want to try and set this up at a plug-in level as well. And what's neat with plugins is you can set it up to leverage different MCP servers, skills, as well as hooks. You can effectively have a whole config of a number of different tools.

Now, within the skills repo from Anthropic, there are a number of great skills that you can build on top of. And just to give you some ideas, so they do have a front-end design skill. They do also have a web app testing skill. Just to give you an idea in terms of how these can be leveraged, if you're working on a web application, if this skill is installed, you can say test my application and leverage all of these different tools to test your application, things like Playright or the Chrome MCP, so on and so forth.

Now another thing in terms of how you can actually leverage these learnings and continual learning and this is a little bit outside of cloud code per se but what you could do is you could actually take these learnings and improve your system prompt like I mentioned within the open lovable example of spending time writing a system prompt or just doing that generally for any agentic system. What you can do is as you capture failures and successes, you could potentially even set up a system where it will PR your system prompt or even PR your skills if you have them within Git. There are a ton of really cool things that you can do with this.

Now, all in all, skills aren't just instructions. They're persistent team memory that can compound with every session. I don't see a ton of people doing really interesting stuff with this quite yet, but hopefully with this video, it can inspire some ideas in terms of how you can leverage skills and continuous learning within Cloud Code as well as other agentic systems. Otherwise, that's it for this video. If you found this video useful, please like, comment, share, and subscribe. Otherwise, until the next

</details>
