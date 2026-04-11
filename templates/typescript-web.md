# CONTEXT.md — TypeScript Web Application

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a [React/Next.js/Vue] web application that [does X for Y users].

- **Primary users**: [end users / developers / internal team]
- **Live URL**: [https://example.com]
- **Package manager**: [npm / pnpm / bun]

## Architecture

```
project-name/
├── src/
│   ├── app/                  # Next.js App Router (or pages/)
│   │   ├── layout.tsx        # Root layout, providers
│   │   ├── page.tsx          # Home page
│   │   └── dashboard/
│   │       └── page.tsx      # Dashboard page
│   ├── components/
│   │   ├── ui/               # Reusable UI primitives (Button, Modal, etc.)
│   │   ├── layout/           # Header, Footer, Sidebar
│   │   └── features/         # Feature-specific components
│   ├── hooks/                # Custom React hooks
│   ├── lib/                  # Utility functions, API clients
│   │   ├── api.ts            # API client (fetch/axios wrapper)
│   │   ├── auth.ts           # Auth utilities
│   │   └── utils.ts          # General helpers
│   ├── stores/               # State management (Zustand/Redux)
│   ├── types/                # TypeScript type definitions
│   └── styles/               # Global CSS, theme
│       └── globals.css
├── public/                   # Static assets
├── package.json
├── tsconfig.json
├── next.config.js            # or vite.config.ts
└── tailwind.config.ts        # if using Tailwind
```

### Data Flow

```
User Action → Component → Hook/Store → API Client → Backend
                 ↓
         State Update → Re-render → UI Update
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Framework | Next.js 14 | App Router |
| Language | TypeScript 5.x | Strict mode enabled |
| Styling | Tailwind CSS 3.x | <!-- or CSS Modules, styled-components --> |
| UI Library | shadcn/ui | <!-- or Material UI, Ant Design --> |
| State | Zustand | <!-- or Redux Toolkit, Jotai --> |
| Data Fetching | TanStack Query | <!-- or SWR, native fetch --> |
| Auth | NextAuth.js | <!-- or Clerk, Auth0 --> |
| Testing | Vitest + Testing Library | `npm run test` |
| Deployment | Vercel | <!-- or Netlify, AWS --> |

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `app/layout.tsx` | Root layout, global providers | Understanding app structure |
| `lib/api.ts` | All API calls centralized here | Adding/modifying API calls |
| `stores/*.ts` | Global state definitions | Understanding state shape |
| `components/ui/*.tsx` | Design system primitives | Building new UI |
| `types/index.ts` | Shared TypeScript types | Understanding data shapes |
| `tailwind.config.ts` | Custom theme, colors, spacing | Modifying design tokens |

## Conventions

- **File naming**: kebab-case for files, PascalCase for components
- **Components**: One component per file, co-located styles
- **Imports**: Use `@/` path alias for `src/` directory
- **API calls**: Always go through `lib/api.ts`, never raw `fetch` in components
- **State**: Local state for UI, Zustand for cross-component state, TanStack Query for server state
- **Error handling**: Error boundaries for component errors, try-catch in API calls
- **Types**: No `any` — define explicit types in `types/`

## Gotchas

- Next.js App Router: `'use client'` directive required for hooks/state/browser APIs
- Server Components cannot use `useState`, `useEffect`, or event handlers
- Tailwind classes won't auto-complete without the VS Code extension
- Environment variables: `NEXT_PUBLIC_*` prefix required for client-side access
- Image optimization: Use `next/image` instead of `<img>` tags
