# Code Base Link

This repository is a `pnpm` workspace with two main apps:

- `artifacts/api-server`: Express API for RAG, image description, and chat endpoints
- `artifacts/rag-bot`: React + Vite frontend chat UI

The project has been adjusted for local Windows development:

- no PostgreSQL is required
- no Replit files are required
- no Unix shell is required for install
- OpenAI credentials are optional

## Prerequisites

- Node.js 20 or newer
- `pnpm` 10 or newer

Install `pnpm` if needed:

```powershell
npm install -g pnpm
```

## Install

From the repository root:

```powershell
cd C:\Users\IKIO\parul\Code-Base-Link\Code-Base-Link
pnpm install
```

## Local Data

The API now persists data in:

`artifacts/api-server/data/local-db.json`

That file stores:

- seeded knowledge-base documents
- document chunks
- query history cache
- conversations
- messages

## Optional Environment Variables

Backend:

- `PORT` default: `3001`
- `AI_INTEGRATIONS_OPENAI_API_KEY`
- `AI_INTEGRATIONS_OPENAI_BASE_URL` default: `https://api.openai.com/v1`
- `OPENAI_MODEL` default: `gpt-4o-mini`

Frontend:

- `PORT` default: `5173`
- `BASE_PATH` default: `/`
- `API_BASE_URL` default: `http://localhost:3001`

If you want OpenAI enabled, set:

```powershell
$env:AI_INTEGRATIONS_OPENAI_API_KEY = "your-api-key"
$env:AI_INTEGRATIONS_OPENAI_BASE_URL = "https://api.openai.com/v1"
$env:OPENAI_MODEL = "gpt-4o-mini"
```

If you do not set these variables, the app still runs:

- RAG uses local extractive fallback
- image description returns a local fallback caption
- OpenAI chat/image endpoints return fallback behavior or a clear disabled message

## Run Locally

Open two PowerShell terminals.

### Terminal 1: API server

```powershell
cd C:\Users\IKIO\parul\Code-Base-Link\Code-Base-Link
$env:PORT = "3001"
pnpm --filter @workspace/api-server dev
```

API URL:

`http://localhost:3001`

### Terminal 2: Frontend

```powershell
cd C:\Users\IKIO\parul\Code-Base-Link\Code-Base-Link
$env:PORT = "5173"
$env:BASE_PATH = "/"
$env:API_BASE_URL = "http://localhost:3001"
pnpm --filter @workspace/rag-bot dev
```

Frontend URL:

`http://localhost:5173`

## Useful Commands

Type check:

```powershell
pnpm typecheck
```

Build everything:

```powershell
pnpm build
```

## Notes

- The frontend proxies `/api` requests to the API server during local development.
- The API seeds its local knowledge base automatically on first start.
- The workspace still prefers `pnpm`; `npm` and `yarn` are intentionally blocked.
