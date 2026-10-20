---
title: "Vite+ is OPEN SOURCE and FREE!"
video_id: AJxH3Gvb-PU
channel: "[[channels/VoidZero]]"
uploaded: 2026-03-13
processed: 2026-07-05
duration: "5:47"
url: https://www.youtube.com/watch?v=AJxH3Gvb-PU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [monorepo-tooling-setup, frontend-build-tooling]
tools: [Vite Plus, Vitest, TypeScript, ESLint, oxlint, Node.js]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Vite+ is OPEN SOURCE and FREE!

![thumbnail](https://i.ytimg.com/vi/AJxH3Gvb-PU/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=AJxH3Gvb-PU) | 📅 Uploaded [[uploaded/2026-03-13]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> VoidZero announces the alpha release of Vite+, a unified toolchain (runtime, package manager, task runner, linter/formatter) built around Vite, now fully open source under the MIT license. The video walks through creating a monorepo project, running/caching tasks, catching format/lint/type errors with `vp check`, migrating an existing project, and pinning a project's Node.js version with `vp env`.

**Watch this if:** you manage a JS/TS monorepo and want one CLI to replace Vite + your task runner + linter + Node version manager.

## Key Takeaways
- Vite+ is a new unified entry point for web app development: it manages the runtime, package manager, and frontend toolchain in one binary, released free and open source (MIT license).
- `vp create` scaffolds a monorepo, standalone app, library, or custom template; when creating a project you can opt in to generating AI agent config so coding agents know which Vite+ commands to use from the start.
- `vp run` (no arguments) lists every task across all packages in a monorepo, grouped by package, with fuzzy search to jump straight to a task and run it.
- Task caching is built in and content-aware: `vp run <task> --cache` skips re-running a task if its actual inputs haven't changed (e.g. changing an unrelated package's file doesn't invalidate the cache for a package that wasn't touched).
- `vp check` runs formatting, linting, and type checking across the whole repo in one command, and `vp check --fix` auto-fixes what it can (e.g. formatting issues) while still surfacing real type errors.
- `vp migrate` upgrades an existing project's tooling to Vite+ (e.g. migrating ESLint rules to oxlint), rewriting imports as needed — requires Vite 8 and Vitest 4.1 first if migrating from an older setup, and may need manual adjustments depending on prior tooling.
- `vp env` manages per-project Node.js version and package manager, letting you pin a specific Node version (e.g. pinning one project to Node 25 while another defaults to Node 24) to eliminate "works on my machine" runtime mismatches.

## 🛠 Tools & Software
- [[topics/Vite Plus]] — the subject of the video: a unified CLI (`vp`) for creating, running, checking, migrating, and environment-managing Vite-based projects, demoed end to end.
- [[topics/Vitest]] — cited as a version dependency for migrating an existing project to Vite+ (requires Vitest 4.1+).
- [[topics/TypeScript]] — used in the demo project; `vp check` catches a deliberately introduced type error.
- [[topics/ESLint]] — existing linter config that `vp migrate` can convert over to oxlint.
- [[topics/oxlint]] — the linter Vite+'s `vp migrate` can migrate ESLint rules to.
- [[topics/Node.js]] — version-managed per project via `vp env`, including pinning a specific version (e.g. Node 25).

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install the Vite+ binary and run `vp help` to see all available commands.
- Try `vp create` with the "agents" option enabled so AI coding assistants get Vite+-specific config from the start of a new project.
- Run `vp check --fix` on an existing project to catch formatting, lint, and type issues in one pass.
- If migrating an existing Vite/Vitest project, upgrade to Vite 8 / Vitest 4.1 first, then run `vp migrate`.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: Vite+ alpha release, unified toolchain, MIT open source.
- `0:15` — Get started: installing the Vite+ binary and running `vp help`.
- `0:29` — Creating a project with `vp create`: monorepo, app, library, or custom template, plus optional AI-agent config.
- `1:36` — Task runner: `vp run` listing and fuzzy-searching tasks, and content-aware caching with `--cache`.
- `3:44` — `vp check` catching formatting, linting, and TypeScript errors, with `--fix` for auto-fixable issues.
- `3:53` — `vp migrate` for upgrading an existing project's tooling (e.g. ESLint to oxlint) to Vite+.
- `4:32` — `vp env`: pinning per-project Node.js versions to avoid "works on my machine" issues.
- `5:24` — Outro: docs, Discord, and GitHub for feature requests/bug reports.

## Transcript
<details>
<summary>Full transcript</summary>

Today were excited to announce the alpha release of Vite+ the new unified toolchain and entry point to web application development. Vite+ is there to manage your runtime package manager and frontend toolchain and is now available fully open source under the MIT license. Lets try it out. To get started we have to install the Vite+ binary through a very simple shell command or PowerShell if you are on Windows and after setting up Vite+ you are just up and ready. To check you can type vp help to see all the commands that are available.

Now that Vite+ is up and ready we start creating a project and we can do this by writing vp create. We have a couple options now to create a monorepo a Vite+ application a Vite+ library or use a custom template. Now that Vite+ has monorepo support we stick with that and we use vp-demo as the package name. We can choose the agents so AI straightaway knows about Vite+ from the getgo and which commands to use and not to use. Then we can also add our .vscode folder for the editor and eventually also set up pre-commit hooks so there is no need for husky or lint-staged thats also built into Vite+ straightaway. And then the monorepo is being created and we jump into the project right in our editor.

The first thing we want to do is running the dev server of course. So we can run vp dev and then type in apps/website because thats where our website is in the monorepo structure and the classic Vite dev server will start here. Switching over to the browser we can see the new Vite 8 starter template here for TypeScript and Vite application. The count is as usual working through the button and the HMR also works as expected. Of course we dont have to start a dev server for vp dev and then writing the folder. We can also straightaway go into apps/website and run vp dev there and we will see the same result.

But of course thats not all. We have a lot of tasks and scripts that we can run in our application. For that we can use vp run. And instead of taking a look at every package.json we can just run vp run without any arguments and see all the tasks in our project right away. Also grouped by package. Here we have dev prepare and ready at the root and then for utils and for website different tasks. We can go through them easily through arrow keys but we can also type something. Like we can type ubd which is fuzzy search and we get utils#build. Which we can then straightaway run by hitting enter.

But thats not all that vp run can do. We can actually run the same command utils#build but with caching enabled by using --cache. You can of course also configure that if you need something like env variables that affect the whole caching. Now if we run it again we see okay obviously no cache hit it ran for the first time. But if we run it again we see okay perfect. 500 milliseconds saved no problem the cache hit and we are doing the replay. If we now change a file in the utils package like the index.ts and say hello friends and add another exclamation mark and run the same command. Theres a cache miss and we run the same command again. Now if we do it again of course the cache is hit. The cache is actually smart enough to infer input. So if we now change lets say the counter.ts in our website and say counter starts at 1 and we run the same command the cache is still there and being hit. Because the utils they didnt change.

But of course building is one thing. What we want to do is also catch errors early on. Formatting linting type errors you name it. For that lets introduce something and say const a equals 2 and lets say a is actually a number which obviously is not fully correct. Now we can run the vp check command and this will check the whole repository. Here we see first of all formatting issues found yep semicolon lets run vp check --fix and this is fixed right away. But now obviously we still have a type error here and this is reported correctly. So we get the info here whats wrong and we can for example add a // @ts-ignore and run the command again and we should be good to go. Now only the linter is complaining saying that well a is unused so we use underscore a run the same thing again and voila no more errors and were good.

Oh and of course we know that you cant start on a green field all the time actually rarely. Thats why we created vp migrate. So if you have an old project thats based on some of the tooling already no problem you can use it to eventually migrate over. So here we run vp migrate we can do the same selections as before and now we have the option to migrate ESLint rules over to oxlint for example. Lets skip that for here there will be still a few things happening like imports being rewritten and then the project is ready for Vite+. Keep in mind that you need Vite 8 and Vitest 4.1 if you used Vitest before to migrate over. If you are not on these versions then migrate over there first and also most projects might need some manual adjustments depending on the tools and your workflow that you've had before. You can also find more information about the migration flow the recommended workflow and migration prompts plus other help over at viteplus.dev in our migration guide.

Now that we talked about tooling lets talk about vp env because Vite+ can also manage your Node.js version and your package manager. For that we can run vp env which is enabled by default and we can check what the current vp env is set up to. Here we see by default we have LTS up and ready version 24 the time of recording and we can also pin certain projects to certain versions. So here we can say vp env pin and then say 25 for example. So now the project that has been migrated before is using Node version 25 now. We can double check that by using vp env which node to check that and we see thats correct 25.8. If we now go to the main programming folder we can do the same thing and run vp env which node. Here we will see we will default to 24 again. So Vite+ will make sure that it doesn't come to these it works on my machine issues anymore at least regarding to runtime and package manager.

And that concludes the basic Vite+ feature overview. Of course theres always more to learn so take a look at our docs at viteplus.dev. Join our Discord to connect and chat with us. And if you have a feature request or bug report then drop that in our GitHub repository. And now lets build things together!

</details>
