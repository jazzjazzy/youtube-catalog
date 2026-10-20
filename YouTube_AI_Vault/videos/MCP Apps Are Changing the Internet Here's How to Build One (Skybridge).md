---
title: "MCP Apps Are Changing the Internet. Here's How to Build One! (Skybridge)"
video_id: 9X8GRGcl5oA
channel: "[[channels/Better Stack]]"
uploaded: 2026-05-24
processed: 2026-07-05
duration: "9:20"
url: https://www.youtube.com/watch?v=9X8GRGcl5oA
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [mcp-app-development, chatbot-widget-integration]
tools: [Skybridge, React]
llms: [Claude, ChatGPT]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# MCP Apps Are Changing the Internet. Here's How to Build One! (Skybridge)

![thumbnail](https://i.ytimg.com/vi/9X8GRGcl5oA/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=9X8GRGcl5oA) | 📅 Uploaded [[uploaded/2026-05-24]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> Skybridge is an open-source TypeScript framework from Alpic that handles the protocol bridging and state sync needed to build interactive MCP apps — widgets shared live between a human and an LLM inside a chatbot. The video walks through installing the Skybridge skill, having Claude generate a full e-commerce widget (search, compare, checkout), testing it in a local emulator dashboard, and connecting it to Claude as a live connector.

**Watch this if:** you want to build an interactive widget (not just markdown/JSON output) that both a user and an LLM can operate live inside a chatbot.

## Key Takeaways
- MCP apps have two simultaneous users sharing one interface — the human clicks/types/slides, the LLM instantly sees that state, and the LLM can update data in the background with the UI reflecting it in real time.
- Skybridge is an open-source TypeScript framework that handles protocol bridging, state sync, and security rules so developers can just write standard React code for the widget.
- Skybridge 1.0's redesigned dev tools ship three tools in a local emulator dashboard: the Alpic playground (hot-reload widget testing without touching an LLM), an integrated one-click public tunnel (no more manual tunnel setup), and the Beacon audit tool (scans metadata/tools/security policies for common app-store rejection triggers).
- You can install the Skybridge skill into your AI agent (globally or per-repo) and simply ask it (in this demo, Claude) to build the MCP app — Claude asks clarifying questions about intended functionality before generating the widget.
- The demo builds a camera-lens e-commerce MCP app with search, side-by-side comparison, cart, and checkout, all testable locally in the emulator before ever touching a live chatbot.
- Connecting to Claude requires activating the built-in tunnel, copying its URL into Claude's Connectors settings as a custom connector, and choosing whether tools run automatically or need per-use approval.
- Once connected, asking Claude a natural-language question ("best lenses under $2,000 for portrait shooting") triggers the MCP app to open live inside the chat, with the same search/compare/checkout flow as the local test.

## 🛠 Tools & Software
- [[topics/Skybridge]] — open-source TypeScript framework by Alpic for building interactive MCP apps; provides the emulator dashboard, playground, tunnel, and Beacon audit tool used throughout the demo
- [[topics/React]] — the framework widgets are written in; Skybridge abstracts away the MCP plumbing so developers just write standard React components

## 🤖 LLMs Mentioned
- [[topics/Claude]] — used to generate the MCP app from a prompt, and as the chatbot the finished widget is connected to and demoed live in
- [[topics/ChatGPT]] — mentioned alongside Claude as a chatbot MCP apps can be built for and connected to

## 📡 Protocols & Standards
- [[topics/MCP]] — the core protocol/concept of the video: interactive apps built on Model Context Protocol that share state between human and AI assistant

## ✅ Action Items
- Install the Skybridge skill into your AI agent (globally or per-repo) before starting your first MCP app.
- Use the Alpic playground in the local emulator to hot-reload and test widgets before connecting to any live LLM.
- Run the Beacon audit tool before submitting an MCP app to a public app store to catch common rejection triggers early.
- Use the built-in one-click tunnel instead of manually configuring public tunnels when testing against a real chatbot connector.

## 🔗 Related Videos
- [[videos/Anthropic Just Connected Claude Code to Your Browser]] — shared: ChatGPT, Claude, MCP
- [[videos/Master Local AI in 29 minutes (LM studio AnythingLLM)]] — shared: ChatGPT, Claude, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude, MCP
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude, MCP
- [[videos/Anthropic Just Shipped 10 Wall Street AI Agents, GitHub 1]] — shared: Claude, MCP
- [[videos/Anthropic Will Pay You $15,000 A Month To Use Claude Ai]] — shared: ChatGPT, Claude

## Timeline
- `0:00` — The AI paradigm shift and what MCP apps are
- `0:47` — How interactive MCP apps work: human and LLM sharing one live interface
- `1:34` — Meet the Skybridge framework
- `1:52` — Redesigned dev tools: emulator dashboard with playground, tunnel, and Beacon audit
- `2:52` — Coding the e-commerce MCP app with Claude as the AI agent
- `4:37` — Testing the widget inside the developer dashboard (search, compare, checkout)
- `6:08` — Connecting the app to Claude via a custom connector
- `6:57` — Live demo of the MCP app running inside the Claude chatbot
- `7:57` — Auditing the app before public release
- `8:13` — The future of the modern web with MCP widget apps

## Transcript
<details>
<summary>Full transcript</summary>

There's a huge paradigm shift happening across the industry because of AI. More and more users are using chatbots nowadays for their routine searches or research, and that's why the concept of MCP apps is getting more and more popular. Instead of spitting out a JSON file or a markdown document, more apps and services are switching to providing these interactive and helpful widgets inside a chatbot. And the company Alpic recently released a cool new framework called Skybridge that makes it super easy to create your own custom MCP apps for all sorts of different use cases. So, in today's video, we'll take a look at Skybridge, see how it works, and try it out for ourselves. It's going to be a lot of fun, so let's dive into it.

To really understand why Skybridge is such a big deal, you have to understand how these new apps work. When you build a traditional web app, you are building it for one user, the human. But with an MCP app, you're actually building for two users at once, the human and the AI assistant, because they both share the exact same interface. The human can click buttons, type inputs, and slide sliders, and the LLM instantly sees that state. And conversely, the LLM can update the data in the background and the UI changes in real time right in front of you.

And Skybridge is an open-source TypeScript framework for that that handles all the complex plumbing, the protocol bridging, the state sync, and the security rules. So, you can just focus on writing standard React code. Now, if you've ever tried to build MCP apps for ChatGPT or Claude before, you know that the local testing loop used to be a massive headache. You had to manually set up public tunnels, copy-paste configurations, and restart your chat sessions just to fix a tiny CSS typo. But the coolest part of Skybridge 1.0 is that it completely redesigned the dev tools control panel. Now, when you run your local dev server, it fires up an emulator dashboard in your browser. And inside this dashboard, you have three nice tools. The first one is the Alpic playground, a local sandbox where you can test your tools and tweak your React widgets using live hot module replacement. And you can see the changes instantly without touching an actual LLM yet. And secondly, there's an integrated tunnel, which allows you with literally a single click to expose your local server through a secure public URL. So, you don't have to mess around with external tunneling anymore. Just paste this URL into ChatGPT's developer settings, and you're live. And third is the beacon audit tool. And this is a lifesaver if you plan to submit your apps to public stores. It scans your apps' metadata, tools, and security policies to catch common rejection triggers before you submit your app for review. And the coolest thing is that even if you've never built an MCP app, you can easily install the Skybridge skill onto your favorite AI agent to get started instantly.

So, now let's try to build a small MCP app on our own and see how it works. So, for this demo, I've went ahead and created this little e-commerce website where you can shop for different camera lenses. And it's basically a fully built React-based store with a cart and checkout functionality. And now, I want to add an MCP app for it. So, that if a potential customer uses a chatbot like ChatGPT or Claude to search for camera lens recommendations, it will immediately call our MCP app to show our product listings for the end user. So, as I said before, the easiest way to get started is just to install the Skybridge skill. And we can install it globally or just for our specific repo. And for this demo purpose, I'm going to go ahead and install it in the repo. And now, you can see we have this dot agents directory with the Skybridge skill present. And all I have to do now is just ask Claude to build me an MCP app for my e-commerce shop. And before building it, Claude will first ask me some follow-up questions about the intent of the app to better understand what kind of functionality we need to include in it. And for this demo, I want to have an app that lists lenses based on what the user is looking for and then we can select them and compare them side by side and also add them to our cart and provide a quick checkout solution for our customers. And that's basically all I need to do and now I just let Claude do its thing. And in about a few minutes, we see that Claude has generated our MCP app.

And the coolest part is that now we can open the developer dashboard provided by Skybridge and try it out for ourselves. So now if we open the dashboard, we can see how it looks. And here we have our search lenses tool and the place order tool. So first of all, for search lenses, I'm just going to insert the max price for the lenses I'm looking for and let's limit it to five lenses maybe. And there you go. It found 14 matches that are under $2,000. Here's how the app looks on desktop. We can also preview the mobile view. Looks good. We also have a dark mode and a light mode. And here we have the tool output and the state. And watch what happens if I select some of the lenses. As you can see, the state updates on the fly, which is super cool. So now let's choose three lenses. And now if we click compare, we now get to the compare screen and here we can see all our three lenses side by side with all the parameters. And if we're happy with the selection, we can also go to the checkout. This moves to the checkout stage where we can put in our full name, email, and shipping address, and place our order. So, as you can see, this dashboard is really cool for testing out your widgets to see if everything is working as expected.

And now, if we go to Claude and in settings, we have the section called connectors. And we have to click customize. And for this, you will need the tunnel URL, so make sure you have activated the tunnel. And we can just copy this URL, and in the connector section, you just have to add a custom connector, give a name, and paste in that tunnel URL and just click add. I've already added it here. And last thing you need to do is click connect. And you can also set the permissions if you want these tools to run automatically or you want an approval from the user. And then we can just go ahead and start a new chat. And in the new chat, I can now ask, "Give me some recommendations for the best lenses under $2,000 for portrait shooting." And we can now see that it says it will search the lens shop catalog for some great portrait options under $2,000. And look at that, it opened our MCP app. How cool is that? And we can do the same things over here. We can select some of the lenses over here, and then go to the compare section, and it has this little comparison table. The only thing I noticed is that we have this white space from the previous state of our tool. So, this is probably something you can fix in CSS.

But everything is looking great and we also have the option to check out. And we get to the checkout section where we can place our order. So how cool is this? And lastly and most importantly to see if your app is ready to be published to the public app stores, we can also run an audit of our app through the developer dashboard and check if we have any issues with it. And basically that's it. In just a few minutes we were able to build a production ready MCP app with Skybridge that we could theoretically submit to the AI app store. So I hope this shows you how easy it is to get up and running with Skybridge and honestly it feels like the future of the modern web. I think we will start seeing more and more of these interactive MCP widget apps inside our chatbots. So it's nice that there are frameworks like Skybridge out there that are making the process of creating these kinds of apps so much easier for us developers. So there you have it folks. That is Skybridge in a nutshell. So what do you think about Skybridge? Have you tried it? Will you use it? Let us know in the comment section down below. And folks, if you like these types of technical breakdowns, please let me know by smashing that like button underneath the video and also don't forget to subscribe to our channel. This has been Andres from Better Stack and I will see you in the next videos.

</details>
