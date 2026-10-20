---
title: "Google's New Universal Commerce Protocol"
video_id: yDKpF6CjBUo
channel: "[[channels/Sam Witteveen]]"
uploaded: 2026-01-12
processed: 2026-07-06
duration: "11:07"
url: https://www.youtube.com/watch?v=yDKpF6CjBUo
playlist: "[[Agents skills n8n]]"
type: news
difficulty: intermediate
use_case: [agentic-commerce]
tools: []
llms: [ChatGPT, Gemini]
protocols: [UCP, AP2, MCP, A2A, AGUI]
transcript: true
tags: [youtube, ai-automation]
---

# Google's New Universal Commerce Protocol

![thumbnail](https://i.ytimg.com/vi_webp/yDKpF6CjBUo/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=yDKpF6CjBUo) | 📅 Uploaded [[uploaded/2026-01-12]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Sundar Pichai announced Google's Universal Commerce Protocol (UCP) at NRF 2026, an open standard letting AI agents discover products, add them to carts, and check out across retailers. It builds on Google's earlier agent protocols (A2A, AP2, AGUI) and competes with OpenAI's own agentic-commerce approach, with Shopify, Etsy, Target, Walmart, and Wayfair as launch partners.

**Watch this if:** you build or advise on agent commerce integrations and want to know where UCP fits versus MCP, A2A, and AP2.

## Key Takeaways
- UCP is an open standard (not a Google-only product) for agentic commerce, letting AI agents talk to retailers, payment providers, and digital wallets.
- It's the latest in a string of Google agent protocols: MCP (tools), A2A (agent-to-agent messaging), AP2 (payments), AGUI (dynamic UIs) — UCP extends these into a retail layer.
- The core problems UCP targets: product discoverability (agents currently rely on ad-hoc browsing) and one-time integration so retailers expose their catalog once instead of per-platform.
- Co-developed with Shopify, Etsy, Target, Walmart, and Wayfair; notably Amazon is not on board.
- UCP will power new checkout features in Google AI Mode and the Gemini app, plus a "business agent" feature letting shoppers chat directly with brands in search.
- OpenAI already shipped its own agentic-commerce/instant-checkout protocol, but the presenter hasn't seen much retailer adoption of it yet.
- Full protocol spec, docs, sample schemas, and a playground are published at ucp.dev; reference implementations (e.g. for ADK) are expected.

## 🛠 Tools & Software
- None identified.

## 🤖 LLMs Mentioned
- [[topics/ChatGPT]] — referenced as the platform where OpenAI's own agentic-commerce/instant-checkout protocol runs.
- [[topics/Gemini]] — the Gemini app and Google AI Mode in search are named as where UCP-powered checkout will appear.

## 📡 Protocols & Standards
- [[topics/UCP]] — the Universal Commerce Protocol itself: the video's main subject, an open standard for agent-driven product discovery, cart, and checkout.
- [[topics/AP2]] — Google's earlier agent payment protocol; UCP reuses some of its payment ideas.
- [[topics/MCP]] — cited as the earlier "tools" protocol that started Google's run of agent standards.
- [[topics/A2A]] — cited as Google's agent-to-agent message-passing protocol that preceded UCP.
- [[topics/AGUI]] — cited as Google's protocol for building dynamic agent UIs on the fly.

## ✅ Action Items
- Read the UCP spec and sample schemas at ucp.dev to see how product/cart/checkout data is structured.
- If you run an e-commerce site, check whether your platform (Shopify, etc.) already exposes a UCP-compatible catalog.
- Compare UCP against OpenAI's agentic-commerce protocol before committing integration effort to either.

## 🔗 Related Videos
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: ChatGPT, Gemini, MCP
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, MCP
- [[videos/Claude Code Channels — Build Your Own Claude Code Experience]] — shared: ChatGPT, MCP
- [[videos/Clawdbot (OpenClaw) is everything I was hoping AI would be]] — shared: ChatGPT, Gemini
- [[videos/Google Stitch 20 Antigravity Free Design-to-Code Workflow Nobody Talks About]] — shared: Gemini, MCP
- [[videos/How Hermes Agent Can Save You 85 (Or More) in BG Task Token Cost]] — shared: Gemini, MCP
- [[videos/How I Watch ANY Video with AI in Seconds]] — shared: ChatGPT, Gemini
- [[videos/JEV Breakdown The First AI Model Built For Code]] — shared: Gemini, MCP

## Timeline
- `0:00` — Intro: after MCP, A2A, AP2, and AGUI, Google now ships UCP.
- `0:23` — Sundar Pichai announces UCP at the NRF conference, pitching retailers on enabling agents to buy things.
- `2:04` — Recap of Google's protocol lineage: MCP (tools), A2A (agent messaging), AP2 (payments), AGUI (dynamic UI).
- `2:56` — Comparison to OpenAI's own agentic-commerce/instant-checkout protocol.
- `3:52` — What UCP actually is: an open standard for agents, businesses, and payment providers to communicate.
- `4:26` — Product discovery framed as UCP's most interesting use case.
- `5:27` — Launch partners named: Shopify, Etsy, Target, Walmart, Wayfair (Amazon notably absent).
- `6:15` — UCP will power checkout in Google AI Mode and the Gemini app; "business agent" feature announced.
- `7:20` — The problem UCP solves: duplicated per-retailer integrations and poor discoverability.
- `8:55` — Developer resources: full protocol docs, schema reference, and playground at ucp.dev.
- `10:19` — Closing take: 2026 trend of companies monetizing agents, not just experimenting with them.

## Transcript
<details>
<summary>Full transcript</summary>

Okay, so firstly it was MCP, then Google introduced A2A followed by AP2 and AGUI as protocols. Well, now Google's just dropped UCP. This is the Universal Commerce Protocol. And in this video, I'm going to go through what it is, how it relates to you building agents, and later on I'll talk about some of the consequences that this may actually have for agentic commerce.

So, yesterday at the National Retail Federation Conference, Sundar Pichai himself showed up to announce the Universal Commerce Protocol. And basically it seems that he was pitching to people in retail — you're talking about everything from small brands right up to major department stores and big e-commerce platforms, etc. And while it seems he announced a number of things there, the main focus was around enabling agents to be able to buy things online. Now, this may not be as complicated as agents going off by themselves online. It might be that as you're having a chat on AI search mode in Google, perhaps even other platforms as well, an agent can run in the background, find a product for you, and then present it to you where you would actually then be able to go ahead and pay for it all on the same platform.

So, while it's early days of me looking at this, this definitely seems to be a protocol more aimed at retailers and at people who are actually selling things than people are actually creating the agents to buy things. But it certainly does seem like this is going to be a very important protocol for anyone who is doing some sort of agent agency or AI agency where they're helping small businesses to be able to sell their products and services online, to be able to provide customer support, and to be able to help them with things like AEO, or the sort of answer-engine optimization that we're seeing come along and take over from SEO.

So, what are the core goals of this new protocol? So, I'll start off by saying if we think back, we've got MCP, which is kind of like the tools protocol which allows agents to basically access tools and stuff. We've then got A2A, which came along from Google, which was a message-passing system or a way to basically have multiple agents interact with each other and do a variety of different tasks together. And then late last year we had AP2, which was a protocol built all around payments. And in many ways that's gone quiet. We've had AGUI, which is a protocol for being able to develop dynamic UIs on the fly. So, Google is certainly working overtime with coming up with all these agent protocols. And UCP seems to be an extension of some of these that's focused really on this retail layer.

Now, Google's not the first to actually do this, right? A few months back, OpenAI themselves introduced a protocol for agentic commerce. And this whole idea of the instant checkout, of helping agents to be able to discover different products and stuff like that. Now, I don't know exactly how well this went. I haven't actually seen it a lot when I've done searches in ChatGPT for things. So, I'm not sure if that's just based on the locations that I've been in at the time or just retailers have been wary about getting on board. One of the advantages that Google has is that most retailers are very comfortable with things like AdWords and doing advertising on Google and using a lot of the Google services for their businesses. So, I think it's a safe bet to say that Google is actually trying to leverage that as much as possible.

So, what actually is UCP and what does it do? So, simply put, this is an open standard, not a Google product per se, that is for agentic commerce. And its goal is to basically let AI agents, probably most of the time those are going to be sort of chat kind of agents, communicate both with businesses that are selling things, but also with some of the payment providers, digital wallets, and a lot of the ideas that were introduced in AP2, the agent payment system. So, for me, where this is going to be most interesting is around product discovery. So, currently people are using things like browsers and stuff like that to enable agents to surf the web and be able to find particular products, etc. But that always seems to be a bit of a hit and miss kind of thing. So, enabling a system where agents can actually find products better and easier is definitely going to be a win for retailers who actually decide that they want to sell to agents or at least have their products discovered by agents or presented to people.

So, the discoverability seems to be the main part, right? It allows businesses to expose what they're trying to sell or the services that they're offering without them to having to build a whole new sort of integration for every single kind of agent out there. On top of the discovery element, the protocol is also set up to be able to do things like putting something in a cart, being able to handle some kind of payment, although I'm not sure whether that part actually uses AP2 or can be done without AP2. It's still early days here. But it is certainly interesting that Google states straight up that this was co-developed with companies like Shopify, Etsy, Target, Walmart, and Wayfair. And along with them, they've also managed to get a number of other really big retail providers to join in on this. Obviously, the big one missing here would be Amazon, but I guess that's not really that surprising here.

And I think for the retailers, this is a pretty sort of straight-up proposition that Google, even in their own blog post, talks about that UCP will soon power a new checkout feature on Google products like AI mode in search and the Gemini app. And with the Gemini itself adding hundreds of millions of users over the past few months, it's a no-brainer for the retail organizations to jump on board here. The other thing that they announced, which I think could be a sort of shot at a number of startups that are out there, is this idea of a business agent. And they talk about this as being a new way for shoppers to chat brands right on search. And it's like having a virtual sales associate that can answer product questions in a brand's voice. So, this is definitely a power move on Google's part to actually become the agent of choice for retailers to actually deal with customers for sales, for customer inquiries, and maybe even later on for customer support as well.

So, on top of the UCP, they've also announced this business agents. And also a way that retailers can actually have direct offers showing in AI mode. So, all those people that were worried that, okay, Google was dead because people weren't going to use the 10-blue-link system anymore, probably don't need to worry too much about Google. It does seem that the AI mode is clearly getting enough traction, and this is perhaps one of the new ways that they can actually monetize this.

So, what is the problem that UCP is actually solving? You can think about it as right now every platform needs custom integrations with every retailer. And then retailers need to decide if they're going to build separate integrations and connections for things like Google Shopping, any of the social networks, and then that's just going to be amplified with AI agents of things like AI mode search, etc. So, the idea here is that this one protocol is going to create sort of universal compatibility. Businesses just need to expose what they're selling and how they're selling it once, and then it should work everywhere.

And I think that the big problem that this is trying to solve, and I stress trying to solve because it's such a big problem, is the idea of discoverability. We still don't know, for example, with the ChatGPT apps, if you've got a travel app, just like Booking.com has a travel app, which one does ChatGPT decide to show? And is that based on which one is better for the customer or which one is paying more to the AI agent provider? So, even with this new protocol, it's going to be interesting to see how things like that actually play out.

Another thing that this is trying to solve is everything around the sort of checkout area. So, the whole idea of you not having to fill in shipping forms for every site or even things like your payment wallet. If you're using something like Google Wallet here, it's going to make it actually quite easy and quick to be able to find, select, buy, and then pay for everything in one sort of place.

Now, for us as developers, Google published the whole protocol already. This is up on their site, ucp.dev. They've also got quite extensive documentation and even sample files of the whole sort of schema reference that this is going to be able to use. So, clearly a lot of thought has gone into this, and it does seem like it's going to be reasonably easy for people who are already selling things online via an e-commerce site, etc., to basically adopt this and to be able to start exposing their products for sale on various different sites. So, if you are interested in checking this out, come in here, you can see there's a whole breakdown of all the core different concepts of what's going on here, the different roles that agents can actually take, I guess, in relation to this. They've also got a playground up for this, and I think we're going to see some sort of reference implementations perhaps for ADK and stuff like that come along as well, which will be interesting.

Along with this, they've also published a roadmap of where this goes. And I guess really time will tell whether this is actually a protocol that people end up using a lot for building agents as well as for retailers, or if it really just becomes a protocol that retailers use to be able to sell things on the new Google search AI mode and in the Gemini app.

Overall though, this clearly highlights a trend that I think we're going to see more and more in 2026 of that people don't just want to play with agents anymore, especially big companies. They're looking for ways to actually make money with this. And for Google, it certainly does seem that being able to sell things in your actual answer engine and chat apps like Gemini, like AI mode in search, could end up being a huge win for them.

Anyway, let me know in the comments what you think, whether you think this is just yet another protocol coming out. We've certainly seen a lot of them over the past year. Or is this something you, as perhaps an AI agency who's dealing with e-commerce customers, etc., uh actually going to get behind a lot? I'd love to hear from people what they think. Anyway, as always, I will talk to you in the next video. Bye for now.

</details>
