# CONTEXT.md — API Service

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a [REST/GraphQL] API service that [provides X data/functionality to Y consumers].

- **Consumers**: [frontend app / mobile app / third-party integrations]
- **Auth**: [API keys / OAuth 2.0 / JWT]
- **Base URL**: `https://api.example.com/v1`

## Architecture

```
api-service/
├── src/
│   ├── app.ts                # Express/Fastify app setup
│   ├── routes/
│   │   ├── v1/
│   │   │   ├── users.ts      # /v1/users endpoints
│   │   │   ├── products.ts   # /v1/products endpoints
│   │   │   └── webhooks.ts   # /v1/webhooks
│   │   └── health.ts         # /health check
│   ├── controllers/          # Request handling logic
│   ├── services/             # Business logic
│   ├── models/               # Database models
│   ├── middleware/
│   │   ├── auth.ts           # Authentication
│   │   ├── rateLimit.ts      # Rate limiting
│   │   ├── validate.ts       # Request validation (Zod/Joi)
│   │   └── errorHandler.ts   # Global error handler
│   ├── utils/
│   │   ├── database.ts       # DB connection
│   │   ├── cache.ts          # Redis cache layer
│   │   └── logger.ts         # Structured logging
│   └── types/
│       └── index.ts
├── prisma/                   # Prisma schema & migrations
│   └── schema.prisma
├── tests/
├── docker-compose.yml
└── package.json
```

### Request Pipeline

```
Request → Rate Limit → Auth → Validate → Controller → Service → DB/Cache → Response
                                                                    ↓
                                                              Error Handler
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Runtime | Node.js 20 | <!-- or Deno, Bun --> |
| Framework | Express 4.x | <!-- or Fastify, Hono --> |
| Language | TypeScript 5.x | Strict mode |
| ORM | Prisma | <!-- or Drizzle, TypeORM --> |
| Database | PostgreSQL 15 | Primary data store |
| Cache | Redis 7 | Session + query cache |
| Validation | Zod | Request/response schemas |
| Auth | JWT + API Keys | Different auth for different consumers |
| Logging | Pino | JSON structured logs |
| Deployment | Docker + K8s | <!-- or serverless --> |

## API Overview

### Authentication

```
# API Key (for server-to-server)
Authorization: Bearer sk_live_xxxx

# JWT (for user sessions)
Authorization: Bearer eyJhbG...
```

### Key Endpoints

| Method | Path | Auth | Rate Limit | Description |
|--------|------|------|------------|-------------|
| GET | `/v1/products` | API Key | 100/min | List products |
| GET | `/v1/products/:id` | API Key | 100/min | Get product |
| POST | `/v1/products` | JWT (admin) | 20/min | Create product |
| POST | `/v1/webhooks` | API Key | 10/min | Register webhook |
| GET | `/health` | None | — | Health check |

### Error Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "details": [{ "field": "email", "issue": "must be valid email" }]
  }
}
```

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `prisma/schema.prisma` | Database schema | Changing data model |
| `middleware/auth.ts` | Auth logic + API key validation | Auth issues |
| `middleware/rateLimit.ts` | Rate limit config per route | Adjusting limits |
| `services/*.ts` | All business logic | Modifying behavior |

## Conventions

- **Versioned routes**: All routes under `/v1/`, enables future breaking changes
- **Controller → Service**: Controllers handle HTTP, services handle logic
- **Validation**: Zod schemas co-located with route files
- **Errors**: All errors go through `errorHandler.ts`, consistent format
- **Logging**: Every request logged with correlation ID
- **Pagination**: Cursor-based (`?cursor=xxx&limit=20`), not offset

## Gotchas

- Rate limits are per API key, not per IP
- Webhook delivery: At-least-once — consumers must handle duplicates
- Database connections: Pool size = 10 by default, increase for high traffic
- Redis: Used for both cache AND rate limiting — separate instances in production
- Prisma migrations: Run `npx prisma migrate deploy` (not `dev`) in production
