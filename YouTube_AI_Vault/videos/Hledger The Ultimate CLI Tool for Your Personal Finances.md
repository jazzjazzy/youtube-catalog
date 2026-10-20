---
title: "Hledger: The Ultimate CLI Tool for Your Personal Finances"
video_id: hshDr2Af2RU
channel: "[[channels/Coder Kaylee]]"
uploaded: 2025-11-05
processed: 2026-07-06
duration: "5:42"
url: https://www.youtube.com/watch?v=hshDr2Af2RU
playlist: "[[Agents skills n8n]]"
type: tutorial
difficulty: beginner
use_case: [personal-finance-tracking]
tools: [Hledger, Git]
llms: []
protocols: []
transcript: true
tags: [youtube, ai-automation]
---

# Hledger: The Ultimate CLI Tool for Your Personal Finances

![thumbnail](https://i.ytimg.com/vi/hshDr2Af2RU/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=hshDr2Af2RU) | 📅 Uploaded [[uploaded/2025-11-05]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> A hands-on intro to Hledger, a free open-source command-line plain-text accounting tool. The video shows installing Hledger, creating a single `main.journal` text file, recording a double-entry transaction, and instantly generating balance sheet, register, and income statement reports — all from one human-readable file you fully own.

**Watch this if:** you want to ditch subscription budgeting apps (Mint, YNAB, etc.) for a private, future-proof, git-trackable plain-text ledger you control from the terminal.

## Key Takeaways
- Hledger is free, open-source, cross-platform (Mac/Windows/Linux), and installs in one command (`brew install hledger` on Mac).
- Your entire financial history lives in one plain-text file (e.g. `main.journal`) that's human-readable and editable in any text editor.
- Putting the finance folder under Git version control gives you a full backup/history ("time travel") of every change.
- The core concept is double-entry bookkeeping: every dollar leaving one account must appear in another, so the ledger always balances to zero and Hledger can auto-calculate the second amount.
- Colon-separated account names (e.g. `expenses:food:groceries`) create a hierarchy, letting you drill down from broad categories to specific ones in reports.
- Hledger generates instant balance sheet, running register, and income statement reports directly from the text file with no syncing or loading spinners.
- Bank CSV files can be imported directly into Hledger so you don't have to hand-enter every transaction (covered in a separate linked video/script).

## 🛠 Tools & Software
- [[topics/Hledger]] — the plain-text accounting CLI tool taught end-to-end: install, journal file setup, recording a transaction, and running balance/register/income reports.
- [[topics/Git]] — recommended for version-controlling the finance folder so every change creates a recoverable snapshot.

## 🤖 LLMs Mentioned
- None identified.

## 📡 Protocols & Standards
- None identified.

## ✅ Action Items
- Install Hledger for your OS and run `hledger --version` to confirm it works.
- Create a `finance/main.journal` file and put the folder under Git version control.
- Record a first double-entry transaction (e.g. a grocery purchase) using hierarchical account names like `expenses:food:groceries` and `assets:bank:checking`.
- Run Hledger's balance, register, and income-statement commands against your journal to see instant reports.
- Set the `LEDGER_FILE` (or equivalent shell config) so Hledger always finds your journal by default.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: ditching Mint/subscription apps for a plain text file; preview of the final balance sheet and reports.
- `0:55` — Installing Hledger (`brew install hledger` on Mac) and verifying with `hledger --version`.
- `1:35` — Creating a `finance` folder and `main.journal` plain-text file; noting it's human-readable and editable in any editor.
- `2:05` — Recommending Git version control on the finance folder for backup/history.
- `2:20` — Explaining double-entry bookkeeping: every dollar leaving one account appears in another.
- `2:55` — Recording a grocery transaction with hierarchical account names (`expenses:food:groceries`, `assets:bank:checking:TD`) and letting Hledger auto-balance the amount.
- `4:00` — Running reports: balance sheet, chronological register filtered by category, and an income statement.
- `5:00` — Mentioning CSV bank import as the next step to avoid manual entry, linked in a separate video.

## Transcript
<details>
<summary>Full transcript</summary>

The presenter deleted Mint three years ago, cancelled a YNAB subscription, and hasn't paid to track money since — the secret is a plain text file that gives more control, privacy, and power than any app, and will outlive every financial app on the market. The video promises to record a first transaction, run a first financial report, and explain why developers and accountants have used this system for decades. A preview shows the end result: an actual financial snapshot — every asset, liability, and expense calculated instantly from the plain text file, with instant filtered reports like "every food purchase this year" or an income statement.

First step: install Hledger — free, open-source, works on Mac, Windows, and Linux (install commands for each OS are in the description; Mac with Homebrew is just `brew install hledger`). Verify with `hledger --version`. Unlike subscription apps that lock data in proprietary formats and cloud servers, your entire financial life will live in a simple text file you own and control. Create a folder (e.g. "finance") and inside it a file called `main.journal` — this plain text file holds every transaction, human-readable, editable even in Notepad. A power move: put this folder under Git version control so every save creates a complete backup snapshot — "time travel" for your finances.

The one concept that makes the whole system work is double-entry bookkeeping: every dollar that leaves one account must show up in another — money can't vanish. It's the same system banks and Fortune 500 companies use. Demonstrating with a grocery trip: recording a transaction with description "Safeway Groceries," first account `expenses:food:groceries` (case-sensitive; the colons act like folders for money, enabling drill-down from all expenses to just food to just groceries), amount $50 CAD, second account `assets:bank:TD:checking` — Hledger automatically fills in the second amount because every transaction must balance to zero. The entry is written to the plain text file, human-readable forever. You could even hand-write entries without the CLI at all.

With a transaction logged, running reports shows the payoff: an instant balance sheet (every account balanced, snapshot of what you own and owe, no loading or syncing), a chronological register of every expense (filterable to just food expenses via the account hierarchy), and — the presenter's favorite — an income statement (income minus expenses) formatted like a real financial report, all from the plain text file, fully queryable in milliseconds with no ads or subscription tracking your spending.

One more setup step: Hledger doesn't automatically know where your journal is, so you add a config line to your shell config (Mac/Linux) or the Windows equivalent, then reload the config so Hledger always finds it.

Finally, acknowledging that hand-typing every transaction isn't realistic, the presenter notes there's a simple way to import bank CSV files directly into Hledger — one command and months of transactions appear in the journal — covered in a separate linked video with the exact import script.

</details>
