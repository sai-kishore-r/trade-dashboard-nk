# AGENTS.md — trade-dashboard-nk

Instructions for AI agents working in this repository.

## Project overview

React 18 SPA (Vite 5) for a trading dashboard: watchlist, charts (TradingView), paper trading, market breadth, scans, and Upstox integration. State managed with **Redux Toolkit**. UI built with **MUI v7**.

**Sibling repo:** Backend API at `C:\sai\trade-dashboard-backend` — runs on port **3015**.

## Essential commands

```bash
npm install           # Install dependencies
npm run dev           # Vite dev server (port from VITE_PORT, default 5173)
npm run build         # Production build → dist/
npm run lint          # ESLint (max 0 warnings)
npm run test          # Jest (upstoxs.spec.js)
npm run preview       # Preview production build
```

Deployed via **AWS Amplify** (`amplify.yml`) — env vars must be set at **build time**.

## Architecture

```
src/main.jsx           # Entry — Redux Provider, BrowserRouter, axios interceptors
src/App.jsx            # Routes, auth guards, global WS/data init
src/utils/config.js    # Central BACKEND_URL and isUpstoxsWs flag
src/utils/axiosSetup.js # Global 401 interceptor (logout on backend 401)
src/Store/             # Redux slices (auth, upstoxs, portfolio, paperTrade, etc.)
src/Components/        # UI components
src/hooks/             # WebSocket hooks (Upstox, sandbox, portfolio)
public/charting_library/  # TradingView library (vendored — avoid editing)
```

### Redux slices (`src/Store/index.js`)

| Slice | File | Purpose |
|-------|------|---------|
| `auth` | `authSlice.js` | App JWT + Upstox token |
| `orders` | `upstoxs.js` | Orders, metrics, Upstox API |
| `portfolio` | `portfolio.js` | Holdings, user settings |
| `paperTrade` | `paperTradeSlice.js` | Paper trading |
| `marketBreadth` | `marketBreadth.js` | Market breadth data |
| `marketStatus` | `marketStatusSlice.js` | Market timings, holidays |
| `settings` | `settings.js` | User preferences |

### API integration patterns

1. **Backend URL:** Import `BACKEND_URL` from `src/utils/config.js` — do not hardcode
2. **App auth:** JWT in `localStorage.getItem('token')`; Upstox token in Redux `state.auth.token`
3. **HTTP:** Axios for backend; fetch for Upstox direct APIs
4. **Async state:** `createAsyncThunk` + `createSlice` pattern throughout Store
5. **WebSockets:** `useUpstoxWS` toggles live vs sandbox via `VITE_IS_SANDBOX`

### Known inconsistencies (do not replicate)

- `src/Components/molicules/SAInsights.jsx` — hardcodes `localhost:5000/api` instead of `config.js`
- `src/Components/Watchlist/OrderPanel.jsx` — hardcodes `localhost:3015/place-order`
- `upstoxs.js` / `marketBreadth.js` use `VITE_ENV` + `VITE_PROD_HOST`; most other files use `VITE_BACKEND_URL`

## Environment variables

All `VITE_*` vars are injected at **build time** via Vite. Set in `.env` (gitignored).

| Variable | Default | Purpose |
|----------|---------|---------|
| `VITE_PORT` | `5173` | Dev server port |
| `VITE_BACKEND_URL` | `http://localhost:3015` | Backend API base URL |
| `VITE_ENV` | — | `'DEV'` → localhost; else uses `VITE_PROD_HOST` |
| `VITE_PROD_HOST` | — | Production backend URL |
| `VITE_IS_SANDBOX` | — | `'false'` → live Upstox WS; otherwise sandbox feed |
| `VITE_UPSTOXS_ACCESS_KEY` | — | Upstox API bearer token fallback |
| `VITE_UPSTOXS_ANALYTICS_TOKEN` | — | Upstox news/fundamentals |
| `VITE_UPSTOXS_SANDBOX_ACCESS_KEY` | — | Sandbox order auth |
| `VITE_UPSTOXS_SANDBOX_BASE_URL` | — | Sandbox order API base |

## Coding conventions

- **ES modules**, JSX in `.jsx` files
- **ESLint** (`.eslintrc.cjs`): React 18, hooks rules, react-refresh
- **Folder naming quirks:** `molicules` (not `molecules`), `usePorfolio.js` (typo) — match existing names
- **Routing:** `ProtectedRoute` / `PublicRoute` in `App.jsx` check `localStorage.token`
- **Components:** Functional components with hooks; MUI for UI

## Do / Don't

**Do:**

- Use `BACKEND_URL` from `config.js` for new backend calls
- Follow `createAsyncThunk` pattern for new async Redux logic
- Run `npm run lint` before finishing
- Prefer editing `src/` over vendored `charting_library/`

**Don't:**

- Hardcode backend URLs in new code
- Edit `public/charting_library/` or `src/charting_library/` unless necessary
- Commit `.env` files
- Assume SSR — this is a static SPA

## Verification

1. `npm run lint` — no errors
2. `npm run dev` — app loads on `http://localhost:5173`
3. Backend running on 3015 — login/signup flow works

## Token optimization

| Rule | Action |
|------|--------|
| Search before read | Grep/Glob `src/Store`, `src/Components`, hook names |
| Never bulk-read | `charting_library/`, `universe.json`, lock files, `node_modules/` |
| Narrow reads | `offset`/`limit`; ~80 lines max unless editing |
| Start tasks | Read [SKILLS.md](SKILLS.md) or run `/find-context` first |
| Cross-repo | Open backend only when API/auth contracts change |
| Budget | One skill + one `reference.md` per task |

Always-on rules: `.cursor/rules/token-optimization.mdc`, `.trae/rules/token-optimization.md`

## Skills

Project skills — see [SKILLS.md](SKILLS.md). Load **one** skill per task:

| Skill | When |
|-------|------|
| `trade-feature` | Redux, UI components, API integration |
| `market-data-ui` | WebSocket, sandbox feed, TradingView wrappers |

Cursor review skills:

| Skill | When to use |
|-------|-------------|
| `/review-bugbot` | Full bug review via Bugbot subagent |
| `/review-security` | Security-focused review |

## Commands

| Command | Purpose |
|---------|---------|
| `/find-context <task>` | Gather context; reads SKILLS.md first |
| `/review-staged` | Review git staged changes before commit |

## IDE support

This repo is configured for multiple AI IDEs. **`AGENTS.md` is the canonical source** — other files point here or mirror these instructions.

| IDE | Instructions file | Slash commands |
|-----|-------------------|----------------|
| **Cursor** | `AGENTS.md` | `.cursor/commands/find-context.md`, `.cursor/commands/review-staged.md` |
| **Trae** | `AGENTS.md`, `.trae/rules/project.md` | `.trae/commands/find-context.md`, `.trae/commands/review-staged.md` |
| **VS Code** (GitHub Copilot) | `.github/copilot-instructions.md` | `.github/prompts/find-context.prompt.md`, `.github/prompts/review-staged.prompt.md` |
| **Claude Code** | `CLAUDE.md` | — |

**VS Code setup:** `.vscode/settings.json` enables `chat.promptFiles`. Type `/find-context` or `/review-staged` in Copilot Chat.

**Trae setup:** Enable **Include AGENTS.md** in Settings → Rules.
