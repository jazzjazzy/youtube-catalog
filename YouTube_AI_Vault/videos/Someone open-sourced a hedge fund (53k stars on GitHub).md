---
title: "Someone open-sourced a hedge fund (53k stars on GitHub)"
video_id: 9FoEsXNGLwI
channel: "[[channels/Indie Hacker News]]"
uploaded: 2026-04-28
processed: 2026-07-05
duration: "8:26"
url: https://www.youtube.com/watch?v=9FoEsXNGLwI
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [algorithmic-trading-analysis, multi-agent-orchestration]
tools: [TradingAgents, LangGraph, Docker]
llms: [Claude, Gemini, Grok, DeepSeek, Qwen, GLM, GPT-4]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Someone open-sourced a hedge fund (53k stars on GitHub)

![thumbnail](https://i.ytimg.com/vi/9FoEsXNGLwI/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=9FoEsXNGLwI) | 📅 Uploaded [[uploaded/2026-04-28]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> TradingAgents is a Python framework, out of a UCLA arXiv paper, that simulates a full Wall Street trading firm with LLM agents: four parallel analysts, two debating bull/bear researchers, a trader, a risk team, and a portfolio manager with final approval. It just crossed 53k GitHub stars in four months, runs on LangGraph, and shipped v0.2.4 with structured-output decision agents and Docker support.

**Watch this if:** you want a fast rundown of what's actually inside the trending TradingAgents repo before deciding whether to clone it yourself.

## Key Takeaways
- TradingAgents mirrors a real trading firm's org chart: 4 parallel analyst agents (fundamentals, sentiment, news, technical) each write independent reports that are deliberately never collapsed into a single score — the disagreement between them is treated as signal.
- Two researcher agents, one structurally bullish and one structurally bearish, debate the analyst reports for a configurable number of rounds before handing off to a trader agent, then a risk team, then a portfolio manager with final buy/reject authority.
- The whole pipeline runs as a LangGraph directed graph — every agent is a node, every transition is checkpointed, so an opt-in resume feature lets a crashed run pick back up without losing completed analyst work.
- A persistent decision log (always on) writes each run's decision and reasoning to a markdown file, and on the next run for the same ticker the system pulls the realized return, computes alpha vs. SPY, and injects a reflection into the portfolio manager's prompt.
- Setup is a straightforward clone/pip-install/CLI flow, and the CLI supports essentially every major LLM provider — OpenAI, Gemini, Claude, Grok, DeepSeek, Qwen, and Ollama for local models.
- Version 0.2.4 (shipped 3 days before this video) added Pydantic-based structured-output decision agents across the research manager, trader, and portfolio manager, plus DeepSeek/Qwen/GLM/Azure OpenAI support and Docker with multi-stage builds.
- Honest caveats stated in the video: heavy LLM token spend per analysis cycle (four analysts plus multiple debate rounds plus trader/risk/portfolio calls), it's explicitly a research framework and not financial advice, and the exchange is a backtest — there's no live broker integration.

## 🛠 Tools & Software
- [[topics/TradingAgents]] — the 53k-star repo under review: its architecture, analyst/researcher/trader/risk/portfolio agent chain, setup flow, and v0.2.4 release are walked through in detail
- [[topics/LangGraph]] — the orchestration engine underneath TradingAgents; every agent is a graph node with checkpointed transitions enabling crash recovery
- [[topics/Docker]] — new in v0.2.4: Docker support shipped with multi-stage builds as an added way to run the framework

## 🤖 LLMs Mentioned
- [[topics/Claude]] — listed among the LLM providers the TradingAgents CLI supports
- [[topics/Gemini]] — listed among the supported LLM providers
- [[topics/Grok]] — listed among the supported LLM providers (via xAI)
- [[topics/DeepSeek]] — supported provider, and explicitly added as a new provider option in the v0.2.4 release
- [[topics/Qwen]] — supported provider, and explicitly added as a new provider option in the v0.2.4 release
- [[topics/GLM]] — added as a new supported provider in the v0.2.4 release
- [[topics/GPT-4]] — OpenAI's GPT models listed among the supported LLM providers

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Clone the TradingAgents repo and read through its LangGraph wiring as a reference implementation for multi-agent debate architectures.
- Try running the CLI against a real ticker with the debate-round count turned up to see how the bull/bear disagreement changes the final call.
- If experimenting locally, weigh the token cost of four analysts plus multiple debate rounds before running it repeatedly.
- Read the underlying arXiv paper (2412.20138) for the full architecture and evaluation behind the framework.

## 🔗 Related Videos
- [[videos/Someone open-sourced a hedge fund — I ran it locally on Qwen3 with Ollama]] — shared: Claude, DeepSeek, Docker, GLM
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Claude, DeepSeek, Gemini, Grok
- [[videos/I Let Strix Attack My App Here's What It Found]] — shared: Claude, Docker, Gemini
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: DeepSeek, Docker, Qwen
- [[videos/Stop Prompting Claude Use Karpathy's Method Instead]] — shared: Claude, Gemini, Grok
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, Gemini, Qwen
- [[videos/7 new open source AI tools you need right now]] — shared: Claude, Gemini
- [[videos/Agent memory resolved]] — shared: Claude, GLM

## Timeline
- `0:00` — Intro: a Python repo just crossed 53k GitHub stars this weekend
- `1:09` — The README: what TradingAgents actually simulates
- `2:24` — Why it matters: teams that argue produce defensible positions
- `3:02` — The spec sheet: stars, forks, license, release cadence
- `3:19` — The 4 parallel analyst agents explained
- `4:45` — Under the hood: LangGraph nodes, checkpoints, persistent decision log
- `5:30` — Installation: clone, pip install, set API key, run CLI
- `6:04` — Latest release: v0.2.4's structured outputs and Docker support
- `6:48` — Who it's for: quant researchers, hobbyist traders, fintech founders
- `7:25` — Verdict: real project, real caveats, worth cloning

## Transcript
<details>
<summary>Full transcript</summary>

Somebody just open-sourced a hedge fund. Okay, so here's something kind of wild that's been climbing the GitHub trending list this weekend. There's a Python project called TradingAgents that just crossed 53,000 stars, and what it actually does is pretty unhinged when you think about it. It's a multi-agent LLM framework that mirrors the structure of a real Wall Street trading firm. You spin it up, point it at a stock ticker, and it runs an entire simulated firm under the hood: fundamentals analyst, sentiment analyst, news analyst, technical analyst, bullish researcher, bearish researcher who actually debate each other, a trader agent, a risk management team, and a portfolio manager who approves or rejects every transaction. All of them powered by LLMs talking to each other. 53,678 stars, 9,768 forks, Apache 2.0 license, and version 0.2.4 shipped 3 days ago. It started as a research paper out of UCLA in late 2024, then quietly got open-sourced, and the GitHub repo has been doubling stars every couple months since.

Let me show you what's actually in it. So the core idea is that real hedge funds don't have one person picking stocks — they have entire teams, and those teams argue with each other because that argument is what produces a defensible position. The authors broke a typical trading firm's operations into specialized roles and built one LLM agent per role. The analyst team is four agents working in parallel: fundamentals digs into company financials, sentiment scrapes social media and public mood, news monitors macroeconomic indicators, and technical runs MACD, RSI, and the usual chart indicators. Then it gets interesting: the researcher team has two agents, a bull and a bear, explicitly designed to disagree. They take the analyst reports and argue against each other for a configurable number of rounds before handing off. The trader agent reads everything, decides timing and position size, and proposes a transaction. The risk management team evaluates that proposal against volatility and liquidity, and finally the portfolio manager either approves or rejects it. The whole graph runs on LangGraph, so every agent transition is a node — you can resume from a checkpoint if it crashes, and there's a persistent decision log that learns from how previous trades actually played out.

Why is this a big deal when there are already a hundred other algorithmic trading frameworks? Most of them are either really mechanical rule-based systems or black-box ML models that spit out a signal with no explanation. TradingAgents sits in between — every decision is fully traceable. You can read the analyst reports, the bull/bear debate transcripts, exactly why the trader picked that position size, and why the portfolio manager rejected it. It's auditable in a way traditional quant systems are not. The repo is Python, 53,000 stars, 9,700 forks, Apache 2.0, and the underlying paper is on arXiv as 2412.20138 with full citations.

Getting into the actual agents: the fundamentals analyst pulls the latest filings, runs ratio analysis, and writes an intrinsic value estimate. Sentiment scores Reddit, X, and other social signals. News tracks global macro indicators and breaking events that move prices. Technical runs MACD, RSI, Bollinger Bands, and standard pattern detection. All four run in parallel, all four produce a written report, and the system explicitly does not collapse them into a single vector — the disagreement is signal, not noise. Then two researcher agents read everything: one structurally bullish, one structurally bearish, arguing across multiple configurable debate rounds, citing specific numbers from the analyst reports. At the end, the trader agent reads the full debate transcript and makes a call. The risk team then evaluates volatility and liquidity, and the portfolio manager has final approval — if approved, the order goes to a simulated exchange; if rejected, the loop ends with a written explanation.

Under the hood, the whole orchestration runs on LangGraph, meaning every agent is a node in a directed graph and every transition is checkpointed. That checkpoint-resume feature is opt-in, but if a run crashes halfway through you don't lose the analyst work. There's also a persistent decision log, always on, that appends every completed run's decision and reasoning to a markdown file. On the next run for the same ticker, the system fetches the realized return, computes alpha against the SPY benchmark, generates a reflection on what went right or wrong, and injects that history into the portfolio manager prompt — the system literally learns from past trades.

Setup is painless: clone the repo, create a Python environment, pip install, set the API key for whichever LLM provider you want, and run the CLI. It supports basically every major model — OpenAI GPT, Google Gemini, Anthropic Claude, xAI Grok, DeepSeek, Qwen, and Ollama for local models. The CLI drops you into an interactive picker for ticker, analysis date, provider, and debate rounds. Version 0.2.4 shipped 3 days ago and is a significant release: structured-output decision agents. The research manager, trader, and portfolio manager now use Pydantic schemas with each provider's native structured output mode, so decisions parse cleanly and failure modes drop dramatically. They also added DeepSeek, Qwen, GLM, and Azure OpenAI as supported providers, shipped Docker support with multi-stage builds, and introduced a five-tier rating scale — buy, overweight, hold, underweight, sell — used consistently across the research manager, portfolio manager, and decision log.

Who should pay attention to this? Quant researchers doing systematic strategy work get a clean reference implementation of wiring LLMs into a multi-agent decision graph. Hobbyist traders can spin this up against their own portfolio in about 10 minutes. Fintech founders get a permissively licensed foundation to fork and extend. And indie hackers curious about multi-agent LLM systems get one of the cleanest examples around. Being honest about tradeoffs: running this on every analysis cycle burns real money in LLM tokens since each ticker triggers four parallel analyst calls plus multiple debate rounds plus trader and portfolio manager calls. The authors explicitly say this is a research framework, not financial advice — don't yolo your retirement into whatever the portfolio manager spits out. The simulated exchange is a backtest, not a live broker integration, so you'd have to wire that part yourself. But for everything that's a caveat, the project is real: Apache 2.0, 53,000 stars in 4 months, weekly releases, multi-language documentation, and an actual published paper backing the architecture. If you build with LLM agents in 2026 and haven't at least cloned this repo and read the LangGraph wiring, you're missing one of the cleanest reference implementations out there.

</details>
