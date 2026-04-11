# CONTEXT.md — WenYuan (文渊)

> Real-world example from [cyq1017/wenyuan](https://github.com/cyq1017/wenyuan)

## What

**WenYuan** is an AI-driven academic productivity system built on Obsidian + Claude Code, providing 12 slash commands (skills) for researchers to manage daily planning, literature review, and knowledge organization.

- **Primary users**: Researchers, graduate students, knowledge workers
- **Core value**: Turn Obsidian into an intelligent research assistant powered by agentic AI
- **Integration**: Claude Code (primary), also works with Cursor, Codex

## Architecture

```
wenyuan/
├── skills/                   # 12 agentic skills (slash commands)
│   ├── start-my-day/
│   │   └── SKILL.md          # Morning planning: review deadlines, plan tasks
│   ├── end-my-day/
│   │   └── SKILL.md          # Evening review: summarize, log, plan tomorrow
│   ├── literature-review/
│   │   ├── SKILL.md          # Search, read, and annotate papers
│   │   └── scripts/
│   │       └── search_arxiv.py
│   ├── add-paper/
│   │   └── SKILL.md          # Import paper with structured note
│   ├── weekly-digest/
│   │   └── SKILL.md          # Weekly summary of research progress
│   ├── brainstorm/
│   │   └── SKILL.md          # Structured idea generation
│   └── ... (6 more skills)
├── templates/                # Note templates (Templater format)
│   ├── paper-note.md
│   ├── daily-plan.md
│   ├── meeting-note.md
│   └── concept-note.md
├── vault-structure/          # Recommended Obsidian vault organization
│   └── README.md
├── AGENTS.md                 # Rules for AI agents working in this vault
├── GEMINI.md                 # Antigravity-specific rules
├── setup.sh                  # One-click installation script
└── README.md                 # User guide (EN + ZH)
```

### Skill Execution

```
User: /start-my-day
  → Claude Code reads skills/start-my-day/SKILL.md
  → Reads AGENTS.md for vault rules
  → Scans daily/ folder for recent notes
  → Checks deadlines in knowledge/projects/
  → Generates today's plan in daily/YYYY-MM-DD.md
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Platform | Obsidian 1.5+ |
| AI Agent | Claude Code (primary) |
| Skills | SKILL.md (markdown instructions) |
| Scripts | Python 3.9+ (for search, API calls) |
| Templates | Templater plugin format |
| Sync | Syncthing / iCloud |
| Key Plugins | Templater, Dataview, Calendar |

## Key Files

| File | Read When |
|------|-----------|
| `AGENTS.md` | Always — defines all vault rules |
| `skills/*/SKILL.md` | Running or modifying a skill |
| `templates/*.md` | Creating new note types |
| `setup.sh` | First-time installation |

## Skills Inventory

| Skill | Trigger | Category |
|-------|---------|----------|
| start-my-day | `/start-my-day` | Planning |
| end-my-day | `/end-my-day` | Review |
| literature-review | `/lit-review [topic]` | Research |
| add-paper | `/add-paper [url]` | Research |
| weekly-digest | `/weekly-digest` | Review |
| brainstorm | `/brainstorm [topic]` | Ideation |
| concept-map | `/concept-map` | Knowledge |
| ... | ... | ... |

## Conventions

- One skill per folder, SKILL.md is the entry point
- Notes: YAML front matter required (tags, date, status)
- Tags: `#type/paper`, `#type/concept`, `#status/draft`
- Links: `[[wikilinks]]` for internal vault references
- Daily notes: `daily/YYYY-MM-DD.md` format

## Gotchas

- Skills assume vault structure exists — run `setup.sh` first
- Python scripts need absolute paths (agent CWD varies)
- Syncthing + Obsidian: avoid editing same note on two devices
- SKILL.md is literally interpreted as instructions — precision matters
