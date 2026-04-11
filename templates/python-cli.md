# CONTEXT.md — Python CLI Project

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a Python CLI tool that [does X for Y users].

- **Primary users**: [developers / data scientists / DevOps engineers]
- **Core value**: [one sentence on why someone would use this]
- **Install**: `pip install project-name`

## Architecture

```
project-name/
├── src/project_name/
│   ├── __init__.py          # Version and package metadata
│   ├── cli.py               # Click/Typer command definitions (entry point)
│   ├── core.py              # Core business logic (no CLI dependencies)
│   ├── parser.py            # File/data parsing utilities
│   ├── display.py           # Rich/terminal output formatting
│   └── config.py            # Configuration loading & defaults
├── templates/               # Template files shipped with the package
│   └── *.md.template
├── tests/
│   ├── test_cli.py          # CLI integration tests
│   └── test_core.py         # Unit tests for core logic
├── pyproject.toml            # Build config (hatchling/setuptools)
└── README.md
```

### Data Flow

```
User Input (CLI args) → cli.py → core.py → parser.py → display.py → Terminal Output
                                    ↓
                              config.py (loads defaults)
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Language | Python 3.9+ | Minimum supported version |
| CLI Framework | Click 8.x | <!-- or Typer, argparse --> |
| Terminal UI | Rich | Tables, panels, colored output |
| Build System | Hatchling | pyproject.toml based |
| Testing | pytest | Run with `pytest tests/` |
| Distribution | PyPI | `pip install project-name` |

## Key Files

<!-- List the 5-8 most important files an AI agent should read first -->

| File | Purpose | Read When |
|------|---------|-----------|
| `cli.py` | All CLI commands defined here | Adding/modifying commands |
| `core.py` | Business logic, no I/O | Changing behavior |
| `parser.py` | Parses project files (HANDOFF.md, etc.) | Fixing parsing bugs |
| `display.py` | Rich formatting for terminal output | Changing how things look |
| `pyproject.toml` | Dependencies, version, build config | Adding deps, bumping version |

## Conventions

- **Naming**: snake_case for files/functions, PascalCase for classes
- **CLI commands**: `@cli.command()` decorators in `cli.py`, logic delegated to `core.py`
- **Error handling**: Use `click.echo()` for user-facing errors, raise exceptions in core
- **Output**: All terminal formatting goes through `display.py` (never print directly in core)
- **Testing**: Each command has a corresponding test in `test_cli.py` using `CliRunner`
- **Version**: Kept in sync between `pyproject.toml` and `__init__.py`

## Current State

<!-- Update this section as your project evolves -->

| Feature | Status | Notes |
|---------|--------|-------|
| `command-a` | ✅ Done | Core functionality |
| `command-b` | ✅ Done | Extended functionality |
| `command-c` | 🚧 WIP | In progress |
| `command-d` | 📋 Planned | Not started |

## Gotchas

<!-- Things that are non-obvious and will trip up an AI agent -->

- Python 3.9 compatibility: Don't use `match` statements or `X | Y` type unions
- `pip install -e .` requires setuptools on older Python — use venv
- Template files in `templates/` must be included in `pyproject.toml` package data
- Version number must be updated in BOTH `pyproject.toml` and `__init__.py`
