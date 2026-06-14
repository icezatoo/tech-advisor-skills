# Tech Catalog

A starting catalog of modern, widely-adopted tools by category. These are **starting signals, not final answers** — always re-verify currency and fit at use time, and prefer what matches the existing stack.

> The catalog deliberately lists a primary option plus alternatives so recommendations always carry choices.

## HTTP clients

| Language | Primary | Alternatives |
| --- | --- | --- |
| Go | Resty | net/http, Heimdall (resilience) |
| Node/TS | undici / native fetch | axios, got, ky |
| Python | httpx | requests, aiohttp |
| Java | Spring WebClient | OkHttp, Apache HttpClient |

## Logging / observability

| Language | Primary | Alternatives |
| --- | --- | --- |
| Go | slog (stdlib) | zap, zerolog |
| Node/TS | pino | winston |
| Python | structlog | logging (stdlib), loguru |
| Cross-cutting | OpenTelemetry | vendor SDKs (Datadog, etc.) |

## Testing

| Language | Primary | Alternatives |
| --- | --- | --- |
| Go | stdlib testing + testify | gomock, httptest |
| Node/TS | Vitest | Jest, Playwright (e2e) |
| Python | pytest | unittest, hypothesis |
| Java | JUnit 5 | Testcontainers, Mockito |

## Frontend

| Need | Primary | Alternatives |
| --- | --- | --- |
| App framework | Next.js / React | Nuxt/Vue, SvelteKit, Astro |
| State | TanStack Query + Zustand | Redux Toolkit, Jotai |
| Styling | Tailwind CSS | CSS Modules, vanilla-extract |
| Forms | React Hook Form + Zod | Formik |

## Backend / API

| Need | Primary | Alternatives |
| --- | --- | --- |
| Node API | Fastify / NestJS | Express, Hono |
| Python API | FastAPI | Django REST, Flask |
| Validation | Zod (TS) / Pydantic (Py) | io-ts, marshmallow |
| Queue | BullMQ (Redis) | RabbitMQ, SQS, Kafka |

## Data

| Need | Primary | Alternatives |
| --- | --- | --- |
| SQL DB | PostgreSQL | MySQL, SQLite (embedded) |
| ORM (TS) | Prisma / Drizzle | TypeORM |
| Cache | Redis | Memcached, in-process LRU |
| Search | OpenSearch / Meilisearch | Elasticsearch, Typesense |

## DevOps / platform

| Need | Primary | Alternatives |
| --- | --- | --- |
| Containers | Docker | Podman |
| Orchestration | Kubernetes | Nomad, ECS |
| CI/CD | GitHub Actions | GitLab CI, CircleCI |
| IaC | Terraform / OpenTofu | Pulumi, CDK |

## Maintenance note

Catalogs age. Before recommending, confirm the tool is still actively maintained (see `popularity-criteria.md`) and matches the project's language, runtime, and constraints.
