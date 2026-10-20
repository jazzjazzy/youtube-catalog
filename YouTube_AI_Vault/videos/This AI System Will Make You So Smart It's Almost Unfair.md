---
title: "This AI System Will Make You So Smart It's Almost Unfair"
video_id: b4d32pBa3UY
channel: "[[channels/Dan Martell]]"
uploaded: 2026-06-25
processed: 2026-07-05
duration: "12:02"
url: https://www.youtube.com/watch?v=b4d32pBa3UY
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [ai-second-brain, personal-knowledge-management]
tools: [Obsidian, Notion, Google Drive, Granola]
llms: [Claude]
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# This AI System Will Make You So Smart It's Almost Unfair

![thumbnail](https://i.ytimg.com/vi_webp/b4d32pBa3UY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=b4d32pBa3UY) | 📅 Uploaded [[uploaded/2026-06-25]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Dan Martell walks through building a personal "AI brain": a paid AI subscription, a structured Obsidian vault with identity files and topic folders, an extraction pipeline that feeds meeting/decision context into that vault, and a nightly automated consolidation job — so the AI carries persistent context instead of forgetting everything between chats.

**Watch this if:** you want your AI assistant to remember who you are, your decisions, and your relationships instead of re-explaining context every conversation.

## Key Takeaways
- Pay for a real AI membership — free tiers give you older, slower models; paying alone puts you ahead of 99.7% of users.
- Give AI a permanent place to read from: Google Drive (basic folders), Notion (AI-native data store), or Obsidian (free, markdown-based, visual graph view) — Obsidian is the recommended default.
- Give the brain an identity with three files: `user.md` (who you are, how you communicate, your frameworks), `soul.md` (the AI's voice/tone/values and how it should challenge you), and `identity.md` (who the AI is and its role) — have the AI interview you and draft these itself rather than writing them by hand.
- Organize the vault into structured folders — people, projects, decisions, companies, meetings, daily, knowledge, plus an optional MOC (maps of content) folder — going from no structure to these folders raised his AI's answer accuracy from 60% to 85%.
- Feed the brain by extracting only decisions, commitments, preferences, and key insights from raw sources (e.g. meeting transcripts via Granola with a custom extraction prompt) rather than dumping raw, unfiltered data into it.
- Compound the brain nightly: run a consolidation prompt (manually, or automated via a scheduled/cron task) that finds orphan notes, creates missing files, merges duplicates, updates MOCs with new links, and flags strategic items for review — this is what turns static storage into a self-improving brain.

## 🛠 Tools & Software
- [[topics/Obsidian]] — recommended vault tool for the AI brain; free, markdown-based, with a graph view showing how notes connect
- [[topics/Notion]] — alternative "AI-native" cloud data store option for the brain
- [[topics/Google Drive]] — basic folder-based option for storing the brain, described as limited and unstructured
- [[topics/Granola]] — used to auto-transcribe meetings and extract decisions/commitments/preferences/insights via a custom prompt template

## 🤖 LLMs Mentioned
- [[topics/Claude]] — used via its scheduled task feature to run a nightly cron job that consolidates the Obsidian vault

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Upgrade to a paid AI plan before building anything else.
- Create `user.md`, `soul.md`, and `identity.md` files by having your AI interview you about how you work and what you want from it.
- Set up the core vault folders in Obsidian: people, projects, decisions, companies, meetings, daily, knowledge, and an MOC folder once things get messy.
- Use a meeting-notes tool like Granola with a custom extraction prompt (decisions / commitments / preferences / key insights) instead of saving raw transcripts.
- Schedule a nightly "compound the brain" prompt (via cron or Claude's scheduled task) to find orphan notes, consolidate duplicates, and update MOCs automatically.

## 🔗 Related Videos
- [[videos/The Best MCP Servers of 2025]] — shared: Claude, Notion, Obsidian
- [[videos/Andrej Karpathy Just 10xd Everyones Claude Code]] — shared: Claude, Obsidian
- [[videos/Claude Code just Built me an AI Agent Team (Claude Code + Skills + MCP)]] — shared: Claude, Notion
- [[videos/Claude HeyGen Just Changed Content Creation Forever]] — shared: Claude, Google Drive
- [[videos/Convert Any MCP Server to Code Execution (Template)]] — shared: Google Drive, Notion
- [[videos/Docker Just Fixed 90% of AI Coding By Releasing This]] — shared: Claude, Notion
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Notion

## Timeline
- `0:00` — Intro: the AI-powered brain overview
- `0:18` — Step 1: Go pro — pay for a real AI membership
- `0:42` — Step 2: Install the brain — Google Drive vs. Notion vs. Obsidian
- `2:19` — Step 3: Give your brain an identity (user.md, soul.md, identity.md)
- `5:07` — Step 4: Wire the brain — 7 core folders plus the MOC folder
- `7:23` — Step 5: Feed the brain — extracting from meetings via Granola
- `9:12` — Step 6: Compound the brain — manual vs. automated nightly consolidation
- `10:48` — Recap of all six steps

## Transcript
<details>
<summary>Full transcript</summary>

I built a fully AI-powered brain that runs across every part of my life. It helps me run dozens of companies, and it gets days of my life back. So, today I'm going step-by-step on how you can build the same AI brain I use to become part of the 0.0001% of AI users in the world, starting with going pro. Simple, get a pro membership for your AI. It doesn't matter which AI, invest the money. Free versions of AI give you the worst version of the tool, slow to answer. They're older models. So, as soon as you pay, you've now become part of the 0.3% of all users in the world that have a paid membership. But we want you in the 0.01%.

So, let's get into how we actually do that. Install the brain. Every AI conversation forgets the second you close it. Sure, they have some tools for memory, but it's basic things. The 0.01% give AI a permanent place to read from. That place has to be your files, in your structure that any AI can read your digital brain. So, here are three options you can pick from. The first is a Google Drive. Most people have this already, and it's kind of where it all started. But the problem is that it's pretty limited, and it's not process. The second is Notion. This is a cloud-based data structure system where I believe that the way it's built is AI native. Google is a basic digital version of a folder system. Notion is a modern AI-powered data store. So, yes, it has the files, but it also has the context, it also has the data. If you want to go to the next level, and this is what I use, I use Obsidian. The challenge with a lot of these AI systems is that you can't read what it's saved in. You can't read the information. So, Obsidian uses what's called markdown files. It's free, and it's visual. So, not only is it like a big wiki that sits on your computer, but you can also see how the brain forms and all the connections and links to the information within it. And the cool part is the graph view within Obsidian is the only one that actually feels like a brain. At the end of the day, it comes down to personal preference. There's literally hundreds of other tools you can use. These are the ones I've used and where I'm at today. So, if you're not sure, just start with Obsidian, download it, and just have the AI create a second brain. It takes 5 minutes.

Now you have a brain that's installed, but if AI reads it, there's nothing in it. So, how do you make sure that actually has the information in it sounds like you? Give your brain an identity. Without an identity, the AI is just going to sound like some robot. But to have the agent act like you, you have to tell it how to act. That's the identity. These three files will literally turn your AI from a tool to a digital clone that sounds exactly like you. Number one, user.md. Who are you? What is your role? How do you communicate? What are the frameworks you live by? How you present problems to you? Two is the soul.md file. This is for the AI. It's kind of wild, but you can define the voice, the tone, the values that essentially the AI will adopt so that it can interact and operate like you. So, the user.md file is how you are, the soul is how it acts, and then the third is the identity.md file. That is who the AI is and what they do. For example, I named my Kai. I actually didn't even name him. I used him for 2 weeks and I had him name himself.

So, for example, in my user.md file, I included who I am. You know, I'm a founder, I'm a CEO, I'm an author, I'm an investor. My communication style, things like being direct, fast, concise, frameworks over fluff, and things I care about, like freedom, execution, systems, leverage, some of my operating principles, theory of constraints, minimum effective dose, the 1-3-1 rules, a lot of different frameworks that I've taught you, I put those in there so it can operate from those principles by default. Then my soul.md includes instructions for my AI. So, for example, talk like Dick. I'm direct, high conviction, founder to founder, challenge me with love. No hedgy words. I don't like try, I don't like hope, I don't like maybe. Get rid of those. And then be resourceful. Try to solve the problem before you ask me. These are things that are in the soul file. And then my identity file. Kai is part coach, part chief of staff, part accountability partner. These are things that we define so that he can operate from that place.

Now, here's a pro tip. Don't write these yourself. You can get any AI to draft them for you. It's kind of the coolest thing in the world. You can ask it, "Hey, I need to create this new AI, so can you interview me about how I work, what I value, how I like to communicate, and what I need from an AI assistant?" Then have it draft the agent files, and it'll know user, soul, and identity files. And once you have those, now we can just save them and then point our AI to it so we can reference back to it every single time.

Now, look, this is great for you, but what about the rest of your team? That's why I built a whole AI company operating system playbook around how to integrate AI into every department of your business. It's got all the tools, the workflows, the templates, everything your team needs to use AI to get 10x the results.

So, the brain knows who you are now. Cool. Now, you probably want to start feeding it information. Not yet. Before you do that, you have to make sure it's organized first. Wire the brain. AI needs a way to clearly identify the context of the brain. No structure means AI just drowns in noise and eventually hallucinates. I went from 60% accuracy in asking it questions to 85% just by setting up the right folders. So, create these seven folders inside your vault to get your brain organized. The first one is people. You should have a place where every person in your life has a people file and has all the context on those people. Two is projects. What's one place where all of your projects, timestamped, are listed and located with all the context that it needs. Third is decisions. What are the decisions you've made in the past? How did you decide? What the alternatives are? Four is companies. This is any information on the company I'm dealing with, the research, the competitors, etc. Essentially, it's like another index of companies that I might be interacting with. Number five is meetings, cuz that's where a lot of the decisions are made, that's a lot of preferences are made, that's where team and information about people is made. So, we need a meetings folder. Six is daily. I use this as a daily dump to analyze and lock in every day daily decisions that are three to five lines that explain what happened throughout that day. Then seven is knowledge. This is where I'm extracting insights, frameworks, quotes, anything that kind of makes me me that I could reuse in the future, I want to save it in this knowledge folder.

Now, here's a pro tip. I have an eighth folder. It's called an MOC folder, a maps of content. It's a folder that includes files that is summaries of bodies of work. So, for example, I could have a youtube.md MOC linking all my scripting frameworks, all my hook libraries, all my thumbnail task, all living in different folders, but the MOC pulls it together. It's kind of like consolidating information into one simple reference file. Now, you don't have to build an MOC from day one, that's why it's a pro tip, but you build them when a topic seems to get messy. Think of it like this, your brain has different parts of your brain that's responsible for different things, motor functions, smells, vision. That's kind of what we're doing for a AI brain that's going to have to do things on our behalf. That's why we've created these folder structures. Now, you can create a bunch more over time, but this is where we start.

Now, the brain is organized and it's ready to be fed information, but how do you actually feed it? Then the next step, you have to feed the brain. So, what you do is you connect all your system, then you have your AI extract all that information into the folder structure that your brain is structured in, because the brain only needs the information it needs to use to make decisions. There is a hundred thousand data points that are being sent to me right now from the light to the temperature to everything. And my brain is filtering out all the noise, and it's only capturing the stuff I need to know. This system works the exact same way because it doesn't need the raw stuff, it's pointed back to it, but it does need to synthesize and extract the people, the decision, the knowledge that happened inside those meetings. You just have your AI do it. You have your raw files where you point it to with your connectors, and then you just have your AI extract every day all of the information based on the folder structure within Obsidian. You just improve your brain at the speed of links. That's where we're at right now.

Now, I use Grainola to auto transcribe all my meetings and then extract decisions, commitments, and actions. And the cool part is in Grainola settings, you can set a custom template for this exact prompt to do the extraction. Just write this down. Extract from this meeting: one, decisions, what did I decide today, by whom, and why? Two, commitments, who promised what, by when? Three, preferences, how people work and communicate. And four, key insights, frameworks, strategic shifts, non-obvious observations. Output as a markdown, skip small talk. Now, Grainola drops those outputs into the meetings folders as, again, the date, meeting name.md.

Now, this is where things get cool. The brain is installed. It knows who you are. It's organized and it's starting to feed itself. But the real brain doesn't just hold things, it rewires itself overnight. But how do you get the brain to get smarter overnight? Compound the brain. Now, I'm going to process the brain the way my real brain works. See, when we go to sleep every night, it takes everything that you were exposed to, and it organizes, synthesizes, it consolidates, it summarizes, it looks at things that it needs to connect, and then it even prunes things that it needs to forget. And an AI brain works the exact same way. And this is what separates everything else we talked about in the past, storage, into an actual brain.

Here's two ways to refine your brain. The first way is manual. At the end of the day, if you want, you can type in your AI a prompt that's going to tell it to go into your brain and run this process. Essentially, you just say, "Read everything that you've added to my vault today, and I need you to find orphan notes, mentions of people, projects, companies that don't have their own files. You got to create those files, you have to consolidate duplicates, you have to update the relevant map of contents with new links. You have to flag anything strategic for me to review for tomorrow." It'll take 60 seconds, but you'll wake up tomorrow to a cleaner, more connected brain. The second, and this is what I do, is automate it. I actually use Claude's scheduled task to run a cron job that runs the same prompt I just gave you every night at 11:00. And then, once you set this up, your brain will constantly improve itself. Every morning, I wake up and I click the graph view within my Obsidian brain, and I see it morph and evolve every night. It's pruning, it's cleaning up, it's essentially getting smart because the more links that it creates, the higher the signal is for context. So, when I get my AI to talk to my brain, it comes back with better answers.

So, let's do a quick recap. Number one, we went pro. We decided to pay for real power in AI. Then, we installed the brain. We figured out where we're going to save it, and then for most of you, you probably use Obsidian. Then, we gave it an identity. We created the files it needed to know how to react and respond as an AI. Then, we wired it to a brain, so it knew the folder structure of how we're going to save information. Then, we fed the brain. And now, it gets smarter overnight. You can't have an autonomous agent unless it has context. Using the brain is how we build that. If it knows the meetings you were in, the decisions you made, the people in your life, you can say things like, "Send the invite to John," and it knows who John is because John has the most links in the brain for the word John, and it knows John's email, and it knows his cell number. It's crazy how all this information is available, but it's never reused in our AI prompts. If you build the AI-powered brain, you will start to buy back days of your life because the AIs can actually run your life.

</details>
