# Awesome CONTEXT.md [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) · [中文](README_zh.md)

> A curated collection of **CONTEXT.md** files — structured project descriptions that help AI coding agents instantly understand your codebase.

Drop a `CONTEXT.md` into your project root, and every AI agent (Claude Code, Cursor, Copilot, Codex, Windsurf) can skip the "What does this project do?" phase and start contributing immediately.

## Why CONTEXT.md?

Every time an AI agent enters a new project, it wastes tokens and time trying to understand:
- What does this project do?
- What's the tech stack?
- How is the code organized?
- What are the key conventions?

**CONTEXT.md solves this in one file.** It's like a README for machines — concise, structured, and optimized for AI consumption.

```
Traditional onboarding:  Agent reads 20+ files → builds mental model → starts working (slow, error-prone)
With CONTEXT.md:         Agent reads 1 file → understands everything → starts working (fast, accurate)
```

## How It Works

```bash
# 1. Copy a template that matches your project type
cp templates/python-cli.md your-project/CONTEXT.md

# 2. Fill in your project details (5 minutes)

# 3. Every AI agent that enters your project now "gets it" instantly
```

## Templates

Ready-to-use templates organized by project type:

### By Language / Framework

| Template | Best For | Key Sections |
|----------|----------|-------------|
| [Python CLI](templates/python-cli.md) | CLI tools, scripts | Entry points, arg parsing, package structure |
| [Python Web](templates/python-web.md) | FastAPI, Flask, Django | Routes, models, middleware, DB schema |
| [TypeScript Web](templates/typescript-web.md) | React, Next.js, Vite | Components, state, routing, build pipeline |
| [ML / AI](templates/ml-ai.md) | Training pipelines, inference | Models, datasets, configs, evaluation |

### By Project Pattern

| Template | Best For | Key Sections |
|----------|----------|-------------|
| [Obsidian Plugin/System](templates/obsidian-system.md) | Vaults, plugins, skill systems | Skills, slash commands, vault structure |
| [Monorepo](templates/monorepo.md) | Multi-package projects | Package relationships, shared deps, build order |
| [API Service](templates/api-service.md) | REST/GraphQL backends | Endpoints, auth, rate limits, data models |

## Real-World Examples

CONTEXT.md files extracted from real, production projects:

| Project | Type | What You'll Learn |
|---------|------|-------------------|
| [Conductor](examples/conductor.md) | Python CLI | How to describe a CLI tool's command structure |
| [WenYuan](examples/wenyuan.md) | Obsidian System | How to document a skill-based agentic system |
| [Web App (Generic)](examples/webapp-generic.md) | Full-Stack Web | How to map routes, components, and data flow |

## The CONTEXT.md Spec

A good CONTEXT.md should answer these questions in order:

### 1. What (2-3 lines)
> What does this project do? Who is it for?

### 2. Architecture (diagram or list)
> How is the code organized? What are the main modules?

### 3. Tech Stack (table)
> What languages, frameworks, databases, tools?

### 4. Key Files (annotated tree)
> Which files matter most? What does each do?

### 5. Conventions (bullet list)
> Naming patterns, error handling, testing approach?

### 6. Current State (optional)
> What's done, what's in progress, what's planned?

### 7. Gotchas (optional)
> Non-obvious things that will trip up an AI agent?

## CONTEXT.md vs Other Files

| File | Audience | Purpose |
|------|----------|---------|
| **README.md** | Humans (users) | How to install and use |
| **CONTEXT.md** | AI agents | How to understand and modify the code |
| **CONTRIBUTING.md** | Humans (contributors) | How to submit changes |
| **CLAUDE.md / AGENTS.md** | AI agents | Rules and constraints for behavior |
| **ARCHITECTURE.md** | Humans (developers) | Deep-dive into design decisions |

> **Key insight**: CONTEXT.md is *complementary* to CLAUDE.md/AGENTS.md. The context file says "here's what the project is", the rules file says "here's how to behave".

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Ways to contribute:
- 📝 **Add a template** for a project type we don't cover yet
- 🌟 **Share your CONTEXT.md** from a real project (sanitized)
- 🐛 **Improve existing templates** based on your experience
- 🌐 **Translate** templates into other languages

## Related Projects

- [awesome-agent-rules](https://github.com/cyq1017/awesome-agent-rules) — Rules & best practices for AI coding agents
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — DESIGN.md files for frontend projects
- [Conductor](https://github.com/cyq1017/conductor) — CLI for orchestrating multiple AI coding agents
- [repomix](https://github.com/yamadashy/repomix) — Pack your codebase into AI-friendly formats

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work. See [LICENSE](LICENSE).
