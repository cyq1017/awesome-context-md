# CONTEXT.md — Generic Web Application

> Example template for a typical full-stack web application

## What

**TaskFlow** is a project management web application that helps small teams track tasks, deadlines, and team workload.

- **Primary users**: Small teams (5-20 people)
- **Core value**: Simple, fast task management without enterprise bloat
- **Live**: https://taskflow.example.com

## Architecture

```
taskflow/
├── frontend/                 # React SPA
│   ├── src/
│   │   ├── App.tsx           # Root component, routing
│   │   ├── pages/
│   │   │   ├── Dashboard.tsx # Main dashboard with task board
│   │   │   ├── Projects.tsx  # Project list and creation
│   │   │   └── Settings.tsx  # User/team settings
│   │   ├── components/
│   │   │   ├── TaskCard.tsx  # Draggable task card
│   │   │   ├── KanbanBoard.tsx # Drag-and-drop board
│   │   │   └── TeamAvatar.tsx
│   │   ├── hooks/
│   │   │   ├── useTasks.ts   # Task CRUD + real-time updates
│   │   │   └── useAuth.ts   # Auth state management
│   │   ├── api/
│   │   │   └── client.ts     # Axios wrapper, interceptors
│   │   └── types/
│   │       └── index.ts      # Shared TypeScript types
│   ├── package.json
│   └── vite.config.ts
│
├── backend/                  # FastAPI REST API
│   ├── app/
│   │   ├── main.py           # App factory, middleware
│   │   ├── routes/
│   │   │   ├── tasks.py      # GET/POST/PUT/DELETE /tasks
│   │   │   ├── projects.py   # /projects endpoints
│   │   │   └── auth.py       # /auth/login, /auth/register
│   │   ├── models/
│   │   │   ├── task.py       # Task SQLAlchemy model
│   │   │   └── user.py       # User model + password hashing
│   │   └── services/
│   │       └── notification.py # Email/Slack notifications
│   ├── migrations/           # Alembic
│   └── requirements.txt
│
├── docker-compose.yml        # Frontend + Backend + DB
└── README.md
```

### Data Flow

```
Browser → React Component → API Client → FastAPI Route → Service → PostgreSQL
                                              ↓
                                     WebSocket (real-time task updates)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + TypeScript + Vite |
| Styling | Tailwind CSS |
| State | TanStack Query (server) + Zustand (client) |
| Backend | FastAPI + SQLAlchemy 2.0 |
| Database | PostgreSQL 15 |
| Auth | JWT (access + refresh tokens) |
| Real-time | WebSockets (FastAPI) |
| Deployment | Docker Compose → AWS ECS |

## Key Endpoints

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/auth/login` | No | Returns JWT pair |
| GET | `/tasks` | Yes | List tasks (filtered) |
| POST | `/tasks` | Yes | Create task |
| PUT | `/tasks/:id` | Yes | Update task |
| DELETE | `/tasks/:id` | Yes | Soft delete |
| WS | `/ws/tasks` | Yes | Real-time updates |

## Conventions

- Frontend: Feature-based folder structure under `pages/`
- Backend: Route → Service → Model (no DB access in routes)
- API: RESTful, JSON responses, snake_case fields
- Auth: JWT in `Authorization: Bearer` header
- Errors: Consistent `{ "detail": "..." }` format
- Testing: pytest (backend), Vitest (frontend)

## Gotchas

- WebSocket auth: Token passed as query param (`?token=xxx`), not header
- Soft deletes: Tasks are never physically deleted, only `is_deleted=true`
- Timezone: All timestamps stored as UTC, converted in frontend
- File uploads: Max 10MB, stored in S3 (not local disk)
