# Trade feature — reference

## Canonical example

`src/Store/paperTradeSlice.js` — `executePaperOrder`, `fetchPaperTradesAsync`

## Config

```javascript
import { BACKEND_URL } from '../utils/config';
```

## Store

`src/Store/index.js` — add reducer to `configureStore`

## Routes

```jsx
<Route path="/my-page" element={<ProtectedRoute><MyPage /></ProtectedRoute>} />
```

## Sibling backend

`C:\sai\trade-dashboard-backend` — port 3015, `trade-api` skill for new endpoints
