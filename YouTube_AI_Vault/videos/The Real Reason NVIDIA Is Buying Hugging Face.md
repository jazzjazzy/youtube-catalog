---
title: "The Real Reason NVIDIA Is Buying Hugging Face"
video_id: 8_FjjgbQpKs
channel: "[[channels/Devsplainers]]"
uploaded: 2026-08-28
processed: 2026-09-11
duration: "7:31"
url: https://www.youtube.com/watch?v=8_FjjgbQpKs
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [model-mirroring, platform-risk]
tools: [Hugging Face, llama.cpp, Transformers, Gradio, Safetensors, GitHub, GitHub Copilot, CUDA, olah]
llms: [DeepSeek, Qwen, Kimi, Llama, Nemotron]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# The Real Reason NVIDIA Is Buying Hugging Face

![thumbnail](https://i.ytimg.com/vi_webp/8_FjjgbQpKs/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=8_FjjgbQpKs) | 📅 Uploaded [[uploaded/2026-08-28]] | 🗓️ Processed [[created/2026-09-11]]

## TL;DR
> NVIDIA has reportedly agreed to buy Hugging Face for $12.9 billion — roughly 86x revenue — and the deal includes llama.cpp, the engine that runs models on hardware NVIDIA doesn't sell. The video argues the real prize is data (a live feed of what every developer downloads) and defaults (every `from_pretrained` call points at huggingface.co), with Microsoft's GitHub acquisition as the playbook. It closes with a practical hedge: mirror your weights with HF_ENDPOINT and olah, pin versions, and watch four warning signals.

**Watch this if:** your production or CI pipelines pull models from the Hugging Face Hub and you want cheap insurance before the deal closes.

## Key Takeaways
- The $12.9B price can't be justified by [[topics/Hugging Face]]'s ~$150M revenue — the multiple buys control of the platform: [[topics/Transformers]] (3M installs/day), [[topics/Safetensors]], [[topics/Gradio]], the Hub client, and 13M users whose scripts default to one domain.
- Open models were never a threat to NVIDIA: [[topics/DeepSeek]], [[topics/Qwen]], [[topics/Kimi]], and [[topics/Llama]] are overwhelmingly served on NVIDIA GPUs, and NVIDIA is itself the biggest open-weight publisher on the Hub with 45M+ downloads of its [[topics/Nemotron]] models.
- The real threat is rival chips: a Chinese frontier-scale open model trained end-to-end on Huawei processors gives adopters a stack with no need for [[topics/CUDA]], and Chinese labs took 41% of Hub downloads last year.
- Owning the Hub gives NVIDIA two levers — download telemetry before competitors see trends, and control over which builds sit on top of search results.
- Microsoft's [[topics/GitHub]] acquisition is the template: the platform stayed open, [[topics/GitHub Copilot]] got woven into every corner, and neutrality expired anyway after seven years.
- [[topics/llama.cpp]] is where tilt would show first — its Metal and Vulkan backends now depend on maintainers whose paychecks would come from NVIDIA; a community fork gets the code but not the payroll.
- The working escape hatch is one environment variable: point HF_ENDPOINT at a self-hosted [[topics/olah]] mirror and the entire client stack, Transformers included, follows.

## 🛠 Tools & Software
- [[topics/Hugging Face]] — the acquisition target: 3M+ models, 1M datasets, and the default model hub in nearly every AI script and CI pipeline.
- [[topics/llama.cpp]] — included in the deal; runs models on Macs, AMD cards, and CPUs — hardware NVIDIA doesn't sell — making it the first place to watch for neglect.
- [[topics/Transformers]] — Hugging Face's Python library with 3M+ daily installs; the `from_pretrained` default endpoint is the core of what NVIDIA is buying.
- [[topics/Gradio]] — Hugging Face's demo framework, part of the acquired library stack.
- [[topics/Safetensors]] — Hugging Face's weight format that modern models ship in, also part of the package.
- [[topics/GitHub]] — Microsoft's $7.5B purchase of it is presented as the playbook for how platform buyouts play out.
- [[topics/GitHub Copilot]] — the strategic product Microsoft wove into GitHub, foreshadowing what NVIDIA could do with the Hub.
- [[topics/CUDA]] — the software moat keeping AI glued to NVIDIA GPUs; non-CUDA backends are the deal's collateral risk.
- [[topics/olah]] — open-source self-hosted Hugging Face mirror recommended as the escape hatch via the HF_ENDPOINT variable.

## 🤖 LLMs Mentioned
- [[topics/DeepSeek]] — cited as an open model served overwhelmingly on NVIDIA GPUs.
- [[topics/Qwen]] — same argument: every open-weights release sells more NVIDIA hardware.
- [[topics/Kimi]] — listed among the major open models running on NVIDIA silicon.
- [[topics/Llama]] — listed alongside the other open-weight model families benefiting NVIDIA.
- [[topics/Nemotron]] — NVIDIA's own open-weight models, 45M+ downloads on the Hub.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Mirror the model weights and datasets your production and CI depend on tonight — it's cheap insurance whether or not the deal closes.
- Pin your library versions; open licenses can't be clawed back and pinned versions keep working.
- Stand up a self-hosted mirror with olah and run one staging test against your own HF_ENDPOINT so a cutover is a known quantity.
- Watch the four warning signals in order: account walls or rate limits on anonymous downloads; GGUF/MLX/ROCm builds losing placement to NVIDIA-optimized ones; NVIDIA badges creeping into rankings and search; Gerganov or core Transformers maintainers leaving.

## 🔗 Related Videos
- [[videos/Best 120b Model for Offline Use Nemotron 3 Super Out Now]] — shared: Hugging Face, Nemotron, Qwen
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: DeepSeek, Kimi, Qwen
- [[videos/Pick the Wrong Gemma 4 and You'll Think It's Broken FOUR Models Compared]] — shared: Kimi, Qwen, llama.cpp
- [[videos/The Most Powerful Free TTS Model You've Never Heard Of]] — shared: GitHub, Gradio, Hugging Face
- [[videos/Using GitHub Spec Kit with your EXISTING PROJECTS]] — shared: GitHub, GitHub Copilot, Llama
- [[videos/Google Just Released an AI That Predicts the Future]] — shared: GitHub, Hugging Face
- [[videos/OpenSource AI Tools That Feel ILLEGAL To Get Free]] — shared: DeepSeek, Qwen
- [[videos/Someone open-sourced a hedge fund (53k stars on GitHub)]] — shared: DeepSeek, Qwen

## Timeline
- `0:00` — The $12.9B deal, with llama.cpp included
- `0:14` — Gerganov and the llama.cpp team joined Hugging Face in February
- `0:35` — What NVIDIA actually gets: Transformers, Safetensors, Gradio, the Hub client, 13M users
- `1:30` — Price analysis: 86x revenue vs Microsoft's $7.5B for GitHub
- `1:51` — Hugging Face rejected NVIDIA's $500M investment at a $7B valuation in January
- `2:19` — Follow the GPUs: DeepSeek, Qwen, Kimi, and Llama all sell NVIDIA hardware
- `3:04` — The real threat: a Huawei-trained frontier model and a stack with no need for CUDA
- `3:38` — Two levers: download telemetry and control of defaults
- `4:14` — The GitHub playbook: open platform, Copilot everywhere, neutrality expired anyway
- `5:12` — llama.cpp's Metal/Vulkan backends now depend on NVIDIA paychecks
- `5:37` — Why torrent mirrors like The Hugging Bay won't hold at scale
- `6:01` — The one-line escape hatch: HF_ENDPOINT plus an olah mirror
- `6:26` — What to do now: mirror, pin, staging-test, and the four warning signals

## Transcript
<details>
<summary>Full transcript</summary>

Nvidia has reportedly agreed to buy Hugging Face for 12.9 billion dollars and the deal [music] includes llama.cpp, the engine that runs AI models on hardware Nvidia doesn't sell. In February, Georgi Gerganov and the llama.cpp team joined Hugging Face to give local AI a stable home. Six months later, that home seems close to being sold to Nvidia. Is this the end of open source? We'll show you what Nvidia gets for those billions and what you should do before the deal closes. Hugging Face hosts over 3 million models and a million data sets and the files are the least valuable part. The product developers depend on is the library stack. Transformers, the Python library half the AI tutorials on Earth start with, gets installed over 3 million times a day. SafeTensors is the format [music] modern model weights ship in and Hugging Face Hub is the client baked into almost every AI tool and CI pipeline. Every from pre-trained call in your code calls [music] out to huggingface.co by default. At Gradio, the framework behind most model [music] demos, a version control layer for huge files and a robotics team that slots [music] straight into Nvidia's own robot ambitions. 13 million registered users and every one of their scripts points at the same domain out of the box.

Hugging Face makes about 150 million dollars a year. The reported price is roughly 86 times that revenue and Microsoft paid 7 and 1/2 [music] billion for GitHub on more revenue than Hugging Face has today. A multiple like that buys control of the platform because the cash flow can't justify it. In January, the Financial Times reported that Hugging Face rejected a $500 million dollar from Nvidia at a 7 billion valuation because it didn't want a single big investor influencing its decisions. Now, it just sold the whole company to that same investor for 26 times the money it turned down. Founder Clément Delangue spent years calling Hugging Face the Switzerland of AI. Switzerland isn't supposed to be for sale. Open models were supposed to be the counterweight to Nvidia, [music] so the deal reads like Nvidia T-boning open source. The money flows the other way. Deep Seek When, Kimi, and Llama all get served overwhelmingly on Nvidia GPUs. So, every open weights release sells more Nvidia hardware. Morgan Stanley ran the scenarios in August and called Nvidia the leading beneficiary whether closed labs win, open models win, or the market splits.

Jensen Huang said it himself in July. Free AI should be great for chips. Nvidia is even the biggest open weight publisher on Hugging Face with over 45 million downloads of its own Nemotron models. The threat Nvidia [music] does face is rival chips. In February, a Chinese lab shipped a frontier-scale open model trained end-to-end on Huawei processors. A default model that comes tuned for someone else's hardware hands every [music] company adopting it a software stack with no need for CUDA, the software layer that keeps AI glued to Nvidia GPUs. And Chinese labs took [music] 41% of all Hugging Face downloads last year by Hugging Face's own count. Owning the hub gives Nvidia [music] two levers against that future. The first is data, a live feed of what [music] every developer downloads and what hardware they run it on before any competitor sees the trend. The second is defaults. The hub is where adoption decisions happen, and the owner decides which [music] build sits on top of the search results. Many hub users prefer Nvidia over anyone else since Nvidia earns from every open model that runs anywhere and has less reason to break the platform than Microsoft, OpenAI, or Cloud would.

Keeping the platform open costs Nvidia nothing, and both levers work fine on an open platform. Microsoft ran this play once already with GitHub, and the fears in 2018 sounded identical. The exodus never came. Microsoft kept the platform open, invested in it, and let it run independently for years. It also wove Copilot, its own strategic product, into every corner of the site. And 7 years in, GitHub CEO left, and what remained got folded into Microsoft's AI division. The platform stayed open the whole time, and the neutrality expired anyway. [music] There's one big difference this time. Microsoft in 2018 was one software giant among several. Nvidia today is the dominant company in AI. Buying the distribution layer for the part of AI [music] it doesn't already control. Hugging Face got to 13 billion because it belonged to nobody and served everyone. And that trade doesn't transfer with the servers.

llama.cpp is where you'll notice it first. Its value is running models well on Macs, AMD [music] cards, and plain CPUs. And its Metal and Vulcan backends now depend on maintainers whose paychecks would come from Nvidia. If those backends start lagging behind the CUDA one, the community can fork the project, but a fork gets the code without the payroll. So, couldn't we just torrent everything? A mirror called The Hugging Bay was being passed around before Nvidia's name was even attached to the sale. It won't hold at scale. 3 million models means a long tail nobody seats and the files were the easy part anyway. The hard [music] part to replace is the search placement, the model cards and every script on Earth defaulting to the same domain.

The escape hatch that does work is one environment variable. Point HF endpoint at a mirror you host yourself with an open [music] source tool like Ola and the whole client stack Transformers included follows it to the new address. One line redirects everything. Nothing changes for your workflow today. The libraries carry open licenses nobody can claw back and your pinned versions keep working. The cheap insurance is worth taking anyway. Mirror the weights and data sets your production and CI depend on, pin your library versions and run one staging test against your own HF endpoint mirror so a cutover is a known quantity. Then watch for signals in the order they would appear. First, anonymous downloads getting an account wall or tighter rate limits. Second, GGUF, MLX and ROCm builds losing their spot next [music] to Nvidia optimized ones. Third, Nvidia badges creeping into rankings and search. Fourth, the people. Garganov or the core Transformers maintainers leaving. Mirror your models tonight though. It's cheap and it pays off whether this deal closes or not. [music]

</details>
