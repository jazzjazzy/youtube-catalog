---
title: "The Digital Gadgets Experts Use To Vanish Online"
video_id: 3VJ5Htyhm7k
channel: "[[channels/Proton]]"
uploaded: 2026-09-15
processed: 2026-09-18
duration: "10:48"
url: https://www.youtube.com/watch?v=3VJ5Htyhm7k
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [online-privacy, ad-blocking]
tools: [Tails, Flipper Zero, GL iNet, Arduino, Kiwix, Rockbox, Pi-hole, Unbound, Raspberry Pi, Framework Laptop, Linux]
llms: []
protocols: [DNS]
transcript: true
tags: [youtube, ai-automation]
---

# The Digital Gadgets Experts Use To Vanish Online

![thumbnail](https://i.ytimg.com/vi_webp/3VJ5Htyhm7k/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=3VJ5Htyhm7k) | 📅 Uploaded [[uploaded/2026-09-15]] | 🗓️ Processed [[created/2026-09-18]]

## TL;DR
> Josh, a privacy expert at Proton, walks through the eight gadgets he personally uses to stay off Big Tech's radar: a Tails USB bracelet, a Flipper Zero, a GL.iNet travel router, a self-programmed Arduino smartwatch, Kiwix with offline Wikipedia, a Rockbox-modded iPod Classic, a Pi-hole plus Unbound DNS stack on a Raspberry Pi, and a modular Framework laptop running Linux. Each item is demonstrated live and mapped to the specific threat it counters — tracking, surveillance, or data collection. The through-line: the default setting is just the path of least resistance, and control is what makes a setup private.

**Watch this if:** you want concrete, demonstrated hardware and software picks for reducing tracking at home and while traveling — especially self-hosted options like Pi-hole on a Raspberry Pi.

## Key Takeaways
- Tails is an amnesic operating system bootable from a USB bracelet: no persistent storage, everything is forgotten at power-down, and it ships with a browser for the onion network.
- The Flipper Zero is a "Swiss Army knife for wireless technology" — demoed live cloning the room's AC remote signal and replaying it.
- A GL.iNet travel router puts one masked device between you and hotel or Airbnb networks, hides how many gadgets you connect, and auto-starts a VPN over everything.
- A self-programmed Arduino e-ink smartwatch keeps all data on-device instead of phoning home to an app or server — steps, dates, and custom widgets included.
- Kiwix lets you download entire reference collections, including Wikipedia, and search them fully offline — demonstrated with the network deliberately unreachable.
- A modded iPod Classic (USB-C, microSD, Rockbox firmware) plus wired headphones replaces streaming services that harvest listening data and avoids constant Bluetooth pinging.
- Pi-hole on an old Raspberry Pi 3B acts as a network-level ad blocker by resolving DNS queries and binning anything on community block lists; Unbound goes further by doing recursive DNS resolution locally so no third-party resolver sees your lookups.
- A Framework modular laptop with hot-swappable ports running Linux gives inspectable open-source control — not private by default, but configurable into privacy.

## 🛠 Tools & Software
- [[topics/Tails]] — amnesic live operating system booted from Josh's USB bracelet; forgets everything on shutdown and includes an onion-network browser.
- [[topics/Flipper Zero]] — pocket wireless multi-tool demonstrated learning, cloning, and emulating the room's AC remote signal.
- [[topics/GL iNet]] — travel router connected to hotel Wi-Fi so all personal devices sit behind one masked connection with an auto-starting VPN.
- [[topics/Arduino]] — the small computer powering his self-programmed e-ink smartwatch that stores everything locally.
- [[topics/Kiwix]] — open-source offline reader demoed searching a downloaded copy of Wikipedia with the internet turned off.
- [[topics/Rockbox]] — replacement firmware running on the modded iPod Classic, adding customization (and Doom).
- [[topics/Pi-hole]] — network-level DNS ad blocker; dashboard and query log demoed showing blocked ad domains.
- [[topics/Unbound]] — recursive DNS resolver paired with Pi-hole so lookups are performed and cached locally instead of via another company's server.
- [[topics/Raspberry Pi]] — an old Raspberry Pi 3B hosts the whole Pi-hole + Unbound stack.
- [[topics/Framework Laptop]] — modular laptop with hot-swappable port modules, assembled by the owner, demoed live.
- [[topics/Linux]] — Josh's operating system of choice on the Framework: open-source code you can inspect and control.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/DNS]] — explained as the internet's phonebook; the Pi-hole intercepts DNS lookups to block ad domains and Unbound performs recursive resolution locally.

## ✅ Action Items
- Flash Tails onto a spare USB stick (or bracelet) and try booting a laptop into an amnesic session.
- Pick up a travel router and configure it to auto-connect a VPN before your next hotel stay, so only one masked device ever touches the venue network.
- Install Kiwix and download the Wikipedia archive for offline reference.
- Set up Pi-hole on any spare Raspberry Pi, load community block lists from GitHub, then add Unbound for local recursive DNS resolution.
- Audit your defaults: swap Bluetooth headphones for wired when out, and consider a Linux install on hardware you control for inspectable, configurable privacy.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: what do Proton's own privacy experts actually use?
- `0:27` — Tails USB bracelet: boot an amnesic OS from your wrist, onion-network browser included
- `1:20` — Flipper Zero: understanding the invisible signals around you
- `1:46` — Live demo: cloning the AC remote and emulating it back
- `2:18` — GL.iNet travel router: one masked connection for all devices, VPN auto-start
- `3:21` — Self-programmed Arduino smartwatch: e-ink, fully local, no app or server
- `4:28` — Kiwix + offline Wikipedia: searching "edible mushrooms" with the network unreachable
- `5:24` — Modded iPod Classic: USB-C, microSD, Rockbox firmware, wired headphones over Bluetooth
- `6:39` — Doom running on the iPod
- `6:54` — Pi-hole on a Raspberry Pi 3B: DNS as the internet's phonebook, ads thrown in the bin
- `8:33` — Unbound: recursive DNS lookups done and cached locally
- `8:53` — Framework laptop + Linux: hot-swappable ports, open-source control
- `10:22` — Closing thought: the default setting is just the path of least resistance

## Transcript
<details>
<summary>Full transcript</summary>

This bracelet has an entire operating system on it. Turns out, it's not always size that matters. >> Proton employees spend all day making privacy tools. But what do they actually use to stay off of Big Tech's radar? Today, we've asked Josh. >> Hi, my name is Josh. I'm a privacy expert at Proton, and here is a selection of gadgets that I use to enhance my privacy. >> Tails USB bracelet. >> It's yours for just $69.99. Psych, it's an operating system. Look at that. There is an operating system called Tails. It is one of the most recommended tools for activists, people who need that deep level of privacy. What this bracelet allows me to do is take it off my wrist, plug it into a computer, boot the operating system from this bracelet instead of whatever is loaded into it. So yeah, it's a very, very easy thing to travel around with. Comes preloaded with a browser, which allows you to access the onion network. The A in Tails is amnesic, and it is an operating system which is built to just forget. Every single time you power it down, there is no persistent storage. It is gone. >> Are you a spy? >> I might be a spy.

>> Flipper Zero. >> This little device is called a Flipper Zero. It's a small tool that allows us to understand some of the signals that exist around us. We have many, many different ways in which data is transferred, whether it's switching on air conditioning or getting into your building. And what the Flipper does is allow you to clone these signals and then emulate them. This is the AC remote for the room that we're in currently. So, what I'm going to do now is make it so that the Flipper is in a learning mode. So, I point the remote at it, and it registers. And now I've cloned that signal. So, if I take it and emulate it, I can turn the AC on or off. And there you go. For me, it's really a tool for understanding and experimenting with all these invisible signals that we're surrounded by on any given day. It's kind of like a Swiss Army knife for wireless technology.

Travel router. Travel creates a considerable stream of data. When you go to the new places, you have to access the internet through new technologies, different routers, different connections in different places. And all of this means that you're exposed. Enter this item, my travel router. This is a GL.iNet travel router, which I take with me whenever I go on holiday. One of the cash grabs that exists in hotels is that sometimes you have to pay extra money in order to connect extra devices. For me, I'm just connecting one. I connect this router to the network wherever I'm staying. And then afterwards, I connect all of the devices that I have with me, which means that there is a mask stopping the router in the hotel or the Airbnb from seeing which devices are connected to it. So, I don't have to type the password in on multiple different gadgets. On top of that, I've got a VPN that starts up automatically on this, which also masks my traffic.

Self-programmed smart watch. This here is my programmable smart watch. It's a device that leverages a small computer called an Arduino. What I wanted was a device that I could make decisions about, something where I could input code and have it do the things that I wanted, rather than having a device that is consistently sending things back to an app or a server. Everything is stored on the device itself. It's e-ink, which means it's extremely low power consumption. Think of it like a tiny Kindle for your wrist. Every single minute it updates so that you can see the number of steps you've done for the day and you can see what the time is and the date is. It's counting my steps. It's counting my steps. These are some big steps. And 10 steps, very small. So, zoom in. I've also programmed it so that I have my friends' birthdays and significant dates come up at the bottom. And finally, I've got a combination of things that I am very much into such as a Momento Mori candle and uh every second counts right at the top from the TV program The Bear because every second does count and that show absolutely rocks.

>> Kiwix and offline Wikipedia. >> Imagine you lose connection to the internet and you're in a place where you're in desperate need of some kind of information. Here's where another one of my tools comes into play. This is Kiwix. It's an open-source tool that lets you download huge collections of information and access them completely offline, including Wikipedia. Let's turn off the internet or just make sure for a second that my internet is turned off. There we can see network unreachable. Let's start up Kiwix Wikipedia and let's get a search term that might be useful. >> Edible mushrooms. >> Edible mushrooms. That sounds like a a good thing to be searching for. We input it. Edible mushroom, there we go. And we can see we've got the entirety of this page downloaded locally to my computer. It's basically a little piece of the internet but without the internet.

>> Modded iPod Classic. >> The year is 2026 and I use a modded iPod Classic to play music. Music streaming services like Spotify and YouTube Music collect large quantities of data on you. So, instead of paying for a subscription service, what I do is I load it up onto this, which was built for me by someone who was on this channel quite recently, Harley. It's had a bunch of different things done to it. For example, you can see there's a USB-C port, and the storage is done by microSD cards rather than the previous setup. That disk is long dead. But on top of this, I use wired headphones. When you walk around with your Bluetooth headphones on, you are constantly pinging any device around you which is looking for a connection with Bluetooth. Instead, what I do is I switch my Wi-Fi and my Bluetooth off when I'm walking around with my phone, and I instead use this to listen to music. This device doesn't run the standard firmware that you get from Apple. Instead, we're using a distribution called Rockbox, which allows me a lot more customizability over the look of the thing, and also, crucially, because we are talking about technology here, it can run Doom. I'm going to play this really badly cuz I can't really see what's happening, but you can see I, you know, I'm probably about to die. There you go. Game over already. That's Doom on a on an iPod.

>> Pi-hole and Raspberry Pi. >> What I have right here is a very small computer. It's a Raspberry Pi 3B. It's quite old. And what it is doing is running a piece of software called Pi-hole alongside another piece of software called Unbound, which I'll come to in a minute. So, Pi-hole is a network-level ad blocker, which means you hand over the ability to resolve DNS queries to this little device. DNS is a phonebook for the internet. What computers see are sets of numbers, IP addresses, >> and what humans see are word.com, google.com, proton.me, whatever it is. The translation between these two things is called a DNS lookup. And what this does is performs those lookups for me whilst also taking anything that looks like it's coming from an ad domain and throwing it in the bin. So, this shows the total number of queries that you've made, the number of queries which have been blocked. So, these are the queries which exist on the block lists that I've got preloaded into this device.

The lists, the things which need to be blocked or not blocked are freely available on sites like GitHub. People compile these lists in order to help you have a better of ad blocking experience. Let's have a demo of the query log, which is where I can see all of the queries which are being made on my network or have been made previously. All of these existed on the block list that I've got loaded up and they were stopped before they even got to my computer. The Pi-hole sat in the middle and like a good internet bouncer said, "You're not coming in." I've taken this one step further with something called Unbound. Normally, when you type a website into your browser, your device asks another company's server where it can find it. My Raspberry Pi can do more of that work itself and remembers the answers locally. So, that over time I'm essentially building my own small local map of the internet.

>> Framework laptop and Linux. >> Now, we come on to the main act of my setup, which is my laptop um which comes from a company called Framework. This company makes modular laptops, which means that I had to assemble this myself. So, these are all what we'd call hot swappable, which means that if I'm sat in a situation where the power here, which is currently on the right, would be better off on the left, I just pop that like that. Pick a port on the other side, which is not going to be useful, let's say the USB, and I flip them out. And there we go. We've got a laptop which has a different configuration in kind of seconds. This choice of laptop also means I can choose the operating system that I run on it, which for me is Linux. This means that there is a much greater degree of control when it comes to the way in which my computer functions.

The majority of the code that goes into this operating system is open source, which means that any individual who has the technical ability and the the want can look and inspect the code and make sure that whatever is running on the device is doing something which is not hostile to the user and what the developers of the distribution say it is doing. This doesn't mean that by default the computer is more private or secure, but it does give me more control, which means that I am able to make it both of those things. Many of the tools that I've talked to you about today are about control. Just remember, the default setting is not the only one, it's just the path of least resistance. If I slam it down there, don't move. So, Visa credit and it's given me the details of your card and the number of PIN attempts that you have left. If I enter this information on a website, I WOULD BE >> NO! >> THREE DIGITS AWAY FROM BUYING SOMETHING.

</details>
