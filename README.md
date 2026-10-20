# youtube-catalog

Obsidian knowledge base built automatically from a YouTube playlist. Each new
video in the playlist becomes a rich vault page (metadata, extracted
tools/LLMs/protocols, timeline, full transcript), cross-linked through topic,
channel, and date hub pages plus a `Home.md` dashboard.

Powered by the **yt-catalog** Claude Code plugin (lives in the
`od-marketplace` repo at `plugins/yt-catalog/`).

## Layout

| Path | What |
|------|------|
| `YouTube_AI_Vault/` | The Obsidian vault — open this folder in Obsidian |
| `YouTube_AI_Vault/videos/` | One page per video |
| `YouTube_AI_Vault/topics/`, `channels/`, `created/`, `uploaded/` | Auto-maintained hub pages |
| `YouTube_AI_Vault/Home.md` | Dashboard — recently added, stats, live library |
| `YouTube_AI_Vault/Library.base` | Obsidian Bases live-query views over the vault |
| `.yt-catalog.json` | Plugin config (see below) |
| `AI Automate play list/` | Old vault (pre-rename) — superseded by `YouTube_AI_Vault` |
| `docs/` | Planning docs/specs from development sessions |

## Config — `.yt-catalog.json`

Key fields:

- `vault_path` — where pages are written (`YouTube_AI_Vault`)
- `default_playlist` — playlist processed when no argument given ("Agents skills n8n")
- `chrome_profile` — dedicated Chrome automation profile holding the YouTube
  session for private-playlist access (`~/.cache/chrome-devtools-mcp/chrome-profile`).
  Never the personal `~/.config/google-chrome` profile.
- `vpn` — `"piactl"` to force fetching through PIA VPN, `"off"` to fetch bare
- `skip_processed` — `true`: already-cataloged videos are never refetched, so
  interrupted runs resume exactly where they stopped
- `venv_path` — Python venv used by the fetch scripts (`~/.yt-catalog/venv`)

## Commands (run inside this directory)

- `/yt-catalog:process [playlist]` — catalog new videos; updates hubs + Home.md
- `/yt-catalog:login` — refresh the YouTube session in the automation profile
  (needed when runs fail with HTTP 401)
- `/yt-catalog:setup` — first-time setup wizard

## Nightly cron

Runs at **23:00** daily:

```
cd ~/Workspace/youtube-catalog && claude -p "/yt-catalog:process" >> ~/.yt-catalog/cron.log
```

(wrapped with `===== yt-catalog run start/end <timestamp> =====` marker lines
so each run in the log is dated and delimited).

## Logs

Two logs, two jobs:

### `~/.yt-catalog/history.log` — permanent audit log

One timestamped row per event, appended **the moment it happens** (crash-safe;
written by every run, cron or manual):

```
2026-07-13 08:45:43 | added | LJI7FafIDg4 | This Claude Code Skill Creates Claude Code Skills For You
2026-07-13 23:00:35 | run-start | Agents skills n8n | total 185, new 2, skipped 183
2026-07-13 23:07:30 | run-end | 2 added, 0 failed
```

Events: `run-start`, `added`, `failed` (with reason), `run-end` (including
aborts). Quick queries:

```sh
grep '| added |' ~/.yt-catalog/history.log | tail    # last videos added, with dates
tail -f ~/.yt-catalog/history.log                    # watch a run live
```

### `~/.yt-catalog/cron.log` — raw run output

Full session output of each cron run, bracketed by dated start/end markers.
The same per-video rows from history.log are tee'd in live, so
`tail -f ~/.yt-catalog/cron.log` shows progress mid-run — without them the
log would be silent until the run ends (`claude -p` prints its report only at
completion). Safe to truncate anytime; history.log is the permanent record.

## Troubleshooting

- **HTTP 401 on playlist fetch** — YouTube session expired; run `/yt-catalog:login`.
- **fetch_video exit 5 / HTTP 429** — YouTube has rate-banned transcript
  requests for this IP (bursts trigger it; ban lasts a few hours). Runs space
  fetches 10 s apart and abort after 3 consecutive 429s. Re-run later —
  `skip_processed` resumes cleanly. Fetching over VPN (`"vpn": "piactl"`)
  avoids burning the home IP.
- **Run died mid-way** — check `history.log`: every page written before the
  crash has an `added` row; the next run picks up the rest automatically.
