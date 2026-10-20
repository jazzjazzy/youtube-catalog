---
title: "ShadCN is Way too Powerful Now"
video_id: MFJ0mH72_qI
channel: "[[channels/AI LABS]]"
uploaded: 2026-01-07
processed: 2026-07-06
duration: "9:43"
url: https://www.youtube.com/watch?v=MFJ0mH72_qI
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: advanced
use_case: [reliable-agentic-coding]
tools: [Claude Code, Ralph Loop, shadcn ui, Playwright]
llms: [Claude]
protocols: [MCP]
transcript: true
tags: [youtube, ai-automation]
---

# ShadCN is Way too Powerful Now

![thumbnail](https://i.ytimg.com/vi_webp/MFJ0mH72_qI/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=MFJ0mH72_qI) | 📅 Uploaded [[uploaded/2026-01-07]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Building shadcn/ui-based features with Claude Code often breaks other parts of an app because agents quit early or miss UI regressions. This video pairs Anthropic's Ralph Loop plugin (a stop-hook loop that re-feeds the agent its prompt until it outputs a "completion promise") with test-driven development and Playwright screenshots, then walks through a real failure — Claude prematurely declaring UI work done — and the prompt fix (a "verified" screenshot-prefix protocol forcing at least two loop iterations) that solved it.

**Watch this if:** your Claude Code agent keeps quitting mid-task on UI work, or silently breaks existing features while "completing" a new one.

## Key Takeaways
- AI agents become unreliable on large contexts and often quit tasks abruptly instead of finishing — the Ralph Loop pattern fixes this by re-feeding the same prompt via a Claude Code stop hook until the agent emits a chosen "completion promise" word.
- Ralph Loop is an Anthropic-released plugin (based on a technique originated elsewhere) with three commands: the loop command, a cancel command, and a help command; setting a max-iteration count is recommended to avoid infinite loops on impossible tasks.
- The workflow combines Ralph Loop with test-driven development (TDD): write end-to-end tests and a screenshots folder before implementing a feature (e.g. a command palette, a Notion-style Kanban board view).
- Screenshots are used purely for visual/UI verification, not via the Playwright MCP server — Claude reviews static screenshots taken at each functional step to catch shadcn/ui rendering problems.
- First attempt (command palette) worked fine because there were few chances for UI errors; the harder board-view feature exposed a real bug: Claude passed all functional tests but missed and ignored visible UI errors in its own screenshots, then output the completion promise prematurely.
- Root cause: there was no explicit test tied to the screenshots themselves, so Claude could glance at a few images, mark them "verified," and quit before actually checking all of them.
- Fix: add a "verified" prefix protocol to each screenshot, and force the agent to not output the completion promise on the same iteration it renames screenshots — requiring at least two loop iterations so a later pass can confirm every image is truly verified before allowing completion.
- After the fix, the loop reliably ran two iterations (fix issues, then verify) and correctly caught and resolved the UI errors that were previously missed.

## 🛠 Tools & Software
- [[topics/Claude Code]] — the coding agent running the whole workflow: implementing features, running tests, reviewing screenshots, and driving the Ralph Loop.
- [[topics/Ralph Loop]] — Anthropic's stop-hook-based looping plugin: re-feeds the agent its initial prompt on every stop until it outputs a configured completion promise, with a max-iteration safety limit.
- [[topics/shadcn ui]] — the UI component library whose implementations are prone to breaking other parts of an app when built by an under-verified agent; the whole video is framed around making shadcn/ui builds reliable.
- [[topics/Playwright]] — used for automated end-to-end tests and taking UI screenshots at each functional step for visual verification (explicitly not via its MCP server in this workflow).

## 🤖 LLMs Mentioned
- [[topics/Claude]] — the model powering Claude Code throughout; its tendency to quit early on full context or complex tasks is the central problem the video addresses.

## 📡 Protocols & Standards
- [[topics/MCP]] — explicitly called out and ruled out: the video clarifies it is NOT using the Playwright MCP server for autonomous browser verification, instead relying on static screenshots reviewed by the agent.

## ✅ Action Items
- Install Anthropic's Ralph Loop plugin and set a max-iteration count before running it on any real task.
- Write TDD tests and a dedicated screenshots folder before implementing a UI feature with Claude Code.
- Add a "verified" prefix (or similar marker) to each screenshot the agent reviews, and require the agent to defer its completion promise to a later loop iteration rather than the one where it renames/marks screenshots.
- Separate functional test-passing from image/UI verification as two distinct checks in your prompt's workflow, not one combined step.

## 🔗 Related Videos
- [[videos/Give Me 13mins, I Will Show You The Right Agent Setup]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Claude Code & Cowork Now Run 247 Scheduled Tasks]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Claude Released Something To Fix Your Errors]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Continual Learning in Claude Code]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/How to Build 247 Claude Agents Easy]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/How to Run Claude Code For Hours Autonomously]] — shared: Claude, Claude Code, Playwright, Ralph Loop
- [[videos/I asked Claude Code to make me as much money as possible]] — shared: Claude, Claude Code, MCP, Playwright
- [[videos/Playwright CLI vs MCP - a new tool for your coding agent]] — shared: Claude, Claude Code, MCP, Playwright

## Timeline
- `0:00` — Problem intro: AI agents building with shadcn/ui break other parts of the app; agentic loops (Ralph Loop) are Anthropic's fix for unreliable task completion.
- `0:48` — How Ralph Loop works: a Claude Code stop hook re-feeds the prompt file until a "completion promise" word appears in the output.
- `1:37` — Plugin commands (loop, cancel, help) and the importance of setting a max-iteration count.
- `2:08` — Setting up TDD: command palette and Kanban board-view features, end-to-end test and screenshot folders.
- `3:07` — TDD basics: write failing tests first, then the minimum code to pass them, then refactor.
- `3:12` — Screenshots used purely for visual verification, explicitly not via Playwright MCP.
- `3:48` — Why Ralph Loop is still needed on top of TDD: large contexts make models quit abruptly regardless of tests.
- `4:20` — Command palette run: workflow succeeds in one pass, tests pass, screenshots reviewed, completion promise output.
- `5:39` — Board-view run: functional tests pass but real UI errors are missed and ignored in screenshots.
- `6:37` — Diagnosis: no explicit test tied to screenshot review, so Claude glanced at images and quit prematurely.
- `7:19` — The fix: verified-prefix protocol on screenshots plus forcing at least two loop iterations before allowing completion.
- `8:32` — Result: two-iteration loop reliably catches and fixes major UI errors.

## Transcript
<details>
<summary>Full transcript</summary>

Most of you already know shadcn/ui as one of the most widely used UI libraries, but using an AI agent to build with it can be problematic. If you're building one-shot landing pages, you won't have a huge problem. But if you're building a new app or implementing a new feature, things break, and they break other parts of the app as well. But this isn't anything new — this problem has already been solved, and it's how engineers build apps. Now, AI agents always test the code that they write, but these agents become unreliable with large contexts. Therefore, we need a way to ensure that agents complete the work they're given. This is where the concept of agentic loops comes in, and Anthropic solves this by using the Ralph Loop.

To solve my UI problem, I tried to implement the Ralph Loop. And at first, it completely failed. But I soon learned that it wasn't because of the Ralph Loop — it was because of the process I had implemented with it. So, Ralph is actually a new plugin that has been released by Anthropic themselves. But this wasn't one of their original ideas — it's based on a technique by someone else, and Anthropic implemented and open sourced it. Basically, Ralph is a loop, and if you know about Claude Code hooks, it uses these stop hooks which run when Claude stops outputting an answer. As soon as it stops, the AI agent is fed its initial prompt file again, and this allows it to iteratively improve its work.

Now, here's the important question: when does it actually break out of the loop? There's something called a completion promise, which can be any word you input. When Claude feels like its task is completed, it outputs this promise by itself. For example, in this case, the promise is the word "complete." If the promise is in the return prompt, then the loop doesn't run again. So, until Claude outputs a promise, it doesn't stop. This makes sure that Claude doesn't just quit whenever it wants.

After you install the plugin, you'll have three commands: the Ralph Loop command, a cancel command, and a help command. In the loop command, you need to provide the prompt that is fed to the agent again and again. Sometimes it may get an impossible task that it's not able to solve, and it might get stuck in an infinite loop. So setting a max iteration count is a really good practice. I will leave the link to the repo below because they have some good best practices for the prompts you can give to the Ralph Loop. But in this video, I'm only going to discuss the ones related to the UI workflow that I'm going to show you.

So let's say we want to implement two features in this app. One is a command palette, where we add a menu to search through our app and execute other commands. To make sure that this new feature doesn't break other parts of the app, you would start with the tests — this is called test-driven development. If you're not familiar with this, you can ask Claude Code to set up the TDD structure for you, where it creates an end-to-end test folder, a screenshots folder to check for UI problems, and the corresponding tests as well. The other feature we're going to implement is a board view in the database, similar to what Notion allows us to do with their databases.

If you've caught on, test-driven development is an approach where tests are written before the code is implemented. But this means that the initial tests will always fail. So if I'm implementing the command palette feature, I wouldn't just start writing the code for it — instead, I would first write elaborate tests for it. Then we write the minimum amount of code required to pass those tests. Once that's done, we refactor and add more functionality, and with every addition, we make sure the tests still pass.

Another interesting thing is that these tests are automated, and Playwright can be imported and used for visual verification. If you think that we're using the Playwright MCP to autonomously verify this through the browser, you're wrong. With TDD, for each functional behavior, you can take screenshots. For example, if the functional behavior is adding a card, then the screenshot would show a card added into the board. So now, all the AI agent has to do is look at those screenshots and make sure there are no problems in the way that these shadcn/ui components have been implemented. These test files ensure that whenever something new is added or while a feature is being built, all of our behavioral requirements are fulfilled. But in our case, we want to use the screenshots purely for UI verification.

But if we already have TDD, why do we need the Ralph Loop? As I already stated, with larger tasks and context windows becoming nearly filled, these models abruptly quit their tasks and require constant human input. Therefore, I can have tests written beforehand for any type of function that I want, then use the loop to instruct it on what to do, and it can work autonomously — by telling it what workflow to follow and then giving it the condition for when it can output the promise, it completes the task and exits the loop, which in this case is when it passes all 25 unique tests.

So using the Ralph slash command, I gave it a prompt so that it would iteratively build the command palette feature. In the prompt we were basically telling it to implement the feature along with some basic requirements, which aren't really important because the requirements can be found in the tests as well, but we did outline the whole workflow. In that workflow, it was supposed to start by running the tests. It knows that the tests will fail, and after that it needs to implement the components to make them pass. So that's the whole goal. Now, if this were a much broader task, chances are that when the context window fills up or Claude gets confused, it will quit automatically — it will never output the completion promise. And since it never outputs the promise, the prompt will be fed back again, and it will have to start all over, meaning it will iteratively keep working on it. But since this was a smaller task, it was actually able to implement everything in a single go, write out all the components, and make all of the tests pass.

Now, after the tests pass, the workflow tells it to review all of the screenshots for the command palette. These are screenshots taken at different stages to make sure that the UI, whether it's shadcn/ui or any other component library you're using, is implemented correctly and that there aren't any minor issues. After that, it should run the tests again and make sure they still pass after the UI changes. Since all of the tests were passing and the screenshots were reviewed, it output the completion promise. This is where the loop stopped and didn't continue again.

But there was a really big problem with this, which I didn't notice in the command palette feature because there were very few chances of UI errors there. However, when I moved on to implementing the board view, I realized there was a huge mistake in the system. I started by implementing the board with the same prompt. The requirements were different, of course, but the workflow was pretty much the same. Now, I was kind of surprised when it completed all of the requirements in one go. Don't get me wrong, it was actually making sure that all of the tests were passing. But while it was doing that, there were cases where the number of successful tests would actually decrease, because by changing something, it would break something else. And this is why TDD is actually really important, because of this recursive testing and making sure that everything works.

But the main problem was that after it had verified that it was done and I went ahead and checked the UI, most of the things were implemented correctly, but it had completely missed some UI errors, such as this one. I also checked the screenshots, and the errors were showing up in those screenshots as well. So I asked it, and we analyzed what actually went wrong. The real issue was a process failure, specifically in terms of fixing the UI. What happened was that it did pass all of the tests because it was supposed to run the test files again and again, but there was no specific test for the UI other than the screenshots. It glanced at a few of them and it even ignored some of the UI errors that it had seen. Some files were completely ignored. So, the main issue was that it output its promise statement prematurely and didn't verify whether the UI was actually fixed.

We went through a whole brainstorming session on how we could fix this, and I even gave the prompt-writing best practices from the repo to Claude Code. But in the end, we came up with some specific rules and a change in the process that would ensure the UI was always correct. Now, this had nothing to do with the tests, because they're always going to run. The prompt we used for the command palette is really helpful when the feature or implementation is very large, where Claude doesn't hallucinate that it has completed the task, but instead, due to a full context window or the complexity of the task, it quits abruptly. Now, Claude Code is already really autonomous — there's no doubt about that. But there are still issues like this that we need to fix.

So, we changed a number of things in the main prompt. The first was the screenshot verification protocol. We added a simple prefix to each image that told Claude whether it had read the screenshot or not. But when I first implemented this, it still didn't read all of the images — it would read a few, write "verified" on top of them, and just like before, it would quit early. So to solve this, we encouraged it to think in a different way. We told it that after it renamed all the screenshots, it should not output the promise yet, meaning it should not consider the task completed, and it should let the next iteration confirm completion. So at least two loops should run.

What happens in the next verification is that Claude verifies all the files have the "verified" prefix. Of course, this meant we had to change the tests and separate the image verification from the functional tests. The next iteration makes sure that all the images have verified results, and if Claude misses any, it looks at them again and fixes the output. With this change, the small UI errors we were facing were finally fixed, and it was able to implement all of these features correctly. So, when it entered the next loop, it ran the tests again. Since it found some errors, it fixed them. And because all the files had the word "verified" in them, it ran one final test. This time, it completed its task in two loops and was able to fix all the major UI errors in the app.

Let's talk about Automator now. After teaching millions of people how to build with AI, we started implementing these workflows ourselves. We discovered we could build better products faster than ever before. We help bring your ideas to life, whether it's apps or websites. Maybe you've watched our videos thinking, "I have a great idea, but I don't have a tech team to build it." That's exactly where we come in. Think of us as your technical co-pilot. We apply the same workflows we've taught millions directly to your project, turning concepts into real working solutions without the headaches of hiring or managing a dev team. Ready to accelerate your idea into reality? Reach out at hello@automator.dev.

If you'd like to support the channel and help us keep making videos like this, you can do so by using the super thanks button below.

</details>
