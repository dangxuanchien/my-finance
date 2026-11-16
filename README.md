# my-finance
A scalable personal finance platform with bank statement import, transaction analytics, budgeting, and AI-powered financial insights.

## Backend

The backend is a NestJS application located in `backend/`. It uses Prisma for PostgreSQL access and exposes its API documentation through Swagger.

### Prerequisites

- Node.js 22 LTS
- Docker Desktop with Docker Compose

### Start PostgreSQL

From the repository root, create a local environment file:

```powershell
Copy-Item .env.example .env
```

The example values are for local development only. Change `POSTGRES_PASSWORD` in `.env`, then copy the backend environment template:

```powershell
Copy-Item backend\.env.example backend\.env
```

Keep the PostgreSQL credentials in `backend/.env` aligned with `.env`, then start PostgreSQL:

```powershell
docker compose up -d postgres
docker compose ps
```

To also start pgAdmin, use the optional `tools` profile:

```powershell
docker compose --profile tools up -d
```

pgAdmin is available at `http://localhost:5050`. Register a server with host `postgres`, port `5432`, and the same username, password, and database from the root `.env`. The default host port for PostgreSQL is `5433` to avoid conflicts with a local PostgreSQL installation; keep `POSTGRES_PORT` in the root `.env` aligned with the port in `backend/.env`.

### Run the backend

From the repository root, configure the local backend environment as above, then run:

```powershell
cd backend
npm install
npx prisma generate
'SELECT 1;' | npx prisma db execute --stdin --schema prisma/schema.prisma
npm run start:dev
```

The health endpoint is available at `http://localhost:3000/health`, and Swagger UI is at `http://localhost:3000/api/docs`.

PostgreSQL data is persisted in the `postgres_data` Docker volume. Use `docker compose down -v` only when you intentionally want to delete that local database data.
