# yt-catalog — Claude Code Plugin Design

**Date:** 2026-07-05
**Status:** Approved design, pending implementation plan
**Author:** Jason + Claude

## Purpose

A Claude Code plugin that processes a designated YouTube playlist (including
private playlists) into an interconnected Obsidian knowledge base: one rich,
searchable page per video, plus auto-maintained hub pages for topics, channels,
and dates, so the user can narrow videos down by tool, LLM, protocol,
difficulty, or use-case.

## Decisions Made

| Decision | Choice |
|---|---|
| Platform | Claude Code plugin (markdown commands + skills + Python helper scripts) |
| Development location | Directly in `od-marketplace/plugins/yt-catalog/` — no move step later |
| Marketplace | `https://github.com/jazzjazzy/od-marketplace` (private, personal) |
| Playlist access | `yt-dlp --cookies-from-browser "chrome:<automation profile>"` — headless, primary |
| Chrome profile | Dedicated automation profile `~/.cache/chrome-devtools-mcp/chrome-profile` — personal profile (`~/.config/google-chrome`) NEVER touched |
| Login refresh | `/yt-catalog:login` opens browser with automation profile to re-auth YouTube when cookies stale |
| Entity extraction | Claude in-session by default; local LLM (LMS server) as configurable option (`extractor: claude \| local`) |
| Output vault | `AI Automate play list/` folder in youtube-catalog repo (it IS an Obsidian vault) |
| Transcripts | Inline in video page, collapsed in `<details>` |
| First run | Missing config triggers interactive setup wizard from any command |

## Architecture (Approach A — Hybrid Agentic)

Python scripts do deterministic work; Claude skills do intelligence.

```
od-marketplace/plugins/yt-catalog/
├── .claude-plugin/plugin.json      # name, version, description
├── commands/
│   ├── setup.md                    # /yt-catalog:setup — dependency check, venv create,
│   │                               #   config wizard, optional login step
│   ├── process.md                  # /yt-catalog:process [playlist] — main pipeline
│   └── login.md                    # /yt-catalog:login — open automation-profile browser
│                                   #   → youtube.com → refresh session cookies
├── skills/
│   ├── video-page/SKILL.md         # page template + extraction rules
│   └── hub-pages/SKILL.md          # topic/channel/date/Home page generation rules
├── scripts/
│   ├── fetch_playlist.py           # playlist → video list JSON (yt-dlp + profile cookies)
│   ├── fetch_video.py              # one video ID → metadata + transcript JSON
│   └── extract_local.py            # optional entity extraction via local LLM
└── config.example.json
```

### Data flow — `/yt-catalog:process`

1. Load config (`.yt-catalog.json`); missing → run setup wizard first, then continue.
2. `fetch_playlist.py` → full video list for playlist (private OK via profile cookies).
3. Diff against vault: skip video IDs already present in existing page frontmatter
   (`skip_processed: true`).
4. Per new video: `fetch_video.py` → metadata (yt-dlp) + transcript
   (youtube-transcript-api) as JSON.
5. Extraction (per `extractor` config):
   - `claude`: Claude reads transcript, extracts entities, writes page directly.
   - `local`: `extract_local.py` calls LMS server (OpenAI-compatible API), Claude
     validates/formats the result.
6. `video-page` skill writes the video page.
7. `hub-pages` skill updates `topics/`, `channels/`, `created/`, `uploaded/`,
   `Home.md` — creating hub pages that don't exist, appending links to ones that do.
8. Report: N processed, M skipped, hub pages touched, any failures.

### Error handling

- **Stale cookies / auth failure:** fetch scripts detect yt-dlp auth errors →
  instruct user to run `/yt-catalog:login`; process resumes after.
- **No transcript available** (disabled/none): page still created; Transcript
  section notes "No transcript available"; extraction falls back to
  title + description metadata only, flagged `transcript: false` in frontmatter.
- **Video removed/private-to-uploader:** skipped with note in run report.
- **Partial runs:** each video is atomic (page written fully or not at all);
  re-running process picks up where it left off via the skip-processed diff.

## Configuration

`.yt-catalog.json` (per-vault; `config.example.json` ships in plugin):

```json
{
  "vault_path": "/home/jason/Workspace/youtube-catalog/AI Automate play list",
  "chrome_profile": "~/.cache/chrome-devtools-mcp/chrome-profile",
  "default_playlist": "Agent Skills n8n",
  "extractor": "claude",
  "local_llm": {
    "base_url": "http://192.168.1.211:1234/v1",
    "model": "google/gemma-4-26b-a4b"
  },
  "venv_path": "~/.yt-catalog/venv",
  "transcript_languages": ["en"],
  "skip_processed": true
}
```

**First-run wizard:** any command finding no config asks: vault path, default
playlist, playlist private/public, extractor choice, which Chrome profile
(scans for candidates and lists them), then verifies deps (Chrome present,
creates venv, installs `yt-dlp` + `youtube-transcript-api`), offers login step,
writes config, continues with the original command.

**Portability:** nothing hardcoded. New machine = install plugin from
marketplace, run any command, answer wizard. Private playlists additionally
need the one-time `/yt-catalog:login`. Public playlists need zero login.

## Vault Layout

```
AI Automate play list/           (Obsidian vault)
├── Home.md                      # dashboard MOC: recently added, by topic,
│                                #   by difficulty, by use-case
├── videos/                      # one page per video
├── topics/                      # hub page per entity (tools, LLMs, protocols)
├── channels/                    # hub page per channel
├── created/                     # one page per processing date
└── uploaded/                    # one page per upload date
```

Date pages replace the previous `Upload Calendar.md` / `Creation Calendar.md`
files.

## Video Page Template

```markdown
---
title: "Video Title"
video_id: abc123
channel: "[[channels/Channel Name]]"
uploaded: 2026-06-12
processed: 2026-07-05
duration: "14:32"
url: https://youtube.com/watch?v=abc123
playlist: "[[Agent Skills n8n]]"
type: tutorial            # tutorial | build-along | news | review | comparison
difficulty: intermediate  # beginner | intermediate | advanced
use_case: [email-automation, rag]
tools: [n8n, docker]
llms: [claude, gpt-4o]
protocols: [mcp, webhooks]
transcript: true
tags: [youtube, ai-automation]
---

# Video Title

![thumbnail](https://img.youtube.com/vi/abc123/maxresdefault.jpg)
▶️ [Watch](https://youtube.com/watch?v=abc123) | 📅 Uploaded [[uploaded/2026-06-12]] | 🗓️ Processed [[created/2026-07-05]]

## TL;DR
> 2-3 sentence summary — what the video teaches, who it's for.

**Watch this if:** one-line relevance test.

## Key Takeaways
- 3-7 bullets, actual substance.

## 🛠 Tools & Software
- [[topics/n8n]] — one line: how it's used in this video.

## 🤖 LLMs Mentioned
- [[topics/Claude]] — context of mention (compared? recommended? demoed?).

## 📡 Protocols & Standards
- [[topics/MCP]] — how it features.

## ✅ Action Items
- Concrete things to try yourself, drawn from the video.

## 🔗 Related Videos
- Auto-links to other videos sharing 2+ topics.

## Timeline
- `03:12` — timestamped chapter/moment descriptions from transcript.

## Transcript
<details>
<summary>Full transcript</summary>
...collapsed transcript text...
</details>
```

Entities appear BOTH in frontmatter lists (machine-queryable — Obsidian
search/Dataview can answer "beginner videos using n8n + MCP but not Docker")
AND as body wikilinks (graph view + backlinks).

## Hub Pages

- **`topics/<Entity>.md`** — entity description, official link, `aliases:`
  frontmatter (canonicalization: "GPT4o" → "GPT-4o", "model context protocol"
  → "MCP"), table of videos mentioning it, related topics.
- **`channels/<Name>.md`** — channel link, list of cataloged videos.
- **`created/<date>.md`**, **`uploaded/<date>.md`** — videos for that date.
- **`Home.md`** — regenerated each run: recently added, topic index,
  by-difficulty and by-use-case tables.

Alias normalization is mandatory in the extraction rules — without it the
topic web fragments and cross-linking dies.

## Extraction Rules (video-page skill, summary)

From transcript + metadata, extract:
- `type`, `difficulty`, `use_case` (problem-first vocabulary)
- Tools & software, LLMs, protocols & standards — canonicalized against a
  shipped alias table (extendable per-vault)
- TL;DR, "Watch this if", key takeaways, action items, timeline
- Related videos: computed by ≥2 shared topics with existing pages

## Testing Strategy

- Scripts: unit-testable pure functions (playlist JSON parsing, diff logic,
  frontmatter read/write) + a live smoke test against one known public video.
- End-to-end: run `process` against a small public test playlist first, then
  against 'Agent Skills n8n'.
- Wizard: delete config, run command, verify full question flow + config write.
- Login flow: verified manually (needs real browser session).

## Publish Steps (after user is happy)

1. Add entry to `od-marketplace/.claude-plugin/marketplace.json`.
2. Commit + push od-marketplace to GitHub (with user approval).
3. Install locally via the marketplace; verify commands appear.

## Out of Scope (YAGNI)

- Auto-cron scheduling (user can add later; `extractor: local` keeps the door open)
- Watching multiple playlists in one run
- Editing/updating already-processed pages when videos change
- Obsidian plugin / Dataview dependency (pages work with vanilla Obsidian;
  Dataview enhances but is not required)
