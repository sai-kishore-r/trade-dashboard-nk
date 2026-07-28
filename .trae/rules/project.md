---
description: Core project conventions for trade-dashboard-nk frontend. Always follow AGENTS.md.
alwaysApply: true
---

# Project rules — trade-dashboard-nk

Follow **AGENTS.md** and **SKILLS.md** at the repository root.

## Essentials

- React 18 + Vite 5 SPA on port **5173**; package manager is **npm**
- Use `BACKEND_URL` from `src/utils/config.js`
- Redux: `createAsyncThunk` + `createSlice`
- Sibling backend: `C:\sai\trade-dashboard-backend` (port 3015)
- Run `npm run lint` before finishing changes

## Skills (load one per task)

- `trade-feature` — Redux, UI, API integration
- `market-data-ui` — WebSocket, TradingView wrappers

## Commands

- `/find-context <task>` — reads SKILLS.md, gathers context
- `/review-staged` — review staged git changes
