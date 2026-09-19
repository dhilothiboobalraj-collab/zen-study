# Zen Study

Zen Study is a private, adaptive Python practice space with confidence-aware assessments and progress tracking.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (legacy Node entrypoint; the managed API workflow runs Flask)
- `python artifacts/api-server/flask_app.py` — run the Flask API locally
- `pnpm --filter @workspace/zen-study run dev` — run the React frontend
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- SQLite data is stored at `artifacts/api-server/zen_study.sqlite3` during development and is ignored by git.
- Required env: `SESSION_SECRET` for signed Flask sessions.

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9, Python 3.11
- Frontend: React + Vite + Wouter + TanStack Query
- API: Python Flask
- DB: SQLite with parameterized SQL and server-side sessions
- Validation: OpenAPI-generated TypeScript hooks and server-side request validation
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/zen-study/src/` — learner-facing React app, auth, dashboard, path, quest, and progress screens.
- `artifacts/api-server/flask_app.py` — Flask API, SQLite schema, question bank, scoring, recommendations, and private calibration analysis.
- `lib/api-spec/openapi.yaml` — API contract source of truth.
- `lib/api-client-react/src/generated/` — generated React Query client hooks.

## Architecture decisions

- The browser never calls a model provider directly; question content and answer grading are server-owned.
- Confidence ratings are persisted with answer history and only returned to the signed-in student.
- SQLite keeps the Flask service portable while preserving real persistence and relational ownership boundaries.
- The original topic map and confidence-weighted mastery model were retained, with a richer React presentation.

## Product

- Students can create an account, sign in, practice adaptive Python topics, submit MCQ or code answers, rate confidence, and receive feedback.
- The dashboard shows mastery, XP, pace, activity, and personalized recommendations.
- Progress includes a private confidence calibration report with confident hits and misses.

## User preferences

No additional preferences recorded.

## Gotchas

- If the API contract changes, run `pnpm --filter @workspace/api-spec run codegen` before typechecking or editing hook consumers.
- The API artifact is configured to run `artifacts/api-server/flask_app.py`; do not switch it back to the legacy Express command without updating the artifact service configuration.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
