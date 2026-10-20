---
title: "The Claude Code Feature Senior Engineers KEEP MISSING"
video_id: u5GkG71PkR0
channel: "[[channels/IndyDevDan]]"
uploaded: 2026-01-19
processed: 2026-07-06
duration: "27:29"
url: https://www.youtube.com/watch?v=u5GkG71PkR0
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: advanced
use_case: [self-validating-agents]
tools: [Claude Code, GitHub, uv, Ruff, pandas]
llms: [Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The Claude Code Feature Senior Engineers KEEP MISSING

![thumbnail](https://i.ytimg.com/vi_webp/u5GkG71PkR0/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=u5GkG71PkR0) | 📅 Uploaded [[uploaded/2026-01-19]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> IndyDevDan shows how Claude Code's newest release — hooks embedded directly inside custom slash commands, subagents, and skills — lets you build "specialized self-validating agents" that catch and fix their own mistakes deterministically. He builds a CSV-edit prompt from scratch with a PostToolUse hook that runs a pandas-based validator script, shows the agent detect and repair a broken CSV automatically, then scales the same pattern into a subagent (parallelized across 4 files) and into a full multi-agent finance-review pipeline running on Claude Opus.

**Watch this if:** you build multi-step Claude Code agents/skills/commands and want a way to make their output verifiably correct instead of just hoping the model got it right.

## Key Takeaways
- Claude Code now supports PreToolUse, PostToolUse, and Stop hooks defined directly in the front matter of custom slash commands, subagents, and skills — not just globally in `settings.json`.
- A focused agent that does one thing extraordinarily well (e.g. "edit CSV files") consistently outperforms a generalist agent trying to do everything, especially at scale (tens/hundreds/thousands of runs).
- Demoed pattern: a `/csv-edit` command with a PostToolUse hook on Read/Write/Edit that runs `uv run` against a project-local `validators/csv_single_validator.py` (built on pandas) after every file operation.
- When the validator finds a broken CSV (a missing quote), it feeds an error message back into the agent's context ("resolve this CSV error in [file]..."), and the agent immediately fixes it and re-verifies — a closed-loop, self-correcting prompt with no manual intervention.
- The same hook pattern moves into subagents to get parallelization: 4 CSV-edit subagents ran concurrently, one per file, each independently validating its own edit.
- A stop-hook variant runs project-wide validators/linters/formatters (e.g. `uv` + `Ruff`) once an entire build agent finishes, versus a PostToolUse hook that validates one file at a time.
- Everything — slash commands, subagents, skills — boils down to the same "core four": context, model, prompt, tools; hooks add a deterministic trust layer on top of that. Claude Code is also merging slash commands and skills internally since they're functionally the same prompt-invocation mechanism.
- The full demo pipeline (`/review-finances`) chains multiple specialized agents (categorize CSV, merge accounts, normalize CSV, generative UI) each with its own hooks, running on Claude Opus, and ends by generating a financial dashboard UI from mock data.
- You can go further and pass an entire hooks-enabled `settings.json` as JSON directly into a primary agent invocation via `claude -p`.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the CLI being extended with hooks in custom slash commands, subagents, and skills; run with Claude Opus for the finance-review pipeline.
- [[topics/GitHub]] — hosts the "Agentic Finance Review" example codebase referenced and demoed throughout.
- [[topics/uv]] — used via `uv run`/`uvx` to execute the CSV validator scripts triggered by hooks.
- [[topics/Ruff]] — mentioned as part of the "Astral" linting/formatting tooling run in a Stop-hook after a build agent finishes.
- [[topics/pandas]] — used inside the validator script to parse and check CSV file structure/validity.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — the model running the Claude Code instances and the multi-agent finance-review pipeline (referenced as Opus 4.5).

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Add a PostToolUse hook to any custom slash command, subagent, or skill that edits a specific file type, and point it at a small deterministic validator script rather than relying on the model to "hope" it got the edit right.
- Keep validators hyper-specific to one file format/purpose (e.g. a CSV validator) rather than building one giant catch-all validator.
- Use subagents when you need to parallelize the same self-validating pattern across many files at once.
- Use a Stop hook for project-wide checks (linting/formatting everything) versus a PostToolUse hook for validating a single file right after it's touched.
- Read Claude Code's actual hooks documentation (for skills, subagents, and slash commands) instead of copy-pasting patterns without understanding them.

## 🔗 Related Videos
- [[videos/RAW Agentic Coding ZERO to Agent SKILL]] — shared: Claude Code, Claude Opus, GitHub, uv
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, Claude Opus, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, GitHub
- [[videos/Claude Code Task System ANTI-HYPE Agentic Coding (Advanced)]] — shared: Claude Code, Claude Opus, Ruff
- [[videos/Claude Code is Amazing Until It DELETES Production]] — shared: Claude Code, Claude Opus, uv
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Opus, GitHub
- [[videos/Elite Context Engineering with Claude Code]] — shared: Claude Code, Claude Opus, uv
- [[videos/Engineers Claude Code Output Styles Are Here Dont Miss This TREND]] — shared: Claude Code, Claude Opus, uv

## Timeline
- `0:00` — Intro: why self-validation matters and the new hooks-in-skills/subagents/slash-commands release.
- `0:46` — Kicks off a background `/review-finances` multi-agent pipeline as the running example.
- `1:54` — Building a `/csv-edit` custom slash command from a prompt template, specializing it to one purpose.
- `3:50` — Adding a PostToolUse hook that runs a CSV validator script after Read/Write/Edit.
- `7:25` — Demo: the agent detects a broken CSV (missing quote) and self-fixes it via the validator's feedback loop.
- `10:14` — Side rant: read the documentation, don't just vibe-code by pasting release notes into an agent.
- `15:57` — Rebuilding the same self-validation pattern as a CSV-edit subagent.
- `17:56` — Running 4 CSV-edit subagents in parallel, each validating its own file.
- `22:34` — Full finance-review agent pipeline: chained specialized agents, each with hooks, producing a generated finance dashboard.
- `25:29` — Passing an entire hooks-enabled settings.json as JSON into `claude -p`.
- `27:00` — Closing: agentic engineering, and a warning not to delegate learning to your agents.

## Transcript
<details>
<summary>Full transcript</summary>

If you want your agents to accomplish loads of valuable work on your behalf, they must be able to validate their work. Why is validation so important? Validation increases the trust we have in our agents, and trust saves your most valuable engineering resource: time. The Claude Code team has recently shipped a ton of features, but one in particular stands above the rest: you can now run hooks inside of your skills, subagents, and custom slash commands. This is a big release most engineers have missed because it means you can build specialized self-validating agents.

Inside of this codebase, we're going to kick off a new Claude Code instance and run `/review-finances-february`, pointing it at a specific February CSV file. Imagine you're doing your monthly finances — this is a system I'm building to automate financial processing. This is going to kick off an end-to-end pipeline of agents to review finances, do formatting, generate graphs, and offer insights into this month's finances. The important thing isn't the actual tool itself — whenever there's a new valuable feature, I like to build against it and truly understand its value proposition. This entire multi-agent pipeline is going to run specialized self-validation every single step of the way. We'll let this run in the background and circle back to it.

What I want to show you is how to build specialized self-validating agents step by step, starting with the most foundational element: the prompt. In Claude Code, prompts come in the form of custom slash commands. I'm going to open the commands directory and build a `csv-edit.md` file — a new prompt that helps us edit CSV files. We're specializing this command to do one thing extraordinarily well, and therefore specializing an agent to do just that. I have an "agentic prompt template" snippet I use — at the top there's a payload of front matter, and that front matter is what allows us to build our specialized self-validation via hooks. You can see support for pre-tool-use, post-tool-use, and stop — this is what's supported in prompt, subagent, and skill hooks.

We'll intake a CSV file and a modification (the user request), specialize the tools to search/read/write/edit, and turn off context-forking since we want this to run in the current agent. Now the juicy part: the hook. Whenever we're operating on CSV files, we want our agent to validate that the CSV is in the correct format — so we want the PostToolUse hook, because it lets us run a check after Edit, Write, and Read. After any of those commands run, we run a specific script. The way I organize codebases now, in the age of agents with these self-validation techniques, is: alongside commands/agents/skills, I keep a `hooks/validators` directory with a whole bunch of validators. We're going to use `csv_single_validator.py` here — I'll invoke it with `uv run`, referencing the project directory via Claude Code's built-in path variable. Every one of my validators outputs its own log file, which we'll dig into shortly.

Now we have an agent that after every PostToolUse call runs this script — I removed a "run once" flag so it keeps self-validating on every call. Then we have the actual prompt: read the CSV file (first arg), make the modification or report (second arg), then report the results. I've written thousands of prompts by now, and one of the most important things is creating reusable formats so neither you nor your agents have to think about the structure each time.

Let's test this in a new terminal — a Claude Code instance running Opus, and a brand new `/csv-edit` command with argument hints. I'll pass in a mock CSV file (mock input data, raw savings in February) and ask it to "read and report on the file structure." It found the file, reported on the data structure — nothing fancy, but the agent ran the self-validation. The big idea is that this self-validation is specific to this use case; it's hyper-focused on the purpose of this prompt. That same pattern extends to subagents and skills — whatever packaging you put your prompts in doesn't matter, because it all boils down to the core four: context, model, prompt, tools.

Let me show you the result — this is why observability and logging everything matters. We can see the output for the CSV single validator, and everything passed fine; we perfectly parsed a valid CSV file. Now let's break it and see what our agent does when it has a specialized self-validation tool. I'll remove a closing quote from the CSV to corrupt it, clear the agent's context, and rerun the exact same `/csv-edit` command. Watch: it read and immediately, because the PostToolUse hook ran, the validator caught the broken CSV and said "resolve this error." The agent immediately fixed it, reran the report properly, and mentioned the fixed issue. That's our PostToolUse hook inserting determinism directly into the agent's workflow.

Some engineers will say "that was so simple, why do you need a whole prompt for CSV validation, the models are good enough now" — stop, full stop. You want to build focused agents that do one thing extraordinarily well, because a focused agent with one purpose outperforms an unfocused agent with many purposes and many end states. We can push this further with specialized hooks embedded in prompts, subagents, and skills — this is critically important because my CSV agent can now validate its work deterministically. I'm shocked more engineers aren't talking about this; it shows a weird gap right now with a lot of vibe coding happening, even among engineers.

Side note: you have to actually read the documentation. Too many engineers and vibe coders just copy the top of a docs page, paste it into their coding tool, and say "build this." When you do that, you learn nothing — the whole point of the learning journey is the journey itself. If you don't read the docs, you don't know what your agent is doing, which is leaning too heavily on vibes. The big difference between real engineering and vibe coding/vibe engineering is that engineers know what their agents are doing, and that requires reading the documentation of the thing you're building against. I'm seeing too many engineers outsource learning entirely, which is how the self-deprecation process begins — you stop learning. Take the time to read through the docs so you can teach your agents to do it.

Anyway — that CSV-edit prompt now self-validates permanently; every time you run the command, the agent validates its work when it finishes. That alone is the whole idea: self-validation is now specializable. Before this, we were stuck writing only global hooks in `settings.json` (still useful — e.g. a "Claude Code damage control" skill that blocks dangerous commands). But now we get something extraordinary: specialized self-validation embedded per prompt/agent/skill.

Let's look at what this looks like inside a subagent and a skill — similar structure, a couple of caveats. Looking at Claude Code's release notes, hooks were buried in a bullet list even though it's a huge feature — the team has been "cooking." There's also a weird trend right now of the Claude Code team merging custom slash commands and skills into one concept, since they realized both are really just "a prompt that runs in your agent" — again validating the core-four framing: context, model, prompt, tools.

Building the CSV-edit agent (subagent) version: same tools mirrored from the prompt, no disallowed list, no skill needed, same hooks (delete pre/stop, keep post), same prompt — just slightly reworded since subagents take the prompt passed into them rather than arguments. By now our background `/review-finances` agentic workflow had completed after about 8 minutes, automatically handling the mock month's finances end-to-end.

Now the subagent demo: deploy one CSV-edit subagent per file to append three new rows across the mock input/expenses files, properly incrementing the running balance (deposits add, so a $650 deposit increases the balance accordingly). As we run this, four CSV agents kick off in parallel, one per file, and after each one runs, it validates the file it just edited — so we have both individual self-validating prompts and self-validating subagents that scale via parallelization. Other examples: a build command has two Stop hooks — a linter and a formatter using Astral's `uv` and `Ruff` tooling — that run only when the build agent finishes, not on every tool call.

All four CSV subagents validated their edits at basically the same time, proving parallel execution with guaranteed, verified edits — because we gave the agents the tools to validate their own work. The idea generalizes: imagine you're doing a database migration or any work you'd normally check by hand — you can now teach agents to validate that automatically, turning any prompt into a closed-loop system. You could still hand-write "validate your work with `uv run ...`" inside the prompt text itself, but the advantage of putting it in a hook is that it always runs, every time a relevant tool is called — a guarantee, not a suggestion. This is part of why techniques like the Ralph Wiggum loop and "agents plus code beats agents alone" are gaining popularity: you're adding trust to the system by setting it up right, not by doing the validation yourself. This is "the new ring around your codebase" — in agentic engineering, you work on the agents that run your application, not the application itself.

Every good engineer validates their own work, and soon every good specialized agent will validate the one thing it does well. That's why a small, focused `csv-edit` agent will consistently outperform a big generalist agent over tens, hundreds, thousands, or millions of runs — it's not that a bigger agent (like Opus) can't do the task, it's that specialization plus self-validation scales more reliably.

Turning to the full `/review-finances` pipeline: it's the same agentic-workflow pattern used consistently throughout the channel, with an HTML validator at the top level and a chain of specialized subagents underneath — categorize CSV, merge accounts (with its own CSV validator), normalize CSV (running two validators on Stop), and a generative-UI agent (with its own HTML validator). Rule of thumb: use a Stop hook to test many files at the end of a run, and a PostToolUse hook to validate one file right after it's touched (giving your script access to the specific path that was read/edited/written).

The result: a generated financial dashboard comparing January and February — partly static template, partly agent-generated tables and insights about spending, burn rate, income, and balance that IndyDevDan didn't explicitly design. He was confident the whole pipeline would work end-to-end precisely because of these specialized validators at every step. You can push this even further by passing an entire hooks-enabled `settings.json` as JSON directly into a primary agent invocation via `claude -p`.

Closing thoughts: specialized self-validation via hooks in prompts, subagents, and skills isn't getting enough attention. Claude Code (running on models like Opus 4.5) is the leader in agentic coding and enables this new "agentic engineering" role — but be careful not to overuse these models to the point where you stop learning. Read the docs, follow the major releases from the tools you depend on, and don't delegate the learning process to your agents, or you'll be stuck. Definitely check out specialized self-validation via hooks in your own custom slash commands, subagents, and skills. Stay focused and keep building.

</details>
