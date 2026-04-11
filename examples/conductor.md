# CONTEXT.md — Conductor

> Real-world example from [cyq1017/conductor](https://github.com/cyq1017/conductor)

## What

**Conductor** is a Python CLI tool for orchestrating multiple AI coding agents with structured handoff, trust calibration, and continuous improvement.

- **Primary users**: Developers who use multiple AI coding agents (Claude Code, Cursor, Codex, etc.)
- **Core value**: Prevent context loss across sessions, track agent reliability, and systematize human-agent collaboration
- **Install**: `pip install conductor-ai`

## Architecture

```
conductor/
├── src/conductor/
│   ├── __init__.py          # Version (0.4.0)
│   ├── cli.py               # Click CLI: status, init, digest, retro, memory
│   ├── core.py              # Command logic (StatusAnalyzer, ProjectInitializer)
│   ├── parser.py            # Markdown file parsers (HANDOFF, ERROR_BOOK, etc.)
│   ├── display.py           # Rich terminal output (tables, panels, trees)
│   ├── digest.py            # v0.2: Extract decisions/errors from project history
│   ├── retro.py             # v0.3: Interactive agent retrospective
│   └── memory.py            # v0.4: Cross-session knowledge store (JSON-based)
├── templates/
│   ├── HANDOFF.md.template
│   ├── ERROR_BOOK.md.template
│   ├── TRUST_PROFILE.md.template
│   └── METHODOLOGY.md       # 12-dimension Human-Agent interaction framework
├── docs/
│   ├── methodology/          # Three methodology documents
│   └── discussion-notes.md   # Design decisions and reasoning
├── tests/
│   ├── test_cli.py
│   └── test_core.py
└── pyproject.toml            # hatchling build, conductor-ai on PyPI
```

### Command Flow

```
conductor status  → parser.py (reads HANDOFF/ERROR_BOOK) → core.py (analyzes) → display.py (renders)
conductor digest  → digest.py (extracts from history files) → display.py (formatted output)
conductor retro   → retro.py (interactive Q&A) → writes to ERROR_BOOK + TRUST_PROFILE
conductor memory  → memory.py (add/search/list/export/extract) → JSON file store
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.9+ |
| CLI | Click 8.x |
| Terminal UI | Rich |
| Build | Hatchling |
| Distribution | PyPI (`conductor-ai`) |
| Testing | pytest |
| Memory Store | JSON files (no external DB) |

## Key Files

| File | Read When |
|------|-----------|
| `cli.py` | Adding/modifying CLI commands |
| `core.py` | Changing status analysis logic |
| `parser.py` | Fixing markdown parsing |
| `memory.py` | Modifying knowledge store |
| `templates/METHODOLOGY.md` | Understanding the 12-dimension framework |

## Conventions

- CLI commands in `cli.py`, logic in dedicated modules
- All terminal output via `display.py` (never `print()` in core)
- Templates use `.md.template` extension
- 8 trust domains: code_generation, debugging, architecture, testing, documentation, refactoring, devops, ui_frontend
- Version synced in `pyproject.toml` + `__init__.py`

## Gotchas

- Python 3.9: No `match` statements, no `X | Y` type syntax
- `pip install -e .` needs setuptools on older Python
- Memory is stored as flat JSON — no vector DB, by design
