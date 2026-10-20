---
title: "NVIDIA’s New AI Just Changed Everything"
video_id: ZQAz_HrUq68
channel: "[[channels/Two Minute Papers]]"
uploaded: 2026-04-07
processed: 2026-07-05
duration: "8:10"
url: https://www.youtube.com/watch?v=ZQAz_HrUq68
playlist: "[[Agents skills n8n]]"
type: news
difficulty: beginner
use_case: [open-source-llm-releases, llm-inference-speedup]
tools: []
llms: [Nemotron]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# NVIDIA's New AI Just Changed Everything

![thumbnail](https://i.ytimg.com/vi_webp/ZQAz_HrUq68/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=ZQAz_HrUq68) | 📅 Uploaded [[uploaded/2026-04-07]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Two Minute Papers breaks down NVIDIA's Nemotron 3 Super, a free, fully open 120-billion-parameter AI assistant (trained on 25 trillion tokens) released with a full 51-page technical paper covering training data and methodology. Its NVFP4 quantized version matches a full-precision variant's accuracy while running up to 7x faster than similarly capable open models.

**Watch this if:** you want a plain-English explanation of how NVIDIA made an open model both roughly frontier-level (from ~1.5 years ago) and dramatically faster to run, without sacrificing accuracy.

## Key Takeaways
- Nemotron 3 Super is fully open: NVIDIA released the model, weights, and a 51-page paper detailing training steps and the dataset (25 trillion tokens) used, unlike typical closed frontier models.
- At 120B parameters, it roughly matches the best closed frontier models from about a year and a half ago, while remaining free to use.
- Two versions were released — BF16 and NVFP4 — with similar accuracy, but NVFP4 runs about 3.5x faster than the BF16 version and up to 7x faster than similarly smart open models.
- NVFP4 compresses ("rounds off") the math the model uses to run faster, but selectively leaves the most sensitive calculations untouched to avoid the accuracy loss that naive rounding would cause.
- The model uses multi-token prediction, generating and verifying roughly 7 tokens at once instead of one token at a time, for another major speedup.
- It incorporates "mamba layers" — a memory mechanism that takes compressed notes on a conversation rather than re-reading the full context repeatedly, discarding filler while retaining key details, enabling efficient processing of large amounts of data.
- Naive number-rounding compounds errors over many generation steps; NVIDIA fixes this with "stochastic rounding," adding carefully crafted noise that averages to zero so the compounding error cancels out over many steps.
- Even with these speedups, complex reasoning tasks can still take a long time (the presenter notes almost an hour for a complex math question), so heavier workloads may still benefit from faster cloud GPU instances.

## 🛠 Tools & Software
None identified.

## 🤖 LLMs Mentioned
- [[topics/Nemotron]] — NVIDIA's Nemotron 3 Super, a 120B-parameter, fully open model (BF16 and NVFP4 variants) that roughly matches frontier models from ~1.5 years ago while running up to 7x faster in its quantized form.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Read NVIDIA's Nemotron 3 Super technical report for the full training methodology and dataset details if building or fine-tuning open models yourself.
- Compare the NVFP4 and BF16 variants if you need to choose between raw accuracy and inference speed for your own deployment.
- Consider a faster cloud GPU instance for particularly long/complex reasoning workloads even on a fast open model.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: most AI systems are proprietary and secretive, but this one isn't
- `0:52` — Nemotron 3 Super introduced with a full 51-page technical paper covering training and data
- `1:07` — 25 trillion training tokens produce a 120B-parameter assistant matching frontier models from ~1.5 years ago
- `1:58` — Two versions compared: BF16 and NVFP4, with similar accuracy but very different speed
- `2:20` — NVFP4 is 3.5x faster than BF16 and up to 7x faster than similarly smart open models
- `2:41` — Secret 1: NVFP4 compresses math while protecting sensitive calculations from accuracy loss
- `3:52` — Secret 2: multi-token prediction generates and verifies ~7 tokens at once
- `4:27` — Secret 3: "mamba layers" take compressed notes instead of re-reading full context
- `5:16` — The problem: rounding errors compound over many generation steps
- `6:04` — Secret 4: stochastic rounding adds noise that averages to zero, canceling compounding error
- `6:30` — Limitation: complex reasoning tasks can still take up to an hour; faster cloud GPUs help
- `6:53` — Closing thoughts: NVIDIA investing heavily in open systems, shifting the AI landscape

## Transcript
<details>
<summary>Full transcript</summary>

Remember that most AI systems are proprietary, we have to pay a subscription for them, and no one knows how they work or what data they were trained on? Well, now hold on to your papers Fellow Scholars and check out this incredible work, and when I first saw it, my jaw hit the floor. They absolutely knocked it out of the park. They spilled all the secrets. This is an AI assistant that is free for all of us forever, but not just the model itself. They also gave us a 51-page research paper which might be the holy bible of creating such a system for now. Why is that? Well, they show us every step of the way of how it was done, and the dataset it was trained on as well. That is extraordinary. Usually something is always missing. Not here. They call it Nemotron 3 Super and we are going to find out whether it is indeed super or not.

Okay, so in goes 25 trillion tokens as training data, and out comes a 120 billion parameter AI assistant that is how smart exactly? It roughly matches the best closed frontier models from about a year and a half ago. Note that those models cost billions of dollars to train and every detail about them was kept in secret. And now, we just get this kind of stuff for free. That is mind blowing. This is amazing for us, consumers and Fellow Scholars.

So as you see, it is really smart. Up with some of the best open models out there in most tests, but note that it's still a bit behind some areas. Here's something that surprised me: in this result, they showcase two versions of the new model, BF16 and NVFP4. They perform roughly the same in terms of accuracy, so why the big fuss about this? Well, look at this. Holy mother of papers. Wow. Well, the NVFP4 version is about 3.5 times faster than their other model, and it is up to 7 times faster than similarly smart open models. So the story is not just the similarly smart part, the story is that it is 7 times faster while it is similarly smart. Goodness.

Okay, so how on Earth did they do that? So here are 4 secrets they gave us from the paper, in very simple words. Dear Fellow Scholars, this is Two Minute Papers with Dr. Károly Zsolnai-Fehér.

Okay, NVFP4. What is that? This is a way for speeding up the AI to run a great deal faster by essentially compressing the mathematics it uses. Seeing a long number and rounding off a few digits. You get a smaller format. Less work! What's wrong with that? Well, everything. Normally, if you do that, you lose too much accuracy and the system will output nonsense. However, here, scientists did it the smart way: they left the most sensitive calculations alone, and did this rounding for the rest, where it does not cause trouble. The result is that it runs up to 7 times faster than many other techniques. And we saw that it gives us no meaningful loss in accuracy. Magic.

But there is more magic. When other AI techniques write their answer, they write it token by token. Let's simplify by saying word by word. Writing one word at a time. But not this one. This one calculates several future words at once. A whole sentence! Almost. Specifically, 7 tokens. And then the system verifies the 7 tokens in one go. Another massive speed up. They call it multi-token prediction.

But why stop there? Let's add even more magic! They showcased these weird things they call the mamba layers. What do these do? Well, traditional AI systems have a bit of a memory problem. They work like a student who constantly re-reads the textbook over and over again when they are given a question. Scientists at NVIDIA say, that's not the way to go. Memory is precious. So instead, read the book only once, and take highly compressed notes. So this kind of memory remembers important details about the conversation. However, it is smart enough to throw away the filler words. Thus, this system can process massive amounts of data efficiently.

All this sounds glorious, but this still does not give us a working system. Why is that? Well, this is why. You see that there is a lot of addition here? That is the problem. The AI generates your answer step by step, and because we rounded off the numbers, there is a little error. That's not a problem. Here's the problem. There are many steps, and the error is magnified through each step. Imagine trying to walk to your car, which is a 100 steps away, but you feel a bit sluggish today and every single one of your steps is a bit smaller than it was before. What's the result? Well, of course, after a 100 steps, you are still really far away from your car! So what is the solution? Well, scientists solved this by adding back some random noise in the system. But wait, this noise is carefully crafted in a way that it averages to zero. So your new steps are sometimes smaller, and sometimes bigger than they used to be, but if you average them out, over a 100 steps, you will be exactly at your car. So good! They call this stochastic rounding and it is a genius idea.

Now, not even this technique is perfect. For instance, when I give it my favorite question about assembling robotic cows, with lots of math, I like this guy a lot, but it thinks for almost an hour to get me an answer for that one. That's a lot. So if I have workloads like that, I like to run it on a much faster Lambda instance. But still I think the AI game has suddenly changed. Closed systems used to dominate. Now, not anymore. It seems to me that Jensen at NVIDIA is not playing games here. It's in the news that they are going to invest tens of billions of dollars into fully open systems like this. I am not a money person, I don't know how that works exactly, but if we get to own more amazing free AI systems. Well, sign me up for this one! What a time to be alive!

And there is just so much more in the paper, I would definitely love to come back for at least another video on it. Let me know in the comments if you would like that, and if you enjoyed this, subscribe, and hit the bell.

</details>
