# Market data UI — reference

## Sandbox toggle

```javascript
// src/utils/config.js
export const isUpstoxsWs = import.meta.env.VITE_IS_SANDBOX === 'false';
```

## Protobuf

`public/MarketDataFeedV3.proto` — grep only, do not bulk-read

## TV backend API

`GET/POST/DELETE /api/tv/1.1/charts` — `C:\sai\trade-dashboard-backend\src\controller\tv.js`

## Upstox backend sibling

`C:\sai\trade-dashboard-backend` — `upstox-backend` skill for OAuth, WS server, cron
