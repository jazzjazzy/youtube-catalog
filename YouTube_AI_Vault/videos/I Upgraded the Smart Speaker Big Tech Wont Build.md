---
title: "I Upgraded the Smart Speaker Big Tech Won’t Build"
video_id: I8AgZPV27Og
channel: "[[channels/Print Your Speakers]]"
uploaded: 2026-10-11
processed: 2026-10-20
duration: "17:15"
url: https://www.youtube.com/watch?v=I8AgZPV27Og
playlist: "[[Agents skills n8n]]"
type: build-along
difficulty: intermediate
use_case: [local-voice-assistant, diy-smart-speaker]
tools: [Satellite 1, Home Assistant, Raspberry Pi, Music Assistant, VituixCAD]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# I Upgraded the Smart Speaker Big Tech Won’t Build

![thumbnail](https://i.ytimg.com/vi_webp/I8AgZPV27Og/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=I8AgZPV27Og) | 📅 Uploaded [[uploaded/2026-10-11]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> The Satellite 1 from FutureProof Homes is an open-source voice assistant and sensor board (mics, audio out, temperature, humidity, mmWave presence detection) that runs fully locally through a Raspberry Pi on Home Assistant OS — a "Hey Jarvis" smart speaker with no data leaving the house. Its 3D-printed speaker housing sounds clear but bass-light and fatiguing, so this build-along measures it properly, designs an 80 Hz port, battles a maddening air-leak saga (caused by mismatched enclosure generations and a mis-sized port), then fixes the response two ways: free DSP filters in Music Assistant, and a custom crossover + DSP designed in VituixCAD. Verdict: the speaker big tech should have built — and the v1.1 you can buy already ships ported, needing only the DSP filters.

**Watch this if:** you want a private, local, hackable alternative to Alexa/Google/Siri speakers — or a real-world lesson in why speaker ports do nothing when the box isn't airtight.

## Key Takeaways
- [[topics/Satellite 1]] is an open-source voice-assistant + sensor platform meant to be the eyes and ears of a smart home: mics, audio, temperature, humidity, and millimeter-wave presence detection, with people hiding 20 boards in ceilings for whole-home "Jarvis" coverage.
- Everything runs locally: a [[topics/Raspberry Pi]] running Home Assistant OS is the brain for lights, AC, security, home theater, and voice — "without a single bit of data ever leaving your house".
- Proper measurement first: 360° horizontal/vertical gated indoor measurements merged with outdoor ground-plane bass measurements revealed three problems — tweeter too loud, uneven tweeter response, and bass rolling off around 120 Hz (target: 70-80 Hz).
- Small boxes make port design hard: low tuning needs a long port that won't fit; the compromise was a 13 cm x 2 cm support-free, bendy printed port tuned to 80 Hz.
- The port initially did literally nothing — because a speaker port is a resonator like a bottle, and a leaky box never builds resonance; glue, clamps, and self-tapping screws couldn't save an enclosure mixing two incompatible part generations and a port printed at 1.5 cm instead of the spec'd 2 cm.
- With matched parts and the right port, the enclosure went airtight and the bass bump appeared exactly as simulated.
- Two equivalent fixes to the tweeter problems: free DSP filters anyone can click into [[topics/Music Assistant]]'s web UI, or a rebuilt crossover + DSP designed in [[topics/VituixCAD]] (fewer parts, technically better) — both targeted the same response and sound essentially identical.
- The platform's real win is being hackable, repairable, and improvable — and the Satellite 1.1 sold today already includes the port, so stock buyers just need to apply the published DSP filters.

## 🛠 Tools & Software
- [[topics/Satellite 1]] — the FutureProof Homes open-source voice assistant/sensor board and 3D-printed speaker that the whole video tears down, ports, and retunes.
- [[topics/Home Assistant]] — the local brain running the voice pipeline, lights, timers, weather, and music, with zero cloud dependency.
- [[topics/Raspberry Pi]] — the local server hardware running Home Assistant OS.
- [[topics/Music Assistant]] — where the free DSP filter fix is applied in a few clicks via the web UI.
- [[topics/VituixCAD]] — the speaker-design software used to process measurements and simulate both the DSP-only fix and the custom crossover.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- If you own or build a Satellite 1, grab the linked DSP filters and instructions from the video description and apply them in Music Assistant.
- Buy the v1.1 board/housing rather than retrofitting — it already ships with the port.
- When porting any small speaker, verify the enclosure is actually airtight (blow test, soapy water) before blaming the port design.
- Measure before modding: merge gated indoor measurements with outdoor ground-plane measurements to see real bass behavior.
- Double-check CAD handoffs — a 2 cm port spec that comes back at 1.5 cm changes the tuning enough to ruin a small box.
- Pair the speaker with a Raspberry Pi running Home Assistant OS for a fully local voice assistant with timers, weather, lights, and music.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Premise: a local, private, open-source smart speaker — with one problem: the sound
- `0:11` — The J.A.R.V.I.S. dream vs the reality of Siri/Alexa/Google: ignored commands, locked ecosystems, privacy nightmares
- `0:55` — Satellite 1 from FutureProof Homes: mics, audio, temperature/humidity sensors, mmWave presence; Raspberry Pi + Home Assistant OS as the local brain
- `1:33` — Live demo: "Hey Jarvis" plays music and switches the workbench lamp, all local
- `2:33` — The 3D-printed housing sounds clear but bass-light and fatiguing; FutureProof Homes issues the challenge
- `3:18` — Proper measurements (360° + outdoor ground plane) expose three problems: hot tweeter, uneven response, bass rolloff at ~120 Hz
- `3:55` — TS parameters and port design: 13 cm x 2 cm port tuned to 80 Hz in a stubbornly small box
- `6:25` — The port does literally nothing — air leaks everywhere; the bottle-resonator explanation
- `7:43` — The sealing saga: self-tapping screws, clamps, an absurd amount of glue, soapy-water leak hunting
- `10:08` — Root cause found: incompatible enclosure generations plus a port printed at 1.5 cm instead of 2 cm
- `11:06` — Matched parts: airtight at last, the simulated bass bump shows up; two fix paths planned (Music Assistant DSP vs custom crossover via VituixCAD)
- `12:27` — A/B listening with DSP on/off, final kitchen build, partner approval, and the verdict: hackable, repairable, and v1.1 ships ported

## Transcript
<details>
<summary>Full transcript</summary>

This is the smart speaker Big Tech won't build. It's local, it's private, and it's open source. But there's one problem, the sound. So, in this video, I'll answer the question, can I make this sound good? When the first Iron Man movie came out, it felt like looking through a window into the future. It had the flying suits, the holographic interfaces, and of course, J.A.R.V.I.S. J.A.R.V.I.S. wasn't just a voice-activated Google search. He was a collaborator. He was competent, local, and always there. That movie was released 18 years ago. And the Siri app launched 16 years ago. So, why does the future feel so disappointing? >> Disappointing! >> [screaming] >> Whether it's Siri, Alexa, or Google Assistant, we usually just bark the same five phrases at them, only to be ignored half the time. Hey Google. Hey Google. Hey Google. They also lock you into their shitty ecosystems. And that's before we even talk about the privacy nightmare of greedy tech companies listening to all your conversations.

This is where this circuit board comes in, the Satellite 1 from Futureproof Homes. This is an open-source voice assistant and sensor platform. It's designed to be the eyes and ears of your smart home. It runs through a local server like this Raspberry Pi running Home Assistant OS. Home Assistant is the brain. It can run your lights, your air conditioning, your home security, your home theater, even all the voice stuff without a single bit of data ever leaving your house. The Satellite 1 is packed. It doesn't just have mics and audio output. It has temperature sensors, humidity sensors, and even millimeter wave presence detection, so it actually knows if you're in the room. Check this out. Hey J.A.R.V.I.S. Play The Squad. >> Done. >> Hey J.A.R.V.I.S. Turn off my workbench lamp. >> Done. >> Hey Jarvis. Turn on my workbench lamp. >> Done. >> Hey Jarvis. Stop the music. >> Done.

>> Not bad, right? There are people buying like 20 of these circuit boards and hiding them in their ceilings to create a true whole home Jarvis. But Future Proof Homes have also designed this, a custom 3D printed speaker housing for the board. I love the design, but as an audio node, how does it actually sound? Honestly, it sounds pretty clear, but the bass is a little bit lacking and after you've listened to it for a while, it can be a little bit fatiguing. [music] Future Proof Homes sent this to me with a challenge, improve the sound and that's a mission I'm happy to take on. This isn't a kit I sell, but it's the kind of problem I love working on. So, let's tear this thing down and get an understanding of what we're working with. The top just unclips like this and the Future Proof Homes Satellite One board just unscrews. This exposes the speaker wires, so I have a chance now to measure the sound. The speaker measurements will tell us exactly what we need to work on to get this sounding good.

I'm going to measure this properly. I'll take 360° measurements horizontally and vertically. And because indoor gated measurements don't capture bass well, I'm going to take ground plane measurements outside and merge it. Here's the measured data. There are three problems we really need to solve. First, the tweeter is way too loud compared to the woofer. Second, >> [music] >> the tweeter response is pretty uneven. The Sat One has DSP, so these problems should be pretty solvable. But before touching the DSP, there's a third issue we can't ignore. The bass is kind of weak. Right now it's rolling off around 120 Hz and I'd really like to get that [music] close to 70 or 80 hertz. To do this, I'm going to add a port, but before we can design a port, we need the driver's TS parameters. So, let's tear down the rest of the speaker.

The sealing approach is actually super interesting. [music] You partially screw in all the screws, and then they just sort of hit hook into the other enclosure [music] half. Then once you're done that, you tighten everything down. That then [music] squeezes the gasketing tape and in theory makes an airtight seal. This design uses absolutely no glue. I'll be honest, I'm taking notes. >> Uh-huh. Uh-huh. Okay. >> Inside we've got a little off-the-shelf crossover, tweeter, and the woofer. This woofer is chunky. It has a big rubber surround, decent magnet, and then if you look inside, [music] it has heaps of coil overhang as well. I've been really surprised we couldn't get decent bass out of this. It's time to measure the TS parameters and design the port. This is a very small enclosure, which makes port design tricky. To get deeper bass, we need a low tuning frequency, [music] but small boxes naturally have high tuning frequencies. Lower tuning means a longer port, but fitting a long port inside a small speaker is problematic. We could use a passive radiator, but the brief here is to improve the [music] sound, not increase the cost, complexity, and part count.

So, we're going to try a port first. This is the port tuning I landed on. The port is 13 cm long and 2 cm in diameter, >> [music] >> with a tuning frequency of 80 hertz. In simulation, it adds a decent chunk of bass, but don't worry about the unevenness for [music] now. DSP can tidy that up later. Right now, the goal is simple. Get as much bass as possible. Because the box is so small, these port dimensions are pretty extreme. Long and narrow ports can lose efficiency in the real world, but the only way to know how much is to test it. One of the best parts of this project is that I can send these dimensions to Futureproof Homes, and they'll just send me back a modified CAD file. That's luxury. No CAD work for me. All right, they sent me back a file and I've printed it out, and this is what we got. A long, bendy, skinny port, but it prints support free. I guess the only thing left to do now is to try it.

All right. So, my ported version versus the original sealed version. Here are the results. No, you're not reading that wrong. The port did literally nothing. I don't think I've ever had a port fail this badly before. This might be a personal best. But, I think I know what's going on. >> [snorts] >> If I blow into the port, you can hear air leaking everywhere. A speaker port is like a resonator. It's like blowing across a bottle. If the bottle is sealed, it rings at a clear pitch. But, if I drill a hole in it, >> Yep, that's me. You're probably wondering how I ended up in this situation. >> [sighs] >> It doesn't. The energy leaks out instead of building up. A speaker port works the same way. If the box leaks, the resonance never forms, and the port does nothing. The speaker uses these fine threaded machine screws. They don't bite into the plastic very well. So, next I'm swapping them out to these really coarse threaded self-tapping screws, and we'll see if that changes anything.

>> [music] >> These screws use a 3 mil Allen key and it doesn't fit in the holes, so going to have to do some drilling. All right, I'm done messing about with this. It's not even close to airtight. So, I think what I'm going to do is pull it apart, new gasket tape, and then I'm just going to hold it together with clamps. This is I think at this point I'm just going to do what I do best and glue the out of it and we can sort out the screws later. >> [music] >> All right, it's a new day. Looks like I got in a bit of a frenzy last night and put an absurd amount of glue on this in frustration, but the crazy part is it's still not airtight. I think at this point what I'm going to do is go around with soapy water and just pour a bit on it and blow through it and seal it where there's bubbles. At this point, all I want to do is test the port. I don't really care if I destroy the enclosure. I just want that precious data.

I measured the speaker again and it's a bit better, but honestly, this is still a pretty disappointing result. The more I mess with this enclosure, the more it feels like something is fundamentally off. I'm starting to think something got lost in translation between me and the [music] CAD guy from Future Proof Homes. The port just seems way smaller than I think it should be. I mean, I can't even stick my pinky finger in this. >> And what hurt me is I was already all the way in. >> So, I'm going to measure everything and compare it to the spec I [music] sent to the CAD guy. Then hopefully this port starts doing what it's supposed to do. By the way, if designing a speaker seems like a lot of work >> [music] >> and you'd rather skip the research, testing, and that ends, check out the kits and plans at printyourspeakers.com. So, these are the new enclosure sections. Remember my total failure to seal the last enclosure? Well, it turns out the ported files had an updated flange design that's totally incompatible with the original front section. I was essentially trying to force a marriage between two different generations of hardware. No amount of glue was going to fix that leak. And to make matters worse, the port diameter got lost in translation. I spec'd 2 cm, but they sent me 1 and 1/2. That dropped the tuning frequency by 20 Hz, which sounds good on paper, but in a box this small, it's a disaster. With actual matching parts and the right port [music] dimensions, I've much better feeling about this one. It's time to test these enclosure sections out.

This thing is completely airtight. Okay, now we're getting somewhere. That's the nice little bump in the bass we're hoping for. With the port finally working, we've fixed the bass problem, but the speaker still has two issues. The tweeter [music] is too loud and the response is still pretty bumpy. So, I'm going to try fixing this in [music] two ways. First, the easy version. A few DSP filters you can apply in Music Assistant for free. This is something you can do yourself using the web UI in just a few clicks. Then I'm going to do a more involved version a new custom crossover and DSP set up that require a bit of soldering and a few cheap parts. This is a setup future proof homes could implement themselves in a future version of the speaker. So first up I'm going to re-measure the speaker now that I have the new port. Then I'll process those measurements and bring them into V2X CAD. [music] From there I can design and simulate the DSP only fix and then once that's done I can design and simulate the custom crossover version as well. And with both setups designed and the simulation showing a reasonably flat response [music] there's nothing left to do but to build them and test them.

>> [music] >> So I have the speaker partially assembled for the minute partly because I want to compare the old crossover to the new one and partly because I have a new enclosure printed and I want to know which one sounds best before I put it together. First up I'm going to test the old crossover with my DSP settings. Before all our mods the bass was pretty lacking and the sound was a bit fatiguing. So let's start with the DSP turned off and then I'll switch it on mid-song. >> [music] >> All right time for DSP. It already sounds so much better. >> [music] >> This port is definitely doing something there's so much more bass. >> [music] >> Let's switch back again. Oh, with the day without the DSP, the highs are so harsh. >> [music] >> Yeah, this sounds a lot more natural with DSP. I'm calling this a success. >> Great success. >> Overall, I think both solutions sound largely the same. And this isn't surprising because I targeted the same frequency response for both of them. I'm going to assemble the final speaker with Micro Server, partly because my version has fewer components, and partly because the crossover is technically better for this speaker. I've printed this new enclosure to match the kitchen. My hope is that this, combined with the voice assistant and the sound quality, will convince Speaker Girlfriend that it's a worthy long-term addition.

>> Hi there. >> How you doing? >> on, honey? >> I got something to show you. >> Oh my goodness. What's happening? Oh, it's finally done. >> [applause] >> Good job. >> we have a new friend in the kitchen. But >> It looks so cute. >> Yeah, check this out. Hey Jarvis, start a 1-minute timer. >> Done. >> Hey Jarvis, what's today's weather? >> Today should reach a high of 22° with a low of 19. It should stay dry over the next hour. Overall, around 0.2 mm of rain is forecast for today. >> What do you think? >> Sounds very good. >> It's pretty useful, too. I mean, you know, you >> Yeah, for the cooking. >> Yeah. >> Just putting timer on. >> Yeah, and you know when you get up in the morning, you're like, "Oh, what clothes do I have to wear today?" You just ask it. >> Okay. >> Yeah, is it going to rain? Is it not? [laughter] >> All right, and how is the music? >> Hey Jarvis, play Distant Sunrise. >> Playing distant sunrise. >> Oh, time is up. >> timer? >> Hey Jervis. Stop the music. >> Done. >> Well done. >> What do you think? >> It's very cute and very handy and the music was good. >> Yeah? >> So thank you for this addition. >> Do you think it can live in the kitchen for a while? >> Yes. >> Yeah, awesome. >> Approved. >> [laughter]

>> So after all of that, what do I think of the satellite one smart speaker? I think this is exactly the kind of smart speaker I wish big tech had built years ago. It's local, it's open source, it's private and it's actually designed to be part of your home instead of another lockdown gadget listening to all your conversations sending data up to the cloud. In stock form, the sound is fine. It's clear enough for voice responses and background music, but the bass is limited and the top end can get a bit fatiguing. But the important thing is this platform is fixable and that's what makes it so exciting to me. This isn't just a smart speaker, it's a hackable, repairable, improvable smart speaker and even better, the 1.1 version you can buy today already has the added port. So all you need to do is set the DSP filters and you'll pretty much have a speaker that sounds exactly the same as this one. If you've got a satellite one or you're thinking of building one, I've linked the DSP filters and instructions in the description. And if you like the idea of 3D printing your own speakers, but you'd rather build something designed from the start as a proper hi-fi speaker, check out printyourspeakers.com. That's where I sell my kits, plans and build guides. And with that, I'll see you in the next one.

</details>
