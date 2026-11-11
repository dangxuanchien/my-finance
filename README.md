# my-finance
A scalable personal finance platform with bank statement import, transaction analytics, budgeting, and AI-powered financial insights.

## Backend

The backend is a NestJS application located in `backend/`. It uses Prisma for PostgreSQL access and exposes its API documentation through Swagger.

### Prerequisites

- Node.js 22 LTS
- PostgreSQL

### Run locally

From the repository root, run:

```powershell
cd backend
npm install
Copy-Item .env.example .env
```

Set `DATABASE_URL` in `backend/.env` to your PostgreSQL connection string, then run:

```powershell
npx prisma generate
npm run start:dev
```

The health endpoint is available at `http://localhost:3000/health`, and Swagger UI is at `http://localhost:3000/api/docs`.
