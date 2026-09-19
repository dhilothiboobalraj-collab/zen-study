# Zen Study

A private, adaptive Python learning platform with a React frontend and Flask API.

## Included

- `artifacts/zen-study` — React/Vite frontend
- `artifacts/api-server/flask_app.py` — Flask API, SQLite schema, authentication, assessments, recommendations, and progress analysis
- `lib/api-spec/openapi.yaml` — API contract
- `lib/api-client-react` and `lib/api-zod` — generated API client libraries
- `pyproject.toml`, `uv.lock`, and `requirements.txt` — Python dependency configuration
- `original/` — original uploaded HTML frontend

## Run locally

1. Install Node.js 24+, pnpm, and Python 3.11+.
2. Install frontend dependencies with `pnpm install`.
3. Install Python dependencies with `python -m pip install -r requirements.txt`.
4. Set `SESSION_SECRET` to a private random value.
5. Start the Flask API from `artifacts/api-server` with `python flask_app.py` on port 8080.
6. Start the frontend with `PORT=5173 BASE_PATH=/ pnpm --filter @workspace/zen-study run dev`.

The Flask service creates `artifacts/api-server/zen_study.sqlite3` automatically on first start. Do not commit that local database file.
