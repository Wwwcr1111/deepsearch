# HelloAgents Deep Research

A lightweight full-stack deep research assistant with a Vue frontend and a FastAPI backend.

This repository is organized for public sharing. Local secrets, machine-specific settings, caches, notes, and dependency directories are intentionally excluded from version control.

## Project Structure

```text
helloagents-deepresearch/
├─ frontend/   # Vue 3 + Vite client
└─ backend/    # FastAPI service and research workflow
```

## What The App Does

- Accepts a research topic from the browser UI
- Streams structured task progress from the backend
- Aggregates notes, summaries, and a final Markdown report
- Supports configurable web search and OpenAI-compatible LLM backends

## Local Development

### Backend

```bash
cd backend
cp .env.example .env
uv sync
uv run python src/main.py
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

By default the frontend talks to `http://localhost:8000`. You can override that locally with `frontend/.env.local`.

## Privacy And Safety

The following are kept out of Git on purpose:

- API keys and local `.env` files
- Browser-facing local env overrides
- Research notes generated on a developer machine
- Python virtual environments and package caches
- Frontend dependency folders and build output

## Publishing Notes

Before pushing to GitHub, verify that:

1. `backend/.env` is not staged.
2. `frontend/.env.local` is not staged.
3. `backend/notes/`, `backend/.venv/`, and `frontend/node_modules/` are not staged.

## License

MIT. See `LICENSE`.
