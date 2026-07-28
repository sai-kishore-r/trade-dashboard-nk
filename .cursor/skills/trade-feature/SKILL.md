---
name: trade-feature
description: Adds Redux slices, thunks, MUI components, and routes in trade-dashboard-nk. Use for new UI features, API integration from frontend, createAsyncThunk, or cross-repo API changes.
disable-model-invocation: true
---

# Trade feature (frontend)

## Checklist

```
- [ ] Grep slice/feature in src/Store/ and src/Components/
- [ ] createAsyncThunk + createSlice (paperTradeSlice.js pattern)
- [ ] BACKEND_URL from config.js; JWT from localStorage
- [ ] Register reducer in src/Store/index.js
- [ ] MUI component; route in App.jsx if new page
- [ ] ProtectedRoute if auth required
- [ ] npm run lint
```

## Redux + API

1. Thunk: `axios` to `${BACKEND_URL}/...` with `Authorization: Bearer ${token}`
2. User id: `JSON.parse(localStorage.getItem('user')).id || user._id`
3. Slice: `extraReducers` for pending/fulfilled/rejected
4. Register in `src/Store/index.js`

## UI

- Place under `src/Components/` (folder: `molicules` spelling)
- Functional components, MUI v7, hooks
- New page: route in `App.jsx` under `<Navbar />` layout

## Cross-repo

New backend endpoint needed? Flag `C:\sai\trade-dashboard-backend` — use backend `trade-api` skill there.

Known URL debt (fix if same area): `SAInsights.jsx`, `OrderPanel.jsx` hardcode URLs.

## Do not

- Hardcode backend URLs — use `config.js`
- Edit `charting_library/` unless unavoidable

## Additional resources

- [reference.md](reference.md)
