# deepsearch

A lightweight full-stack deep research assistant with a Vue frontend and a FastAPI backend.

The project accepts a research topic, breaks it into structured tasks, streams progress to the UI, and produces a final Markdown report. This repository has been cleaned for public publishing, so local secrets, machine-specific files, caches, and personal notes are excluded from version control.

## Highlights

- Vue 3 + Vite frontend for interactive research sessions
- FastAPI backend for orchestration and streaming updates
- Task-based research workflow with summaries and final report output
- Configurable search providers and OpenAI-compatible LLM backends
- Public-repo-safe setup with sensitive local files ignored by Git

## Tech Stack

- Frontend: Vue 3, TypeScript, Vite
- Backend: FastAPI, Python, uvicorn
- Model integration: OpenAI-compatible providers, local or remote
- Search integration: DuckDuckGo by default, with optional alternatives

## Project Structure

```text
deepsearch/
|- frontend/   # Vue 3 + Vite client
`- backend/    # FastAPI service and research workflow
```

## Quick Start

### 1. Start the backend

```bash
cd backend
cp .env.example .env
uv sync
uv run python src/main.py
```

### 2. Start the frontend

```bash
cd frontend
npm install
npm run dev
```

The frontend talks to `http://localhost:8000` by default. If needed, override it locally with `frontend/.env.local`.

## Configuration

Backend configuration lives in `backend/.env`. Common settings include:

- `LLM_PROVIDER`
- `LLM_MODEL_ID`
- `LLM_BASE_URL`
- `LLM_API_KEY`
- `SEARCH_API`

See [`backend/.env.example`](backend/.env.example) for the full template.

## Privacy Notes

The following are intentionally kept out of Git:

- API keys and local `.env` files
- Browser-side local environment overrides
- Generated notes and research artifacts from a local machine
- Python virtual environments and package caches
- Frontend dependency folders and production build output

## Development Notes

- Backend setup details are documented in [`backend/README.md`](backend/README.md).
- Frontend dependencies are locked with `package-lock.json`.
- Python dependencies are locked with `uv.lock`.

## License

MIT. See [`LICENSE`](LICENSE).
