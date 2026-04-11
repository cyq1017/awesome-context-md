# CONTEXT.md — Python Web Application

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a [FastAPI/Flask/Django] web application that [does X for Y users].

- **Primary users**: [end users / API consumers / internal team]
- **API style**: [REST / GraphQL / hybrid]
- **Deployment**: [Docker / Cloud Run / Vercel / bare metal]

## Architecture

```
project-name/
├── app/
│   ├── __init__.py           # App factory / initialization
│   ├── main.py               # FastAPI app instance, startup events
│   ├── routes/
│   │   ├── auth.py           # Authentication endpoints
│   │   ├── users.py          # User CRUD
│   │   └── items.py          # Domain-specific endpoints
│   ├── models/
│   │   ├── user.py           # SQLAlchemy/Pydantic models
│   │   └── item.py
│   ├── services/
│   │   ├── auth_service.py   # Business logic for auth
│   │   └── item_service.py   # Business logic for items
│   ├── middleware/
│   │   ├── cors.py           # CORS configuration
│   │   └── auth.py           # JWT/session middleware
│   └── utils/
│       ├── database.py       # DB connection, session management
│       └── config.py         # Environment variables, settings
├── migrations/               # Alembic database migrations
├── tests/
├── docker-compose.yml
├── Dockerfile
└── requirements.txt
```

### Request Flow

```
HTTP Request → Middleware (auth, CORS) → Route Handler → Service Layer → Database
                                              ↓
                                      Response Model → HTTP Response
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Framework | FastAPI 0.100+ | <!-- or Flask, Django --> |
| ORM | SQLAlchemy 2.0 | Async support |
| Database | PostgreSQL 15 | <!-- or MySQL, SQLite --> |
| Migrations | Alembic | `alembic upgrade head` |
| Auth | JWT (python-jose) | <!-- or session-based --> |
| Validation | Pydantic v2 | Request/response models |
| Testing | pytest + httpx | `pytest tests/` |
| Deployment | Docker | `docker-compose up` |

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `main.py` | App setup, middleware registration | Understanding app bootstrap |
| `routes/*.py` | API endpoint definitions | Adding/modifying endpoints |
| `models/*.py` | Database schema + Pydantic schemas | Changing data structures |
| `services/*.py` | Business logic | Modifying behavior |
| `utils/database.py` | DB connection pool | Debugging connection issues |
| `utils/config.py` | All env vars / settings | Understanding configuration |

## API Endpoints

<!-- List the key endpoints -->

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/auth/login` | No | Get JWT token |
| GET | `/users/me` | Yes | Current user profile |
| GET | `/items` | Yes | List items (paginated) |
| POST | `/items` | Yes | Create item |

## Conventions

- **Route → Service → Model**: Routes never access DB directly
- **Pydantic models**: Separate `Create`, `Update`, `Response` schemas per entity
- **Error handling**: Raise `HTTPException` in routes, custom exceptions in services
- **Database**: Use async sessions, always close on exit
- **Environment**: All config via environment variables (never hardcoded)
- **Testing**: Each route file has a corresponding test file

## Gotchas

- Database URL format differs between sync (`postgresql://`) and async (`postgresql+asyncpg://`)
- Alembic `env.py` must import all models for auto-detection to work
- CORS middleware must be added BEFORE route registration in FastAPI
- JWT secret must match between token creation and validation middleware
