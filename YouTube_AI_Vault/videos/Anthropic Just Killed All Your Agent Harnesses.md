---
title: "Anthropic Just Killed All Your Agent Harnesses"
video_id: nBH07G-zayk
channel: "[[channels/AI LABS]]"
uploaded: 2026-03-31
processed: 2026-07-05
duration: "14:02"
url: https://www.youtube.com/watch?v=nBH07G-zayk
playlist: "[[Agents skills n8n]]"
type: comparison
difficulty: advanced
use_case: [agent-harness-design, ai-coding-framework-selection]
tools: [Claude Code, GSD, BMAD, Spec Kit, Superpowers, Git, Playwright]
llms: [Claude Opus, Claude Sonnet, Claude Haiku]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Anthropic Just Killed All Your Agent Harnesses

![thumbnail](https://i.ytimg.com/vi_webp/nBH07G-zayk/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=nBH07G-zayk) | 📅 Uploaded [[uploaded/2026-03-31]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Anthropic stripped components out of its own agent harness one at a time and measured what actually still matters with Opus 4.6, finding that most of what popular frameworks like BMAD, GSD, Spec Kit, and Superpowers do (micro-detailed planning, context isolation via resets, sprint contracts) is now dead weight. Their conclusion: a modern harness needs only three roles — a high-level planner, a generator, and a separate evaluator using scored rubrics instead of pass/fail checks — and the video maps exactly what to keep, strip, or combine from each existing framework.

**Watch this if:** you're running (or building) an agent harness like BMAD, GSD, Spec Kit, or Superpowers and want to know what Opus 4.6 has made obsolete.

## Key Takeaways
- Every harness component encodes an assumption about what the model can't do on its own — those assumptions go stale as models improve, and Anthropic's own experiments (removing components one by one) found most of what BMAD, GSD, Spec Kit, and Superpowers do is now overhead for Opus 4.6.
- Micro-detailed upfront planning (BMAD/Spec Kit-style task sharding into small, prescriptive steps) now backfires: a single planning error cascades through every implementation step and locks the agent out of making its own discoveries — planning should stay high-level, describing desired deliverables rather than technical implementation.
- BMAD's PRD-generation phase is still worth keeping (its specialized agents understand product requirements better than Claude alone due to author-added external context); Superpowers' edge-case questioning session is a good high-level alternative to detailed task documentation.
- Self-evaluation is the second major failure mode: an agent grading its own code tends to praise it confidently even when subpar, especially for non-quantifiable outcomes like UI quality — every framework covered (GSD, BMAD, Superpowers) already keeps the evaluator separate from the implementer, and that separation should be non-negotiable in any custom setup.
- Sprint contracts (generator and evaluator agreeing upfront on what "done" looks like) still helped Opus 4.5 but became unnecessary with Opus 4.6, which is capable enough to handle high-level plans directly — smaller models (Sonnet, Haiku) still need documented sprint structures and explicit done-criteria agreement.
- Context isolation via periodic resets addressed "context anxiety" in smaller models (losing coherence and prematurely claiming success as the context window fills) — starting with Opus 4.5, models no longer show this behavior and can run continuously through Claude's normal compaction without resets or detailed external task breakdowns.
- The generator agent implements feature-by-feature, integrates with Git for version control, and hands work to the evaluator, which acts as an adversary assuming bugs exist rather than doing a generic pass — using tools like Playwright to simulate user interactions and check against predefined criteria before approving.
- Anthropic's evaluator uses graded, scored rubrics rather than pass/fail — e.g. four frontend criteria (design coherence, originality/avoiding AI's default purple-gradient look, craft details like typography and spacing, and functionality) — because agents have no way to know what "good" looks like to you without an explicit rubric.
- Practical recommendation: use GSD if you want an easier out-of-box planner/generator/evaluator loop, but swap its pass/fail verifier for Anthropic's scored-criteria approach; or build Anthropic's model from scratch using agent teams (not sub-agents) so generator and evaluator can communicate directly instead of writing to shared documents.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the platform the agent-team-based generator/evaluator setup is built and run in throughout the video
- [[topics/GSD]] — recommended as the easiest out-of-box framework already using a planner/generator/evaluator loop, though its pass/fail verifier is described as weaker than Anthropic's scored approach
- [[topics/BMAD]] — its detailed task-sharding is now considered overkill, but its PRD-generation agents are still recommended for the planning phase
- [[topics/Spec Kit]] — its spec-as-source-of-truth verification approach is compared against Anthropic's harness and found to lack scored rigor
- [[topics/Superpowers]] — its strict TDD enforcement (blocking code before tests exist) and edge-case questioning session are both discussed as still-useful patterns
- [[topics/Git]] — the generator agent integrates with Git for version control while implementing features
- [[topics/Playwright]] — used by the evaluator agent to simulate user interactions and test the implemented app, including via Playwright MCP in the agent-team setup

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Opus 4.5 and 4.6 are the specific models whose increased capability is shown to make sprint contracts, context resets, and micro-detailed planning unnecessary
- [[topics/Claude Sonnet]] — noted as still needing documented sprint structures and explicit done-criteria, unlike Opus 4.6
- [[topics/Claude Haiku]] — grouped with Sonnet as still requiring the older, more structured harness scaffolding

## 📡 Protocols & Standards
- [[topics/MCP]] — the evaluator agent in the agent-team setup runs browser tests via Playwright MCP while the generator implements in parallel

## ✅ Action Items
- Audit your current agent harness (BMAD, GSD, Spec Kit, Superpowers, or custom) for components that assume the model needs micro-guidance — strip anything Opus 4.6 clearly no longer needs.
- Rewrite your planner prompts to specify desired deliverables and product-level scope rather than detailed technical implementation steps.
- Make sure your evaluator agent is always a separate agent instance from the one that wrote the code, never self-graded.
- Replace pass/fail evaluation criteria with scored rubrics (e.g. design quality, originality, craft, functionality) so the agent has an explicit definition of "good."
- If using GSD, swap in a scored evaluator instead of its default plan-matching pass/fail verifier.
- Consider building a custom generator/evaluator pair as an agent team (not sub-agents) so they can communicate directly instead of writing to shared documents.

## 🔗 Related Videos
- [[videos/Anthropic Just Dropped the New Blueprint for Long-Running AI Agents]] — shared: BMAD, Claude Opus, Claude Sonnet, MCP
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Code, Claude Opus, Claude Sonnet, Git
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude Code, Claude Opus, Claude Sonnet, MCP
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Code, Claude Haiku, Claude Opus, Claude Sonnet

## Timeline
- `0:00` — Introduction: Anthropic's harness-stripping experiments
- `0:32` — What an agent harness is and why every framework shares the same core
- `1:53` — Planning: why micro-detailed upfront specs now backfire
- `4:44` — Sponsor segment
- `5:39` — Self-review: why the same agent shouldn't grade its own code
- `6:46` — Sprint contracts: needed for Opus 4.5, unnecessary for Opus 4.6
- `7:39` — Context isolation and why context anxiety no longer applies to newer models
- `8:36` — Generator agent: implementation workflow
- `9:17` — Evaluator agent: adversarial verification
- `10:42` — Graded evaluation: scored rubrics vs. pass/fail
- `12:17` — What your tech stack should actually look like now

## Transcript
<details>
<summary>Full transcript</summary>

Many AI coding frameworks have been covered previously — BMAD, GSD, Spec Kit, and Superpowers — but Anthropic ran experiments on its own agent harness, removing components one by one and measuring impact, and concluded that most of it is now dead weight. Every component in a framework encodes an assumption about what the model can't do on its own, and with Opus 4.6 those assumptions have gone stale. Agent harnesses matter for making agents work over long horizons, and while implementations differ, frameworks like GSD (focused on context isolation) targeted a problem — losing context over long tasks — that Opus 4.6 no longer really has, partly due to its million-token context window and partly for another reason covered later. Anthropic's experiments concluded that all a harness actually needs is agents for planning, generation, and evaluation — everything else is dead weight given current model capability, and any harness should keep evolving as the underlying model does, since staying on

principles laid out months ago means falling behind. Planning remains the one universal step, but how you plan has to change. Older long-running harnesses required detailed upfront specs — frameworks like BMAD and Spec Kit sharded tasks into small, prescriptive micro-steps because older models needed to be closely guided. With Opus 4.5 and 4.6, Anthropic found that if the planner specifies micro technical details upfront, a single planning error cascades through every implementation level, locking the agent out of deviating to fix its own issues — so planning is now better kept high-level, describing needed deliverables and letting the agent find its own path. This makes BMAD's and Spec Kit's detailed sharding less relevant, though BMAD's planning phase up through PRD generation is still worth keeping,

since its specialized agents understand product requirements better than Claude alone (thanks to author-added external context). Alternatively, Superpowers' edge-case-identifying questioning session can be more effective than multi-level task documentation — the core problem with overly detailed planning is that it locks the agent down and leaves no room for its own discovery. Anthropic's example planner-agent output emphasizes going big on scope and staying at the product level rather than the implementation level, since drilling into implementation detail within the plan risks losing sight of what the complete product actually needs. Claude's own plan mode isn't quite this, since it still focuses heavily on implementation detail rather than true product-level planning. With a proper planner agent in place, Claude can generate a full product-level plan with phase-by-phase user stories describing what each phase looks like from the user's perspective, helping it implement the workflows users actually expect. [Sponsored segment: MiniMax's Max Claw / MiniMax Agent, a cloud-deployed AI agent platform connecting to Telegram, Slack, and Discord, powered by their M2.7 model.] The agent that writes the code should never be the one evaluating it — a widely underdiscussed problem. Self-evaluation fails because

the same agent grading its own work tends to respond confidently and praise itself even when quality is clearly subpar. This is manageable for quantitatively verifiable tasks (does the API work) but far worse for subjective outcomes like UI quality, where the agent may consider its own work well done even when it misses your actual intent. Every framework covered (GSD, BMAD, Superpowers) already recognizes this and keeps evaluation separate from implementation, significantly improving evaluation accuracy — any custom setup should enforce the same separation. Before implementation, generator and evaluator agents can negotiate a "sprint contract" defining what done looks like so both sides know what to build and verify. Testing with Opus 4.5 showed removing this contract made the evaluator less efficient (it still had to catch issues the contract would have prevented), but with Opus 4.6 the model became capable enough that the contract was no longer necessary — for smaller models like Sonnet or Haiku, documented sprint structures and explicit done-criteria agreement are still needed, but Opus 4.6 can execute a high-level

plan without that extra scaffolding. On why context isolation used to matter: smaller models experience "context anxiety," losing coherence as their context window fills and prematurely claiming success on unfinished work. The fix was clearing context before implementation and relying on externally documented task breakdowns that survive the reset — but this anxiety was severe enough that compaction alone wasn't sufficient. Starting with Opus 4.5, models no longer show this behavior; they can run continuously through an entire session, and Claude's normal compaction handles it fine, making context resets and detailed external task breakdowns (as used in BMAD and Spec Kit) unnecessary — high-level guidance alone suffices. The generator agent is the main implementer, building feature by feature from the plan's specs while integrating with Git for version control, and hands

work to the evaluator for feedback after each feature. Its workflow moves through understanding, implementing (itself split into four sub-phases), and refining, following the design direction and verifying its own work before handoff — a structured, step-by-step pattern letting it implement an entire app independently. The evaluator agent is deliberately adversarial, approaching the work from the assumption that bugs exist rather than doing a generic bug-finding pass. It can use tools like Playwright to simulate real user interactions, identify bugs against predefined criteria, and send feedback to the generator, reading the plan to understand exactly what "done" should mean. Each framework validates differently: BMAD uses specialized code-review and QA agents testing from multiple angles; GSD uses a verifier sub-agent that checks implementation against the plan and produces a documentation report; Superpowers enforces strict

TDD, blocking any code written before its tests exist. Spec Kit treats specs as the source of truth for verification. None of these provide the level of scoring rigor Anthropic aimed for — its evaluator is closest to the Ralph loop's strict implementation enforcement, but paired with a proper graded evaluation mechanism. Since an agent has no inherent way to know what "good" looks like to you, especially for non-quantifiable work, graded evaluation criteria fill that gap. Anthropic's frontend example sets four grading criteria for both generator and evaluator: design quality (a coherent field vs. disconnected components), originality (since AI defaults to the same purple-and-white gradient look, unlike deliberate human design choices),

craft (typography, spacing consistency, balanced color contrast rather than generic styling), and functionality (each component genuinely enhancing the user experience). Claude already scores well on craft and functionality but struggles more with quality and originality, so prompts need to push it there deliberately. The same scored-criteria approach can extend to code architecture, UX flows, and any other feature area — each with its own dedicated score referenced directly by the evaluator agent as its rubric. Practical recommendation: for an easier setup, use GSD, since it already runs a planner/generator/evaluator loop by default — though its evaluator only matches code against the existing plan via pass/fail user-acceptance testing rather than scoring. You can combine the best of both by swapping GSD's evaluator for a scored-criteria version. Alternatively, build Anthropic's

approach from scratch using agent teams (not sub-agents, since sub-agents can't communicate directly and would need to write to a shared document, adding overhead) — one team member as generator, one as evaluator, working in parallel with the evaluator running Playwright MCP browser tests while the generator implements, coordinating directly to deliver an app matching your standards.

</details>
