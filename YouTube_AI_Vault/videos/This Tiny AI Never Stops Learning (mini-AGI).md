---
title: "This Tiny AI Never Stops Learning (mini-AGI)"
video_id: L-6O7R71CCg
channel: "[[channels/Better Stack]]"
uploaded: 2026-09-30
processed: 2026-10-20
duration: "13:52"
url: https://www.youtube.com/watch?v=L-6O7R71CCg
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [local-model-training, continual-learning]
tools: [TinyStories]
llms: [mini-AGI]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This Tiny AI Never Stops Learning (mini-AGI)

![thumbnail](https://i.ytimg.com/vi/L-6O7R71CCg/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=L-6O7R71CCg) | 📅 Uploaded [[uploaded/2026-09-30]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> mini-AGI is an open-source language model you train from absolute zero on consumer hardware, designed to never stop learning: it reads text one chunk at a time like a person reading a book, stores every mixture-of-experts specialist as its own file on disk (so the model can be bigger than your GPU), spawns new experts and deletes unused ones automatically, and dodges catastrophic forgetting by letting experts learn fast while the shared core changes 10x slower (99.84% knowledge retention vs ~50% loss in a normal setup). The experiment: teach it English on the TinyStories dataset on an M2 Max MacBook (~2-4 hours), then feed it Tarantino screenplays with Reservoir Dogs held out as a hidden test — ending in a hilariously incoherent but structurally-correct screenplay chat demo and an honest verdict: not AGI, not production, but a super cool trainable toy.

**Watch this if:** you want to feel what training a model from scratch is actually like on a laptop — including memorization vs learning, catastrophic forgetting, and why continual learning on disk-based experts is a big deal.

## Key Takeaways
- Every model you run locally was trained once on a GPU cluster and frozen; training takes roughly 3-4x the memory of inference, which is why you can chat with a 30B model on a MacBook but can't train even a small one — [[topics/mini-AGI]] attacks exactly this.
- Its architecture: a mixture-of-experts where each expert is a separate file on disk holding everything needed to train it; before each chunk only the needed experts load onto the GPU, new experts appear as files, unused ones get deleted — a self-governing workspace bigger than your graphics card.
- Catastrophic forgetting fix: experts change quickly, the shared core (which every byte passes through) learns 10x slower, so new knowledge lands in specialists while the foundation stays intact — the author's chess test kept 99.84% of prior knowledge vs ~50% loss in a normal setup.
- Training from zero on an M2 Max (32 GB) — a repo only ever tested on NVIDIA — produced gibberish at 7 minutes, "Once upon a time, there was very down" at 2 hours, and simple [[topics/TinyStories]]-style English at 4 hours.
- Learning vs memorizing is measurable: after ~15 minutes on five Tarantino scripts, the hidden Reservoir Dogs score plateaued while training-script scores kept improving — the model had switched from learning Tarantino to memorizing those scripts (fixed by adding more scripts).
- Continual learning works both ways: switching back to children's stories restored English in ~5 minutes (the knowledge was never erased, just on disk), and snapping back to Tarantino mode later was nearly instant, with the best hidden-script score yet.
- The scene-partner demo (character, scene heading, reply length, temperature) is charmingly broken — Freddy's answer to a bank-robbery question is "Tonics" and the model is obsessed with "a silence" — but it even switched scenes by itself.
- Verdict: toy-scale, weights not yet released, barely coherent — but going from random numbers to Tarantino characters apologizing like kindergarteners in ~9 hours on a MacBook is the point: anyone can now train continuously on consumer hardware.

## 🛠 Tools & Software
- [[topics/TinyStories]] — the children's-stories dataset used for phase one, teaching the blank model basic English in a few hours.

## 🤖 LLMs Mentioned
- [[topics/mini-AGI]] — the star of the video: a byte-level, continually-training, disk-based mixture-of-experts model trained from scratch on a MacBook and tested on held-out Tarantino.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Clone the mini-AGI repo and train a model from zero on your own machine — expect gibberish for the first hour and basic English within ~2-4 hours on Apple Silicon.
- Hold out a test document (like the hidden Reservoir Dogs script) so you can tell learning from memorizing when the training-set score keeps improving but the held-out score plateaus.
- When the model starts memorizing, add more diverse data rather than training longer on the same files.
- Exploit the continual-learning loop: alternate datasets and watch old skills come back in minutes because experts persist on disk.
- Probe the model's state with a fixed prompt every few minutes during training — a cheap window into what it currently knows.
- Keep expectations honest: coherent conversation needs hundreds of millions of characters and days of nonstop training.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Not real AGI: mini-AGI, a tiny model trained from zero that never stops learning; first sentences after 7 minutes
- `1:08` — The plan: TinyStories for English, then Tarantino screenplays, with Reservoir Dogs hidden as the held-out test
- `2:39` — Training on an M2 Max MacBook Pro (32 GB) despite the repo only being tested on NVIDIA
- `2:57` — Why this matters: shipped models are frozen, training needs 3-4x inference memory, and fine-tuning causes catastrophic forgetting
- `4:04` — How it works: chunk-by-chunk never-ending training, each expert a file on disk, loaded on demand, spawned and deleted automatically
- `5:04` — Check-in at 2 hours: "Once upon a time, there was very down" and "Timmy was sad because he was so happy"
- `5:24` — The recurring probe: a fake Tarantino scene opener answered in pure bedtime-story voice
- `6:03` — The forgetting fix: fast experts, 10x-slower shared core — 99.84% retention on the author's chess test
- `7:07` — Phase two: five Tarantino scripts; screenplay layout learned in 5 minutes, cast names in 30, English degrading into mashups
- `8:03` — Learning vs memorizing: hidden-script score plateaus; pause, retrain English (back in 5 minutes), add three more scripts, best hidden score yet
- `9:36` — Scene-partner demo: John and Freddy, "Tonics", the "a silence" obsession, and a spontaneous scene change
- `11:50` — Why it can't converse (needs hundreds of millions of characters) and the verdict: not AGI, not production, but a super cool trainable toy

## Transcript
<details>
<summary>Full transcript</summary>

Guys, AGI is finally here. Well, okay, not the real AGI. I'm talking about mini AGI. It's a tiny language model that you train from absolute zero on your own computer, and it's designed to never ever stop learning. I've been having so much fun lately with this model. So, I trained one on my MacBook, and 7 minutes into the training, it gave me sentences like thousand worded their lone Sheraton. But, just a few hours later, we got something like this. "It's okay," Lily said. It was capable of learning English in less than 2 hours. And then, I fed this model a bunch of screenplays from Quentin Tarantino to see if I can actually produce a model that would be capable of writing like Quentin Tarantino. So, in this video, we'll take a look at how mini AGI works. I'll show you what happened when I trained one from scratch, and I'll show you some of the weirdest and funniest things it said along the way. It's going to be a lot of fun, so let's dive into it.

So, first, before I get into the weeds of how this model works, let's just start training one from scratch. So, step one, we start with a completely blank model. This model doesn't know any words or grammar or nothing. It's just a bunch of random numbers, and it reads text byte by byte, letter by letter. So, first things first, we got to teach this model plain basic English. And the cool part about mini AGI is that you don't have to teach it a language, you can basically start teaching it whatever you want. But, for this model, we'll start with the tiny stories dataset, which contains a lot of examples of short children's stories, and try to give it a voice. And once step one is done, and we will have confirmed that the model can indeed write short English sentences, then we will switch to step two, and I will try to feed this model a bunch of Quentin Tarantino screenplays. Because by the end of this training, I want this model to speak in a voice of Quentin Tarantino and spit me out some script-like sentences from his famous movies. And since this is a continual training experiment, we will keep one script, Reservoir Dogs, hidden from the model the whole time, so we can test it on a Tarantino script it has never seen.

So, by the end of this, I'm hoping we can get two things. One, a model that writes something that at least smells like a Tarantino movie, and two, the answer to the big question, can this model keep learning new things without forgetting the old ones or without degrading at some point? So, let's start the training. Now, I'm training this on my M2 Max MacBook Pro with 32 GB of RAM, and this repo was only ever tested on an Nvidia card. So, yeah, we're already going off script here a bit. But, while it is learning, let me tell you what this thing actually is. So, what exactly is Mini AGI? Well, every model you've ever run locally was once trained on a giant GPU cluster and then frozen in time. And that's why these older models, whenever you would ask them, for example, what is the current US president, it would give you an outdated answer. Basically, it stopped learning the day it shipped. And a much bigger problem is that you can't really train a big model at home yourself because training needs roughly three or four times more memory than just running a model. And that's why you can chat with a 30-billion-parameter model on a MacBook, but training a model, even a small one, is a job for a giant hyperscaler data center.

And there's another problem. If you fine-tune a model on your own stuff, you get something called catastrophic forgetting. So, for example, if you would take a model trained on basic English sentences and then teach this model chess, it would suddenly forget how to write English. Which, to be honest, is how my brain works sometimes when I have to learn a new JavaScript framework. But, MiniAGI is trying to fix all of these problems. So, how does it differ from any other model? Well, first, it never stops training. It reads text in order, one chunk at a time, like a person reading a book, and it takes a small learning step after every chunk. And there is no finish line. You can just do this forever. And second, it's pretty efficient with memory. It's a mixture of experts model, and we've covered mixture of experts models a lot on this channel, so I'm not going to tell you how they work. But, basically, TLDR is it's a team of small specialist networks, and only [snorts] some of them are active at any given moment. But, here, every expert is its own file on disk, holding everything needed to train it. And before each chunk, the model loads only the experts the text needs onto the GPU. So, the model can be way bigger than your graphics card. And the specialist team grows by itself. New experts pop up as files in the folder, and the ones nobody uses gets deleted. So, it's basically a very efficient, self-governing workspace.

So, let's check in on how it's doing. 2 hours in, and it's already cracking the most important sentence in all children's literature. "Once upon a time, there was very down." Close enough. And it was already producing some material, like, for example, "Timmy was sad because he was so happy." >> [snorts] >> Same, Timmy. And just for fun, every 5 minutes, I'm also giving the English-only model a little test, the opening of an imaginary Tarantino scene that we wrote ourselves. Two men sit in a booth, one of them leans in, "Vincent." And the model has to write what Vincent says next. It doesn't learn anything from this. It's just a peek inside its brain on on it's doing at that current training stage. But so far it has only ever read bedtime stories. So Vincent is saying things like, "They said you are mine. They said you are their mom. They say you are cone." Well, this isn't going to make for a very good movie.

So 4 hours in, I finally had a model that writes simple English. And remember I mentioned catastrophic forgetting? So the author of Mini AGI tested exactly that. He took the model that had learned eight different subjects, like stories, code, and math, and then fed it half a million characters of nothing but chess. And with a normal setup, the model lost roughly half of what it knew about everything else. But Mini AGI kept 99.84% of it. And the trick to make this work was surprisingly simple. So the model has two parts, a shared core that every single letter passes through, and the experts, which are the specialists. When it learns something new, the experts are allowed to change quickly, but the shared core is only allowed to change 10 times slower. So the new stuff mostly lands in the specialists, while the foundation everything else relies on stays pretty much intact. It's like renovating a few rooms without touching the foundation of the house, if that makes sense.

Okay, so let's test that ourselves. Step two, let's teach it how to write like Tarantino. So we're going to add Pulp Fiction, Jackie Brown, Inglourious Basterds, Django Unchained, and his segment of Four Rooms to the data set, and that is basically what our screenplay data set mostly consists of. And within 5 minutes of running the second phase, it learned the layout of a screenplay, so that's already nice. We have some indentation, the character names in caps. And now within half an hour, the cast is already showing up as well, Ordell, Louis, Schultz. But now it's kind of morphing with the children's stories. So now the Tarantino movie characters are kind of apologizing like kindergarteners. Stephen, I'm soaring. Calvin's them, I'm soared. Sounds like old English. Meanwhile, its English got worse and worse until even once upon a time came out as screenplay fragments. So you can see we have some problems here.

So the problem was that after about 15 minutes it stopped getting better on the hidden reservoir script because we only have one script to compare it against, but it kept getting better on the ones it was already reading. So it stopped learning Tarantino and started memorizing those specific scripts. It's basically like learning to be funny from your uncle versus just memorizing his five favorite jokes. So then I decided to pause the training and pick it up the next day. And the next morning I switched it back to children's stories. And this is the best thing I love about this model. 5 minutes in it remembered to speak English again. So remember learning for the first time took the model hours, but now that span is a lot shorter because the knowledge was never erased. It was already on the disk. And after 2 more hours it had gotten even better at writing those children stories again. So now it was time to test it on the Tarantino data set again. But this time I added three more additional scripts so we have more data to work with and it snapped back into the Tarantino mode almost instantly. Bill from Kill Bill showed up and it got the best score yet on the hidden reservoir dogs script. And the crossover between the children's stories and Tarantino got even better. The bastards who should be more companion show up to the food court. I mean that's that's kind of nice. At least everyone's getting along.

So I kept training it for a while and after about an hour and a half I had a somewhat coherent Frankenstein model ready to go. So to test it out, I built this little screenplay page where you can test this model as a screen partner in a non-existent Tarantino movie. So, let's take it for a spin. So, as you can see here, this is our screenplay chat application here. And here you can just define what kind of character you're going to play, who's going to be your scene partner, and then we're setting a scene with a heading and an action to begin with. And then we can also choose the reply length. And then we can also tone the temperature crazy we want the responses to be. What if we invent new characters? So, I'm going to be John. And I'm going to be talking to Freddy. I'm just going to ask Freddy, "So, what are you thinking, man? Should we rob the bank today or not?" What is Freddy going to reply? Tonics. Freddy is setting some tonics. Arlene's just about her. She's almost her. Who's Arlene, man? To him. To me. All right. She's not but I a silence. You're being very mysterious, Freddy. What? Arlene's makes a way they're making him. She's cold. I mean, I do agree Arlene can be very cold sometimes. All right, Freddy. I have no chance. I have to rob this bank. Are you coming with me or not? Last chance. Freddy's setting the tone again. Shrinks car but when a silence.

Oh my god, this this this model really likes using the word a silence. Interesting. Interesting. All right, I'm hopping in the car and I'm driving away. What is Freddy going to say? She's notch and I'm sure a silence. He just had anyway still her. Man, this guy this guy is a poetic soul. I can I can feel it. >> [laughter] >> This this word just comes up so much. A silence. What if I play along? What if I just say a silence. There's always die then looks up. She's them. Oh my god, it switched to a new place by itself. [laughter] Oh my god, that is interesting. I've never encountered this before. All right, so we're now in a new scene. Where is my money, Freddy? Let's see what Freddy replies. What? What do you mean, what? Where's the money, Freddy? There's somebody girls the car. She's coming back. So, it may look quite dumb, and I understand that, but you got to realize this is a result of 7 hours of training, maybe even more, maybe like 9 hours. It's quite impressive that you can train a model from literally zero, and in 9 hours it will start spitting out some Tarantinisms. Although they don't make sense, at least at least it's something, you know?

So, as we saw there, it can't really hold a conversation. It learned what a Tarantino script looks like and who's in it, but to actually talk like him, it would need hundreds of millions of characters of English, which means we would need to train this model for several days non-stop just to get it to say basic grown-up sentences. So, I hope this shows that training models is really hard and time-consuming. But, the cool part is that with Mini AGI, you can do just that. You can now have a model that you can continuously train on your consumer hardware until you get something better out of it than the bear said, "I want to be a greatest fish." So, there you have it, folks. That is Mini AGI in a nutshell. The author calls it a toy-scale model, and the weights aren't even out yet. So, is it AGI? Hell no. Can it write a coherent sentence? Well, barely. Should you use it in production? Absolutely not. But, on a simple M2 MacBook Pro, it was capable of getting from random gibberish to Tarantino cast apologizing to each other. So, I think this is a super cool training model. So, what would you teach your own Mini AGI? Let me know in the comments down below. And folks, if you like these types of technical breakdowns, please let me know by smashing that like button underneath the video. And also, don't forget to subscribe to our channel. This has been Andrus from BetterStack, and I will see you in the next videos. >> [music]

</details>
