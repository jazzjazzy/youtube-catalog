---
title: "The Claude Shutdown Is a Total Sh*tshow"
video_id: R4nFEQb7kZo
channel: "[[channels/House of El - AI]]"
uploaded: 2026-06-18
processed: 2026-07-05
duration: "22:22"
url: https://www.youtube.com/watch?v=R4nFEQb7kZo
playlist: "[[Agents skills n8n]]"
type: news
difficulty: beginner
use_case: [ai-safety-regulation, ai-industry-news]
tools: []
llms: [Claude, Claude Mythos, Claude Fable, GPT-5, Kimi]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The Claude Shutdown Is a Total Sh*tshow

![thumbnail](https://i.ytimg.com/vi_webp/R4nFEQb7kZo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=R4nFEQb7kZo) | 📅 Uploaded [[uploaded/2026-06-18]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> A US government export-control order forced Anthropic to pull its two most advanced Claude models (Mythos 5 and Fable 5) worldwide after Amazon researchers found that asking the model to "fix this code" bypassed guardrails that blocked "review this code" — a jailbreak cybersecurity experts call an unfixable dual-use problem, unfolding against a backdrop of Anthropic's Pentagon standoff over autonomous weapons and its pending IPO.

**Watch this if:** you want the technical and political context behind a major AI model shutdown, including why "dual-use" cybersecurity capabilities can't be cleanly patched.

## Key Takeaways
- On June 12, 2026, the US government ordered Anthropic to disable its two most advanced models — Claude Mythos 5 and Claude Fable 5 — for all users worldwide, framed as an export-control action citing national security.
- The jailbreak, discovered by Amazon researchers, was trivial: asking the model to "review this code" for vulnerabilities was refused by guardrails, but asking it to "fix this code" complied — because fixing bugs requires identifying them first, and the model can't distinguish defensive from offensive intent (the "dual-use problem," which also exists in nuclear physics and biotech research).
- Independent cybersecurity expert Katie Moussouris (Luta Security), asked by Anthropic to review Amazon's findings, concluded the jailbreak is real and simple but cannot meaningfully be fixed without weakening the model's value for legitimate defensive security work.
- Because US export-control law treats giving a non-citizen access to a technology as an "export" regardless of physical location, Anthropic had no way to restrict the ban geographically and had to pull the models globally, including for its own non-citizen employees.
- The shutdown follows months of conflict between Anthropic and the Pentagon over autonomous weapons: CEO Dario Amodei publicly refused a Pentagon demand to allow Claude for fully autonomous weapons and mass surveillance, after which the administration barred federal agencies from using Anthropic's tech, OpenAI secured a Pentagon deal, and Sam Altman publicly dismissed Anthropic's safety disclosures as "fear-based marketing."
- An open letter signed by 100+ cybersecurity professionals from Nvidia, Adobe, Zoom, Google and others pointed out that the same code-review capability exists in OpenAI's GPT-5.5, other Claude models, and Chinese models like Moonshot AI's Kimi 2.7 — undercutting the claim that Fable posed a uniquely dangerous capability.
- The timing coincided with Anthropic's confidential IPO filing at a reported ~$965B valuation, raising the question of whether the shutdown reflects genuine unique risk or competitive/political dynamics between Anthropic, Amazon, and OpenAI.

## 🛠 Tools & Software
None identified.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — Anthropic's overall AI system/competitor to ChatGPT and Gemini, referenced throughout as the affected product line
- [[topics/Claude Mythos]] — Anthropic's restricted, cybersecurity-specialized model (Project Glasswing), the more powerful precursor to Fable
- [[topics/Claude Fable]] — the public-facing model with guardrails derived from Mythos; the one pulled worldwide over the jailbreak
- [[topics/GPT-5]] — referenced (as "GPT-5.5") in the open letter as having comparable code-review/vulnerability-finding capability to Fable
- [[topics/Kimi]] — Moonshot AI's model, referenced (as "Kimi 2.7") in the open letter as another model with comparable capability

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Read Katie Moussouris's/Luta Security's assessment of the Fable jailbreak for the technical case on why "dual-use" cybersecurity AI capabilities resist simple patching.
- Read the Free Fable open letter (100+ cybersecurity professionals) for the argument that pulling defensive AI tools while adversary capabilities advance is itself a security risk.
- Track Anthropic's IPO filing and the Pentagon/OpenAI contract dynamics as context for whether AI regulation actions here are driven by safety or by competitive and political incentives.

## 🔗 Related Videos
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Claude, GPT-5, Kimi
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, GPT-5
- [[videos/How I Watch ANY Video with AI in Seconds]] — shared: Claude, Claude Fable
- [[videos/The 3-Rule Prompt That Stops ChatGPT, Gemini, and Claude From Guessing]] — shared: Claude, GPT-5

## Timeline
- `0:00` — Three words, global shutdown: the order to pull Fable and Mythos worldwide
- `2:15` — Meet the AI models they pulled: Mythos (Project Glasswing) and Fable
- `4:48` — "Fix this code": how the jailbreak actually worked and the dual-use problem
- `11:45` — This was never just about cybersecurity: the Pentagon/autonomous-weapons conflict
- `14:45` — Did they just torpedo Anthropic's IPO? The ~$965B valuation timing
- `17:19` — The AI problems we're ignoring: cognitive impact, surveillance, job losses, cost spirals
- `18:40` — The real fire burning: closing argument on misplaced regulatory priorities

## Transcript
<details>
<summary>Full transcript</summary>

Three words, "fix this code," is what it took for the United States government to order the most powerful AI model on Earth pulled from every user on the planet. On June 12th, 2026 at 5:21 p.m. on a Friday, Anthropic received a directive from the US government ordering it to immediately disable two of its most advanced AI models, Claude Fable 5 and Claude Mythos 5, for all users worldwide, not just in the US. The stated reason was an export control action citing national security. The underlying trigger, according to multiple reports and Anthropic's own account, was a jailbreak — a way of getting the model to do something guardrails were supposed to prevent — and that jailbreak consisted of asking the model to fix some code.

Anthropic is the company behind Claude, the AI system that competes with OpenAI's ChatGPT and Google's Gemini. In April 2026, Anthropic previewed a model called Mythos. Mythos was, by Anthropic's own description, exceptionally capable at finding security vulnerabilities in software — during internal testing it identified flaws in every major operating system and web browser it was tested against, and it was the first AI model to successfully complete both cybersecurity test ranges used by the UK AI Security Institute. It could autonomously find and chain multiple vulnerabilities together — orchestrating entire attack sequences without human intervention. Anthropic did not release Mythos publicly; it restricted access through a program called Project Glasswing, sharing it with roughly 50 vetted organizations including Amazon, Apple, Google, Microsoft, and CrowdStrike, exclusively for defensive cybersecurity work. Then on June 9th, Anthropic released Fable 5 — essentially Mythos, but with guardrails designed to block the model's most dangerous capabilities in cybersecurity and biology while preserving general intelligence for everyday use. Fable immediately benchmarked as the most capable AI model available to the public. According to testing by Val AI, it was live for 3 days.

What is a jailbreak? When an AI company releases a model publicly, it adds guardrails — instructions and classifier systems telling the model what it should and shouldn't do (don't help make weapons, don't provide instructions for illegal activity, don't generate cybersecurity exploits). A jailbreak is a prompt that gets the model to bypass those guardrails. Every frontier model has jailbreaks; they're discovered, patched, and new ones found continuously — that's normal. What's not normal is a government pulling a model from every user on Earth over one.

The specific jailbreak was discovered by researchers at Amazon. They gave Fable software code with known vulnerabilities. When they asked the model to review the code for security issues, it refused — the guardrails caught it. But when they asked it to fix this code, it complied without hesitation, because fixing code requires identifying what's wrong with it first. The model had to find the vulnerabilities in order to generate the patch, and a researcher could then manually turn those fixes into scripts that could potentially exploit the very flaws the model identified. The model was trained to refuse explicit security analysis requests, but it wasn't — and arguably can't be — trained to refuse fixing code, because fixing code is one of the most common and valuable things an LLM does, and the model has no way to know whether the person asking intends to use the identified flaw offensively. This is the "dual-use problem," and it isn't unique to AI — it exists in nuclear physics (enrichment powers both reactors and bombs) and biotechnology (gain-of-function research that helps vaccines could also help engineer a pathogen). Any capability that helps a defender find and fix a vulnerability also helps an attacker find and exploit it.

Katie Moussouris, founder of Luta Security, a former Microsoft cybersecurity expert with two government advisory roles, was asked by Anthropic to review Amazon's research. Her assessment: the jailbreak was real, it was simple, and it cannot meaningfully be fixed — any attempt would only weaken the model for defense. She wrote that defenders need to be able to ask AI to fix bugs in a file, explain why the fix matters, and write tests confirming the patch works; otherwise, cybersecurity professionals are fighting sophisticated nation-state hackers without their best tools. She also noted Fable's guardrails were, if anything, too aggressive on launch day, blocking legitimate defensive research.

On the mechanics: the government's directive was framed as an export control restricting access by foreign nationals, but US export control law treats distributing restricted technology to any non-citizen as an export even if that person is physically in the US. There's no way to filter users by citizenship in real time across a global platform serving hundreds of millions of people, so Anthropic had to disable the models for everyone, including its own non-citizen employees — applying a Cold War-era regulatory framework designed for physical weapons and nuclear material to a chatbot software update.

An open letter — "Free Fable" — signed by over 100 cybersecurity professionals from Nvidia, Adobe, Zoom, Google, and others made a further point: this capability isn't unique to Fable. OpenAI's GPT-5.5, Anthropic's own other Claude models, and Chinese models including Moonshot AI's Kimi 2.7 can all perform similar code reviews. The stated justification — that Fable provides unique uplift beyond other models — doesn't hold against the evidence, and the letter warns that pulling the best defensive tools from cybersecurity professionals while adversaries' capabilities advance is dangerous.

Here's where the story stops being just about a jailbreak. In February 2026, the Pentagon demanded Anthropic allow its AI to be used for all lawful purposes, including fully autonomous weapons and mass domestic surveillance. Anthropic CEO Dario Amodei publicly refused, saying Anthropic cannot in good conscience exceed that request and that autonomous weapons and mass surveillance are outside the bounds of what today's technology can safely and reliably do. The Pentagon's under secretary for research and engineering, Emil Michael, responded on X by calling Amodei a liar with a god complex. On February 27th, President Trump ordered all federal agencies to immediately stop using Anthropic's technology, and the Pentagon designated Anthropic a supply chain risk — a classification normally reserved for companies tied to foreign adversaries. Within days, OpenAI announced a Pentagon deal, with Sam Altman positioning OpenAI as the cooperative alternative and later describing Anthropic's handling of Mythos as "fear-based marketing" — "it is clearly incredible marketing to say we have built a bomb, we were about to drop it on your head, we will sell you a bomb shelter for $100 million."

Three months later, that same administration ordered Anthropic's models pulled — triggered by research from Amazon, which is simultaneously Anthropic's largest investor and a competitor via its own Bedrock and Titan AI platforms. Amazon CEO Andy Jassy reportedly went straight to the Oval Office about it. The directive arrived at 5:21 p.m. on a Friday. Axios reported the administration was further inflamed because Anthropic asked a cybersecurity expert it viewed as a "radical Democrat" to review the jailbreak, and because Chris Krebs — the election security official Trump fired in 2020 — vouched for her analysis.

A pattern emerges: a company refuses to allow its AI to be used for autonomous weapons; that company is banned from government contracts; its competitor gets the deal; the first company then releases its most powerful model; that model gets pulled by the same administration, triggered by research from the company's own investor-competitor, on a Friday evening. The timing is also notable commercially: Anthropic had filed a confidential IPO prospectus at a reported valuation of around $965 billion. Anthropic's own public response was unusually direct: "We disagree that the finding of a narrow potential jailbreak should be the cost for recalling a commercial model deployed to hundreds of millions of people. If this standard was applied across the industry, we believe it would essentially halt all new model deployments for all frontier model providers."

On the autonomous weapons question specifically, the host states personal agreement with Amodei's position: no autonomous weapons — only circumstance, not humans or algorithms, should decide who lives or dies. There's also an irony worth noting: Anthropic was, by most accounts, the most transparent AI company about the dangers of its own technology — it disclosed Mythos's vulnerability-finding capability, restricted it via Project Glasswing, and built Fable's guardrails specifically to prevent misuse. That transparency became the justification used to shut it down, which teaches every other AI company the opposite lesson from what good governance should incentivize: if you find something dangerous, stay quiet about it.

The video closes by arguing the real priorities are elsewhere: AI's measurable effects on how developing minds process information and build (or fail to build) cognitive abilities; cities banning data centers because the communities paying for AI infrastructure aren't the ones benefiting; 142,000 jobs lost in 5 months while the companies doing the firing post record revenue; enterprise AI costs spiraling with no clear economics; surveillance infrastructure nobody can figure out how to turn off; and a search engine redesigned around AI that gets things wrong tens of millions of times per hour. A three-word jailbreak on a model that 100+ cybersecurity experts say is no more capable than its competitors doesn't rise to the level of emergency those other problems represent — and the longer political and regulatory attention stays on the wrong fire, the more time the actual fires have to spread.

</details>
