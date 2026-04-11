# CONTEXT.md — Monorepo

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a monorepo containing [N] packages that [describe the system].

- **Packages**: [list main packages]
- **Package manager**: [pnpm / npm workspaces / Turborepo / Lerna]
- **Shared**: [what's shared across packages — types, utils, configs]

## Architecture

```
project-name/
├── packages/
│   ├── core/                 # Shared business logic
│   │   ├── src/
│   │   └── package.json
│   ├── web/                  # Frontend application
│   │   ├── src/
│   │   └── package.json
│   ├── api/                  # Backend API
│   │   ├── src/
│   │   └── package.json
│   └── shared/               # Shared types, utils, constants
│       ├── src/
│       │   ├── types.ts
│       │   └── utils.ts
│       └── package.json
├── configs/                  # Shared configs (tsconfig, eslint, etc.)
│   ├── tsconfig.base.json
│   └── eslint.base.js
├── scripts/                  # Build/deploy scripts
├── package.json              # Root workspace config
├── pnpm-workspace.yaml       # Workspace definition
└── turbo.json                # Build pipeline (if using Turborepo)
```

### Package Dependencies

```
shared ← core ← web
              ← api
```

## Build Order

| Order | Package | Command | Notes |
|-------|---------|---------|-------|
| 1 | `shared` | `pnpm --filter shared build` | Must build first — others depend on it |
| 2 | `core` | `pnpm --filter core build` | Depends on `shared` |
| 3 | `web` + `api` | `pnpm --filter web build` | Can build in parallel |
| All | — | `pnpm turbo build` | Turborepo handles ordering |

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `pnpm-workspace.yaml` | Defines which folders are packages | Adding new packages |
| `turbo.json` | Build pipeline and caching config | Modifying build process |
| `packages/shared/src/types.ts` | All shared TypeScript types | Changing data models |
| `configs/tsconfig.base.json` | Base TS config inherited by all | TypeScript issues |

## Conventions

- **Internal deps**: Use `"@project/shared": "workspace:*"` in package.json
- **Imports**: Each package exports from `src/index.ts`
- **Versioning**: All packages share the same version (synced releases)
- **Testing**: Each package has its own test suite, run all with `pnpm turbo test`
- **New package**: Copy template from `packages/shared`, update workspace config

## Gotchas

- Must run `pnpm install` from root — never from individual package directories
- TypeScript project references: `tsconfig.json` in each package must reference dependencies
- Hot reload: Changes in `shared` require rebuild before `web` picks them up (unless using `--watch`)
- CI: Cache `node_modules` AND `.turbo` directory for fast builds
