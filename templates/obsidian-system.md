# CONTEXT.md — Obsidian Plugin / Skill System

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is an [Obsidian vault / plugin / agentic system] that [does X for Y users].

- **Primary users**: [researchers / students / knowledge workers]
- **Integration**: [Claude Code / Cursor / standalone Obsidian]
- **Core pattern**: [Slash commands / Skills / Templates]

## Architecture

```
vault-name/
├── .obsidian/
│   └── plugins/              # Installed Obsidian plugins
├── skills/                   # AI agent skills (slash commands)
│   ├── start-my-day/
│   │   └── SKILL.md          # Skill definition + instructions
│   ├── literature-review/
│   │   ├── SKILL.md
│   │   └── scripts/
│   │       └── search.py     # Helper scripts
│   └── weekly-digest/
│       └── SKILL.md
├── templates/                # Document templates
│   ├── paper-note.md
│   ├── meeting-note.md
│   └── daily-plan.md
├── knowledge/                # Knowledge base
│   ├── papers/               # Literature notes
│   ├── concepts/             # Concept definitions
│   └── projects/             # Project notes
├── daily/                    # Daily notes
│   └── YYYY-MM-DD.md
├── inbox/                    # Quick capture
├── AGENTS.md                 # Rules for AI agents
└── CONTEXT.md                # This file
```

### Skill Execution Flow

```
User: /skill-name → Agent reads SKILL.md → Executes instructions → Writes output to vault
                         ↓
                   Reads AGENTS.md (rules)
                   Reads CONTEXT.md (context)
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Platform | Obsidian 1.5+ | Desktop + mobile |
| Agent | Claude Code | <!-- or Cursor, Copilot --> |
| Skills | SKILL.md (markdown) | One folder per skill |
| Scripts | Python 3.9+ | Helper scripts in skills |
| Sync | Syncthing / iCloud | Cross-device sync |
| Plugins | Templater, Dataview | <!-- list key plugins --> |

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `AGENTS.md` | Rules for AI agents in this vault | Always read first |
| `skills/*/SKILL.md` | Skill definitions | Running or creating skills |
| `templates/*.md` | Document templates | Creating new notes |
| `.obsidian/plugins/` | Plugin configs | Debugging plugin issues |

## Skills Inventory

<!-- List all available skills/commands -->

| Skill | Trigger | Description |
|-------|---------|-------------|
| `start-my-day` | `/start-my-day` | Morning planning routine |
| `literature-review` | `/lit-review [topic]` | Search and summarize papers |
| `weekly-digest` | `/weekly-digest` | Summarize week's notes |
| `add-paper` | `/add-paper [url]` | Import and annotate a paper |

## Conventions

- **Note naming**: `YYYY-MM-DD` for daily, descriptive titles for others
- **Tags**: `#type/paper`, `#type/concept`, `#status/draft`, `#status/reviewed`
- **Links**: Use `[[wikilinks]]` for internal, `[text](url)` for external
- **Skills**: Each skill is self-contained in its folder with SKILL.md
- **Templates**: Templater syntax `<% tp.date.now() %>` for dynamic content
- **Front matter**: YAML front matter for metadata on every note

## Gotchas

- Skill scripts must use absolute paths (agent CWD may vary)
- Syncthing conflicts: Never edit the same note on two devices simultaneously
- Obsidian plugins must be installed manually on each device
- SKILL.md is read as instructions — be precise, avoid ambiguity
- Daily notes folder must exist before skills try to write to it
