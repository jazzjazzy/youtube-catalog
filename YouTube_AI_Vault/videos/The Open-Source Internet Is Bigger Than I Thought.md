---
title: "The Open-Source Internet Is Bigger Than I Thought"
video_id: X0NW94-F8BE
channel: "[[channels/Data Slayer]]"
uploaded: 2026-10-04
processed: 2026-10-20
duration: "12:01"
url: https://www.youtube.com/watch?v=X0NW94-F8BE
playlist: "[[Agents skills n8n]]"
type: review
difficulty: beginner
use_case: [off-grid-communication, mesh-networking]
tools: [Meshtastic, MeshCore, MicroReticulum]
llms: []
protocols: [Reticulum, LoRa, Bluetooth]
transcript: true
tags: [youtube, ai-automation]
---

# The Open-Source Internet Is Bigger Than I Thought

![thumbnail](https://i.ytimg.com/vi_webp/X0NW94-F8BE/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=X0NW94-F8BE) | 📅 Uploaded [[uploaded/2026-10-04]] | 🗓️ Processed [[created/2026-10-20]]

## TL;DR
> A 1,500-mile family road trip from Central Florida to New Hampshire becomes a wardriving experiment: a 915 MHz mag-mount whip antenna on the car feeds a battery-powered consumer Meshtastic node in the trunk, announcing GPS position on the public LongFast channel. The rig discovered 458 mesh nodes along the East Coast — including solar-powered infrastructure — and kept working through two grid blackouts, which leads into a comparison of Meshtastic's managed flooding against Reticulum's path-based routing and its ability to bridge LoRa, Wi-Fi, TCP, and packet radio into one network of networks.

**Watch this if:** you're curious how much real open-source mesh infrastructure already exists in the wild, or you're weighing Meshtastic against Reticulum for off-grid or emergency communications.

## Key Takeaways
- A consumer-grade, 22 dBm battery-powered node with a mag-mount whip antenna on a moving car found 458 Meshtastic nodes between Florida and New Hampshire — and that's a floor, not a ceiling, since other channels, firmwares, and out-of-range nodes were invisible to it.
- LoRa range is governed almost entirely by obstruction and the curvature of the Earth: elevation and line of sight (e.g., sending from bridges) got acknowledgements roughly half the time even at 70-80 mph on I-95.
- Mesh nodes run on MCUs (microcontrollers, not even Raspberry Pis), and that low power draw is exactly what makes fully self-contained solar nodes practical — unlike 1 W boards that need bigger batteries to actually deliver full power.
- [[topics/MicroReticulum]] now lets the full RNS stack run on the same MCU-class hardware that was historically Meshtastic-only — the presenter ran a transport node on a Heltec V4 strapped to a drone.
- With a ham license you can run [[topics/Meshtastic]] at higher transmit power, but that legally strips encryption; [[topics/Reticulum]] bakes encryption into the protocol and can't realistically remove it.
- During two separate grid outages (Meredith NH and Charleston SC), the mesh stayed alive and messages were acknowledged — the moment it stopped feeling like a hobby and started feeling like infrastructure.
- Meshtastic, [[topics/MeshCore]], and other LoRa networks run in separate lanes: mismatched frequency, bandwidth, spreading factor, coding rate, or encryption keys mean they don't automatically interoperate.
- Meshtastic floods messages until a hop limit runs out, while Reticulum discovers and reuses routes via transport nodes, scaling with route length instead of mesh size — and can bridge LoRa, Wi-Fi, TCP, and packet radio, which is its killer feature.

## 🛠 Tools & Software
- [[topics/Meshtastic]] — the firmware/app used for the whole experiment: car node announcing GPS on the public LongFast channel, phone app over Bluetooth to watch activity and send messages.
- [[topics/MeshCore]] — named as one of the other LoRa firmwares running in a separate, incompatible lane alongside Meshtastic.
- [[topics/MicroReticulum]] — the MCU port of the Reticulum network stack that runs on self-contained boards, enabling his drone-mounted transport node.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/Reticulum]] — the encrypted, path-routing network stack positioned as the mesh movement's next step: scales with route length and bridges mixed transports.
- [[topics/LoRa]] — the radio layer everything here rides on; range depends on line of sight, and parameters like spreading factor and coding rate fragment networks into lanes.
- [[topics/Bluetooth]] — how the phone running the Meshtastic app drives the trunk-mounted node.

## ✅ Action Items
- Build a car rig: 915 MHz mag-mount whip antenna on the roof/hood, coax into the trunk, battery-powered Meshtastic node (USB-C topped up from the car outlet) named and set to announce GPS.
- Stay on the public LongFast preset with a hop limit of ~3 if you want to be discovered by (and discover) the broadest set of nodes.
- Send test messages from elevated spots like bridges — line of sight dramatically extends LoRa range and acknowledgements prove two-way reach.
- Try MicroReticulum on an MCU board (e.g., Heltec V4) to run an RNS transport node as cheap, self-contained infrastructure.
- Consider a technician-class ham license, but understand the trade-off: higher Meshtastic transmit power legally requires unencrypted traffic.
- Check a node database after a trip to see how much mesh actually exists around you before assuming you'd need to build from scratch.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Road trip premise: Central Florida to New Hampshire, ~1,500 miles, with an experiment running from the trunk
- `0:22` — The rig: magnetic 915 MHz whip antenna, coax into the trunk, battery-powered consumer node capped at 22 dBm
- `1:26` — GPS position announcements plus Meshtastic over Bluetooth from the phone, everything on the public LongFast channel
- `2:00` — Node clusters appear (15 around the start); caveats about hop limit 3, beacon intervals, and highway speed
- `2:54` — Bridge experiments: messages acknowledged about half the time, first reply crossing the Arthur Ravenel Bridge in South Carolina
- `3:33` — LoRa loves elevation: range governed only by obstruction and Earth's curvature
- `3:50` — Handheld companion nodes vs self-contained infrastructure nodes; MCUs' low power draw makes solar nodes viable
- `5:14` — MicroReticulum brings the full RNS stack to MCU hardware; the Heltec V4 drone transport node story
- `6:05` — Ham license arrives; Meshtastic's high-power-means-no-encryption trade-off vs Reticulum's mandatory encryption
- `7:11` — Power outage in Meredith, NH: the mesh acknowledges messages while the grid is down; second outage later in Charleston
- `9:08` — Final tally 458 nodes — the floor, not the ceiling — and the fragmentation problem across Meshtastic, MeshCore, and other LoRa lanes
- `9:59` — Managed flooding vs Reticulum's path discovery and transport nodes; bridging LoRa, Wi-Fi, TCP, and packet radio into a network of networks

## Transcript
<details>
<summary>Full transcript</summary>

This past month, my family and I took a road trip from Central Florida all the way to New Hampshire, which is about 1,500 mi up the East Coast of the United States. And [music] since Tesla FSD does most of my driving at this point, I decided to run a little experiment from the trunk. [music] I wanted to see how much of a mesh presence we could discover along our journey. For that setup, I finagled a magnetic Mouser 915 MHz whip antenna onto the back of my car. Then I ran the coax into the trunk [music] and connected it to this battery-powered R1 Neo from MouserWorks. Now, >> [music] >> this is a consumer device, so it's not some heavy-duty base station. It caps out transmit power at 22 dBm, which isn't enormous, but it does help conserve battery [music] power. So, basically, you can buy these mag mount antenna stands, and these can go right on the hood of your car. So, this one just has an SMA connector. You can take my 915 whip antenna, plop that on here, and I'll be able to put that right on the car. And I just run the coax right into the trunk. And for the node, I'm going to use this guy. This is the Neo One, so I could take off the sort of handheld antenna, and then this guy can just go right into the trunk. I can basically just put it on like that. Yeah, so that's a mobile whip antenna. And I aptly named the node Data Slayer Parallel Car Node. And because it has GPS, it could announce our position to other nodes while I use Meshtastic over Bluetooth to watch for activity and send the occasional message from my phone.

If its battery ran low, the Tesla has an outlet in the back that I could plug into this USB-C to provide continuous power. Now, I wasn't using a private channel. Everything was on the public channel for everyone to see on the long fast presets. Now, most of the highway was pretty quiet, but then a node would appear, and then another. In some places like Concord, New Hampshire, were surprisingly just packed with nodes and activity. >> And it's crazy. We just we found so many different nodes. It looks like there's 15 nodes in total. Again, we're on the long fast channel. So, like there could be other nodes on other channels, other firmwares, like uh Reticulum or Mesh Core. This is just long fast on Meshtastic. And this is where we started. This orange node is actually my node. So, there was nothing there initially, but then when we got up to Palm Bay, Jacksonville, >> I had the hop limit on this set to three. Yeah, of all those nodes we saw, not all of them are direct peers, because the other thing is like probably more nodes, they only announce themselves at various intervals. And we're literally driving, you know, on the highway on 95, you know, 70-80 mph. So, we're not in any one location for any like long period of time to really kind of receiving any potential beacons that are going out. So, and we'll see what the rest of the trip has in store.

>> And every time we crossed a decently sized bridge, I'd try to shoot out a message to see if it would return an acknowledgement. And surprisingly, about half the times it actually did go through. >> Just went over the Bridge of Lions, and I just sent a message. Sent acknowledge, so sounds promising. >> When we crossed the Arthur Junior Ravenel Bridge in South Carolina, someone actually replied to say that they received my message, which was pretty neat. That was the first moment this stopped feeling so theoretical. >> Um and we just sent a message over long fast, and it was acknowledged in a couple seconds. Again, it's one of those things where if you have a solid line of sight, then it just dramatically increases the range, and we got some nodes out here apparently. >> Now, LoRa loves elevation, and a little bit of line of sight can suddenly extend your messages much further than you could ever imagine. And most people don't really fully grasp that it's really only governed by obstruction and the curvature of the Earth. Other than that, those waves just keep going.

So, this right here is a handheld node. So, it's basically designed to be a companion piece to something that drives it, usually your phone that has like the Meshtastic or Meshtastic app on it. But, this over here is a fully self-contained unit. So, it's more like a piece of infrastructure. I don't necessarily need to walk around with this thing, but what I could do is I could deploy this basically someplace with good line of sight. Um this guy will run independently and it will essentially extend the mesh. And what's really interesting is most of these devices run on what are called MCUs. So, they're not full-fledged computers. They're not even Raspberry Pis. They're microcontrollers. And what makes that relevant to this whole objective is that they're low energy. And because they're low energy, you can do things like these fully self-contained solar nodes. Some people talk about using um a higher-powered Laura boards, like this right here is the Null Hat Meshtastic, and it's a 1-W board. But, the thing about it is if you think about it, like to power a 1-W board, it's going to have higher energy draw. You're either going to need a more capable battery or something to basically make this board actually output that full 1 W, which is why when you have these MCUs that are more like 22 dBm or in that neighborhood, those operate at extremely low power draws. So, that's what makes it possible to get away with just using solar.

Historically, that has been relegated to Meshtastic. With Reticulum, the RNS, which usually runs on a computer. But, now you have something called Micro Reticulum. You can run the entire RNS stack on a fully self-contained unit like this now. And so, you can do the same thing that we were able to do with Meshtastic, you can now do with Reticulum. I did it with a Heltec V4, and that's how I was able to put it on my drone and just launch it up in the air, and it became a piece of infrastructure. It was running as a transport node. It's not the quite the same function as a repeater, but it serves the same purpose. And what was interesting is a lot of the nodes that we saw on our trip were actually these guys right here, these Sense HAT nodes. And now that, you know, we can bring um Reticulum to the same set of hardware, it's going to open a lot of new doors for us. >> And apparently, I wasn't the only radio head sporting exotic antennas on my vehicle. Solidarity. I also got a very welcome message from the FCC along the way. My technician class ham radio license had finally come through, which was another side quest that I had been working on. And that brings up an interesting difference between Meshtastic and Reticulum, which is another project that I have really been on a kick with recently. With Meshtastic, if you have a ham radio license, you can configure it to use that higher transmit power, but the drawback is that it will unencrypt your messages. With Reticulum, encryption is not really optional, and it's not really feasible to remove encryption from the protocol, so it can't simply take that same approach. But I'll be exploring other ways to work around that in future videos.

And the more I drove, the more I noticed how many 18-wheelers were on the road. So if my little car rig could hear this much, there might be a real play here. Small nodes mounted on trucks moving up and down the highway. That, combined with store and forward, could really do wonders for the mesh. And we had finally reached Meredith, and even Bruno made a friend. But interestingly, one day when we were getting a lunch, we suddenly lost power. >> Okay, so you can't make this stuff up, but we just got to our destination in New Hampshire here. The whole town, or at least this side of the town, is has no electricity. Power just went out. >> And the utility provider website confirmed that a major section of the city had lost power, and it lasted for several hours. So of course, I had to try to send a message at that critical point just to see what would happen. And when I posted in the primary channel that Meredith's power grid was down, the message was actually acknowledged, which was really cool to have that parallel communications layer stay alive while the main grid was down. And for that moment, it felt less like a hobby and more like real infrastructure.

>> But what's interesting is the the mesh here is pretty healthy. So we are Neo 1 right there, and you can see all the nodes we picked up from our whole thing. If the grid did go down, you can still get comms out. And I'm like I, you know, I'm not in any particular nice vantage point here. Fun scenario here to be able to test out this technology, and it is working. It's at 182 nodes coming up from Florida all the way to New Hampshire. We are now making our way back. >> Then on the way home, the power went out again during a storm in Charleston, which was twice in two separate states that the electrical grid had failed while this little parallel communications layer stayed alive and healthy. >> So on this trip, we've experienced three blackout {slash} brownouts, which is just kind of interesting. I don't know if it's a has to do with how much power people are using nowadays or what, but uh seems to be happening more frequently. >> Maybe it's just intuition, but I do think that brownouts and outages in general are going to become a bigger part of normal life as energy demands increase and the grid basically struggles to keep up. I could be wrong, but I watched it happen in real time across more than one state. And that's exactly why decentralized infrastructure matters.

At that point, between the bridge replies and the outage messages, I thought I'd already seen the result of the experiment. But when we finally got home, I checked the node database. And this basic consumer-grade radio in my trunk had discovered a total of 458 nodes. That was far more than I had expected, and it was only the network that we could see. There were almost certainly other nodes using different frequency radio parameters or encryption keys, and anything that was simply out of range when we passed by. So that 458 figure wasn't the ceiling, it was probably more like the floor. And that proves something important. The interest, infrastructure, and community already exist, but it also exposes a limitation. Meshtastic, Mesh Core, and other LoRa networks operate in separate lanes. If their frequency, bandwidth, spreading factor, coding rate, or encryption keys don't match, they don't automatically talk to each other. And the way they move traffic matters, too.

Meshtastic relies primarily on managed flooding. A message is broadcast, nearby nodes rebroadcast it, and the process continues until its hop limit runs out. Reticulum works differently. It discovers a path to a destination, and its transport nodes learn the next hop needed to move traffic along that route. Instead of flooding the mesh with every message, it can reuse an established path. That lets Reticulum scale with the length of the route, rather than the size of the entire mesh, which is a difference that's going to become more salient as the movement grows. Not to mention, Reticulum can bridge traffic across LoRa, Wi-Fi, TCP, packet radio, and really any other transport. And that's truly Reticulum's killer feature, its ability to seamlessly bridge mixed mediums. Now, Reticulum is still early, but its tooling and hardware support are moving pretty quickly, which does leave an open question. What should happen to the existing Meshtastic infrastructure already out there? Should we bridge those nodes into Reticulum through software? Should those boards eventually be reflashed to run Reticulum natively? Or does the future use a mix of both?

And I don't have the answer to that question, but I do think that's the juncture that we're currently at. So, the problem might not be that nobody is building infrastructure, the problem might be that that infrastructure is still a tad fragmented. And the future probably isn't a series of isolated networks running in parallel, it's probably a network of networks that uses internet when it's available, Laura at the edge, Wi-Fi where it makes sense, [music] and packet radio over longer distances, and really whatever else regular people can build and bridge into [music] Reticulum. This trip convinced me that the open-source internet isn't some finished thing waiting to launch. It's already out there. It's just not evenly distributed yet. But if you know how to listen, you can [music] probably hear it from your trunk. Anyways, guys, thanks for watching and happy meshing.

</details>
