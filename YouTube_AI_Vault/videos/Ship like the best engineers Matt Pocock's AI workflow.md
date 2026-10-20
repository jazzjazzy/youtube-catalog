---
title: "Ship like the best engineers: Matt Pocock's AI workflow"
video_id: Q3uuE2adUT8
channel: "[[channels/The Hype Kevin]]"
uploaded: 2026-10-09
processed: 2026-10-20
duration: "9:05"
url: https://www.youtube.com/watch?v=Q3uuE2adUT8
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [agentic-coding-workflow, spec-driven-development]
tools: [Matt Pocock Skills, Agent Skills, GitHub, pstack]
llms: [Claude Opus]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Ship like the best engineers: Matt Pocock's AI workflow

![thumbnail](https://i.ytimg.com/vi/Q3uuE2adUT8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Q3uuE2adUT8) | 📅 Uploaded [[uploaded/2026-10-09]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> An animated walkthrough of Matt Pocock's agent-skills workflow (his skills repo has more GitHub stars than React; v1.3 shipped October 4), traced through one feature — a Pause button for a coffee subscription app and the bag that was already packed when the customer paused. The flow: the "grill me" interview maps a decision tree and empties its frontier before any code exists, a glossary pins one word to one thing, /to-spec writes the destination, /to-tickets slices it to fit the ~150k-token "smart zone", implement-spec builds one agent per ready ticket, review happens at two fresh desks (spec vs coding standards), /pr adds a merge-danger section, and /retro turns session pain into lint rules and instruction lines. Your job in all of it: the decisions.

**Watch this if:** your agent ships whole features unsupervised and you want the discipline — grilling, specs, tickets, two-desk review, retros — that keeps its silent guesses from becoming production behavior.

## Key Takeaways
- Agents fill every unstated gap with a guess and keep going ("agents are polite like that") — a one-sentence prompt silently decided billing cutoffs, pause duration, reminder emails, and the fate of the packed bag.
- The grilling skill in [[topics/Matt Pocock Skills]] inverts the conversation: it maps the feature as a decision tree in fog, asks the current frontier in one numbered round with recommended answers, fetches facts from the code itself via helper agents, and cannot write code until the frontier is empty (6 questions on small changes, ~20 normal, once 46).
- Grill-with-docs maintains a glossary — pause vs skip, each one line plus forbidden synonyms — so the agent stops using twenty words where one would do; "wait what" re-pitches the agent's last message in plain glossary English.
- Ungrillable questions (what should the screen look like?) get throwaway prototypes in a fresh session; you click through and pick, and the answer returns to the grilling.
- /to-spec writes the problem, fix, user stories, and agreed test seams (ideally one); /to-tickets slices the spec into vertical, independently shippable slices sized to the ~150k-token smart zone (a term borrowed from Dex Horthy) — guess the job's tokens and divide by 150k.
- Implementation is test-first with one clean head per ticket (or v1.3's implement-spec: one agent per ready ticket in its own repo copy, landing on one branch); the refactoring step was dropped because the agent "never, ever, ever did it" — it moved to review.
- Review happens at two separate desks with fresh agents: one reads the diff against the spec, the other against coding standards and Fowler's code smells — standards the implementer deliberately never saw; /pr writes descriptions with before/after proof and a merge-danger section (one-way vs two-way door, blast radius).
- /retro mines the session for environment fixes — a pointer line in the instructions, a lint rule for machine-spottable mistakes — but only suggests, never autopilot, because an agent fixing its own findings chases false positives; a real 41-story spec became 10 linked tickets in 4 minutes and ~14,000 lines merged in just over two hours.

## 🛠 Tools & Software
- [[topics/Matt Pocock Skills]] — the skills repo at the center of the video: grilling, grill-with-docs, wait-what, to-spec, to-tickets, implement, implement-spec, code review, the new /pr and /retro, with 16 of 27 skills lazy-loaded (660 tokens installed) and skills deleted as models catch up.
- [[topics/Agent Skills]] — the mechanism itself: one-line entry points (grill me is a single line calling a 28-line skill) whose value is the questions, not the code.
- [[topics/GitHub]] — where the specs become issues labelled ready-for-agent, the ten-ticket run and merge-danger PRs live, and where the repo out-starred React.
- [[topics/pstack]] — the lighter-weight alternative stack one builder switched to, arguing Matt's skills are too defensive for today's models.

## 🤖 LLMs Mentioned
- [[topics/Claude Opus]] — Matt read out a real Opus reply ("It is genuinely load bearing though...") as the jargon problem that motivates the glossary and the wait-what skill.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Before any feature work, run a grilling pass and refuse to let the agent code until the decision frontier is empty.
- Keep a glossary in the repo: one line per term, plus the synonyms to avoid; use it to disambiguate every new word mid-conversation (skip ≠ pause).
- Settle visual/UX questions with throwaway prototypes in a fresh session rather than more talking.
- Size tickets by the smart zone: estimated tokens ÷ 150k, each slice vertical (database to button) and independently testable.
- Hide coding standards from the implementer and enforce them with a separate fresh reviewer alongside a spec reviewer.
- Add a merge-danger section to PRs: one-way vs two-way door, plus the blast radius.
- Run /retro after every session and convert machine-spottable mistakes into deterministic checks; keep only judgment calls in written standards — and never put retro on autopilot.
- Treat the spec as disposable: close the issue once the decisions live in code, tests, and glossary.

## 🔗 Related Videos
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Opus, GitHub
- [[videos/15 Claude Code Tricks That Feel Like Cheating]] — shared: Claude Opus, GitHub
- [[videos/Claude Code's Creator Does This Before Every Single Project]] — shared: Claude Opus, GitHub
- [[videos/Complete OpenClaw Setup Guide (With Venice)]] — shared: Claude Opus, GitHub
- [[videos/How to Never Hit Your Claude Session Limit Again]] — shared: Claude Opus, GitHub
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude Opus, GitHub
- [[videos/I Can't Believe Anthropic Messed Up The Ralph Wiggum]] — shared: Claude Opus, GitHub
- [[videos/Meet Sidecar You might never open Cursor again]] — shared: Claude Opus, GitHub

## Timeline
- `0:00` — The question: your agent builds a feature while you make coffee — so what are you there for?
- `0:17` — The silent guess: pause ships in ten minutes, but the agent decided the billing, the duration, and the packed bag
- `0:47` — Why longer prompts fail, and grill me: the agent interviews you before any code exists
- `1:02` — The decision tree in the fog: frontier questions in numbered rounds with recommended answers; facts from helper agents, decisions from you; 6 to 46 questions
- `1:54` — Grill-with-docs keeps a glossary (pause vs skip, banned synonyms); "wait what" re-pitches in plain English after an Opus jargon reply
- `2:41` — Ungrillable questions become throwaway prototypes you click through
- `2:56` — /to-spec: problem, fix, numbered user stories, agreed seams (ideally one — billing), posted as a ready-for-agent issue
- `3:29` — /to-tickets and the smart zone: ~150k tokens per fresh session, vertical slices, dependency-linked tickets
- `4:08` — The build: one clean head per ticket or implement-spec (v1.3) fanning out one agent per ready ticket onto one branch, test-first; refactoring step dropped
- `4:41` — Review at two desks: spec reviewer and standards/Fowler-smells reviewer, standards hidden from the implementer; /pr with proof and merge danger
- `5:40` — /retro: session pain becomes instruction lines and lint rules, suggestions only — then the real run: 41 stories, 10 tickets in 4 minutes, ~14k lines merged in ~2 hours
- `7:06` — Pushbacks answered: not waterfall (the spec is a disposable projection) and not too defensive (lazy-loaded skills, 660 tokens, deleted as models improve); your job is the decisions — agent sergeant, you general

## Transcript
<details>
<summary>Full transcript</summary>

Your agent can build a whole feature while you make a coffee. So what are you there for? Matt Pocock has an answer. He teaches developers for a living, he made Total TypeScript, and his answer is a folder of agent skills with more stars on GitHub than React. On October fourth he shipped version one point three. Say you run a coffee subscription app, and you type: let users pause their subscription. Ten minutes later there's a Pause button, the tests pass, and it works. Then a customer pauses on the twenty-ninth and still gets a bag of coffee on the first, because it was already roasted and packed. Somebody had to decide what happens to that bag. Your agent decided. It also decided whether the bill stops today or at the end of the month, how long a pause can last and what the reminder email says. You wrote one sentence, so it filled every gap with a guess and kept going. Agents are polite like that. Couldn't you write a longer prompt? You'd only write down the decisions you thought of, and the packed bag wasn't one of them.

Matt turns the conversation around. Before any code exists, the agent interviews you, and his skill for it is called grill me: a relentless interview about your plan. Picture the feature as a tree of decisions in the fog. Pause sits at the top. Under it hang billing, the packed bag and how long a pause lasts, and each of those has more decisions hanging off it. The grilling skill maps that tree, finds every decision whose parent is already settled, called the frontier, and asks you all of them in one numbered round. Each question comes with the agent's recommended answer, so a lot of the time you type "yes, yes, no, end of the month". Your answers settle a layer, a new frontier lights up, and the fog moves back. Facts are the agent's job: if the answer is somewhere in the code, it sends a helper agent to go and read it. Decisions are yours. And it can't start on the code until the frontier is empty and you agree you're on the same page. On a small change Matt gets about six questions, and around twenty on a normal one. While filming a lesson for his course, it once asked him forty-six. His post about it: dude, chill, you're scaring the noobs.

Halfway through, you mention customers can skip a month. The agent stops you: is skip the same thing as pause? This version is called grill with docs, and it keeps a glossary in your repo while it grills. Pause gets one line: no deliveries and no charges until the resume date. Skip gets another: one delivery missed, billing carries on. Under each, the words to avoid, like hold and freeze. An agent dropped into a project has to guess its jargon, so it uses twenty words where one would do. Matt once read out a real reply from Opus 5 that ended, "It is genuinely load bearing though, so that's how you know it matters." Then he asked the obvious question. What does that mean? So there's a skill for that moment too. Type wait what, and the agent pitches its last message again in plain English, using the words from your glossary. Some questions won't settle by talking, like what the pause screen should look like. For those ungrillable ones, the agent hands off to a fresh session, builds a throwaway prototype with a few screens that look nothing alike, and you click through them and pick. Then the answer comes back to the grilling.

When the fog is gone, you stay in the same chat and type to spec. No more questions this time. The agent writes up everything you settled: the problem, the fix, and a long numbered list of user stories. As a customer who pauses after my bag is packed, I still get that bag, and my pause starts after it. First, though, it agrees the seams with you, the places where the tests will poke at the feature, and the ideal number of seams is one. For us that's the billing module. The spec goes up as an issue in your tracker, labelled ready for agent. The spec is the destination. The tickets are the journey. Why tickets? Because an agent gets worse the more it's holding. Somewhere past a hundred fifty thousand tokens it stops reasoning as sharply, and the part before that is the smart zone, a term Matt says he stole from Dex Horthy. So to tickets cuts the spec into slices that each fit one fresh session. Each slice runs through every layer, database to button, so it works on its own. Ticket one: pausing stops the next charge. Ticket two: a resume date. Ticket three: the packed bag. Ticket four: the emails. Three and four can't start until one is done. The rule of thumb: guess the tokens a job needs and divide by a hundred fifty thousand, so a million-token refactor becomes seven tickets.

Then the build. Type implement on ticket one, clear the chat, implement ticket two, so every ticket starts in a clean head. Or use implement spec, new in one point three, which builds the whole spec in one go: one agent per ready ticket, each in its own copy of the repo, all landing on one branch. Either way it works test first. A failing test at the agreed seam, then only enough code to pass it, one slice at a time. The skill used to have a refactoring step too. Matt dropped it, because the agent "never, ever, ever did it". Refactoring moved to review, and review happens at a different desk. An agent that has written some code thinks it's fine, because it wrote it. So code review hands the diff to two fresh agents. One reads it against the spec, looking for anything missing, anything nobody asked for and anything that looks done but is wrong. The other reads it against your coding standards and a dozen classic code smells from Martin Fowler's Refactoring. The agent that wrote the code never saw those standards. Models are bad at following a list of don'ts while they build, and a reviewer hunting for exactly those problems has nothing else on its mind. On ticket three, the spec reviewer quotes our user story back: pausing today cancels the packed bag.

When the fix goes up as a pull request, a skill called PR writes the description. It's adapted from Dex Horthy's show me skill: the smallest picture that explains the change, proof from before and after, and a section called merge danger. Is this a one-way door or a two-way door, and how big is the blast radius? Ours adds a column to the subscriptions table. Two-way door, blast radius billing. The last step is the other big one in one point three. Before you clear the chat, type retro. The agent reads back through the session it just had and suggests changes to its surroundings: the repo, the checks, the instructions. That matters, because your agent won't complain. It bumps into problems, keeps pushing until the feature works, and the struggle stays buried in the transcript. Here it spent ten minutes hunting for the billing code, so it suggests one line in your agent instructions that points at it. It called the payment provider directly twice, which your codebase never does, so that becomes a lint rule. A mistake a machine can spot gets a check, full stop, and the written coding standards keep only the judgment calls. Found an error? Do a retro, and make it impossible next time. People keep asking Matt to put retro on autopilot, and he says don't, because an agent fixing its own findings ends up chasing false positives. It only suggests, and you pick which fixes to keep.

A coffee app is a toy, so take something real. On September twenty-fifth, in the app Matt uses to make his courses, a spec went up with forty-one user stories. Within four minutes there were ten tickets, linked by what blocks what: one ticket started the chain, five waited on it, and the last one stayed open on purpose as research. All of it landed on one branch, twenty-eight commits and almost fourteen thousand lines, merged a little over two hours after the spec was written. Five days later, the next feature's pull request had its own merge danger section. Two-way door, blast radius deploy ordering. Isn't this waterfall with extra steps? That's the most common pushback, and Uncle Bob made the case on Matt's own live stream. Watch what happens to the spec, though. Once the work ships, Matt closes the issue and the spec is gone. He calls a spec a projection of the decisions made during grilling, and by then those decisions live in the code, the tests and the glossary. The prototypes keep it from turning into waterfall, and anything small enough for one session gets planned in one session.

The other pushback says smart models don't need this much structure. One builder switched to pstack, the stack from our last video, because Matt's skills felt too defensive for today's models. Most of them cost nothing until you call them, though. Sixteen of the twenty-seven skills in the plugin only exist when you type their name, so the agent never sees them, and in his tutorial the whole installed set took up six hundred sixty tokens. He also deletes skills once the models catch up. Version one point three removed the merge-conflict skill, because the harness can handle it. So what's inside the repo with more stars than React? Open grill me, which skills dot S H counts at over a million installs. It's one line long: call the skill tool with grilling. The grilling skill it calls is twenty-eight lines, and Matt calls the original grill me "the most influential four sentences I've ever written." There's almost nothing in there to copy. The value is in the questions, and only you can answer them.

So what are you there for? The decisions. The agent can write every line of the pause feature, and every call inside it still belongs to you: the bill, the bag, the word skip. Matt thinks of agents as brilliant tactical programmers who need a strategic one above them, so the agent is the sergeant and you're the general. Our customer pauses on the twenty-ninth, gets the bag that was already packed, and pays nothing more until the resume date. You decided that in round two, on your coffee break. I'm Kevin. When something new drops in AI or tech, I take it apart here and tell you if it's worth the hype. Subscribe so you catch the next one.

</details>
