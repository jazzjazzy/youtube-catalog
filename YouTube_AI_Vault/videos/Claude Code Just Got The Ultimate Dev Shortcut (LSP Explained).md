---
title: "Claude Code Just Got The Ultimate Dev Shortcut (LSP Explained)"
video_id: lffYEu5MhSQ
channel: "[[channels/Zen van Riel]]"
uploaded: 2025-12-22
processed: 2026-07-06
duration: "5:41"
url: https://www.youtube.com/watch?v=lffYEu5MhSQ
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: intermediate
use_case: [codebase-navigation, lsp-integration]
tools: [Claude Code, Pyright, Serena MCP, OpenAI]
llms: []
protocols: [LSP, MCP]
transcript: true
tags: [youtube, ai-automation]
---

# Claude Code Just Got The Ultimate Dev Shortcut (LSP Explained)

![thumbnail](https://i.ytimg.com/vi/lffYEu5MhSQ/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=lffYEu5MhSQ) | 📅 Uploaded [[uploaded/2025-12-22]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Claude Code now has native Language Server Protocol (LSP) support, letting it navigate a codebase (find definitions, find all references) the way a professional developer's editor does, instead of naively grepping through files. The video demos installing a Python LSP plugin (Pyright) via `/plugin` and compares LSP-powered lookups against the presenter's prior workaround, the popular Serena MCP server.

**Watch this if:** you use Claude Code on real codebases and want faster, more accurate "find all references"/"go to definition" style lookups instead of relying on plain text search.

## Key Takeaways
- Claude Code's new LSP support lets it communicate directly with a language's actual language server, the same infrastructure professional code editors use for navigation, rather than relying only on grep-style text search.
- Demo 1 (without LSP): asked to find the code invoking an LLM, Claude Code falls back to regular search tools, hunting for text like "chat completions" and OpenAI references to locate the right function.
- Demo 2 (find-all-references without an LSP configured): asking for all references to a function with LSP explicitly requested fails gracefully — no Python LSP server is available, so it falls back to grep, which is noticeably less precise for reference-finding.
- Installing an LSP server is a one-step fix: run `/plugin`, browse for your language, and install one directly (the video installs Pyright, Microsoft's static analyzer for Python).
- After installing Pyright and restarting Claude Code, the same "find references across files" query returns precise results (3 references across 2 files) almost instantly, instead of naive multi-file reads.
- The presenter had already solved this problem for months using the Serena MCP server (17,000+ GitHub stars), which exposes language servers to AI code editors including Claude Code — native LSP support now removes the need to set up that more complex MCP server.
- LSP support also improves type/parameter inference: for a loosely-typed language like Python, Claude Code can query the language server to return a function's full parameter list (required, optional, with descriptions) instead of guessing and introducing errors.
- The overall framing: Claude Code can now work "like a professional developer" — using go-to-definition and find-references shortcuts instead of naive full-codebase reads, which matters most on larger, real-world codebases.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the agent gaining native LSP support, demoed finding LLM invocation code and function references both with and without a configured language server.
- [[topics/Pyright]] — Microsoft's static analyzer for Python, installed as the LSP server via Claude Code's `/plugin` command in the demo.
- [[topics/Serena MCP]] — the presenter's prior solution (used for months on real projects) that exposes language servers to AI code editors including Claude Code, now made less necessary by native LSP support.
- [[topics/OpenAI]] — referenced as the API whose "chat completions" pattern Claude Code searches for while locating the codebase's LLM-invocation function.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- [[topics/LSP]] — the video's central subject: Claude Code's new native support for the Language Server Protocol, enabling precise code navigation (definitions, references) instead of text-based search.
- [[topics/MCP]] — the protocol behind the Serena MCP server, the presenter's previous workaround for giving Claude Code language-server-level code navigation before native LSP support existed.

## ✅ Action Items
- Run `/plugin` in Claude Code and install the LSP server for your primary language (e.g. Pyright for Python).
- Test "find all references" and "find the definition of X" style prompts with LSP enabled on a real codebase to compare accuracy against plain search.
- If native LSP support is broken on the current version, pin to a working Claude Code version as a temporary workaround.
- Share your language's LSP configuration to help others get the same setup working for less common languages.

## 🔗 Related Videos
- [[videos/12 Hidden Settings To Enable In Your Claude Code Setup]] — shared: Claude Code, MCP
- [[videos/12 Hidden Settings to Enable in Claude Code]] — shared: Claude Code, MCP
- [[videos/18 Claude Code Token Hacks in 18 Minutes]] — shared: Claude Code, MCP
- [[videos/6 FREE Tools That Replace Claude Code (And Beat It)]] — shared: Claude Code, LSP
- [[videos/9 NEW Claude Mods that can truly change how you work]] — shared: Claude Code, MCP
- [[videos/Agent Experts Finally, Agents That ACTUALLY Learn]] — shared: Claude Code, MCP
- [[videos/Agent Skills Code Beats Markdown (Here's Why)]] — shared: Claude Code, MCP
- [[videos/Anthropic Just Added These Features to Claude Code]] — shared: Claude Code, MCP

## Timeline
- `0:00` — Intro: Claude Code's new native LSP support explained.
- `0:22` — Demo: finding LLM invocation code without LSP, using regular text search.
- `1:37` — Installing LSP plugins via `/plugin` (Pyright for Python).
- `2:12` — Demo: using LSP to find references across files, compared to the grep fallback.
- `4:04` — Comparison to the presenter's prior Serena MCP server workaround (17,000+ GitHub stars).
- `4:28` — How LSP lets Claude Code work like a professional developer, including parameter/type inference for chat completions calls.
- `5:31` — Call to share language-specific LSP configs in the comments.

## Transcript
<details>
<summary>Full transcript</summary>

The new cloud code update comes with one very important feature that you must know about. Language server protocol support directly baked into cloud code which allows cloud code to communicate with the language that you're writing your code in just like how professional developers have always used code editors to create functional and working code. And now you can do the same in cloud code directly. So let's see how it works.

In this codebase I'm going to just ask find the code that's used to invocate an LM because this is an AI powered application. And now it's not going to use language server yet. It's going to use its regular search tools in order to find the code that I use to call the language models. In this case, it's trying to find some text that relates to chat and completions because that's very common with this AI code. It's trying to find open AI references. And now it already found in my backend transcription file the LLM call here on line 66.

Now, it's not using the language server yet, but you will find that one way that it can really use it effectively is for a question like this one. find all the references in the codebase where this function is used. And these kinds of questions are super effective when you actually want to figure out how code is used in the repository and go ahead and fix any bugs that might have been introduced by AI code.

So now we can go ahead and ask this question, but I will add with LSP. But now we see an issue. It's trying to use the language server on this symbol, but it says that no LSP server is available for Python and it will use grep instead. And the problem with grep is that it's a little bit less effective in finding the right file references compared to something like a language server that's really built to find code references quickly in the language that you're actually programming with.

Now, the absolute simplest way to configure the LSP server is to type /plugin and then go ahead and just check out all the plugins until you find the one for your language. So, in my case, I want to find the Python one. You will see that I find the Pyright LSP right here. I can just simply install it for me and for me only. Now, the great part about this is that most of the standard languages you'll be working for are supported, but I'll leave a link in the description so you can find the right documentation if you need to add your own LSP server if you're using some kind of fancy language.

But in my case, if I type plugin again, you'll see that Pyright LSP is currently installed, which is Microsoft's static analyzer for Python. So, I've just restarted Cloud Code to test it out. And I actually moved to a specific version because in the current main latest version, this feature is broken. It's probably fixed by the time you're watching this, but if not, definitely use this command instead.

And I'm going to go ahead and ask it to just check out this file. And then I'm going to say find the function for LLM invocation in here and use LSP to find references across files. Now, the reason why this is so powerful is because cloud code is not going to just naively read 100 files or use some standard command line tools. Now, it's going to use a proper language server to find all the references to this function, which is much more efficient, especially if you're working with really large code bases.

So, in this case, you can see it's using find references, and immediately it found three references across two files. So, I can do control O here to just expand that a little bit. And you can see that it finds in backend app.py on line 108, which I can just scroll to right here. Indeed, it's using clean with LLM, which is my LLM invocation function. And similarly in this transcription Python file, we of course have the definition on line 56, but it is also used inside of this file, specifically on line 90. You can see it's calling it on its own inside of the same class. So brilliant. It's able to find all those references very quickly.

And this allows cloud code to operate much more like a human developer would because if I want to know where, for example, this function is defined, I would do control and click on it. And indeed, that puts me at the definition of the file very quickly. I also don't just search naively through a bunch of files. I use these kinds of shortcuts and cloud code can now use these shortcuts as well.

If you are still doubting just how powerful this new feature is, I can let you know right now that I've kind of been using it for a couple of months already. I've been using the Serena MCP server which exposes these language servers to all kinds of AI code editors including cloud code. And this MCP server is super popular. It's got over 17,000 stars on GitHub. and I've been using it for bigger projects, not just pet projects or demos that you see all over YouTube. So, the great part about this is that I know that these language servers work very well. And now you don't even need to set up this kind of complex MCP server. It's all easy to set up include code using a simple plug-in.

Another great example of a question to ask is this one. What parameters does chat completions create except? If you're using a language like Python, which isn't strictly typed, cloud code can make a lot of errors when it's trying to come up with code. But the great part is that as it finds code that you're using across the repository, it can query the language server to better understand what kinds of parameters are required for functions. And now you can see that it comes back with this extensive list of all the required parameters, the optional ones, and not just the names of the parameters, but even the description.

So how did it do that? Well, I can actually do this myself. I can go ahead and find where chat completions create is called. It's being called here in the codebase. And I can hover over the word create. And you can see here that it actually exposes a bunch of information about the function. Essentially, claude code is now doing this just like how I would do it as a professional developer. So, it can read way more information about the function definition and pass it back to me or use that to generate much safer and reliable code.

I want you to go to the comments and make sure to share if you're using a different language that I'm not covering in this video because this way we can help each other out with the right configurations to make sure that we all get the most out of cloud code. So, we'll see you in the comments.

</details>
