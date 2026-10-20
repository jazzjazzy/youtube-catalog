---
title: "Proxmox Finally Has Its vCenter — Datacenter Manager 1.0 Is a Big Deal"
video_id: Br34QvOMy48
channel: "[[channels/45HomeLab]]"
uploaded: 2025-12-18
processed: 2026-07-06
duration: "25:25"
url: https://www.youtube.com/watch?v=Br34QvOMy48
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [multi-node-proxmox-management, homelab-infrastructure-management]
tools: [Proxmox, Proxmox Datacenter Manager, Proxmox Backup Server, ZFS]
llms: []
protocols: [EVPN]
transcript: true
tags: [youtube, ai-automation]
---

# Proxmox Finally Has Its vCenter — Datacenter Manager 1.0 Is a Big Deal

![thumbnail](https://i.ytimg.com/vi/Br34QvOMy48/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=Br34QvOMy48) | 📅 Uploaded [[uploaded/2025-12-18]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Proxmox Datacenter Manager (PDM) hit its 1.0 stable release on December 4th, 2025, giving Proxmox homelabbers a single-pane-of-glass, vCenter-style control plane across multiple PVE clusters and Proxmox Backup Server instances. The video walks through what's new in 1.0 — centralized dashboards, cross-cluster live migration, SDN/EVPN management, RBAC-filtered views, and a mini query-language search — then does a live install and tour of the dashboard, remotes, and migration workflow.

**Watch this if:** you run more than one Proxmox node/cluster or a separate Proxmox Backup Server and are tired of juggling browser tabs to manage them.

## Key Takeaways
- Proxmox Datacenter Manager (PDM) reached its 1.0 stable release on December 4th, 2025, after alpha/beta cycles, running on Debian 13.2 "Trixie" with a Rust core and WebAssembly UI.
- PDM acts as a central control plane over multiple independent PVE clusters, standalone nodes, and Proxmox Backup Server instances — aggregating inventory, metrics, and health into one dashboard instead of separate browser tabs per node.
- Its biggest feature is cross-cluster live migration: PDM can migrate a VM between two entirely separate Proxmox clusters (not just between nodes in the same cluster) through a built-in workflow, instead of manual backup/restore.
- Role-based access control (RBAC) lets you build custom, filtered dashboards — e.g. giving someone visibility into "test" VMs by tag without granting access to the underlying host.
- PDM includes centralized lifecycle operations (start/stop/reboot, update management, SSH shell access to remotes) and a mini query language for searching resources by type, status, or tag (e.g. `vm tag:home-assistant status:running`).
- Centralized SDN/EVPN management lets you push VXLAN/EVPN/routed-fabric network configuration across multiple remotes from one interface — useful for multi-site homelab networking (e.g. home-to-office or home-to-colo).
- Community-edition (non-subscription) users need to manually add a `pdm-no-subscription` APT repo entry, or PDM's update panel throws errors once more than ~20% of connected nodes lack a subscription.
- The presenter calls 1.0 "a strong foundation rather than a finished product" — the official roadmap includes deeper PBS integration, Proxmox Mail Gateway support, more migration options, and continued Rust/UI work.

## 🛠 Tools & Software
- [[topics/Proxmox]] — the underlying virtualization platform (PVE) that Datacenter Manager centrally manages across nodes and clusters.
- [[topics/Proxmox Datacenter Manager]] — the video's main subject: a Rust-powered, vCenter-style control plane for managing multiple Proxmox clusters/nodes and PBS instances from one dashboard, demoed via a live install and walkthrough.
- [[topics/Proxmox Backup Server]] — added as a "remote" inside PDM during the demo, showing update status and centralized visibility alongside PVE nodes.
- [[topics/ZFS]] — used during the install demo to mirror boot disks (RAID 1) for the PDM VM.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/EVPN]] — PDM centralizes SDN configuration (VXLAN, EVPN, routed fabric) across remotes from a single zone/interface, discussed as relevant for multi-site homelab networking.

## ✅ Action Items
- If you run more than one Proxmox node or a separate PBS box, install Proxmox Datacenter Manager 1.0 and add all your remotes to get a single dashboard view.
- If you're on Proxmox community edition without subscriptions, add the `pdm-no-subscription` repo entry manually to avoid PDM update errors.
- Try PDM's cross-cluster live migration workflow the next time you retire or replace a Proxmox host, instead of manual backup/restore.
- Use PDM's RBAC-filtered custom dashboards to give household members or collaborators limited visibility (e.g. test VMs only) without full host access.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: the multi-node/browser-tab problem PDM solves.
- `0:50` — PDM background — alpha/beta history, hits 1.0 stable on December 4th, 2025.
- `1:36` — What PDM actually is: a central nervous system for a Proxmox ecosystem (PVE + PBS).
- `3:12` — New in 1.0: Debian 13.2 Trixie base, Rust/WebAssembly stack, key platform details.
- `4:09` — Centralized dashboard and metrics aggregation, with local caching for dropped remotes.
- `5:04` — RBAC-filtered custom dashboards for team/household access control.
- `5:53` — Multicluster management and cross-cluster live migration explained.
- `6:47` — Lifecycle operations, centralized update management, and SSH shell access.
- `7:49` — Query-language search across resources by type, status, and tags.
- `8:42` — Centralized SDN/EVPN networking management across remotes.
- `10:41` — Live install walkthrough of a PDM VM (ZFS mirror, network setup).
- `14:29` — Tour of the PDM dashboard: remotes, nodes, resource usage.
- `18:19` — Adding a Proxmox Backup Server remote to PDM.
- `20:01` — Cross-cluster live migration workflow demoed.
- `23:00` — Roadmap: deeper PBS/mail-gateway integration, more migration options.

## Transcript
<details>
<summary>Full transcript</summary>

Do you have multiple Proxmox nodes, clusters, a PBS box off to the side, maybe a nested lab or two, and about 47 browser tabs open that just keep an eye on everything? Well, Proxmox just hit something that might finally replace all that chaos with a real single pane of glass. Let's talk about Proxmox data center manager 1.0, what's new in the stable release, and what that actually means for HomeLab.

Also, really quick, about 90% of the people watching this aren't subscribed. So, if you like deep dives into Proxmox, ZFS, different tools that make your life easier, do me a favor, hit subscribe and hit the like button. Also, thank you very much. We finally hit 4,000 subscribers right before the end of 2025.

Howdy folks. I'm Zach Perry back here with 45 Home Lab. We've looked at Proxmox data center manager back in the alpha and the beta days, actually about 2 months ago for the beta when it was still bare bones but building with each iteration. Well, as of December 4th, 2025, Proxmox data center manager 1.0 is out as stable, fully supported product. So, in this video, we are going to go and walk through a couple of things. So, what Proxmox data center manager actually is. Very important question for those who don't know. The big highlights in the 1.0 stable release. Why this matters a lot if you're running more than one Proxmox box in your home lab, a walkthrough of the install process, so going from the actual setting up the VM to the process very similar if you've done an install before, and the road map that the PDM Proxmox data center manager has.

What is Proxmox data center manager? Think of it as — and I'm going to call it PDM from now on just to kind of save me going over it over and over again — but it's kind of the central nervous system to your Proxmox ecosystem. So instead of logging into each separate PVE node, keeping separate tabs of your PVE clusters and PBS servers, Proxmox backup server, managing updates, migrations, metrics, and 10 different places. Now, I know there are a ton of tools that can facilitate this. Devolution's RDM, Royal TS, mRemoteNG, and a slew of others. Use them all, they're all great, but it's good to have something right from the Proxmox devs that its sole purpose is everything Proxmox related. And you get one UI, one web UI that connects multiple Proxmox nodes, so PVE, PBS instances, and more. Aggregates inventory and metrics across all of them. Lets you do basic life cycle operations and even cross-cluster live migrations from a single place, which is a huge quality of life update. Officially, it's designed for large distributed environments, multi-site, multi-cluster, data center type sort of setups. But the features that it has and that they map out, they map up nicely with a home lab setup that has a main HL15B or HL15 2.0, or even a couple of them making a Proxmox cluster or a few HL8s, anything like that, and you can have a dedicated Proxmox backup server box integrated into that, and all that can now be treated as one logical data center from the PDM UI.

Now what's new and important in the 1.0 stable release: some of those key platform details, the base OS Debian 13.2 Trixie, kernel 6.17.2-2 as a stable default. ZFS 2.3 doesn't really have much of a place in this besides if you use ZFS for your boot drives. The stack core services plus web UI written in Rust, with Rust/WebAssembly UI for responsiveness and security. And from the data sheet and the press release, the big enterprise themes are simplified management, enhanced visibility, improved efficiency, and future-proof open-source stack for scaling Proxmox environments. So what I mean in plain terms is this is one of the bigger things Proxmox has been lacking compared to ESXi and vCenter. And it's great to see this finally get released into stable.

Now, let's dive into the features that actually matter when you're the person that has to get up and fix things at 3:00 a.m. So, you have that centralized overview and metrics aggregation from a single dashboard. You can see the global health of all of your connected nodes, that being cluster or single servers, Proxmox backup server instances — pretty much everything right now except the mail gateway, which is on the roadmap. You get an aggregate of CPU, RAM, storage IO, VM/container counts and status, and it benefits from local caching, so if a remote briefly drops you still see the last known state instead of an empty dashboard.

You also have RBAC — role-based access control — which lets you build custom dashboards filtered by specific remotes, resource types (nodes, VMs, containers, SDN, PBS data stores), or operational tags like critical, testing, GPU, home automation. These views tie into native RBAC on PDM and give someone access to a view of test VMs without giving them rights to the actual host itself. Great for multi-user home lab households or letting friends/co-workers play in a sandboxed environment.

Then there's multicluster management and cross-cluster live migration. PDM can manage independent clusters and standalone nodes as equals, and allows live migration of VMs between clusters, not just between nodes in the same cluster. Traditionally, cross-cluster moves meant backup/restore or manual `qm`/`pct` shuffling. Now there's a built-in workflow for moving a VM between separate clusters — great for maintenance, retiring old hardware, or shuffling noisy workloads.

Next, lifecycle operations, logs, and centralized updates. PDM isn't trying to replace the full Proxmox VE UI, but gives you a lot of the daily-driver stuff from one place: start/stop/reboot VMs and containers across infrastructure, basic configuration edits, centralized task history and logs across remotes (useful for audits and troubleshooting), a central update management panel showing available updates across connected PVE and PBS systems, and the ability to open SSH shells to remotes directly from the PDM console.

There's also a powerful search and query language — closer to a mini query language inspired by tools like Elasticsearch or GitHub search — letting you filter by resource type, status, and tags (e.g. `vm tag:home-assistant status:running`), which matters a lot once you have dozens or hundreds of VMs.

On networking: centralized SDN/EVPN. If you're using Proxmox SDN — VXLAN, EVPN, routed fabric — you now have a central zone for configuring all of that and can push those configurations across multiple remotes from a single interface. Useful for multi-site networking (home to office, home to colo) and isolated VLAN/VRF setups for IoT, cameras, or labs.

What does this mean for a home lab in practice? If you run a separate PBS VM, a mix of critical services (DNS, Home Assistant, backups, Frigate) and more, PDM gives a single pane of glass to see what's running where, which nodes are hot, which storage pools are filling up, and easier maintenance windows for migrating VMs between clusters or rolling updates across a fleet. If you've only got one Proxmox node and a couple of VMs, PDM is probably overkill right now, but as soon as you add more nodes and infrastructure, it becomes valuable — especially with HA, backup servers, and nested test environments.

The presenter then does a live install: setting up a 2-vCPU, 2GB RAM VM with three virtual disks (using ZFS RAID 1 mirror across two of them), one network interface, running through the standard Proxmox installer, then the PDM installer itself — noting it pins network interface names, similar to recent PVE/PBS installers. After install, PDM is reached over HTTPS on port 8443 (versus 8006 for Proxmox VE or a different port for PBS).

In the dashboard tour: the presenter shows an existing PDM instance with several remotes already connected — eight nodes online. He notes that if fewer than about 80% of connected nodes have a valid subscription, PDM's update mechanism throws errors, since it defaults to enterprise repos; the fix is manually editing `/etc/apt/sources.list.d/pdm-enterprise.sources` to point at the `pdm-no-subscription` repo instead. He walks through dashboard views (CPU/memory usage per node, including nested test nodes), custom views with resource-type filters and RBAC, node configuration, certificates, and subscription status.

He then adds a Proxmox Backup Server remote by IP, letting PDM pick up its TLS fingerprint automatically, creating an API token for authentication, and confirming the connection — after which the PBS remote shows up with its own update status inside PDM, linking through to the PBS web UI itself for actual upgrades.

Finally, he demonstrates the cross-cluster migration workflow: selecting a nested nested Proxmox/Ceph cluster as the source, attempting to migrate a VM to another node within the same cluster (which PDM correctly refuses, since it's the same node), then targeting a genuinely separate cluster/node to show the intended cross-cluster migration path.

Wrapping up, the roadmap includes deeper Proxmox Backup Server integration, Proxmox Mail Gateway integration, more advanced migration options, a more fully featured SDN experience within PDM, and continued evolution of the Rust/WebAssembly UI and API-driven automation. The presenter frames 1.0 as a strong foundation rather than a finished product, and says it feels like the missing piece that makes Proxmox a more complete alternative to the vSphere/vCenter stack, especially for anyone running multiple nodes spread across a home lab.

He closes by asking viewers whether they plan to deploy PDM, wants their setup preferences (bare metal vs. VM), and points to 45HomeLab's store for HL15 systems and financing options.

</details>
