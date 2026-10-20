---
title: "Why OpenAI Built Symphony and Gave It Away for Free"
video_id: n8qDKMPpLXc
channel: "[[channels/Better Stack]]"
uploaded: 2026-05-09
processed: 2026-07-05
duration: "6:19"
url: https://www.youtube.com/watch?v=n8qDKMPpLXc
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [autonomous-coding-agent-orchestration, issue-tracker-agent-automation]
tools: [Symphony, Linear, Codex, uv, Bun, Conductor, Maltego, Monica]
llms: [GPT-5.5, Claude]
protocols: [GraphQL, MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Why OpenAI Built Symphony and Gave It Away for Free

![thumbnail](https://i.ytimg.com/vi_webp/n8qDKMPpLXc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=n8qDKMPpLXc) | 📅 Uploaded [[uploaded/2026-05-09]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Symphony is OpenAI's open-source orchestrator that connects long-running Codex agents to an issue tracker like Linear so agents can autonomously claim tasks, work in isolated workspaces, and only ping a human when review is needed. The video demos a basic Linear-to-PR flow, walks through Symphony's bizarre spec-driven "build it yourself" install option, adds production hooks for real git branches/PRs, and weighs it against closed alternatives like Maltego and Conductor.

**Watch this if:** you're managing more Codex (or other coding-agent) sessions than you can personally supervise and want them claiming tickets from your issue tracker instead of waiting on you.

## Key Takeaways
- Symphony exists because engineers hit a human attention bottleneck — only 3 to 5 concurrent Codex sessions could be supervised before context-switching hurt productivity, so Symphony removes the human middle-manager step.
- Workflow: humans put tasks on a board (e.g., Linear), Symphony spins up an agent to claim and complete the task, and only involves a human when there's something to review.
- In the demo, creating a Linear issue ("build a Hello World app in TypeScript and Bun") gets picked up by Symphony within seconds, Codex fixes a GraphQL validation error along the way, and the issue is marked done with a new local workspace containing the finished code.
- Symphony has two install paths: the conventional clone-and-build route, or the "genius or insane" option of handing your coding agent a 2,000+ line spec file and letting it build its own version of Symphony from scratch in any language — community versions already exist in Go (on Charm CLI) and powered by the Claude SDK.
- Basic setup requires a Linear personal API key and a workflow YAML file (API key, active states, workspace root, and the shell command used to launch the coding agent).
- Out of the box, Symphony isn't ready for a real project — you need to add a "create-after" hook (clone repo, checkout a new branch) and a "run-after" hook (stage, commit, push, open a PR) to make it actually ship pull requests instead of just local workspaces.
- The presenter's verdict: Symphony is a solid bare-bones harness, especially if you're already on Linear/Codex, but closed alternatives like Maltego are easier to set up and offer built-in scheduling — Symphony's appeal is that you build exactly the features you want instead of taking a fully pre-built product.

## 🛠 Tools & Software
- [[topics/Symphony]] — OpenAI's open-source agent orchestrator that connects Codex sessions to an issue tracker; the central subject of the video, demoed end-to-end
- [[topics/Linear]] — the issue tracker Symphony polls for tasks in both demos
- [[topics/Codex]] — OpenAI's coding agent that Symphony spins up per task and that completes the demoed work
- [[topics/uv]] — Astral's Python tool (also acquired by OpenAI) used to run Symphony in the demo
- [[topics/Bun]] — the JavaScript runtime used to build the demo Hello World app
- [[topics/Conductor]] — named as a similar orchestration tool Symphony is compared against
- [[topics/Maltego]] — a closed-source alternative the presenter says is easier to set up and includes built-in task scheduling
- [[topics/Monica]] — named alongside Conductor as a similar tool Symphony is compared against

## 🤖 LLMs Mentioned
- [[topics/GPT-5.5]] — the model the presenter fed the Symphony install spec to (via Codex, on "low effort"), producing a Python build
- [[topics/Claude]] — mentioned as the model powering a community-built version of Symphony via the Claude SDK

## 📡 Protocols & Standards
- [[topics/GraphQL]] — Codex hits and fixes a GraphQL validation error while completing the demoed Linear task
- [[topics/MCP]] — Codex users are noted as able to bring their existing MCP tools and plugins into their Symphony workflow

## ✅ Action Items
- Try the standard clone-and-build install first before attempting the spec-driven "build it yourself" route.
- If you go the spec-driven route, expect to own maintenance of your own version — budget time for fixing bugs and adding features yourself.
- Add create-after and run-after hooks before trusting Symphony with a real project, so it produces actual branches and pull requests instead of local-only workspaces.
- If you want built-in scheduling and easier setup out of the box, evaluate Maltego as an alternative before building your own Symphony workflow.

## 🔗 Related Videos
- [[videos/This single MCP server saves $1000s on token costs]] — shared: Bun, Claude, Codex, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, Codex, MCP
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Codex, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, MCP
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude, MCP
- [[videos/Agent memory resolved]] — shared: Claude, Codex
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: Claude, MCP

## Timeline
- `0:00` — Intro: what Symphony is and the questions this video answers
- `0:25` — Why Symphony exists: the human attention bottleneck of supervising Codex sessions
- `0:47` — How it works: humans post tasks, agents claim them, humans only pulled in for review
- `1:11` — Basic demo: Linear issue "SYN-7" picked up and completed by Symphony/Codex
- `2:09` — Setup option two: the conventional clone-and-build install
- `2:14` — Setup option one: handing your coding agent the 2,000+ line spec to build Symphony itself
- `3:19` — Configuring the Linear API key and the workflow YAML file
- `3:52` — Making it production-ready: create-after and run-after hooks for real branches and PRs
- `4:39` — Second demo: a README-update issue flows through to a real pull request
- `5:11` — Wrap-up: fits naturally for existing Linear/Codex users, vision for a team-wide central agent
- `5:51` — Comparing Symphony to closed alternatives like Maltego and Conductor

## Transcript
<details>
<summary>Full transcript</summary>

This is OpenAI's Symphony, an open-source tool for orchestrating long-running agents using an existing issue tracker like Linear to help your agents autonomously complete tasks without any human supervision. But why does an agent have to build it from scratch before you can use it? Does it only support Codex CLI? And is this the beginning of more open-source tools from OpenAI? Hit subscribe and let's find out.

Symphony only exists because OpenAI hit a human attention bottleneck, which means engineers could only supervise three to five Codex sessions concurrently before context switching began to negatively affect productivity. This, of course, wasn't going to scale. So guess how OpenAI fixed the fast agent slow human managers problem? They got rid of the human managers, kind of. Because with Symphony, humans put tasks on a board, a new agent will be spun up to complete that task, and the agent will only involve the human if there's something to review. But how does Symphony compare to similar tools like Monica and Conductor? Well, watch the demo and that will be made crystal clear. Before we start, however, I just want to say Symphony has the weirdest installation process I've ever seen in my life. Or it could be the most genius way to install something. We'll get to that later. First, however, let's go through a basic example. So, I have a Symphony running polling for tasks in Linear to work on. And in Linear, I'm going to create a new issue, which will be to build a Hello World app using TypeScript and Bun. Right now, Symphony isn't configured to work on backlog tasks, so I'll change the status to to do and hit create issue. Remember the ID of the task, which is SYN-7. So after a while, Symphony picks up on the ID of that task, and a few seconds later, we have a GraphQL validation error, which isn't a big deal and it's very easy for Codex to fix. But after that, we can see that Codex has completed the work, has changed the issue from to do to done, and has left a comment here from Symphony. Which means if we go to our Symphony workspaces directory, we'll talk more about that later, we can see we have a new workspace with the same ID as our issue. And if we go into that workspace, we have the list of files created for the Hello World TypeScript bot app. And if we go into the source directory, we can see that the code for that app is over here. And that's essentially Symphony in a nutshell.

Now, let's go through how to set it up. So, there are two ways to install Symphony according to this repo. Option two, which is what we're used to, we set up Elixir, clone the repo, then build the code, and run it using the existing workflow file. Option one, however, is possibly the weirdest or most forward-thinking way to install something. You just basically give your coding agent this prompt, and it will read the spec file, which is more than 2,000 lines long, but it basically gives your agent detailed instructions on how to build Symphony, which is wild because if everyone went down this route, no two versions of Symphony would look the same. Some people would have different features in different languages, which would be chaos for OpenAI to maintain and support. But it's also kind of genius because if you built your own version of Symphony, you would feel responsible for it. You'd fix the bugs, you'd add the features, and you'd essentially maintain it. And if you didn't want Symphony to use linear or Codex, then that's up to you. Someone built a Go version of Symphony that runs on charm CLI, and someone else built one that was powered by the Claude SDK. I wasn't that creative, so I put the default prompt into Codex using GPT-5.5 low effort, and it gave me a Python version of Symphony, which makes sense because LLMs are very good at Python.

But once that's done, you'll need a linear personal API key, which you can get from security and access, and you can create one by clicking over here. Then you'll have to add that key to your workflow file, which is a file that tells Symphony how to do its job, containing some YAML front matter, which of course has the API key, active states for the agent to know when it can work on a task, as well as the workspace root, and the Codex command, which is the shell command Symphony uses to launch a coding agent. And below that is the markdown prompt sent to the coding agent for each issue. You can access OpenAI's workflow in detail from their repo if you're interested. But as of right now, this workflow isn't fit for a real project. Say I wanted to make changes to my film emulation app that I've been working on. I would need to add a create after hook, which runs after Symphony creates a workspace for an issue, and this hook will first clone the repo to the workspace directory, and then check out to a new branch in that repo. I've also added a run after hook, which runs after Codex finishes working on the issue. So, this one stages the files, then creates a new commit before pushing the branch and creating a new pull request with these files.

So, now if I run Symphony using UV, which was also acquired by OpenAI, but that's the topic for another video, it's polling for new issues. So, now if I create a new issue to update the readme just in the section that shows batch processing to use a wildcard instead of showing multiple files. Again, I'll change it from backlog to to do, then hit create issue. Now, Symphony has picked up on that issue, and if I look at the Symphony workspaces directory, we can see there's a new folder matching our issue ID, which contains the cloned project. And now that Symphony has finished working on the issue, it's changed the status to done, and has created a new PR with a link to the linear circuit and the exact change that I requested. Now, of course, I could change my Symphony code to add a better PR description and to put a link to the PR in the comment, but I'm sure that's very easy for Codex to do.

So, that's a quick overview of Symphony. If you're already comfortable with or work at a company that uses linear, then you'll feel right at home with the interface. And if you're a Codex user, then you can use your skills, MCP tools, and plugins that you already have installed. I personally don't use Codex, but I can definitely see the vision OpenAI were going for with Symphony. Imagine you had a team of developers all working on the same project with AI. Instead of having their own personal harness with their own workflow, there can be a central agent with central skills, central tools, central workflows, and plugins, and each developer can communicate with that by giving it a task, and they can see what other developers are working on, what prompts they've used, and can see at a glance what other features might affect the feature that they're on, even though it's very difficult to come up with a feature that won't touch another part of the code that someone else is working on. But, as cool as Symphony is, in my opinion, Maltego does a better job because it's easier to set up, create, and add different agents, and you can even schedule tasks. Nevertheless, I completely see a place for Symphony. It's kind of like the bare-bones version of Maltego, where you can add the exact features you want instead of having a product that is built for you. So, think of Symphony like the pie harness and other tools like Maltego or Conductor as closed code.

</details>
