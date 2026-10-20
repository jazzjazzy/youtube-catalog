---
title: "Someone open-sourced a hedge fund — I ran it locally on Qwen3 with Ollama"
video_id: rNH7rpRPXbs
channel: "[[channels/Prompt Engineer]]"
uploaded: 2026-05-01
processed: 2026-07-05
duration: "20:22"
url: https://www.youtube.com/watch?v=rNH7rpRPXbs
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [local-multi-agent-systems, algorithmic-trading-analysis]
tools: [TradingAgents, Ollama, LangGraph, Miniconda, VS Code, Git, Docker, OpenRouter]
llms: [Qwen, DeepSeek, GPT-4, GLM, Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Someone open-sourced a hedge fund — I ran it locally on Qwen3 with Ollama

![thumbnail](https://i.ytimg.com/vi/rNH7rpRPXbs/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=rNH7rpRPXbs) | 📅 Uploaded [[uploaded/2026-05-01]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> TradingAgents is a 57.9k-star, Apache-licensed GitHub repo that simulates a full hedge fund with 7 specialized LLM agents (4 analysts, bull/bear debaters, a trader, a risk team, and a portfolio manager) built on LangGraph. The creator clones it, sets it up with Miniconda and Ollama running Qwen 3 8B on an 8GB RTX 4060 with zero API cost, and walks through a full ~41-minute run that produces a BUY recommendation on NVDA with a price target, stop-loss, and position size.

**Watch this if:** you want to see a real, non-trivial multi-agent LangGraph system (debate architecture, not just a chatbot) set up and run entirely offline on consumer hardware.

## Key Takeaways
- TradingAgents mirrors real hedge fund structure: 4 analyst agents (fundamentals, sentiment, news, technical) work in parallel and write independent reports with zero cross-contamination, then hand off to bull vs. bear researcher agents who explicitly argue rather than average toward consensus.
- The debate output plus all four analyst reports go to a trader agent (proposes direction, size, and a rationale), then a risk team (checks volatility/liquidity/correlation), then a portfolio manager with final approve/reject authority — five sequential decision layers built as LangGraph nodes with checkpoints between them.
- Version 0.2.4 (released 5 days before this video) added crash recovery (resume from the last checkpoint instead of losing analyst work) and a persistent memory log that feeds prior runs' realized returns and alpha-vs-S&P reflections back into the portfolio manager's prompt.
- Setup is genuinely reproducible: `git clone` the repo, create a Miniconda Python 3.13 env, `pip install .`, copy `.env`, install Ollama, `ollama pull qwen3`, then run the `trading-agents` CLI and pick ticker/date/analysts/LLM interactively.
- On an 8GB RTX 4060 with Qwen 3 8B (16K context), a full run took about 41 minutes, used 76.5K tokens across 16 LLM calls, and produced a BUY decision on NVDA with a $268 price target, 7-9% position size, and a 190-195 stop-loss.
- Honest limitations stated by the creator: every run is computationally heavy locally (four analyst calls plus 2-6 debate rounds plus trader/risk/portfolio), the exchange layer is simulated research scaffolding with no live broker, and output quality is bottlenecked by the underlying model size (a bigger model like a 20B+ one would sharpen results).
- The repo explicitly supports swapping in other LLM providers (OpenAI, Anthropic, DeepSeek, OpenRouter, etc.) via the `.env` config — Ollama/local was chosen purely to run at zero API cost.

## 🛠 Tools & Software
- [[topics/TradingAgents]] — the 57.9k-star open-source repo simulating a 7-agent hedge fund; cloned, configured, and run end-to-end in this video
- [[topics/Ollama]] — runs Qwen 3 8B fully locally on the creator's GPU, the local-inference backend used instead of any paid API
- [[topics/LangGraph]] — the underlying orchestration framework; every agent is a node and every agent transition is a checkpoint enabling crash recovery
- [[topics/Miniconda]] — used to create the Python 3.13 environment TradingAgents installs into
- [[topics/VS Code]] — the editor used to open the cloned repo and run the setup/CLI commands
- [[topics/Git]] — `git clone` used to pull down the TradingAgents repository
- [[topics/Docker]] — noted as an alternative supported way to run TradingAgents, added last month per the repo's changelog
- [[topics/OpenRouter]] — suggested as a cheap paid alternative (e.g. DeepSeek V4 at $0.2/million output tokens) to avoid the ~41-minute local run time

## 🤖 LLMs Mentioned
- [[topics/Qwen]] — Qwen 3 8B is the model actually run locally via Ollama for the full demo, chosen to fit an 8GB GPU
- [[topics/DeepSeek]] — DeepSeek V4 flash suggested via OpenRouter as a cheap, fast paid alternative to the slow local run
- [[topics/GPT-4]] — mentioned as a larger (~20B-class) local option for users with more GPU headroom than the 8GB used here
- [[topics/GLM]] — GLM 4.7 flash mentioned as another larger (~30B) local option for more capable hardware
- [[topics/Claude]] — referenced as an option for building similar agent workflows and for integrating with Ollama, pointed to a follow-up video

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Clone the TradingAgents repo and read its LangGraph wiring as a reference implementation for multi-agent debate architectures.
- Set up Miniconda + Ollama + Qwen 3 to run the full analyst/debate/trader/risk/portfolio pipeline at zero API cost.
- If a full local run is too slow, swap in a cheap paid model like DeepSeek V4 via OpenRouter instead of waiting ~40 minutes locally.
- Read the underlying arXiv paper (published June 2025) before treating any output as more than a research framework demo.

## 🔗 Related Videos
- [[videos/Someone open-sourced a hedge fund (53k stars on GitHub)]] — shared: Claude, DeepSeek, Docker, GLM
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: DeepSeek, Docker, Ollama, Qwen
- [[videos/You Need To Know This Before Installing OpenClaw]] — shared: Claude, Docker, Ollama, OpenRouter
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: Claude, DeepSeek, Qwen
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Docker, Git, VS Code
- [[videos/TOP 2 Engineering PLAN 2026]] — shared: Claude, OpenRouter, Qwen
- [[videos/This Agent Team Builds 100s of Features While You Sleep]] — shared: GLM, Ollama, Qwen
- [[videos/Agent memory resolved]] — shared: Claude, GLM

## Timeline
- `0:00` — Local LLM running a full hedge fund pipeline: opening demo
- `0:29` — Repo overview: 7 agents, 57.9k stars, Apache license, v0.2.4
- `1:41` — How real hedge funds are structured and how the repo mirrors that
- `2:28` — The 7 specialized agent roles walked through
- `5:51` — The bull vs. bear debate layer as the key architectural choice
- `7:35` — Trader, risk team, and portfolio manager sign-off chain
- `9:04` — Setup: git clone plus Miniconda environment creation
- `10:53` — What's new in v0.2.4: crash recovery and persistent memory
- `13:23` — Running the CLI: choosing ticker, date, analysts, and local LLM
- `18:30` — Final NVDA decision: buy, $268 target, 3-6 month horizon

## Transcript
<details>
<summary>Full transcript</summary>

This GitHub repo turns a local LLM into a hedge fund. So, I cloned this repo and ran it on my local system using local LLMs using Qwen 3 latest on my system. And you can see it's using 100% of the model is loaded on my GPU. And basically, this is running on Ollama and gives the output of a complete hedge fund starting from analyst, researcher, traders, risk managers, portfolio. We're going to see how to set this up. And before that, let's go ahead and talk about this amazing repo. So, we have seven AI agents for analyst. Four analysts here, two debaters whether debating whether it's bullish or bearish. Then we have a trader, a risk team, and a portfolio manager that gives you the ultimate decision of whether you need to take a buy or hold or sell. And all these are arguing with each other before they hand you a sell or a buy decision. And if you take a look at the repo, you can see that it's 57.9 thousand stars, climbing a thousand a day, Apache license, version 0.2.4 dropped 5 days ago. And I just have to clone this repo and ran it on my local system using Ollama. Qwen 3 was the model, about 7.8 GB size. I have an 8 GB GPU 4060 RTX Nvidia. And therefore, 100% of the model is loaded on my GPU. And we have a model working on a local system. Even with the 16,000 context length, I was able to run this whole thing. And then you see we have all the outputs of the analyst, of the researcher, trading, and the risk, and the complete report here. And this is the portfolio, the decision basically. As you can see that this is a decision for S&P 500 that we want to buy now. And this is a bull case, time horizon 3-6 months.

Real hedge funds don't have one person picking stocks. They have entire teams: fundamentals staring at the filings, sentiment people tracking what Reddit is saying, technical analyst running MACD, RSI, and whatnot, and the bear and the bull researchers argue about what all of these means. A trader sizes the position. All these reports that are generated are sent to the bearish and the bullish researcher team, and those outputs are sent to the trader. The trader sizes the position, gives the buying or selling call. Then the risk team sanitizes the volatility, and everything. The portfolio manager has the final call and gives you the decision. Seven specialized roles, seven LLM agents all talking to each other. These LLM agents can be different LLMs — the repo supports OpenAI, Google, Anthropic, DeepSeek, Zephyr, and OpenRouter API keys, configurable in the default config. But there's also the option of using Ollama, which is what was done here.

What happens is that four agents run in parallel, each writing its own report. Then bull researcher and bear researcher take all four reports and debate for as many rounds as you configure. The trader reads the full transcript and proposes a trade. Risk evaluates the proposal. The portfolio manager approves it or kills it. Quick disclaimer: the authors are explicit that this is a research framework, not financial advice — the exchange is simulated, not a live broker. Here's the architectural choice that makes this interesting: the system doesn't collapse the four analyst opinions into one number, doesn't average, doesn't vote. It hands out four reports where the disagreement is intact, and the disagreement between the agents is the signal.

The analyst layer: fundamental analyst pulls the latest filings and writes an intrinsic value estimate; sentiment analysis scrapes Reddit/X to score retail mood; news analyst tracks Fed announcements and geopolitical events and interprets how they bleed into the ticker; technical analyst runs MACD, RSI, Bollinger Bands, moving average crossings, and pattern detection. Four agents, four reports, four wildly different angles on the same stock, written in isolation with no interference between each other, keeping the reports clean before the debate layer kicks in.

Next is the bull vs. bear debate layer. Two researcher agents, one structurally bullish and one structurally bearish, not neutral, explicitly designed to disagree. They both read all four analyst reports, then argue for a configurable number of rounds — the bull pulls quotes from the fundamentals report to justify opening the position, the bear pulls quotes from the technical or sentiment report to argue against it. Most AI systems are consensus engines that average and smooth toward a median answer; this system manufactures dissent on purpose, betting that an LLM defending a position against an opposing LLM produces sharper analysis than one just asked "what should I do."

After the debate, three more agents stand between you and the trade. The trader takes the debate transcript, decides direction (long or short), size, timing, writes a one-paragraph rationale, and submits a transaction proposal. The risk management team checks volatility, liquidity, and correlation against existing positions, and pushes back with specific numbers if the trade is too aggressive. Finally, the portfolio manager reads everything — analyst reports, the bull/bear debate, the trader's proposal, and the risk team's notes — and signs off or kills it with a written reason.

Setup: open VS Code, open a terminal, `git clone` the repo, `cd` into trading-agents. Create a conda environment (Miniconda if you don't already have conda) with Python 3.13, activate it, then `pip install .` to install all dependencies listed in pyproject.toml. The whole thing runs on LangGraph — every agent is a node, every transition between agents is a checkpoint. Version 0.2.4, which dropped 5 days before this video, added crash recovery, so a run that dies mid bull/bear debate doesn't lose the analysts' work; you resume from the last checkpoint even running locally, which matters a lot since a 7B or 14B model run can take real time. It also shipped a persistent memory log: each completed run writes its decision and reasoning to a markdown file, and the next run for the same ticker pulls the realized return, computes alpha against the S&P, generates a reflection on what it got right or wrong, and injects that history into the portfolio manager's prompt. Last month they also added Docker support, plus support for more model providers like DeepSeek, GLM, and Azure OpenAI.

Copy `.env.example` to `.env`. Install Ollama from ollama.com, then `ollama pull qwen3` (5.2GB, 8B model, chosen to fit the 8GB GPU). Run `trading-agents` from inside the folder to launch the CLI: select ticker (NVDA), analysis date, language (English), all four analyst types via spacebar, research depth (shallow, chosen due to low storage), and the LLM — Ollama with Qwen 3 latest as both the quick-thinking and deep-thinking model (larger local options like a ~20B model or GLM 4.7 flash at ~30B are mentioned for users with more GPU headroom). The run then proceeds through analyst team, research team, trader, risk management, and portfolio management in sequence.

After about 41 minutes, the run completed: 8 tools used, 76.5K tokens, seven reports, 12 agents, 16 LLM calls. The report is saved to a reports folder. Fundamentals report: buy. Technical: uptrend, but a mixed news read. Sentiment: hold. The bull/bear debate resolves to a buy recommendation. The trader proposes buy with a stop-loss around 190 and a rationale. The risk team weighs aggressive/conservative/neutral scenarios. Final decision: enter a long position with 7-9% allocation targeting $268 (about 29% upside from the then-current $199 price), stop-loss 190-195, investment thesis with a 3-6 month time horizon.

Honest limitations: every analysis cycle is computationally heavy locally — four analyst calls plus 2-6 debate rounds plus trader, risk, and portfolio manager, which took ~41 minutes on Qwen 3 locally. A cheaper alternative would be a paid model like DeepSeek V4 via OpenRouter at $0.2 per million output tokens. The exchange piece is research scaffolding, not a live broker — you'd have to wire that yourself for real trading or paper trading. Output quality is bottlenecked by the underlying model; a larger model like a 20B-class one would change results. If you're building with multi-agent LLMs in 2026 and haven't at least cloned this repo and read the LangGraph wiring, you're missing one of the cleanest reference implementations on GitHub right now. In summary: seven specialized agents, real architectural choices, honest about its limitations, runs locally on Ollama if you want, and shipping fast with version 0.2.4 just adding crash recovery and persistent memory.

</details>
