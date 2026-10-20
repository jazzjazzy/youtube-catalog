# yt-catalog Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** A Claude Code plugin that turns a designated (possibly private) YouTube playlist into an interconnected Obsidian knowledge base with per-video pages and auto-maintained topic/channel/date hub pages.

**Architecture:** Hybrid agentic — stdlib-only pure helpers (`ytlib.py`) unit-tested with `unittest`; thin CLI scripts running under a dedicated venv do deterministic fetching via yt-dlp + youtube-transcript-api with cookies read from a dedicated Chrome automation profile; Claude skills do all intelligence (entity extraction, canonicalization, page + hub generation); markdown commands orchestrate.

**Tech Stack:** Python 3 (stdlib for logic, `yt-dlp` + `youtube-transcript-api` in runtime venv), Claude Code plugin format (commands/skills), Obsidian-flavored markdown output.

**Spec:** `/home/jason/Workspace/youtube-catalog/docs/superpowers/specs/2026-07-05-yt-catalog-plugin-design.md`

## Global Constraints

- Build location: `/home/jason/Workspace/od-marketplace/plugins/yt-catalog/` (call it `$PLUGIN` below).
- Work on branch `feature/yt-catalog` in od-marketplace (user's rule: feature branches never merge straight to main).
- **User rule: no commits without approval.** Get explicit approval for the plan's per-task commits before the first one; if granted once for this plan, per-task commits proceed.
- Personal Chrome profile (`~/.config/google-chrome`) must NEVER be read. Only the configured automation profile (default `~/.cache/chrome-devtools-mcp/chrome-profile`).
- `ytlib.py` and tests are stdlib-only — no third-party imports, so tests run under system `python3`.
- Scripts that need yt-dlp/transcript-api run under the venv from config `venv_path` (default `~/.yt-catalog/venv`).
- Config file name: `.yt-catalog.json`, discovered by walking up from CWD.
- Vault output dirs: `videos/`, `topics/`, `channels/`, `created/`, `uploaded/`, `Home.md`.
- Frontmatter keys (exact): `title, video_id, channel, uploaded, processed, duration, url, playlist, type, difficulty, use_case, tools, llms, protocols, transcript, tags`.
- `type` vocabulary: `tutorial | build-along | news | review | comparison`. `difficulty`: `beginner | intermediate | advanced`.
- All command files reference scripts via `${CLAUDE_PLUGIN_ROOT}/scripts/...` (matches voicebox pattern).

---

### Task 1: Branch, scaffold, dev venv

**Files:**
- Create: `$PLUGIN/.claude-plugin/plugin.json`
- Create: `$PLUGIN/config.example.json`
- Create: `$PLUGIN/skills/video-page/aliases.json`
- Create: `$PLUGIN/README.md`

**Interfaces:**
- Produces: plugin identity (`yt-catalog`), example config consumed by setup command (Task 10), starter alias table consumed by skills (Task 8) and `extract_local.py` (Task 7), dev venv at `~/.yt-catalog/venv` used by Tasks 5–6 smoke tests.

- [ ] **Step 1: Create branch in od-marketplace**

```bash
cd /home/jason/Workspace/od-marketplace && git checkout -b feature/yt-catalog
```

Expected: `Switched to a new branch 'feature/yt-catalog'`

- [ ] **Step 2: Create directory skeleton**

```bash
mkdir -p /home/jason/Workspace/od-marketplace/plugins/yt-catalog/{.claude-plugin,commands,skills/video-page,skills/hub-pages,scripts,tests}
```

- [ ] **Step 3: Write `plugin.json`**

`$PLUGIN/.claude-plugin/plugin.json`:

```json
{
  "name": "yt-catalog",
  "description": "Catalogs a YouTube playlist (private playlists supported via a dedicated Chrome automation profile) into an interconnected Obsidian knowledge base: rich per-video pages plus auto-maintained topic, channel, and date hub pages. Commands: /yt-catalog:setup, /yt-catalog:process, /yt-catalog:login.",
  "version": "0.1.0",
  "author": {
    "name": "jason"
  },
  "license": "MIT",
  "keywords": ["youtube", "obsidian", "playlist", "transcripts", "knowledge-base"]
}
```

- [ ] **Step 4: Write `config.example.json`**

`$PLUGIN/config.example.json`:

```json
{
  "vault_path": "/absolute/path/to/your/obsidian/vault",
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

- [ ] **Step 5: Write starter alias table**

`$PLUGIN/skills/video-page/aliases.json` — canonical name → accepted variants (case-insensitive matching; skills may extend per-vault):

```json
{
  "tools": {
    "n8n": ["n8n.io", "nodemation"],
    "Docker": ["docker desktop", "docker compose", "docker-compose"],
    "Obsidian": ["obsidian.md"],
    "Zapier": [],
    "Make": ["make.com", "integromat"],
    "Supabase": [],
    "Airtable": [],
    "LM Studio": ["lmstudio", "lm-studio"],
    "Ollama": [],
    "VS Code": ["vscode", "visual studio code"],
    "Claude Code": ["claude-code", "claudecode"],
    "OpenCode": ["open code"],
    "Cursor": ["cursor ai", "cursor ide"],
    "GitHub": ["github.com"],
    "Notion": [],
    "Pinecone": [],
    "Qdrant": [],
    "LangChain": ["lang chain"],
    "LlamaIndex": ["llama index", "llama-index"]
  },
  "llms": {
    "Claude": ["anthropic claude", "claude ai"],
    "Claude Opus": ["opus 4", "claude opus 4"],
    "Claude Sonnet": ["sonnet 4", "claude sonnet 4"],
    "GPT-4o": ["gpt4o", "gpt 4o"],
    "GPT-5": ["gpt5", "gpt 5"],
    "o3": ["openai o3"],
    "Gemini": ["google gemini", "gemini pro", "gemini flash"],
    "Llama": ["llama 3", "llama 4", "meta llama"],
    "Mistral": ["mistral ai"],
    "Qwen": ["qwen3", "qwen 3"],
    "DeepSeek": ["deepseek r1", "deep seek"],
    "Gemma": ["gemma 3", "gemma 4"]
  },
  "protocols": {
    "MCP": ["model context protocol"],
    "webhooks": ["web hooks", "webhook"],
    "REST": ["rest api", "restful"],
    "GraphQL": [],
    "OAuth": ["oauth2", "oauth 2.0"],
    "JSON-RPC": ["jsonrpc", "json rpc"],
    "SSE": ["server-sent events", "server sent events"],
    "WebSocket": ["websockets", "web socket"],
    "A2A": ["agent2agent", "agent to agent protocol"],
    "RAG": ["retrieval augmented generation", "retrieval-augmented generation"]
  }
}
```

- [ ] **Step 6: Write `README.md`**

`$PLUGIN/README.md`:

```markdown
# yt-catalog

Catalogs a YouTube playlist (private playlists supported) into an
interconnected Obsidian knowledge base.

## Commands

| Command | What it does |
|---|---|
| `/yt-catalog:setup` | Dependency check, venv creation, interactive config wizard |
| `/yt-catalog:process [playlist]` | Fetch playlist, create a page per new video, update hub pages |
| `/yt-catalog:login` | Open the automation-profile browser to refresh the YouTube session |

## How it works

Python scripts (running in a dedicated venv) fetch playlist listings,
metadata, and transcripts via yt-dlp + youtube-transcript-api, reading
cookies from a **dedicated Chrome automation profile** — your personal
browser profile is never touched. Claude then extracts tools, LLMs,
protocols, difficulty, and use-cases from each transcript and writes
richly cross-linked Obsidian pages: `videos/`, `topics/`, `channels/`,
`created/`, `uploaded/`, and a `Home.md` dashboard.

Configuration lives in `.yt-catalog.json` next to your vault. Any command
run without a config triggers the setup wizard automatically.

## New machine setup

1. Install plugin from the OD-marketplace.
2. Run `/yt-catalog:process` — the wizard asks vault path, playlist,
   extractor (claude | local LLM), and Chrome profile, then installs deps.
3. Private playlist? Run `/yt-catalog:login` once when prompted.
```

- [ ] **Step 7: Create runtime/dev venv with dependencies**

```bash
python3 -m venv ~/.yt-catalog/venv && ~/.yt-catalog/venv/bin/pip install --quiet yt-dlp youtube-transcript-api && ~/.yt-catalog/venv/bin/python -c "import yt_dlp, youtube_transcript_api; print('deps ok')"
```

Expected: `deps ok`

- [ ] **Step 8: Commit** (only after user approved plan-wide commits)

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): scaffold plugin — manifest, example config, alias table, README"
```

---

### Task 2: ytlib core — config, filenames, vault scanning (TDD)

**Files:**
- Create: `$PLUGIN/scripts/ytlib.py`
- Test: `$PLUGIN/tests/test_ytlib_core.py`

**Interfaces:**
- Produces (consumed by Tasks 5–7 scripts):
  - `find_config(start_dir: str) -> str | None`
  - `load_config(path: str) -> dict` (defaults applied, `~` expanded in `vault_path`, `chrome_profile`, `venv_path`)
  - `safe_filename(title: str) -> str`
  - `extract_video_id_from_md(text: str) -> str | None`
  - `scan_vault_video_ids(vault_path: str) -> set[str]`
  - Constants: `CONFIG_NAME = ".yt-catalog.json"`, `DEFAULTS` dict

- [ ] **Step 1: Write the failing tests**

`$PLUGIN/tests/test_ytlib_core.py`:

```python
import json
import os
import sys
import tempfile
import unittest

sys.path.insert(0, os.path.join(os.path.dirname(__file__), "..", "scripts"))
import ytlib


class TestFindConfig(unittest.TestCase):
    def test_finds_config_in_parent_dir(self):
        with tempfile.TemporaryDirectory() as root:
            cfg_path = os.path.join(root, ytlib.CONFIG_NAME)
            with open(cfg_path, "w") as f:
                f.write("{}")
            child = os.path.join(root, "a", "b")
            os.makedirs(child)
            self.assertEqual(ytlib.find_config(child), cfg_path)

    def test_returns_none_when_absent(self):
        with tempfile.TemporaryDirectory() as root:
            self.assertIsNone(ytlib.find_config(root))


class TestLoadConfig(unittest.TestCase):
    def test_applies_defaults_and_expands_tilde(self):
        with tempfile.TemporaryDirectory() as root:
            cfg_path = os.path.join(root, ytlib.CONFIG_NAME)
            with open(cfg_path, "w") as f:
                json.dump({"vault_path": "~/vault", "chrome_profile": "~/prof"}, f)
            cfg = ytlib.load_config(cfg_path)
            self.assertEqual(cfg["extractor"], "claude")
            self.assertTrue(cfg["skip_processed"])
            self.assertEqual(cfg["transcript_languages"], ["en"])
            self.assertFalse(cfg["vault_path"].startswith("~"))
            self.assertFalse(cfg["venv_path"].startswith("~"))

    def test_explicit_values_beat_defaults(self):
        with tempfile.TemporaryDirectory() as root:
            cfg_path = os.path.join(root, ytlib.CONFIG_NAME)
            with open(cfg_path, "w") as f:
                json.dump({"extractor": "local"}, f)
            self.assertEqual(ytlib.load_config(cfg_path)["extractor"], "local")


class TestSafeFilename(unittest.TestCase):
    def test_strips_illegal_chars_keeps_readables(self):
        self.assertEqual(
            ytlib.safe_filename("n8n + MCP: The *Ultimate* Guide (2026)!?"),
            "n8n  MCP The Ultimate Guide (2026)".replace("  ", " "),
        )

    def test_collapses_whitespace(self):
        self.assertEqual(ytlib.safe_filename("a   b\tc"), "a b c")

    def test_empty_becomes_untitled(self):
        self.assertEqual(ytlib.safe_filename("///"), "untitled")


class TestExtractVideoId(unittest.TestCase):
    def test_reads_id_from_frontmatter(self):
        page = "---\ntitle: X\nvideo_id: dQw4w9WgXcQ\n---\n\n# X\n"
        self.assertEqual(ytlib.extract_video_id_from_md(page), "dQw4w9WgXcQ")

    def test_quoted_id(self):
        page = '---\nvideo_id: "abc-DEF_123"\n---\nbody'
        self.assertEqual(ytlib.extract_video_id_from_md(page), "abc-DEF_123")

    def test_no_frontmatter_returns_none(self):
        self.assertIsNone(ytlib.extract_video_id_from_md("# just a heading\nvideo_id: nope"))

    def test_id_only_in_body_ignored(self):
        page = "---\ntitle: X\n---\nvideo_id: dQw4w9WgXcQ\n"
        self.assertIsNone(ytlib.extract_video_id_from_md(page))


class TestScanVault(unittest.TestCase):
    def test_collects_ids_from_videos_dir(self):
        with tempfile.TemporaryDirectory() as vault:
            vids = os.path.join(vault, "videos")
            os.makedirs(vids)
            with open(os.path.join(vids, "one.md"), "w") as f:
                f.write("---\nvideo_id: aaa111bbb22\n---\n")
            with open(os.path.join(vids, "two.md"), "w") as f:
                f.write("---\nvideo_id: ccc333ddd44\n---\n")
            with open(os.path.join(vids, "notes.txt"), "w") as f:
                f.write("---\nvideo_id: should-ignore\n---\n")
            self.assertEqual(
                ytlib.scan_vault_video_ids(vault), {"aaa111bbb22", "ccc333ddd44"}
            )

    def test_missing_videos_dir_gives_empty_set(self):
        with tempfile.TemporaryDirectory() as vault:
            self.assertEqual(ytlib.scan_vault_video_ids(vault), set())


if __name__ == "__main__":
    unittest.main()
```

- [ ] **Step 2: Run tests to verify they fail**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -p 'test_ytlib_core.py' -v
```

Expected: FAIL / ERROR with `ModuleNotFoundError: No module named 'ytlib'`

- [ ] **Step 3: Write `ytlib.py` core**

`$PLUGIN/scripts/ytlib.py`:

```python
"""Pure helper functions for the yt-catalog plugin scripts.

Stdlib-only so unit tests run under any python3 (no venv required).
"""
import json
import os
import re

CONFIG_NAME = ".yt-catalog.json"

DEFAULTS = {
    "extractor": "claude",
    "venv_path": "~/.yt-catalog/venv",
    "transcript_languages": ["en"],
    "skip_processed": True,
}


def find_config(start_dir):
    """Walk up from start_dir looking for .yt-catalog.json. Path or None."""
    d = os.path.abspath(start_dir)
    while True:
        candidate = os.path.join(d, CONFIG_NAME)
        if os.path.isfile(candidate):
            return candidate
        parent = os.path.dirname(d)
        if parent == d:
            return None
        d = parent


def load_config(path):
    """Load config JSON, apply DEFAULTS, expand ~ in path fields."""
    with open(path, "r", encoding="utf-8") as f:
        cfg = json.load(f)
    merged = {**DEFAULTS, **cfg}
    for key in ("vault_path", "chrome_profile", "venv_path"):
        if merged.get(key):
            merged[key] = os.path.expanduser(merged[key])
    return merged


def safe_filename(title):
    """Filesystem-safe filename (no extension) from a video title."""
    cleaned = "".join(c for c in title if c.isalnum() or c in " -_'&,()").strip()
    cleaned = re.sub(r"\s+", " ", cleaned)
    return cleaned or "untitled"


_VIDEO_ID_RE = re.compile(r"^video_id:\s*[\"']?([\w-]{6,})[\"']?\s*$", re.MULTILINE)


def extract_video_id_from_md(text):
    """Pull video_id out of a page's YAML frontmatter. None if absent."""
    if not text.startswith("---"):
        return None
    end = text.find("\n---", 3)
    if end == -1:
        return None
    m = _VIDEO_ID_RE.search(text[:end])
    return m.group(1) if m else None


def scan_vault_video_ids(vault_path):
    """Set of video_ids already cataloged in <vault>/videos/*.md."""
    ids = set()
    videos_dir = os.path.join(vault_path, "videos")
    if not os.path.isdir(videos_dir):
        return ids
    for name in os.listdir(videos_dir):
        if not name.endswith(".md"):
            continue
        try:
            with open(os.path.join(videos_dir, name), "r", encoding="utf-8") as f:
                vid = extract_video_id_from_md(f.read())
            if vid:
                ids.add(vid)
        except OSError:
            continue
    return ids
```

- [ ] **Step 4: Run tests to verify they pass**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -p 'test_ytlib_core.py' -v
```

Expected: `OK` — all tests pass. If `test_strips_illegal_chars_keeps_readables` fails on exact string, adjust the ASSERTION to the actual (correct) output of the implementation — the intent is: alnum, space, `-_'&,()` kept, everything else dropped, whitespace collapsed.

- [ ] **Step 5: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): ytlib core — config discovery/loading, safe filenames, vault scanning"
```

---

### Task 3: ytlib parsing — playlist refs, subtitles, durations (TDD)

**Files:**
- Modify: `$PLUGIN/scripts/ytlib.py` (append)
- Test: `$PLUGIN/tests/test_ytlib_parsing.py`

**Interfaces:**
- Produces (consumed by Tasks 5–6):
  - `playlist_ref_to_url(ref: str) -> str | None` (None = display name, needs feed lookup)
  - `match_playlist_by_title(feed_json: dict, name: str) -> str | None` (playlist URL)
  - `parse_json3_subs(text: str) -> list[dict]` (`{start: float, duration: float, text: str}`)
  - `format_duration(seconds) -> str` (`"M:SS"` / `"H:MM:SS"`)

- [ ] **Step 1: Write the failing tests**

`$PLUGIN/tests/test_ytlib_parsing.py`:

```python
import json
import os
import sys
import unittest

sys.path.insert(0, os.path.join(os.path.dirname(__file__), "..", "scripts"))
import ytlib


class TestPlaylistRef(unittest.TestCase):
    def test_url_passes_through(self):
        url = "https://www.youtube.com/playlist?list=PLabc123"
        self.assertEqual(ytlib.playlist_ref_to_url(url), url)

    def test_playlist_id_becomes_url(self):
        self.assertEqual(
            ytlib.playlist_ref_to_url("PLabc-123_XY"),
            "https://www.youtube.com/playlist?list=PLabc-123_XY",
        )

    def test_display_name_returns_none(self):
        self.assertIsNone(ytlib.playlist_ref_to_url("Agent Skills n8n"))


class TestMatchPlaylistByTitle(unittest.TestCase):
    FEED = {
        "entries": [
            {"title": "Agent Skills n8n", "url": "https://www.youtube.com/playlist?list=PLagents"},
            {"title": "Homelab", "url": "https://www.youtube.com/playlist?list=PLhome"},
        ]
    }

    def test_case_insensitive_match(self):
        self.assertEqual(
            ytlib.match_playlist_by_title(self.FEED, "agent skills N8N"),
            "https://www.youtube.com/playlist?list=PLagents",
        )

    def test_no_match_returns_none(self):
        self.assertIsNone(ytlib.match_playlist_by_title(self.FEED, "Cooking"))

    def test_empty_feed(self):
        self.assertIsNone(ytlib.match_playlist_by_title({"entries": None}, "x"))


class TestParseJson3Subs(unittest.TestCase):
    def test_parses_events_to_snippets(self):
        payload = json.dumps({
            "events": [
                {"tStartMs": 0, "dDurationMs": 2000,
                 "segs": [{"utf8": "hello "}, {"utf8": "world"}]},
                {"tStartMs": 2000, "dDurationMs": 1500, "segs": [{"utf8": "\n"}]},
                {"tStartMs": 3500, "dDurationMs": 1000, "segs": [{"utf8": "again"}]},
            ]
        })
        snippets = ytlib.parse_json3_subs(payload)
        self.assertEqual(len(snippets), 2)  # newline-only event dropped
        self.assertEqual(snippets[0], {"start": 0.0, "duration": 2.0, "text": "hello world"})
        self.assertEqual(snippets[1]["text"], "again")

    def test_no_events_key(self):
        self.assertEqual(ytlib.parse_json3_subs("{}"), [])


class TestFormatDuration(unittest.TestCase):
    def test_minutes_seconds(self):
        self.assertEqual(ytlib.format_duration(872), "14:32")

    def test_hours(self):
        self.assertEqual(ytlib.format_duration(3661), "1:01:01")

    def test_none_is_zero(self):
        self.assertEqual(ytlib.format_duration(None), "0:00")


if __name__ == "__main__":
    unittest.main()
```

- [ ] **Step 2: Run tests to verify they fail**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -p 'test_ytlib_parsing.py' -v
```

Expected: ERROR with `AttributeError: module 'ytlib' has no attribute 'playlist_ref_to_url'`

- [ ] **Step 3: Append implementations to `ytlib.py`**

```python
_URL_RE = re.compile(r"^https?://")
_PLAYLIST_ID_RE = re.compile(r"^(PL|LL|WL|UU|OLAK)[\w-]*$")


def playlist_ref_to_url(ref):
    """URL for a playlist reference; None when ref is a display name."""
    ref = ref.strip()
    if _URL_RE.match(ref):
        return ref
    if _PLAYLIST_ID_RE.match(ref):
        return f"https://www.youtube.com/playlist?list={ref}"
    return None


def match_playlist_by_title(feed_json, name):
    """Playlist URL from a yt-dlp feed/playlists dump, matched by title."""
    want = name.strip().lower()
    for entry in feed_json.get("entries") or []:
        title = (entry.get("title") or "").strip().lower()
        if title == want:
            return entry.get("url") or entry.get("webpage_url")
    return None


def parse_json3_subs(text):
    """yt-dlp json3 subtitle payload -> [{start, duration, text}]."""
    data = json.loads(text)
    out = []
    for ev in data.get("events") or []:
        segs = ev.get("segs") or []
        snippet = "".join(s.get("utf8", "") for s in segs).replace("\n", " ").strip()
        if not snippet:
            continue
        out.append({
            "start": ev.get("tStartMs", 0) / 1000.0,
            "duration": ev.get("dDurationMs", 0) / 1000.0,
            "text": snippet,
        })
    return out


def format_duration(seconds):
    """Seconds -> 'M:SS' or 'H:MM:SS'."""
    seconds = int(seconds or 0)
    h, rem = divmod(seconds, 3600)
    m, s = divmod(rem, 60)
    return f"{h}:{m:02d}:{s:02d}" if h else f"{m}:{s:02d}"
```

- [ ] **Step 4: Run the full test suite**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -v
```

Expected: `OK` — both test modules pass.

- [ ] **Step 5: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): ytlib parsing — playlist refs, json3 subtitles, durations"
```

---

### Task 4: ytlib extraction prompt/response helpers (TDD)

**Files:**
- Modify: `$PLUGIN/scripts/ytlib.py` (append)
- Test: `$PLUGIN/tests/test_ytlib_extraction.py`

**Interfaces:**
- Produces (consumed by Task 7 `extract_local.py`):
  - `build_extraction_prompt(video: dict, aliases: dict) -> str` — `video` is Task 6's output shape `{metadata: {...}, transcript: [{start,duration,text}]}`
  - `parse_extraction_response(text: str) -> dict` — tolerant of ``` fences and prose around JSON; raises `ValueError` if no JSON object found

- [ ] **Step 1: Write the failing tests**

`$PLUGIN/tests/test_ytlib_extraction.py`:

```python
import os
import sys
import unittest

sys.path.insert(0, os.path.join(os.path.dirname(__file__), "..", "scripts"))
import ytlib

VIDEO = {
    "metadata": {"id": "abc12345678", "title": "Build agents with n8n",
                 "channel": "Some Channel", "description": "We use MCP."},
    "transcript": [{"start": 0.0, "duration": 2.0, "text": "today we use n8n and claude"}],
}
ALIASES = {"tools": {"n8n": []}, "llms": {"Claude": []}, "protocols": {"MCP": ["model context protocol"]}}


class TestBuildExtractionPrompt(unittest.TestCase):
    def test_includes_transcript_title_and_canonical_names(self):
        prompt = ytlib.build_extraction_prompt(VIDEO, ALIASES)
        self.assertIn("Build agents with n8n", prompt)
        self.assertIn("today we use n8n and claude", prompt)
        self.assertIn("MCP", prompt)          # canonical vocab listed
        self.assertIn('"tools"', prompt)      # required output keys named
        self.assertIn('"difficulty"', prompt)

    def test_transcript_truncated_to_limit(self):
        long_video = {
            "metadata": VIDEO["metadata"],
            "transcript": [{"start": 0, "duration": 1, "text": "word " * 20000}],
        }
        prompt = ytlib.build_extraction_prompt(long_video, ALIASES)
        self.assertLess(len(prompt), 60000)


class TestParseExtractionResponse(unittest.TestCase):
    def test_plain_json(self):
        self.assertEqual(ytlib.parse_extraction_response('{"tools": ["n8n"]}'),
                         {"tools": ["n8n"]})

    def test_fenced_json_with_prose(self):
        text = 'Here you go:\n```json\n{"llms": ["Claude"]}\n```\nDone.'
        self.assertEqual(ytlib.parse_extraction_response(text), {"llms": ["Claude"]})

    def test_no_json_raises(self):
        with self.assertRaises(ValueError):
            ytlib.parse_extraction_response("sorry, no can do")


if __name__ == "__main__":
    unittest.main()
```

- [ ] **Step 2: Run tests to verify they fail**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -p 'test_ytlib_extraction.py' -v
```

Expected: ERROR with `AttributeError: ... 'build_extraction_prompt'`

- [ ] **Step 3: Append implementations to `ytlib.py`**

```python
_MAX_TRANSCRIPT_CHARS = 48000  # keep prompts within small local-model contexts


def build_extraction_prompt(video, aliases):
    """Entity-extraction prompt for a local OpenAI-compatible LLM."""
    meta = video.get("metadata", {})
    transcript_text = " ".join(s["text"] for s in video.get("transcript", []))
    if len(transcript_text) > _MAX_TRANSCRIPT_CHARS:
        transcript_text = transcript_text[:_MAX_TRANSCRIPT_CHARS] + " [TRUNCATED]"
    vocab_lines = []
    for group in ("tools", "llms", "protocols"):
        names = ", ".join(sorted(aliases.get(group, {})))
        vocab_lines.append(f"- known {group}: {names}")
    vocab = "\n".join(vocab_lines)
    return f"""You are an entity extractor for a YouTube video knowledge base.

VIDEO TITLE: {meta.get('title', '')}
CHANNEL: {meta.get('channel', '')}
DESCRIPTION: {meta.get('description', '')[:2000]}

TRANSCRIPT:
{transcript_text}

Known canonical names (map variants to these; add new ones if genuinely new):
{vocab}

Respond with ONLY a JSON object, no prose, with exactly these keys:
{{
  "type": "tutorial|build-along|news|review|comparison",
  "difficulty": "beginner|intermediate|advanced",
  "use_case": ["problem-first phrases, kebab-case"],
  "tools": ["canonical tool names actually used or demonstrated"],
  "llms": ["canonical LLM names actually mentioned"],
  "protocols": ["canonical protocol/standard names actually used"],
  "tldr": "2-3 sentence summary",
  "watch_this_if": "one-line relevance test",
  "key_takeaways": ["3-7 substantive bullets"],
  "action_items": ["concrete things a viewer can try"],
  "timeline": [{{"time": "MM:SS", "note": "what happens"}}]
}}"""


def parse_extraction_response(text):
    """Tolerant JSON-object parse of an LLM reply (fences/prose allowed)."""
    start = text.find("{")
    end = text.rfind("}")
    if start == -1 or end <= start:
        raise ValueError("no JSON object found in LLM response")
    return json.loads(text[start:end + 1])
```

- [ ] **Step 4: Run full suite**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -v
```

Expected: `OK` — all three test modules pass.

- [ ] **Step 5: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): ytlib extraction prompt builder and tolerant response parser"
```

---

### Task 5: fetch_playlist.py

**Files:**
- Create: `$PLUGIN/scripts/fetch_playlist.py`

**Interfaces:**
- Consumes: `ytlib.find_config/load_config/playlist_ref_to_url/match_playlist_by_title/scan_vault_video_ids`
- Produces (consumed by process command, Task 10): CLI
  `<venv>/bin/python fetch_playlist.py --config <path> [--playlist <ref>] [--all]`
  → stdout JSON `{"playlist_title": str, "playlist_url": str, "total": int, "new": [{"id","title","url"}], "skipped": int}`; exit 2 + stderr message containing `/yt-catalog:login` on auth failure.

- [ ] **Step 1: Write the script**

`$PLUGIN/scripts/fetch_playlist.py`:

```python
#!/usr/bin/env python3
"""List a playlist's videos minus ones already cataloged in the vault.

Runs under the plugin venv (needs yt-dlp):
  <venv>/bin/python fetch_playlist.py --config /path/.yt-catalog.json \
      [--playlist NAME_OR_URL_OR_ID] [--all]

stdout: JSON {playlist_title, playlist_url, total, new: [{id,title,url}], skipped}
exit 2 with a /yt-catalog:login hint on auth errors.
"""
import argparse
import json
import os
import sys

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)))
import ytlib

AUTH_MARKERS = ("sign in", "private", "login required", "cookies", "members-only")


def ydl_base_opts(cfg, flat=True):
    opts = {"quiet": True, "no_warnings": True, "skip_download": True}
    if flat:
        opts["extract_flat"] = "in_playlist"
    profile = cfg.get("chrome_profile")
    if profile:
        opts["cookiesfrombrowser"] = ("chrome", profile, None, None)
    return opts


def die_auth(err):
    sys.stderr.write(
        f"AUTH ERROR: {err}\n"
        "The automation profile's YouTube session looks stale or missing.\n"
        "Run /yt-catalog:login to refresh it, then retry.\n"
    )
    sys.exit(2)


def resolve_playlist_url(cfg, ref, yt_dlp):
    url = ytlib.playlist_ref_to_url(ref)
    if url:
        return url
    # Display name: look it up in the logged-in account's playlist feed.
    try:
        with yt_dlp.YoutubeDL(ydl_base_opts(cfg)) as ydl:
            feed = ydl.sanitize_info(
                ydl.extract_info("https://www.youtube.com/feed/playlists", download=False)
            )
    except yt_dlp.utils.DownloadError as e:
        if any(m in str(e).lower() for m in AUTH_MARKERS):
            die_auth(e)
        raise
    url = ytlib.match_playlist_by_title(feed, ref)
    if not url:
        titles = [e.get("title") for e in (feed.get("entries") or [])]
        sys.stderr.write(
            f"error: no playlist titled {ref!r} found. Playlists visible: {titles}\n"
            "If it should exist, run /yt-catalog:login and retry.\n"
        )
        sys.exit(3)
    return url


def main():
    ap = argparse.ArgumentParser()
    ap.add_argument("--config", required=True)
    ap.add_argument("--playlist", default=None)
    ap.add_argument("--all", action="store_true", help="include already-processed videos")
    args = ap.parse_args()

    import yt_dlp  # under the plugin venv

    cfg = ytlib.load_config(args.config)
    ref = args.playlist or cfg.get("default_playlist")
    if not ref:
        sys.exit("error: no playlist given and no default_playlist in config")

    url = resolve_playlist_url(cfg, ref, yt_dlp)
    try:
        with yt_dlp.YoutubeDL(ydl_base_opts(cfg)) as ydl:
            info = ydl.sanitize_info(ydl.extract_info(url, download=False))
    except yt_dlp.utils.DownloadError as e:
        if any(m in str(e).lower() for m in AUTH_MARKERS):
            die_auth(e)
        raise

    entries = [e for e in (info.get("entries") or []) if e and e.get("id")]
    known = set()
    if cfg.get("skip_processed", True) and not args.all:
        known = ytlib.scan_vault_video_ids(cfg["vault_path"])

    new = [
        {"id": e["id"], "title": e.get("title") or e["id"],
         "url": e.get("url") or f"https://www.youtube.com/watch?v={e['id']}"}
        for e in entries if e["id"] not in known
    ]
    print(json.dumps({
        "playlist_title": info.get("title") or ref,
        "playlist_url": url,
        "total": len(entries),
        "new": new,
        "skipped": len(entries) - len(new),
    }, indent=2))


if __name__ == "__main__":
    main()
```

- [ ] **Step 2: Syntax check under system python (no yt-dlp import at module level besides inside main)**

```bash
python3 -m py_compile /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/fetch_playlist.py && echo compiled
```

Expected: `compiled`

- [ ] **Step 3: Live smoke test against a public playlist, no cookies**

Create a throwaway config that has no `chrome_profile` (public content needs none):

```bash
cd /tmp/claude-1000/-home-jason-Workspace-youtube-catalog/*/scratchpad 2>/dev/null || cd /tmp
printf '{"vault_path": "/tmp/nonexistent-vault", "default_playlist": "PLBsP89Ea1JBK1KLBSJTaqiOOMUv3sHHYc"}' > /tmp/yt-smoke.json
~/.yt-catalog/venv/bin/python /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/fetch_playlist.py --config /tmp/yt-smoke.json | head -25
```

Expected: JSON with `playlist_title`, `total` > 0, `new` array of `{id,title,url}`, `skipped: 0`. (Any small public playlist ID works if this one is gone — substitute and note it.)

- [ ] **Step 4: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): fetch_playlist script — name/URL/ID resolution, vault diff, auth hints"
```

---

### Task 6: fetch_video.py

**Files:**
- Create: `$PLUGIN/scripts/fetch_video.py`

**Interfaces:**
- Consumes: `ytlib.load_config/format_duration/parse_json3_subs`
- Produces (consumed by process command + `extract_local.py`): CLI
  `<venv>/bin/python fetch_video.py --config <path> --video-id <id>`
  → stdout JSON:

```json
{
  "metadata": {"id": "...", "title": "...", "channel": "...", "channel_url": "...",
                "uploaded": "YYYY-MM-DD", "duration": "M:SS", "duration_seconds": 0,
                "url": "...", "description": "...", "thumbnail": "..."},
  "transcript": [{"start": 0.0, "duration": 0.0, "text": "..."}],
  "transcript_source": "api" | "yt-dlp" | null
}
```

- [ ] **Step 1: Write the script**

`$PLUGIN/scripts/fetch_video.py`:

```python
#!/usr/bin/env python3
"""Fetch metadata + transcript for one video as JSON.

  <venv>/bin/python fetch_video.py --config /path/.yt-catalog.json --video-id ID

transcript_source: "api" (youtube-transcript-api), "yt-dlp" (auto-subs
fallback, uses profile cookies), or null (none available — page still gets
created from metadata alone).
"""
import argparse
import glob
import json
import os
import sys
import tempfile

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)))
import ytlib


def fetch_metadata(cfg, video_id, yt_dlp):
    opts = {"quiet": True, "no_warnings": True, "skip_download": True}
    if cfg.get("chrome_profile"):
        opts["cookiesfrombrowser"] = ("chrome", cfg["chrome_profile"], None, None)
    with yt_dlp.YoutubeDL(opts) as ydl:
        info = ydl.sanitize_info(
            ydl.extract_info(f"https://www.youtube.com/watch?v={video_id}", download=False)
        )
    up = info.get("upload_date") or ""
    return {
        "id": info["id"],
        "title": info.get("title", ""),
        "channel": info.get("channel") or info.get("uploader") or "Unknown",
        "channel_url": info.get("channel_url") or info.get("uploader_url") or "",
        "uploaded": f"{up[:4]}-{up[4:6]}-{up[6:]}" if len(up) == 8 else "",
        "duration": ytlib.format_duration(info.get("duration")),
        "duration_seconds": info.get("duration") or 0,
        "url": info.get("webpage_url") or f"https://www.youtube.com/watch?v={video_id}",
        "description": (info.get("description") or "")[:4000],
        "thumbnail": info.get("thumbnail") or "",
    }


def fetch_transcript_api(video_id, languages):
    from youtube_transcript_api import YouTubeTranscriptApi
    fetched = YouTubeTranscriptApi().fetch(video_id, languages=languages)
    return [{"start": s.start, "duration": s.duration, "text": s.text} for s in fetched]


def fetch_transcript_ytdlp(cfg, video_id, languages, yt_dlp):
    with tempfile.TemporaryDirectory() as tmp:
        opts = {
            "quiet": True, "no_warnings": True, "skip_download": True,
            "writesubtitles": True, "writeautomaticsub": True,
            "subtitleslangs": languages, "subtitlesformat": "json3",
            "outtmpl": os.path.join(tmp, "%(id)s.%(ext)s"),
        }
        if cfg.get("chrome_profile"):
            opts["cookiesfrombrowser"] = ("chrome", cfg["chrome_profile"], None, None)
        with yt_dlp.YoutubeDL(opts) as ydl:
            ydl.download([f"https://www.youtube.com/watch?v={video_id}"])
        files = glob.glob(os.path.join(tmp, "*.json3"))
        if not files:
            return []
        with open(files[0], "r", encoding="utf-8") as f:
            return ytlib.parse_json3_subs(f.read())


def main():
    ap = argparse.ArgumentParser()
    ap.add_argument("--config", required=True)
    ap.add_argument("--video-id", required=True)
    args = ap.parse_args()

    import yt_dlp

    cfg = ytlib.load_config(args.config)
    languages = cfg.get("transcript_languages", ["en"])

    metadata = fetch_metadata(cfg, args.video_id, yt_dlp)

    transcript, source = [], None
    try:
        transcript = fetch_transcript_api(args.video_id, languages)
        source = "api"
    except Exception as api_err:
        try:
            transcript = fetch_transcript_ytdlp(cfg, args.video_id, languages, yt_dlp)
            source = "yt-dlp" if transcript else None
        except Exception as dlp_err:
            sys.stderr.write(f"transcript unavailable: api={api_err}; yt-dlp={dlp_err}\n")

    # Clean text: no newlines inside snippets (they break markdown tables/quotes)
    for s in transcript:
        s["text"] = s["text"].replace("\n", " ").strip()
    transcript = [s for s in transcript if s["text"]]

    print(json.dumps({
        "metadata": metadata,
        "transcript": transcript,
        "transcript_source": source,
    }, indent=2))


if __name__ == "__main__":
    main()
```

- [ ] **Step 2: Syntax check**

```bash
python3 -m py_compile /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/fetch_video.py && echo compiled
```

Expected: `compiled`

- [ ] **Step 3: Live smoke test on a known public video**

```bash
~/.yt-catalog/venv/bin/python /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/fetch_video.py --config /tmp/yt-smoke.json --video-id dQw4w9WgXcQ > /tmp/yt-video-smoke.json && python3 -c "
import json; d = json.load(open('/tmp/yt-video-smoke.json'))
assert d['metadata']['id'] == 'dQw4w9WgXcQ', d['metadata']
assert d['metadata']['uploaded'].count('-') == 2
assert d['transcript_source'] in ('api', 'yt-dlp', None)
print('title:', d['metadata']['title'][:40]); print('snippets:', len(d['transcript']), 'source:', d['transcript_source'])"
```

Expected: title printed, snippets > 0, source `api` or `yt-dlp`.

- [ ] **Step 4: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): fetch_video script — metadata plus transcript with yt-dlp fallback"
```

---

### Task 7: extract_local.py (optional local-LLM extractor)

**Files:**
- Create: `$PLUGIN/scripts/extract_local.py`

**Interfaces:**
- Consumes: `ytlib.load_config/build_extraction_prompt/parse_extraction_response`; Task 6's video JSON on stdin; `skills/video-page/aliases.json`.
- Produces (consumed by process command when `extractor: "local"`): CLI
  `<venv>/bin/python extract_local.py --config <path> < video.json`
  → stdout: the extraction JSON object (keys: `type, difficulty, use_case, tools, llms, protocols, tldr, watch_this_if, key_takeaways, action_items, timeline`). Exit 4 on LLM/HTTP failure with stderr message.

- [ ] **Step 1: Write the script**

`$PLUGIN/scripts/extract_local.py`:

```python
#!/usr/bin/env python3
"""Entity extraction via a local OpenAI-compatible LLM (extractor: "local").

  <venv>/bin/python extract_local.py --config /path/.yt-catalog.json < video.json

stdin:  fetch_video.py output JSON
stdout: extraction JSON (type, difficulty, use_case, tools, llms, protocols,
        tldr, watch_this_if, key_takeaways, action_items, timeline)
Stdlib-only HTTP so the venv needs no extra deps.
"""
import argparse
import json
import os
import sys
import urllib.request

sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)))
import ytlib

ALIASES_PATH = os.path.join(
    os.path.dirname(os.path.abspath(__file__)), "..", "skills", "video-page", "aliases.json"
)


def main():
    ap = argparse.ArgumentParser()
    ap.add_argument("--config", required=True)
    ap.add_argument("--timeout", type=int, default=600)
    args = ap.parse_args()

    cfg = ytlib.load_config(args.config)
    llm = cfg.get("local_llm") or {}
    base_url, model = llm.get("base_url"), llm.get("model")
    if not base_url or not model:
        sys.exit("error: extractor is 'local' but config.local_llm.base_url/model missing")

    video = json.load(sys.stdin)
    with open(ALIASES_PATH, "r", encoding="utf-8") as f:
        aliases = json.load(f)

    body = json.dumps({
        "model": model,
        "messages": [{"role": "user", "content": ytlib.build_extraction_prompt(video, aliases)}],
        "temperature": 0.2,
    }).encode("utf-8")
    req = urllib.request.Request(
        base_url.rstrip("/") + "/chat/completions",
        data=body, headers={"Content-Type": "application/json"},
    )
    try:
        with urllib.request.urlopen(req, timeout=args.timeout) as resp:
            reply = json.load(resp)
        content = reply["choices"][0]["message"]["content"]
        extraction = ytlib.parse_extraction_response(content)
    except Exception as e:
        sys.stderr.write(f"local LLM extraction failed: {e}\n")
        sys.exit(4)

    print(json.dumps(extraction, indent=2))


if __name__ == "__main__":
    main()
```

- [ ] **Step 2: Syntax check**

```bash
python3 -m py_compile /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/extract_local.py && echo compiled
```

Expected: `compiled`

- [ ] **Step 3: Live check ONLY if LMS server reachable (skip cleanly otherwise)**

```bash
curl -s -m 3 http://192.168.1.211:1234/v1/models >/dev/null && echo "LMS up — optional live test possible" || echo "LMS unreachable — skipping live test (fine; prompt/parse already unit-tested)"
```

Either output acceptable. If up, optionally:

```bash
~/.yt-catalog/venv/bin/python /home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts/extract_local.py --config /tmp/yt-smoke-local.json < /tmp/yt-video-smoke.json | head -30
```

where `/tmp/yt-smoke-local.json` = `/tmp/yt-smoke.json` plus the `local_llm` block from `config.example.json`. Expected: JSON with `type`, `tools`, `tldr` keys.

- [ ] **Step 4: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): extract_local script — optional local-LLM entity extraction"
```

---

### Task 8: video-page skill

**Files:**
- Create: `$PLUGIN/skills/video-page/SKILL.md`

**Interfaces:**
- Consumes: Task 6's video JSON shape; `aliases.json` (same dir).
- Produces: the authoritative page template + extraction/canonicalization rules the process command (Task 10) tells Claude to follow. Page filename contract: `<vault>/videos/<safe_title>.md` where safe_title = alnum + ` -_'&,()`, whitespace collapsed.

- [ ] **Step 1: Write `SKILL.md`**

`$PLUGIN/skills/video-page/SKILL.md`:

````markdown
---
name: video-page
description: Use when creating an Obsidian video page for the yt-catalog plugin — defines the exact page template, frontmatter contract, entity extraction and canonicalization rules for turning one video's metadata + transcript JSON into a knowledge-base page.
---

# Creating a Video Page

Input: one video's JSON from `fetch_video.py` (`metadata`, `transcript`,
`transcript_source`) and, when `extractor: "local"`, a pre-computed
extraction JSON from `extract_local.py` (validate it against the rules
below and fix obvious misses instead of extracting from scratch).

Output: ONE file at `<vault>/videos/<Title>.md`. Filename: video title with
only alphanumerics, spaces, and `-_'&,()` kept, whitespace collapsed
(matches `ytlib.safe_filename` so re-runs detect the page).

## Extraction rules

1. **Only what's actually in the video.** Tools listed must be used or
   demonstrated; LLMs must be genuinely mentioned; protocols genuinely
   involved. Passing references in ads/sponsor reads don't count.
2. **Canonicalize every entity** against `aliases.json` in this skill's
   directory (case-insensitive match on canonical names AND variants).
   A genuinely new entity gets a sensible canonical name (proper
   capitalization, no version suffixes unless the version IS the point).
3. **Vocabularies:** `type`: tutorial | build-along | news | review |
   comparison. `difficulty`: beginner | intermediate | advanced.
   `use_case`: kebab-case, problem-first (e.g. `email-automation`,
   `rag-pipeline`, `web-scraping`) — what problem does a viewer solve?
4. **Every entity appears TWICE:** in the frontmatter list (machine-queryable)
   and as a `[[topics/...]]` wikilink in the body (graph + backlinks).
5. **Timeline:** 5-12 timestamped moments from transcript `start` values,
   formatted `M:SS` or `H:MM:SS`.
6. **No transcript?** (`transcript` empty / `transcript_source` null):
   extract from title + description only, set `transcript: false`, write
   "No transcript available." in the Transcript section, and skip Timeline.

## Page template (exact structure)

```markdown
---
title: "{title}"
video_id: {id}
channel: "[[channels/{channel}]]"
uploaded: {uploaded}
processed: {today YYYY-MM-DD}
duration: "{duration}"
url: {url}
playlist: "[[{playlist_title}]]"
type: {type}
difficulty: {difficulty}
use_case: [{use_case, comma separated}]
tools: [{canonical tool names, comma separated}]
llms: [{canonical llm names}]
protocols: [{canonical protocol names}]
transcript: {true|false}
tags: [youtube, ai-automation]
---

# {title}

![thumbnail]({thumbnail})
▶️ [Watch]({url}) | 📅 Uploaded [[uploaded/{uploaded}]] | 🗓️ Processed [[created/{processed}]]

## TL;DR
> {2-3 sentence summary}

**Watch this if:** {one-line relevance test}

## Key Takeaways
- {3-7 substantive bullets}

## 🛠 Tools & Software
- [[topics/{Tool}]] — {one line: how it's used in this video}

## 🤖 LLMs Mentioned
- [[topics/{LLM}]] — {context: compared? recommended? demoed?}

## 📡 Protocols & Standards
- [[topics/{Protocol}]] — {how it features}

## ✅ Action Items
- {concrete things to try yourself}

## 🔗 Related Videos
- [[videos/{Other Page}]] — {shared topics}   <!-- every existing video page sharing ≥2 topics; "None yet." if none -->

## Timeline
- `{M:SS}` — {what happens}

## Transcript
<details>
<summary>Full transcript</summary>

{transcript snippets joined with spaces into readable paragraphs — break
into a new paragraph roughly every 60-90 seconds of `start` time}

</details>
```

Omit an entity section's content with "None identified." rather than
deleting the heading (consistent structure across pages).

## Related Videos computation

Read frontmatter (`tools`, `llms`, `protocols`, `use_case`) of existing
pages in `<vault>/videos/` (Grep for the values — don't read every file
fully). Link pages sharing ≥2 entities, with the shared entities noted.
Update the OTHER page's Related Videos section too if this new video
qualifies (keep both sides of the link in sync).
````

- [ ] **Step 2: Validate frontmatter contract against ytlib regex**

The template's `video_id: {id}` line must be parseable by `ytlib.extract_video_id_from_md`. Verify:

```bash
python3 -c "
import sys; sys.path.insert(0, '/home/jason/Workspace/od-marketplace/plugins/yt-catalog/scripts')
import ytlib
page = '---\ntitle: \"T\"\nvideo_id: dQw4w9WgXcQ\nchannel: \"[[channels/C]]\"\n---\nbody'
assert ytlib.extract_video_id_from_md(page) == 'dQw4w9WgXcQ', 'CONTRACT BROKEN'
print('frontmatter contract ok')"
```

Expected: `frontmatter contract ok`

- [ ] **Step 3: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): video-page skill — template, extraction and canonicalization rules"
```

---

### Task 9: hub-pages skill

**Files:**
- Create: `$PLUGIN/skills/hub-pages/SKILL.md`

**Interfaces:**
- Consumes: video pages created per Task 8's contract.
- Produces: rules for `topics/`, `channels/`, `created/`, `uploaded/`, `Home.md` used by the process command (Task 10).

- [ ] **Step 1: Write `SKILL.md`**

`$PLUGIN/skills/hub-pages/SKILL.md`:

````markdown
---
name: hub-pages
description: Use after creating yt-catalog video pages — defines how to create/update topic, channel, and date hub pages plus the Home.md dashboard so every video page is reachable by topic, channel, date, difficulty, and use-case.
---

# Maintaining Hub Pages

Run AFTER video pages are written. For each new video page, touch exactly
these hubs. Create a hub if missing; otherwise append/update — never
duplicate an entry (check for the video's wikilink before adding).

## topics/<Entity>.md — one per tool, LLM, protocol

```markdown
---
title: {Entity}
kind: {tool | llm | protocol}
aliases: [{known variants from aliases.json, lowercase}]
tags: [topic]
---

# {Entity}

{1-2 sentence description of what it is. Official link if well known.}

## Videos

| Video | Type | Difficulty | Uploaded |
|---|---|---|---|
| [[videos/{Page}]] | {type} | {difficulty} | {uploaded} |

## Related Topics

- [[topics/{Other}]] — {co-occurs in N videos}
```

Related Topics: entities appearing together with this one in ≥2 videos.

## channels/<Name>.md

```markdown
---
title: {Channel Name}
url: {channel_url}
tags: [channel]
---

# {Channel Name}

[Channel on YouTube]({channel_url})

## Cataloged Videos

- [[videos/{Page}]] — {uploaded}, {type}
```

## created/<YYYY-MM-DD>.md and uploaded/<YYYY-MM-DD>.md

```markdown
---
title: {YYYY-MM-DD}
tags: [date, {created | uploaded}]
---

# {created | uploaded}: {YYYY-MM-DD}

- [[videos/{Page}]]
```

## Home.md — regenerate fully every run

```markdown
---
title: Home
tags: [dashboard]
---

# 📺 Video Catalog

## Recently Added

| Video | Channel | Type | Difficulty | Processed |
|---|---|---|---|---|
{10 most recent by processed date}

## By Topic

### 🛠 Tools
[[topics/{Tool}]] ({count}) · ...sorted by count desc

### 🤖 LLMs
[[topics/{LLM}]] ({count}) · ...

### 📡 Protocols
[[topics/{Protocol}]] ({count}) · ...

## By Difficulty

- **Beginner:** [[videos/...]] · ...
- **Intermediate:** ...
- **Advanced:** ...

## By Use Case

- **{use-case}:** [[videos/...]] · ...

_{N} videos cataloged · last run {YYYY-MM-DD}_
```

Counts and lists come from video page frontmatter — Grep the
`tools:`/`llms:`/`protocols:`/`difficulty:`/`use_case:` lines across
`<vault>/videos/*.md` rather than reading whole files.

## Consistency rules

1. A `[[topics/X]]` link in any video page MUST have a matching
   `topics/X.md` — creating those is this skill's job; report any you had
   to create so the run summary can list them.
2. Alias discipline: before creating `topics/X.md`, check no existing topic
   lists `x` (lowercase) in its `aliases:` — if one does, the video page
   used a non-canonical name: fix the video page instead of creating a
   duplicate topic.
````

- [ ] **Step 2: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): hub-pages skill — topic/channel/date hubs and Home dashboard rules"
```

---

### Task 10: Commands — setup, process, login

**Files:**
- Create: `$PLUGIN/commands/setup.md`
- Create: `$PLUGIN/commands/process.md`
- Create: `$PLUGIN/commands/login.md`

**Interfaces:**
- Consumes: all scripts (Tasks 5–7), both skills (Tasks 8–9), `config.example.json` (Task 1).
- Produces: the user-facing `/yt-catalog:setup`, `/yt-catalog:process [playlist]`, `/yt-catalog:login` commands.

- [ ] **Step 1: Write `setup.md`**

`$PLUGIN/commands/setup.md`:

````markdown
---
description: First-time setup for yt-catalog — dependency check, venv creation, interactive config wizard, optional YouTube login. Run automatically by other commands when no config exists.
allowed-tools: Bash, Read, Write, AskUserQuestion
---

Set up the yt-catalog plugin. Work through these stages in order.

## 1. Locate or plan the config

Run: `python3 -c "import sys; sys.path.insert(0, '${CLAUDE_PLUGIN_ROOT}/scripts'); import ytlib, os; print(ytlib.find_config(os.getcwd()) or 'NONE')"`

If a config exists, tell the user its path and ask (AskUserQuestion) whether
to reconfigure it or just verify dependencies. If NONE, continue — the
wizard will create `.yt-catalog.json` in the current working directory.

## 2. Wizard questions (only for missing/reconfigured config)

Ask with AskUserQuestion, one batch:

1. **Vault path** — default: current directory if it looks like a vault
   (has `.obsidian/` or existing `videos/` folder), else ask for absolute path.
2. **Default playlist** — name, URL, or ID. Note: private playlists need
   the login step later.
3. **Extractor** — `claude` (recommended: Claude extracts in-session) or
   `local` (a local OpenAI-compatible server does it; also ask base_url +
   model, defaults from `${CLAUDE_PLUGIN_ROOT}/config.example.json`).
4. **Chrome automation profile** — scan for candidates and list what exists:
   `ls -d ~/.cache/chrome-devtools-mcp/chrome-profile ~/.cache/chrome-profile 2>/dev/null`
   Offer: found candidates / "none — public playlists only" (omits
   chrome_profile from config). NEVER offer ~/.config/google-chrome (the
   user's personal profile).

## 3. Dependencies

```
test -x "$HOME/.yt-catalog/venv/bin/python" || python3 -m venv "$HOME/.yt-catalog/venv"
"$HOME/.yt-catalog/venv/bin/pip" install --quiet --upgrade yt-dlp youtube-transcript-api
"$HOME/.yt-catalog/venv/bin/python" -c "import yt_dlp, youtube_transcript_api; print('deps ok')"
```

Also check Chrome exists if a profile was configured:
`command -v google-chrome || command -v google-chrome-stable || command -v chromium` —
warn (don't fail) if missing.

## 4. Write config

Write `.yt-catalog.json` (structure of `${CLAUDE_PLUGIN_ROOT}/config.example.json`)
with the user's answers. Show the file to the user.

## 5. Login offer

If the playlist may be private and a chrome_profile is set, ask whether to
run the login flow now; if yes, follow `${CLAUDE_PLUGIN_ROOT}/commands/login.md`.

Finish by summarizing: config path, venv path, extractor, and the next step
(`/yt-catalog:process`).
````

- [ ] **Step 2: Write `process.md`**

`$PLUGIN/commands/process.md`:

````markdown
---
description: Process a YouTube playlist into the Obsidian vault — one rich page per new video plus updated topic/channel/date hubs and Home dashboard. Argument optionally overrides the configured default playlist.
argument-hint: [playlist name, URL, or ID]
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, AskUserQuestion, Skill
---

Catalog new videos from a playlist. `$ARGUMENTS` (if given) overrides the
config's `default_playlist`.

## 0. Config gate

Run: `python3 -c "import sys; sys.path.insert(0, '${CLAUDE_PLUGIN_ROOT}/scripts'); import ytlib, os; print(ytlib.find_config(os.getcwd()) or 'NONE')"`

If NONE: tell the user setup is needed, execute the full setup flow from
`${CLAUDE_PLUGIN_ROOT}/commands/setup.md`, then continue here.
Set `CONFIG` to the config path and read it; `VENVPY` = config's
`venv_path` + `/bin/python` (default `~/.yt-catalog/venv/bin/python`).

## 1. Fetch the playlist diff

```
"$VENVPY" "${CLAUDE_PLUGIN_ROOT}/scripts/fetch_playlist.py" --config "$CONFIG" --playlist "$ARGUMENTS"
```

(omit `--playlist` when no argument given). Handle exits:
- exit 2 (auth): tell the user, offer to run the login flow
  (`${CLAUDE_PLUGIN_ROOT}/commands/login.md`), retry after.
- exit 3 (name not found): show the visible playlist titles from stderr,
  ask which to use.
- `new` empty: report "nothing new" with total/skipped counts and stop.

Report: playlist title, total videos, N new, M skipped. If N > 10, confirm
with the user before proceeding (AskUserQuestion: all / first 10 / cancel).

## 2. Per video — strictly one at a time

For each entry in `new`:

a. `"$VENVPY" "${CLAUDE_PLUGIN_ROOT}/scripts/fetch_video.py" --config "$CONFIG" --video-id "<id>"`
   — save stdout to the session scratchpad as `<id>.json`. On failure:
   record the video as failed, continue with the next.

b. Extraction, per config `extractor`:
   - `claude`: you extract, following the video-page skill's rules.
   - `local`: `"$VENVPY" "${CLAUDE_PLUGIN_ROOT}/scripts/extract_local.py" --config "$CONFIG" < <id>.json`
     — on exit 4, warn and fall back to `claude` extraction for this video.

c. Invoke the **yt-catalog:video-page** skill and write the page exactly to
   its template (vault path from config; playlist title from step 1).

d. Progress note to the user: `[k/N] <title> — done (tools: …, llms: …)`.

## 3. Hub pages

Invoke the **yt-catalog:hub-pages** skill: update `topics/`, `channels/`,
`created/`, `uploaded/` for every page written in step 2, then regenerate
`Home.md`.

## 4. Run report

Summarize: pages created (with links), hub pages created vs updated, videos
skipped as already-processed, failures (video + reason), and whether
`Home.md` was regenerated. Suggest opening Home.md in Obsidian.
````

- [ ] **Step 3: Write `login.md`**

`$PLUGIN/commands/login.md`:

````markdown
---
description: Refresh the YouTube session in the dedicated Chrome automation profile so yt-catalog can read private playlists. Opens a browser window for manual login, then verifies access.
allowed-tools: Bash, Read, AskUserQuestion
---

Refresh the automation profile's YouTube login.

## 1. Resolve the profile

Read the config (`python3 -c "import sys; sys.path.insert(0, '${CLAUDE_PLUGIN_ROOT}/scripts'); import ytlib, os, json; p = ytlib.find_config(os.getcwd()); print(json.dumps(ytlib.load_config(p)) if p else 'NONE')"`).
If NONE or no `chrome_profile`: explain that login only applies to private
playlists with a configured automation profile, suggest `/yt-catalog:setup`.

SAFETY: the profile must NOT be under `~/.config/google-chrome`. If it is,
refuse and tell the user to configure a dedicated automation profile.

## 2. Open the browser on that profile

```
BROWSER=$(command -v google-chrome || command -v google-chrome-stable || command -v chromium)
nohup "$BROWSER" --user-data-dir="<chrome_profile from config>" --no-first-run --new-window "https://www.youtube.com" >/dev/null 2>&1 &
```

Tell the user: "Browser opened with the automation profile — log into
YouTube (the account that owns the playlist), then tell me when done."
Wait for their confirmation (AskUserQuestion: Done / Cancel).

## 3. Verify

Ask the user to CLOSE the automation browser window first (Chrome locks the
cookie DB while running). Then:

```
"$VENVPY" "${CLAUDE_PLUGIN_ROOT}/scripts/fetch_playlist.py" --config "$CONFIG"
```

Exit 0 → report success and the playlist stats. Exit 2 → login didn't
take; suggest retrying and checking the right Google account was used.
````

- [ ] **Step 4: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add plugins/yt-catalog && git commit -m "feat(yt-catalog): setup, process, and login commands"
```

---

### Task 11: Marketplace registration

**Files:**
- Modify: `/home/jason/Workspace/od-marketplace/.claude-plugin/marketplace.json`

**Interfaces:**
- Produces: installable `yt-catalog@OD-marketplace`.

- [ ] **Step 1: Add the plugin entry**

In `.claude-plugin/marketplace.json`, append to the `plugins` array (after voicebox):

```json
    {
      "name": "yt-catalog",
      "source": "./plugins/yt-catalog",
      "description": "Catalogs a YouTube playlist (private supported via a dedicated Chrome automation profile) into an interconnected Obsidian knowledge base — per-video pages plus topic/channel/date hubs and a Home dashboard."
    }
```

- [ ] **Step 2: Validate JSON**

```bash
python3 -m json.tool /home/jason/Workspace/od-marketplace/.claude-plugin/marketplace.json >/dev/null && echo "marketplace.json valid"
```

Expected: `marketplace.json valid`

- [ ] **Step 3: Commit**

```bash
cd /home/jason/Workspace/od-marketplace && git add .claude-plugin/marketplace.json && git commit -m "feat: register yt-catalog plugin in marketplace"
```

---

### Task 12: Install + end-to-end verification

**Files:** none created — verification only.

**Interfaces:**
- Consumes: everything.

- [ ] **Step 1: Full unit suite green**

```bash
cd /home/jason/Workspace/od-marketplace/plugins/yt-catalog && python3 -m unittest discover -s tests -v
```

Expected: `OK`, 0 failures.

- [ ] **Step 2: User installs the plugin (interactive — Claude cannot run /plugin)**

Ask the user to run in Claude Code:

```
/plugin marketplace add /home/jason/Workspace/od-marketplace
/plugin install yt-catalog@OD-marketplace
```

(If the marketplace is already added, just the install/update line.)
Then verify `/yt-catalog:setup`, `/yt-catalog:process`, `/yt-catalog:login`
appear in the command list.

- [ ] **Step 3: E2E dry run on a PUBLIC playlist into a throwaway vault**

With the user: run `/yt-catalog:process <small public playlist URL>` after
pointing the wizard at a scratch vault dir (e.g. `/tmp/yt-e2e-vault`).
Verify:
- `videos/` pages exist with valid frontmatter (`video_id`, entity lists)
- every `[[topics/X]]` link has `topics/X.md`
- `channels/`, `created/`, `uploaded/` pages exist
- `Home.md` lists the videos
- re-running reports "nothing new" (skip-processed works)

- [ ] **Step 4: Real run — 'Agent Skills n8n'**

User runs `/yt-catalog:setup` in `/home/jason/Workspace/youtube-catalog`
(vault = `AI Automate play list`), `/yt-catalog:login` (private playlist),
then `/yt-catalog:process`. Spot-check 2-3 generated pages in Obsidian:
graph shows video↔topic↔date connections; Home.md dashboard populated.

- [ ] **Step 5: Push (with user approval) — publish steps**

```bash
cd /home/jason/Workspace/od-marketplace && git push -u origin feature/yt-catalog
```

Then per user's branching strategy: merge `feature/yt-catalog` → `develop`
(create if absent) → `main` via their normal flow. NEVER feature → main
directly.

---

## Self-Review Notes

- Spec coverage: playlist fetch w/ cookies (T5), transcript + fallback + no-transcript path (T6, T8 rule 6), extraction claude/local switch (T7, T10 process step 2b), template with dual frontmatter/body entities (T8), alias canonicalization (T1 aliases.json + T8 rule 2 + T9 consistency rule 2), hubs incl. created/uploaded date pages + Home regeneration (T9), first-run wizard from any command (T10 process step 0), login refresh + personal-profile safety (T10 login), portability (venv + config, T1/T10), marketplace publish (T11, T12 step 5), error handling: auth exit 2, name-miss exit 3, LLM-fail exit 4 with claude fallback, per-video failure isolation (T10 process 2a).
- Types/signatures consistent: `ytlib` function names identical across Tasks 2-7 consumers; video JSON shape defined once (T6) and referenced by T7/T8.
- Out of scope honored: no cron, no multi-playlist, no re-processing changed videos.
