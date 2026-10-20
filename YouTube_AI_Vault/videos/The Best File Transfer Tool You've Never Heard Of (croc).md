---
title: "The Best File Transfer Tool You've Never Heard Of (croc)"
video_id: o_psX5meBo8
channel: "[[channels/Better Stack]]"
uploaded: 2026-07-19
processed: 2026-09-11
duration: "8:29"
url: https://www.youtube.com/watch?v=o_psX5meBo8
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [file-transfer]
tools: [croc, Docker]
llms: []
protocols: [PAKE, SSH]
transcript: true
tags: [youtube, ai-automation]
---

# The Best File Transfer Tool You've Never Heard Of (croc)

![thumbnail](https://i.ytimg.com/vi/o_psX5meBo8/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=o_psX5meBo8) | 📅 Uploaded [[uploaded/2026-07-19]] | 🗓️ Processed [[created/2026-09-11]]

## TL;DR
> croc is a free, open-source Go CLI that hits all three pillars of file transfer — fast, secure, simple — where most tools only manage two. It uses a full-duplex relay (both sides send and receive simultaneously, with automatic LAN detection), PAKE-based encryption from a disposable code phrase instead of a static password, and a single-binary UX: `croc send <file>` on one side, `croc <code-phrase>` on the other. The default public relay only ever sees encrypted bytes, and a built-in relay command plus Docker image lets companies self-host in minutes.

**Watch this if:** you regularly move large files between machines and are tired of expired WeTransfer links, platform-locked AirDrop, or explaining SCP to non-technical people.

## Key Takeaways
- Every popular option fails a pillar: WeTransfer is simple but slow and link-secure; SCP/[[topics/SSH]] are fast and secure but demand a server and port forwarding; upload-then-download link tools are mathematically slower (5 Mbps up + 8 Mbps down = ~3.1 Mbps effective).
- [[topics/croc]] avoids the sequential bottleneck with a relay-brokered full-duplex transfer, and switches to direct local transfer when both machines share a LAN.
- Security uses [[topics/PAKE]] (password-authenticated key exchange): the disposable code phrase isn't the key itself — both sides derive a stronger key on the fly, and a wrong phrase kills the exchange before any data moves.
- The default public relay (run by creator Zack Scholl) sees only encrypted bytes and connection metadata, but it's still third-party infrastructure — a blocker under data-residency policies.
- `croc relay` plus the included [[topics/Docker]] image makes self-hosting your own relay a ~5-minute setup; point transfers at it with the `--relay` flag.
- Transfers resume where they left off after a dropped connection, and the whole UX is one command to send and one code phrase to receive — no account, no browser tab, no server.

## 🛠 Tools & Software
- [[topics/croc]] — the subject of the video: open-source Go CLI for encrypted, resumable, relay-based file transfer, demoed live between a Windows machine and a MacBook.
- [[topics/Docker]] — croc ships a Docker image for spinning up a self-hosted relay in corporate environments.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/PAKE]] — password-authenticated key exchange; croc derives a strong end-to-end encryption key from a disposable code phrase, failing safely on a wrong phrase.
- [[topics/SSH]] — held up as the fast-and-secure-but-not-simple counterexample: great for tech-savvy setups, unreasonable for two laptops in a coffee shop.

## ✅ Action Items
- Install croc (one-line install on Windows and Mac; the GitHub page covers other setups) and try `croc send <file>` / `croc <code-phrase>` between two machines.
- Test the resume feature by killing a transfer mid-way and restarting from the sender.
- For corporate or data-residency-sensitive use, self-host a relay with `croc relay` (or the Docker image) and point transfers at it with the relay flag.

## 🔗 Related Videos
- [[videos/Best 120b Model for Offline Use Nemotron 3 Super Out Now]] — shared: Docker, SSH

## Timeline
- `0:00` — Intro: "the best file transfer tool I've ever used"
- `0:34` — Why file transfer is still a headache: AirDrop, WeTransfer, Dropbox, SCP, USB sticks
- `1:44` — Zack Scholl's three-pillar architecture: fast, secure, simple
- `2:14` — Pillar 1, fast: the sequential upload/download math penalty
- `2:46` — Pillar 2, secure: static shared passwords are the weak link
- `3:05` — Pillar 3, simple: SSH/FTP need servers and port forwarding
- `3:46` — How croc nails all three: Go CLI, full-duplex relay, LAN detection
- `4:23` — PAKE explained: code phrase to strong key, fails safe on interception
- `5:14` — Who runs the relay: public default sees only encrypted bytes
- `5:49` — Self-hosting the relay with the built-in command and Docker image
- `6:15` — Live demo: croc send from Windows to MacBook
- `7:05` — Resuming a killed transfer mid-way
- `7:31` — Final thoughts: fast, secure, simple — hard to go back

## Transcript
<details>
<summary>Full transcript</summary>

This is Croc, and it's one of the coolest tools I've recently stumbled upon. I'm just going to put it out there and say it. I think this is the best file transfer tool I've ever used. There you go. I said it. Croc is not just a file transfer tool. It is genuinely different in the way it's built and how it works. So, in this video, we'll take a look at Croc, see how it works, and I'll show you how extremely easy it is to use it. It's going to be a lot of fun, so let's dive into it.

So, here's a question worth asking. How many ways can you think of right now of sending a large file to someone else's computer? So, there's AirDrop, WeTransfer, Dropbox, Google Drive, SCP, Discord if you're desperate, a USB stick if you're really desperate, mailing a USB stick to someone if you're absolutely insane. So, there are dozens of tools for this, and yet almost everyone has a story about transferring files that should have taken 30 seconds and instead ate their whole afternoon. So, for example, your colleague tries to AirDrop something to you, but sadly you're on Windows. In another scenario, the WeTransfer link expired before the other person got around it. The file was too big for email. The other person doesn't have a Dropbox account and doesn't want to make one. And honestly, I don't judge them. So, here's the real question. With so many tools out there, why does this keep happening? And the answer is because, frankly, none of these solutions use the three-pillar strategy that makes a great file transfer solution.

So, Croc was created by Zack Scholl, and on his website, he explains in great detail what a good file transfer solution architecture should look like. And honestly, it makes so much sense. A good file transfer system needs three pillars. It needs to be fast, secure, and simple. All three at the same time without giving up on any of them. And most tools out there pick two and can't seem to hit the sweet spot of that Venn diagram. So, let's look at each pillar separately. The way most link-based tools work is you upload the file to a server, then the other person downloads it. Sounds fine, but this is actually mathematically slower than it needs to be. If you're uploading at 5 megabits per second and downloading at 8 megabits per second, sequential upload then download gives you an effective rate of about 3.1 megabits per second. And that's slower than either speed on its own. That's just what happens when you do things one after the other instead of at the same time.

Let's talk about secure. A lot of secure transfer tools rely on you setting a single shared password to encrypt the file, which is fine, except passwords are only as strong as the password you actually pick. And if the password gets guessed or leaked, well, then that's it, game over. And three, it needs to be simple. At the moment, we've got amazing tools out there like SSH or FTP, genuinely fast and genuinely very secure, but they require one computer to be running a server with port forwarding enabled, which is a completely reasonable setup for center or a tech-savvy person and a completely unreasonable ask for two laptops in a coffee shop. So, look at the pattern. WeTransfer is simple, but slow and only as secure as its link. SCP is fast and secure, but nobody's non-technical friend is going to know how to use SCP right off the bat. So, almost nothing hits all three pillars.

But, how is Croc different? Well, Croc is an open-source Go-based CLI tool built specifically to not compromise on any of these three pillars. So, first of all, fast. Instead of the upload then download model, Croc uses a relay server to set up a full duplex conversation between both computers. Both sides are sending and receiving data at the same time, so you're not bottlenecked by the sequential upload download math from earlier. And if both machines happen to be on the same local area network, Croc will actually detect that and transfer locally instead, which is faster still. Next, secure. Instead of a static shared password, Croc uses something called PAKE, password authenticated key exchange. It uses a disposable code phrase, but it's not an encryption key by itself. Both sides use this phrase in a back-and-forth cryptographic exchange to generate a much stronger key on the fly. If someone tries to intercept that exchange with the wrong phrase, the whole thing just fails, so no data moves and everyone knows something's wrong.

And finally, it's simple. Single binary, no server to configure, no port forwarding, works straight through NATs and firewalls via the relay server, and on the receiving end, you just have to type Croc followed by the code phrase when it asks, and then accept the transfer and it's done. But wait, who's actually running that relay? Well, by default, Croc routes your transfer through a public relay run by the tool's own creator, Zach himself. Now, because the file itself is encrypted end-to-end via PAKE before it even leaves your machine, that relay only ever sees encrypted bytes and connection metadata. It physically can't read your file contents, but it's still a third-party server sitting in the middle of a transfer by default, and if you're at a company with data residency rules or you have a policy against routing traffic through infrastructure you don't control, that's going to be a blocker.

But the good news is that Croc accounts for this. There's a built-in Croc relay command that spins up your own relay with a Docker image included, and then you just point your transfers at it with the relay command with the relay flag instead of the default. So the public relay is the convenient default for personal use, but for anything in a corporate environment, self-hosting the relay is a 5-minute setup and not a deal breaker. But now I want to show you how extremely easy and convenient it is to use Croc. I've personally been using Croc a lot these past days, and it's so convenient since I have two workstations here. One is a Windows machine and another one is a MacBook, and check out how easy it is to send large files from one to the other using Croc. Installing Croc is super easy. It's just a one-line command for both Windows and Mac, and the GitHub page has instructions for all sorts of setups. And once we have it installed, on the sending side, you need to type Croc send followed by the file, and it spits out a randomly generated code phrase. And on the receiving end, run Croc, type in the code phrase when prompted, type Y to accept it, and boom, magic. It's that easy, that fast.

And here's another thing. It also has the ability to resume transfers when the connection breaks. Let's kill the connection mid-transfer, then resume it from the sending side, and as you can see, it picks up where it left off instead of starting over. So that's it. That is the entire user experience. One command to send, one code phrase to receive, no account, no browser tab, no server to spin up. How cool is that? So there you have it, folks. That is Croc in a nutshell. It's fast because of a full-duplex relay transfer, it's secure because of Paik instead instead static passwords, and it's super simple to use. And once you actually try it against the alternative, like texting someone a WeTransfer link and hoping it doesn't expire, it's honestly hard to go back once you've used it. So, what do you think about Croc? Do you like it? Is it going to be in your toolkit? Let us know in the comments down below. And folks, if you like these types of technical breakdowns, please let me know by smashing that like button underneath the video, and also don't forget to subscribe to our channel. This has been Andras from BetterStack, and I will see you in the next videos.

</details>
