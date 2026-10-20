---
title: "Best Docker Apps of November 2025"
video_id: JqzcGQuA1mE
channel: "[[channels/ServersatHome]]"
uploaded: 2025-12-05
processed: 2026-07-06
duration: "12:27"
url: https://www.youtube.com/watch?v=JqzcGQuA1mE
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [self-hosted-app-discovery, homelab-docker-management]
tools: [Docker, WYGIWYH, Jellyswarrm, Jellyfin, Netvisor, Posterizarr, Bichon, Secret Santa, Zerobyte, PruneMate, rclone, TrueNAS, Backvault, Bitwarden, Vaultwarden, Listing-Lab]
llms: []
protocols: [REST, IMAP, OAuth]
transcript: true
tags: [youtube, ai-automation]
---

# Best Docker Apps of November 2025

![thumbnail](https://i.ytimg.com/vi_webp/JqzcGQuA1mE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=JqzcGQuA1mE) | 📅 Uploaded [[uploaded/2025-12-05]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A rundown of 10 self-hosted Docker apps pulled from the Selfh.st newsletter's November picks, demoed live in each app's UI — spanning finance tracking, Jellyfin server federation, network topology mapping, media poster generation, email archiving, Secret Santa organizing, backups, Docker cleanup, credential-vault backup, and a private real-estate listing tracker.

**Watch this if:** you run a homelab and want quick, demoed picks of new self-hosted Docker containers worth adding to your stack this month.

## Key Takeaways
- WYGIWYH ("what you get is what you have") is a no-budget finance tracker with multicurrency support, dollar-cost-averaging tracking, and net-worth/spending-insight dashboards, aimed at people who want their finances off the cloud.
- Jellyswarrm federates multiple Jellyfin servers on a network into one shared interface so users can see and access each other's media libraries.
- Netvisor auto-discovers and visually maps network topology (compared to Nmap, but with a generated diagram instead of console output), with scheduled scan sessions.
- Posterizarr auto-generates and customizes posters, backgrounds, season art, and title cards for a media library on a schedule.
- Bichon archives IMAP (or no-sync) email accounts to local disk so you never lose email, with OAuth2/access-token support for more secure connections.
- Zerobyte is an automated backup tool supporting many repository backends (local, S3, Cloudflare, Google, Azure, REST, SMTP, or rclone/TrueNAS), with scheduled backup jobs and notifications.
- PruneMate automatically cleans up unused Docker containers, images, volumes, and networks on a schedule (demoed reclaiming 3.9 GB across 188 images in one run).
- Backvault automates hourly backups of a Bitwarden/Vaultwarden credential database, which those tools don't back up automatically on their own.
- Listing-Lab scrapes real-estate listing sites (e.g. Redfin) into a private, ad-free personal Zillow/Redfin-style tracker with built-in team discussion threads per listing.

## 🛠 Tools & Software
- [[topics/Docker]] — the containerization platform underlying every app featured in this best-of roundup.
- [[topics/WYGIWYH]] — a no-budget, multicurrency personal finance tracker with dollar-cost-averaging and net-worth tracking, demoed with sample transaction data.
- [[topics/Jellyswarrm]] — combines multiple Jellyfin servers on a network into a single shared media interface.
- [[topics/Jellyfin]] — the media server whose libraries Jellyswarrm federates across multiple instances.
- [[topics/Netvisor]] — automatically discovers and visually diagrams network topology, with scheduled discovery sessions.
- [[topics/Posterizarr]] — generates and customizes media library posters, backgrounds, and title cards on a schedule.
- [[topics/Bichon]] — archives IMAP email accounts to local disk for permanent local backup.
- [[topics/Secret Santa]] — generates a Secret Santa gift exchange with shareable per-person links and budget/party details.
- [[topics/Zerobyte]] — automated backup tool supporting multiple repository backends (local, S3, Cloudflare, Google, Azure, REST, SMTP, rclone) with scheduled jobs.
- [[topics/rclone]] — used as one of Zerobyte's backup repository backends, set up via TrueNAS.
- [[topics/TrueNAS]] — the NAS OS used to configure and run rclone for Zerobyte's backup target.
- [[topics/PruneMate]] — schedules automatic cleanup of unused Docker containers, images, networks, and volumes; demoed reclaiming several GB of space.
- [[topics/Backvault]] — automates scheduled backups of a Bitwarden/Vaultwarden credential database.
- [[topics/Bitwarden]] — one of the two password managers whose database Backvault is built to back up.
- [[topics/Vaultwarden]] — the other password manager (a Bitwarden-compatible server) Backvault backs up.
- [[topics/Listing-Lab]] — scrapes real-estate listing pages into a private, self-hosted property tracker with built-in team discussion.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/REST]] — listed as one of the backend repository options Zerobyte can back up to.
- [[topics/IMAP]] — the email protocol Bichon uses to pull down and archive mail accounts.
- [[topics/OAuth]] — mentioned as a supported authentication option (OAuth2 and access tokens) for securing Bichon's email account connections.

## ✅ Action Items
- Try WYGIWYH if you want an off-cloud, no-budget personal finance tracker with net-worth and spending-insight views.
- Set up Jellyswarrm if you and others on the same network each run separate Jellyfin servers and want a combined library.
- Add PruneMate to a homelab that frequently spins up and removes Docker containers, to reclaim wasted disk space on a schedule.
- Deploy Backvault alongside Bitwarden/Vaultwarden so credential database backups happen automatically instead of manually.

## 🔗 Related Videos
- [[videos/I Didn't Know This Was Possible Until Now]] — shared: Docker, REST
- [[videos/I Tried the Open Source ElevenLabs Alternative (Voicebox)]] — shared: Docker, REST
- [[videos/Stop Vibe Coding — Use Claude Code SAFELY in Proxmox [2026]]] — shared: Docker, TrueNAS
- [[videos/Suna The FREE Open Source Alternative to Manus AI]] — shared: Docker, REST

## Timeline
- `0:00` — Intro: 10 best self-hosted Docker apps from the Selfh.st November newsletter.
- `0:26` — #10 WYGIWYH: no-budget multicurrency finance tracker with net-worth dashboards.
- `2:15` — #9 Jellyswarrm: combines multiple Jellyfin servers into one shared interface.
- `3:12` — #8 Netvisor: auto-discovers and visually maps network topology.
- `4:22` — #7 Posterizarr: generates and customizes media library poster art on a schedule.
- `5:18` — #6 Bichon: IMAP email archiving to local disk with OAuth2 support.
- `6:22` — #5 Secret Santa: automated gift-exchange organizer with shareable links.
- `7:11` — #4 Zerobyte: automated backup tool with many repository backends including rclone/TrueNAS.
- `8:32` — #3 PruneMate: scheduled Docker cleanup, reclaiming 3.9 GB across 188 images in one demo run.
- `9:49` — #2 Backvault: automated hourly backups of a Bitwarden/Vaultwarden credential database.
- `10:40` — #1 Listing-Lab: scrapes real-estate listings into a private, self-hosted tracker with team discussion.

## Transcript
<details>
<summary>Full transcript</summary>

November is over and we have a fresh round of best of containers from last month. There are some big standouts in this group like the ability to pull media libraries, automatic docker cleanup, and a fun way to do secret Santa this holiday season. All these suggestions come from the self-host newsletters produced by Ethan Shalley. We review his newsletter every Friday on our liveream. This video will cover in no specific order 10 of the best apps we saw in the newsletters for the month of November. I'm your host, Evan, and this is number 10.

Number 10 on the list for what you get is what you have. This is a powerful finance tracker designed for people who prefer a no-budget straightforward approach to managing their money. This is multicurrency support, customizable transactions. Has a built-in dollar cost averaging tracker. Looking at the UI, we can see here it's got the dark mode theme by default. Really nicely split up into a main center pane here and this right side which gives me some overviews and some summaries on what's in all the test data. We can see a summary here with income, expenses, and total. We can see currencies if I want and the accounts that are listed. And for the purposes of this demo, it's just going to be Bank of America checking and credit cards. When I scroll back to the top and go all the way to the left, I can see a monthly spending summary, a yearly spending summary, a calendar, and some spending insights. So, for this month, I can look at the account flow, and I can see here it's got this really nice chart where if I had something besides cash and savings, you could see the breakout here. For example, if I look at the category explorer, right now there's only a credit card and a dollar, but we can see the currency flow here shows that there is some unatategorized expenses, but you can see how this chart will eventually break down with more data. We change the date range to November, we can see the spending tree change directly in front of us. By looking at our net worth calculator, we can see the current projected amount of net worth and projected net worth. And you can see the breakout in the dollar amounts here on the left side. We can look at all transactions if we want. We can see a nice list here from today, yesterday, two weeks going all the way back. We could also see currency and accounts if we want to. On the right side, there's a lot of other options here. And this is a really nice and interesting way to manage money. I haven't seen a tracker like this in quite some time. All the other ones look kind of the same. This looks very different, and it definitely feels very different being in the dashboards and jumping around the menus. If you want to keep all of your finances off of the cloud and all personalized on your server without any data leakage, this is an excellent option. Up next is number nine.

Number nine on the list is Jelly Swarm. Jelly Swarm is a really interesting idea. Let's say you have a bunch of different Jellyfin servers all on the same network. This will allow you to combine all of those servers into one interface. This way, if someone has content on their jellyfin and I have content on my jellyfin, I'll be able to see their content on my server and then they'll be able to see my content on their server. It's very simple to use. You can see here the UI is straightforward. You just add a server, tell it where it is, give it a priority, and click the add button. You have the option here to set users. So, you can say what users can be allowed to go where, and in the settings cog here, you have a public address and your Jelly Swarm proxy. I'm kind of amazed at an idea this simple. Hasn't been done yet, but this one is done very, very well. I haven't seen something as simple as this done before. And this, of course, gives you the ability to massively improve the size of your library in the event that you can get on the same network as other people with their Jellyfin accounts. Up next is number eight.

Number eight on the list is NetViser. NetViser automatically discovers and visually documents network infrastructure. This kind of reminds me of Nap in that it scans your network, but instead of just giving you a console print out with all the things in it, it's going to actually generate a picture for you with topology. You can edit this if you want and actually manually build things or you can have it scan automatically and discover all of your network endpoints. There are sessions here for active discovery sessions. We can schedule ones every so often to make sure new network devices are not missed. There's a history of sessions here. We can see some of the tabs here show us the current networks we have, subnets and groups, any hosts that we have already added here, services, damons, API keys, and users if you want to allow other people access to this interface. I think this could be a really powerful tool for your assistant admin or if you just have a ton of stuff on your network and you don't know what everything is or where everything is or maybe your network changes very frequently and you want to make sure you have an up-to-date topological map of what it is that you're hosting. This can be a very powerful tool to do that and the fact you can schedule scans lets you make sure that you're always up to date every single time you come in here. Up next is number seven.

Number seven on the list is Posterizer. If you have a media server and you're really into the art and the covers of your media, Posterizer allows you to generate and customize covers for all the media that you have. We can schedule this to run anytime we want and it'll automatically rescan our media library and add posters for newly added media. When we go to asset management, we can see here the posters, background, season, title cards, everything that it generates will be listed in asset management. There auto triggers here as well. The configuration lets you mess with a lot of things. The number one thing you're going to want to adjust is the library here. It'll show you whether or not you want to have a language preference, how you want the visuals to look, how you want the overlays to look on the posters, and how you want the collections cards to look. You also have the option of sending a notification here every single time this app runs. This can be a really great tool if you're one of these people who likes to have a lot of customization over the artwork in your media library. This allows you to create something custom without having to depend on one or the other. Up next is number six.

Number six on the list is Bisham. I hope I'm pronouncing that correctly. Vishan is a email archive web manager. This allows you to in your accounts page go ahead and add an account that it has IMAP. Pull it down and it will automatically bring in all of the emails into your mailbox. Once that happens, it archives them on your local disc. This way you never ever lose email. In the event you're someone who needs to make sure your emails are never ever lost, you could always save local copies with an app like this. It's super simple to set up once the account is added. And you don't even need to have IMAP. You can also have a no sync account in the event you want to add one of those. Once that happens, you have the ability to search your mail and you can add all kinds of things like ooth 2 and access tokens in the event you want to make it a little bit more secure. The settings menu is very simple if you want to have a proxy here. Unfortunately, I can't show you a ton of the dashboard because that would require me to actually sync this with a real email client and I can't show you guys that for this demonstration. But in the GitHub page, when we scroll down to the screenshots area, we can see the 30-day trend on this beautiful graph they have here of how many emails you were bringing in and archiving on your local system. Up next is number five.

Number five on the list is Secret Santa. This is an automatic program that creates a secret Santa party where you can go ahead and input all this information and it'll create a secret Santa party for you. Now that I've inputed some sample data for my new party, let's go ahead and create a secret Santa party. The party's been created and now I get a bunch of links to send to these people. You'll notice that I don't know who John Smith's person is. I can just send him his link without looking at it and he'll be told who his person is for Secret Santa. Let's go ahead and copy this link and open it in a new tab. Secret Santa for this person is Will Archer. This is the party details. This is the budget. And this is the overlay of the card. So really a very simple container, but it does something really necessary in the event that you want to create a large amount of people and have them assigned to a secret Santa without knowing who's going to who. Up next is number four.

Number four is Zerobyte. Zerobyte is an automated backup solution very similar to something like Think Thing, except it might be easier for some users to use. In the UI, I get the option to set up a volume, set up a repository to back up, and then set a backup schedule. In this case, I've already made a volume which consists of a directory. In this case, it's my data/configs. I've set up a repository. This is local. But of course, the strength of this is the fact that you have the ability to do many repositories. On the back end, I can do a local, I can do S3, Cloudflare, Google, Azure, Rest, SMTP, or Arclone. Arclone is a pretty amazing backup solution that's built into truness. And I've already constructed the container to use rclone from the host operating system. You can go ahead and run the rclone command in truness to set up rclone and have it automatically sync to this container. To set up a backup job, I just can create a backup job. I select the volume that I want to back up and then I select the target. I can set a frequency, a time and then say what I want to back up and whether or not I want to include anything like exclusions and the retention policy. I can have it notify me anytime it does anything using these notification types here. And I have additional settings if I want to change my password or set up a backup recovery key. Zero bite is pretty simple to use and it works really really cleanly without having to worry so much about permissions like you would on sync thing. Up next is number three.

Number three on the list is PruneMate. Prune mate performs a very important function and that's cleaning up after your Docker containers. If you're frequently experimenting in your home lab with lots of Docker containers by installing stuff, removing stuff, maybe installing different stuff later, you may have a lot of images, volumes, or networks just lying around that aren't actually attached to anything, taking up valuable hard drive space. This container automatically schedules cleanups where you can go ahead and check off every single one of these options to remove unused containers, images, networks, and volumes on a schedule, in this case at 3:00 a.m., or run it immediately. So, I can go ahead and run this now to show you guys how this is going to work. So, we get this notification that the job was executed manually. And we can see how much I saved already. This is a 3.9 GB reclamation. One run, 188 images it saved me. So, I had a lot of stuff laying around on the system and I can set up notifications if I want. So, in this case, it defaults to notify or notify. So, in this case, I would be able to enable the notification, set my URL, set my app token, and have it tell me about everything it cleans as it runs. This container should be on everybody's list if you run a home lab where you're frequently installing and removing Docker containers. Absolutely consider adding this and running this to your daily stack. Up next is number two.

Number two on the list is back vault. Back vault performs a very important function if you're using Bit Warden or Vault Warden in that it backs up the database holding all of your credentials. This is not automatically done by Bit Warden or by Va Warden. It has to be done manually. But this container allows you to automate that solution and in the environment variables set an hourly interval at which you want to back up your database. When I click initialize, I will now get the setup complete message. This UI will now stop and the container will enter normal mode. You can close this window. That's all there is to it. After this, the container just runs in the background and whatever interval you set it, it will back up your database every so often. This makes your passwords completely safe even though they're backed up to your hard drive in the event you ever to lose possession of that hard drive. And now if you lost your Bit Warden or your Vault Warden containers, your passwords are safe no matter what. Up next is number one.

Number one on the list is Listing Lab. Listing Lab creates your own personal Redf Fin or Zillow like experience on your server. To show you how this works, I'm basically going to go over to 90210 on Redfin and just pull the first listing I see, which is 2258 Glaming Way. I'm going to copy just the address and paste it in a new real estate listing. I'm then going to click update property. And there's a scrape request that's built into the app that's going to pull all the information down from whatever listing website currently shows all this information. When I click back to my real estate, I can now see a nice little tile for it on my homepage. And it's listed as active. It shows the price of $10.8 million. And when I click it, I can see all this information in my browser completely privately without having to deal with the pop-ups or any of the other issues of common real estate listing websites or apps. By scrolling down, I can see it scraped successfully all this information about the listing, including tags, tax assessment value, and property features. The really interesting thing about this is not only do I get all this information in a really nice interface, I also get additional functionality within the app. By clicking this home menu here, I can start a discussion on what looks like its own built-in version of Slack for anybody else that's on this app. If I had possibly a team of realtors or if it's just me and my wife looking for something, we can keep all of our discussion in one place surrounding the listings. I could also update the property here by clicking this button and it'll automatically send another scrape request for this listing. In the event something changes, I could always update properties on the fly.

Thank you all for watching another summary of the self-host newsletter. If you like this video, click the thumbs up button below to give it a like. Make sure you're subscribed to this channel to get the latest videos about all things self-hosted. Leave a comment below if there are containers you wanted to see make this list or containers you're already using and absolutely love. If you want to have a longer conversation with us, jump on our Discord server. You can find an invite link in the video description below. As always, stay curious.

</details>
