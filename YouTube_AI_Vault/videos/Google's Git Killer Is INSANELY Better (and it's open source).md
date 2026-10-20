---
title: "Google's Git Killer Is INSANELY Better (and it's open source)"
video_id: cZqFaMlufDY
channel: "[[channels/DevOps Toolbox]]"
uploaded: 2025-05-02
processed: 2026-07-06
duration: "16:27"
url: https://www.youtube.com/watch?v=cZqFaMlufDY
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [version-control-workflow]
tools: [Jujutsu, Git, Carapace, Ghostty, Neovim]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Google's Git Killer Is INSANELY Better (and it's open source)

![thumbnail](https://i.ytimg.com/vi_webp/cZqFaMlufDY/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=cZqFaMlufDY) | 📅 Uploaded [[uploaded/2025-05-02]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> DevOps Toolbox introduces Jujutsu (jj), a Google-originated, Rust-based version control system that uses Git as its underlying storage but replaces Git's staging/branching model with a simpler "everything is a change" workflow. The video walks through installing jj, then hands-on demos of status/log, describing and squashing changes, undo, branchless workflows, merging with multiple parents, rebasing, and jj's standout feature — rebases and merges that always succeed, with conflicts resolved afterward rather than blocking the operation.

**Watch this if:** you already know Git well and want to evaluate a backward-compatible alternative that removes the staging area and makes history rewriting (rebase, squash, edit-in-place) far less error-prone.

## Key Takeaways
- Jujutsu (jj) is a Rust-based VCS, installable via `cargo install`, `brew install`, `nix`, or from `github.com/jj-vcs/jj`, that uses Git as its backing database (`jj git init`) — so it's fully interoperable with existing Git repos and remotes.
- There's no staging area/index in jj: every change in the working copy is effectively already "staged," which removes an entire class of `git add` friction.
- `jj status`/`jj st` and `jj log`/`jj l` show changes with a change ID (stable across rewrites) and a Git-style commit hash (which changes whenever the change's contents are rewritten) — the `@` marker shows the change currently being edited.
- `jj describe` sets/updates a commit message at any time without "finishing" the change; `jj new` starts a fresh change and pushes the previous one to be the parent; `jj squash` combines a change into its parent (and can target a specific file, or open an interactive hunk-picker with `squash -i`).
- `jj abandon` discards the current working-copy change and starts fresh (no more `git reset --soft/--hard` juggling); `jj undo` reverses the last operation (including undoing an undo).
- `jj edit <change-id>` jumps directly to any earlier change to modify it in place, and jj automatically rebases all descendant changes on top — the video's core claim is that this rebase always succeeds.
- Jujutsu has no first-class named branches — "branches" are just changes with different parents (anonymous branches); merging is done by running `jj new <parent1> <parent2> ...` (supporting more than two parents) rather than a separate merge command.
- When a rebase produces a conflict, jj still completes the rebase — the conflict is recorded in the log and resolved afterward via manual markers or the interactive `jj resolve` UI, so you're never left in a broken mid-rebase state.

## 🛠 Tools & Software
- [[topics/Jujutsu]] — the Git-compatible version control system that is the entire subject of the video, demoed end-to-end (init, status, log, describe, new, squash, abandon, undo, edit, branching, merging, rebase, conflict resolution).
- [[topics/Git]] — jj's underlying storage backend; every jj repo is also a valid Git repo, and the video continually contrasts jj's model against Git's staging/branch/rebase behavior.
- [[topics/Carapace]] — shell completion tool demoed providing a fuzzy-finder with command descriptions for jj subcommands.
- [[topics/Ghostty]] — the terminal used to record/demo the video, built by Hashicorp founder Mitchell Hashimoto (mentioned as a notable jj adopter).
- [[topics/Neovim]] — set as jj's `$EDITOR` so commit-message editing uses nvim instead of jj's default pico-like editor.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
None identified.

## ✅ Action Items
- Install jj (`brew install jj`, `cargo install jj-cli`, or via nix) and run `jj git init` inside an existing or new Git repo to try it alongside your normal Git workflow.
- Set `$EDITOR` to your preferred editor (e.g. Neovim) before using `jj describe` so commit-message editing isn't stuck in a barebones default editor.
- Practice the `jj new` / `jj describe` / `jj squash` / `jj abandon` loop on a throwaway repo to build intuition for jj's "everything is a change" model before relying on it for real work.
- Try deliberately creating a rebase conflict and resolving it with `jj resolve` to see the always-succeeds rebase behavior firsthand.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Cold open analogy: trying an unfamiliar-feeling but ultimately better way of doing something you already know well (Git).
- `1:03` — Intro to Jujutsu (jj): Google-originated, endorsed by GitHub's and Hashicorp's founders, even acknowledged by Linus Torvalds.
- `1:26` — Installing jj (cargo/brew/nix) and initializing a repo with `jj git init` on top of a small Go project.
- `2:31` — `jj status` basics: no staging area, root commit, and a working-copy change with change IDs vs. commit hashes.
- `3:23` — `jj log`, the `@` marker for the current change, and using Carapace for fuzzy autocompletion.
- `4:04` — `jj describe` to set commit messages without "finishing" a change; setting `$EDITOR` to Neovim.
- `5:36` — `jj new` starts a new change; edits show up automatically as tracked changes (no untracked-file concept).
- `5:56` — `jj undo` reverses the last operation.
- `6:41` — Describing/squashing changes with `jj squash`, including targeting a specific file and the interactive `squash -i` hunk picker.
- `8:16` — `jj abandon` to discard the current change and start clean.
- `8:41` — The core differentiator: `jj new -B` and `jj edit` to jump back and edit earlier changes, with automatic, always-succeeding rebase of descendants.
- `10:50` — Branches in jj: no named branches, just anonymous changes with different parents (a "branchless workflow").
- `13:02` — Merging via `jj new <parent1> <parent2>` (supporting 3+ parents) instead of a dedicated merge command.
- `13:52` — `jj rebase -s -d` to move a change onto a new destination, plus `@+` to jump to the resulting child commit.
- `14:20` — Demonstrating a deliberate conflict and resolving it with manual markers and the interactive `jj resolve` UI.

## Transcript
<details>
<summary>Full transcript</summary>

You know how sometimes you find a new way of doing something familiar and initially think "Why would I want to do it that way?" Picture this: you've been driving your car the same way forever — steering wheel, pedal, the usual stuff — then one day your buddy pulls up and goes "Dude, do you want to try my new ride, it uses a gamepad instead of a steering wheel." And you're like "A gamepad, really? Sounds ridiculous, why mess with something that works?" But you hop in, put your hands on, feeling totally awkward, but then you think "Huh?" You fly around corners feeling more controlled than ever, and suddenly you're thinking "This is kind of actually awesome." That got me thinking about something we do every day: Git. Everyone uses it, right? But what if I told you there's a better way, built at Google, recommended by industry geniuses like Scott Chacon, founder of GitHub, and Mitchell Hashimoto, founder of Hashicorp (also the creator of the amazing Ghostty terminal) — something that even Linus, yes, this Linus, the actual creator of Git, has officially acknowledged the strength of and how it addresses some of Git's limitations. JJ, or Jujutsu, might not only improve everyone's workflow, it'll change how we think about version control, and trust me, you want to see this one.

Not sure how I dared not mention it: JJ is written in Rust, so you can `cargo install` it if you like — I'm not that cool, and on my Mac `brew install` does the trick, and since I'm expected to say it, it's available through Nix at jj-vcs/jj on GitHub. Good — with jj installed, it's available to us, but now what? Let's start with the simplest Hello World project as if Git doesn't exist. On a brand new project directory, a small Go app is enough to get started — I'll also create a go module so the vim LSP doesn't try to murder me every time I view the file — and the app runs. So here we go: `jj git init` initiates a new jj-based repo. Yes, it used "git" in the command, and if you're like me asking why not just `jj init`, here's the deal, at least what I make of it: jj is like a client to a system that uses Git as a database. At this point jj is still backed by Git, and for a good reason.

Let me show you: instead of a `.git` there's a `.jj` that's slightly different — it holds a working copy with state and a bunch of other files; the repo holds a state of operations and other storage information. The first command we're looking at is `jj st` (jj status), which shows files added, indicated by an "A" next to them, an apparent root commit (how jj repos start), and a working-copy commit with a few interesting details. Unlike Git, jj has no index — no staging area where files are staged then committed. In a way, jj has everything staged already; it sounds weird but will make perfect sense shortly. Back to `jj status`: each line has a series of characters — this is what jj tracks as a change — and next to it a more familiar hash indicating a commit, just like the one you're used to. We'll talk about why these differ and why we need both, but for that we need to make some changes.

`jj l` is short for `jj log`, the most useful command in the system — it shows the same entries as status but adds a timestamp and, more importantly, identifiers next to each entry, the most important being the `@` sign indicating the change we're currently editing. Before making a change, I'll mention that autocompletion is your best friend with any system — this is Carapace giving me a fuzzy finder with easy descriptions, which is extremely useful; it finds commands and their short forms if they exist, and the jj devs were kind enough to produce them for useful subcommands.

Now let's say I'm ready to give my changes a proper description — this is done with `jj describe`, and it can be done more than once on the same change. Giving a description doesn't mean we're done, it just means we have a good description for it — makes sense, right? We can either provide the message with `-m` or use the internal editor, and you'll notice we've been given "pico," which is an absolute blasphemy — making sure `$EDITOR` is set to `nvim` fixes this. Now we can describe the change and save; you'll notice that similar to Git, jj asks for a name and email, which I'll happily provide. That's it — jj now opens the log with the change using my email and description, but you'll probably notice the `@` sign still says we're editing the same change, and that's no accident: a commit, or "change" as jj calls it, is an ongoing, dynamic, ever-evolving creation. Let me say that again: a change doesn't have an end of its own, it ends when a new change starts.

So let's do it: `jj new` starts a new change, and now the `@` sign moved — the previous change ID on the working copy above is now the parent commit, also addressable via `@-`. There's a new change, currently empty with no description; the status shows no changes in the working copy, so let's make some. Adding a small comment shows up as a modification, indicated by "M." A new unfamiliar file will always show up as a change that's "added" with an "A" next to it — in Git it would be an untracked file, but in jj it's a change like any other. Creating another new change works even though the previous one has no description, which is a typical concept in jj: it lets you work even when things aren't "finished."

Before making fixes backwards, here's a mind-blowing concept: jj comes with `undo` — yes, undo — the last change, and voilà, we're back to the previous change. You may have noticed the changes have their first character colored — that's because jj makes it easy to address them without providing the entire ID, another sweet and thoughtful touch.

(A quick self-sponsor break: the video isn't sponsored, so the host plugs his own two workshops — a "Second Brain with Neovim and Obsidian" course and a quick-start Kubernetes workshop — before returning to the demo.)

Now let's describe this change and add another commit — remember, a change in jj is a dynamic creation and doesn't end when we describe it; describing it again opens the editor with the current message, which can be changed and saved. We can also provide the message while starting a new change with `-m`. Now let's make another commit under an "another change" message, but it feels like it could have worked fine with the previous description, and there's no reason to add another change to the tree — `jj squash` does exactly that: it combines the changes and their messages. Once saved, something interesting has happened: both changes were combined into one, and you might notice that while the change ID stayed the same, the commit hash changed, along with the timestamp, indicating this is a different atomic commit. Not only that, there's a new change automatically started on top, which we're currently at.

The even cooler thing about squash is that it doesn't have to address an existing change — if I just add another comment to `main.go`, no description, nothing, I can run `jj squash main.go` and specifically the `main.go` changes get pushed down to the parent commit, again keeping the change ID but recreating the commit hash. Crazy, isn't it? Just to confirm it worked, the status shows the working copy has no changes, and the top of `main.go` does in fact have the fourth comment made earlier. Just to show how fancy jj can get, `squash -i` pops an interactive session where you can literally pick files and even hunks of code to squash down if you want. Here's another gem: if you don't like the current change, you can always `abandon` it, effectively resetting the working copy and creating a new change to work on — no messing about with `reset --soft`/`--hard`, using HEAD, or counting commits with the log.

So we can init, describe, create new changes, undo them, and abandon working copies — but we're just getting started. The next bit is jj's real power over Git, the heart of the difference. Let's create a new change with a descriptive name — I'll add code that prints something else and confirm it — then create a new change on top, this time with an empty description. Now, what if I kept working but realized I actually wanted to make additional modifications to my previous change? There are a few ways to travel back in time with jj — the first is straightforward: create a new change with `-B` ("before") — before what, in this instance, before the current change, which doesn't have to be the one on top. I'll give it a description, and interestingly jj says it "rebased one descendant commit" — because it pushed a change before the currently-edited one, so it had to rebase the changes on top. In short: we created a new change before the one we were working on, and it automatically rebased our original change on top. How's that possible — what if there are conflicts? We'll get there, but the headline claim is: this rebase will always succeed. I know it sounds ridiculous to some, but trust me, you're going to love it.

Let's delete most of the comments in the file — now what if I still want to make changes to an earlier entry, not necessarily the last one? Remember those colored first characters of change IDs — let's use them with jj's most powerful move: `jj edit` with an ID or its colored first character. In this instance, "V" throws us back to it, and as evidence, `main.go` is empty, printing "Hello World" with zero comments on top. `jj next --edit` moves us to the next edit on the tree — the `@` sign shows we've moved from the change starting with V, and now we're at "W," where we added a comment. We can keep going down the list until we reach the current working copy — this could have been done with a direct edit, of course, but it shows the power of jj and how you can literally traverse through changes, find bugs or introduce changes, and have jj rebase them for you.

Now let's address the elephant in the room: we haven't talked about branches. jj doesn't really use them, which at first sounds like crazy talk — you can think of them as anonymous branches, or the host's preference, a "branchless workflow." Here's another head-scratcher: you don't really need to name your branches — rumor has it Meta has been doing that for years with their own system (comment below if you can confirm). Anyway, Git is built around branches, but jj sees the world differently: branches are just changes stemming from different parents — we don't need to give them names as long as we're describing the changes. To branch out in jj you run `jj new` with a reference to a different change than the one we're at — that's pretty much it. `jj new Y` creates a new working copy where the parent is the "removed most comments" change; looking at the log shows a visual branch out of what we just did, making it easier to track later when we decide to merge paths.

I'll make a quick comment to note the branch change; now when I describe it, I end up with a fork in the road described by the change. When I want to go back to the other branch, `jj edit` on the last change puts me right there — here's `main.go` untouched, and I'll add another function rather than a comment so things are easy to track later. Since jj doesn't have branches as first-class citizens and these are just anonymous branches stemming from different places, to list branches we can use the log combined with two internal functions, `heads()` and `all()` — these are called "revsets" (revision sets) and let us cover a range of commits; it's cool but out of scope for this video (comment below if you want a deeper dive).

I think it's time to put branches right where they belong: in a merge. To make things easy I'll use the log's `--limit` flag with both branch tips visible — we want to merge them into one. You'd think `jj merge` does the trick, and that's not the case: all you need to do to merge two paths is create a new change with two parents, so `jj new X Y` with a message, and we have a new merge change ready for work. This is actually more powerful than you'd think — in jj you can add as many parents as you like; we can add three different branched parents and combine them into one new working copy. Looking at `main.go` we have both the branched-out comment and the additional function, both merged successfully. You see what happened there? jj just eliminated the need for an entire command. Are you starting to question why you've been merging and rebasing in Git all this time?

jj does actually have a `rebase` command to instruct the system to put a change on top of another — let's do exactly that, then use the famous `undo` command to get rid of the merge in one simple go (this can be done again to undo the undo, so here's the merge again in case you were worried). Back to the branch: let's rebase one end on top of the other — `jj rebase -s` for source and `-d` for destination — and poof, the rebase places one commit onto the destination; the tree is now flat, but note that we're at the change as we were earlier, not on top of the rebased change; there's a nice trick for that: run `jj edit @+`, sending us to the child commit of where we're at.

Before wrapping up, let's see how jj beautifully handles conflicts. We'll do that by removing a function called "another," then creating a new change described as adding a third function, stemming from an earlier change, creating a branch. Here's the previous version of `main.go` where, instead of removing the second function, we'll add a third — this will definitely create a conflict, forcing jj to come up with a solution. Ready? `jj rebase` using the source and destination change IDs — and here we are: there's a new conflict, but what's more interesting is that the rebase went through. Wait, what? That's right — in jj, rebase always succeeds; conflicts don't leave you stuck. The log shows a conflict, and as before we're at the source of the rebase, so it's time to resolve it. We use `jj edit @+`, where we're told it's a two-sided conflict; `main.go` shows a rather familiar sight with markers pointing to the changes and where they come from, so we fix them, save, and that's it — everything's resolved. But promised to do it with style: jj comes with a `resolve` command that pops an interactive interface where we can find conflicted files (in this instance there's only one), pick it, expand the changes, and choose what goes in and what stays out (mouse support included). Upon saving, jj says existing conflicts were resolved or abandoned, and we can keep working.

So we've closed the loop: initializing a new repo, making changes, going back in time, branching out, merging, rebasing, and having everything we need to get cracking with Jujutsu as our version control. Hopefully jj left its impression on you, and even if not completely, it's worth giving it a small chance — mastering the basics of code version control also means making sure they're ingrained into your daily workflow, at least for basic operations like staging, committing, and pushing. Here are some top recommendations for a complete daily Git workflow.

</details>
