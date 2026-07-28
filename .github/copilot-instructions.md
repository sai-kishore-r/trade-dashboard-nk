# GitHub Copilot instructions — trade-dashboard-nk

> **Canonical source:** [AGENTS.md](../AGENTS.md) — apply every section of that file when working in this repository.

## Project

React 18 + Vite 5 trading dashboard SPA (port **5173**). Redux Toolkit, MUI v7, TradingView charts.

**Sibling repo:** Backend at `C:\sai\trade-dashboard-backend` (port 3015).

## Commands

```bash
npm install && npm run dev   # Dev server on 5173
npm run lint               # ESLint (max 0 warnings)
npm run test               # Jest
npm run build              # Production build
```

## Rules

- Use `BACKEND_URL` from `src/utils/config.js` — do not hardcode backend URLs
- Redux async: `createAsyncThunk` + `createSlice` pattern
- JWT in `localStorage`; Upstox token in Redux `state.auth.token`
- Do not edit vendored `charting_library/` unless necessary
- `VITE_*` env vars are build-time only (Amplify CI)

## Slash prompts

Use `/find-context` or `/review-staged` from `.github/prompts/`.

## Skills

Read [SKILLS.md](../SKILLS.md) — load one skill: `trade-feature` or `market-data-ui`.

## Token rules

Grep before read. Never bulk-read `charting_library/` or `universe.json`. Token rules in `.cursor/rules/token-optimization.mdc`.

## Verification

`npm run lint` → `npm run dev` → login flow against backend on 3015
