# CONTEXT.md — Awesome Context MD

## What is this project?
A curated collection of CONTEXT.md templates and real-world examples. One file dropped into a project → AI agent instantly understands the codebase.

## Structure
```
awesome-context-md/
├── templates/          # 7 templates by project type
│   ├── python-cli.md
│   ├── python-web.md
│   ├── typescript-web.md
│   ├── ml-ai.md
│   ├── obsidian-system.md
│   ├── monorepo.md
│   └── api-service.md
├── examples/           # 3 real-world examples (anonymized)
│   ├── conductor.md
│   ├── wenyuan.md
│   └── webapp-generic.md
├── README.md           # English
├── README_zh.md        # Chinese
├── CONTRIBUTING.md
└── LICENSE             # CC0
```

## Key Design Decisions
- **Templates are standalone**: Each template is a single .md file, no dependencies between them
- **Real examples use anonymized data**: Extracted from actual projects but with paths/names sanitized
- **CC0 license**: Maximum adoption — anyone can use without attribution
- **Bilingual**: README in both English and Chinese for broader reach

## Relationship to Other Projects
```
awesome-agent-rules    = "How to act"      (CLAUDE.md, AGENTS.md)
awesome-context-md     = "What this is"    (CONTEXT.md)  ← this project
awesome-agent-memory   = "What to remember" (HANDOFF.md, ERROR_BOOK.md)
```

## Things to Watch Out For
- Templates should be generic enough to work with ANY AI agent (not just Claude)
- Examples must be thoroughly anonymized — no real paths, usernames, or API keys
- README links use relative paths, not absolute — they must work on GitHub
