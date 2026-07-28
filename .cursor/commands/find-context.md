# /find-context

Gather relevant context for a task before making code changes. **Do not edit any files.**

## Input

Parse the user's task from the text after `/find-context`. If no task is provided, ask what they want to work on.

## Steps

0. **Read SKILLS.md** — pick one of two skills (`trade-feature` or `market-data-ui`); load only that skill file

1. **Identify scope** — Determine which feature, component, slice, or bug the task relates to.

2. **Search this repo** — Use grep and glob to find:
   - Components in `src/Components/`
   - Redux slices and thunks in `src/Store/`
   - Hooks in `src/hooks/`
   - Config and utils in `src/utils/` (especially `config.js`, `axiosSetup.js`)
   - Routes and guards in `src/App.jsx`
   - Tests in `src/**/*.spec.js` or `src/**/*.test.js`

3. **Check sibling repo** — If the task touches API calls, auth, or backend contracts, also search:
   - `C:\sai\trade-dashboard-backend` for controllers, routes, and `dbWrapper` methods

4. **Trace data flow** — Map the path, e.g.:
   - Component → `dispatch(thunk)` → `BACKEND_URL` + endpoint → backend controller
   - `useUpstoxWS` → WebSocket → Redux state update → component re-render

5. **Read AGENTS.md** — Note conventions, env vars, and do/don't rules from the repo root `AGENTS.md`.

## Output format

Return a structured summary:

### Task
(One-line restatement of the goal)

### Relevant files
(Bullet list with paths and one-line purpose each)

### Data flow
(Short description or bullet chain)

### Conventions to follow
(From AGENTS.md and existing code patterns)

### Environment variables involved
(Any `VITE_*` keys that affect this area)

### Suggested next steps
(Ordered list of what to change or investigate)

**Do not make code changes.** Context gathering only.
