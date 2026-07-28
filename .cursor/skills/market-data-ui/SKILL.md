---
name: market-data-ui
description: Works with Upstox WebSocket, sandbox feed, protobuf market data, and TradingView chart wrappers in trade-dashboard-nk. Use for useUpstoxWS, VITE_IS_SANDBOX, live prices, or TV chart/datafeed changes.
disable-model-invocation: true
---

# Market data UI (frontend)

## WebSocket / live feed

| File | Purpose |
|------|---------|
| `src/hooks/useUpstoxWS.js` | Live vs sandbox |
| `src/hooks/useMarketDataSocket.js` | Protobuf decode |
| `src/utils/config.js` | `isUpstoxsWs` from `VITE_IS_SANDBOX` |
| `src/App.jsx` | Global WS init |

Grep symbol before read — use offset/limit on large hooks.

Env: `VITE_IS_SANDBOX=false` → live WS; `true` → sandbox feed.

## TradingView (allowed paths only)

**Never read** `public/charting_library/` or `src/charting_library/`.

| Path | Purpose |
|------|---------|
| `src/Components/TradingView/TVChartContainer/` | Chart mount |
| `src/Components/TradingView/datafeed/` | Custom datafeed |
| Backend `src/controller/tv.js` | Chart save/load API |

Env: `VITE_UPSTOXS_ANALYTICS_TOKEN` for news/fundamentals in `useTVChartContainer.js`.

## Redux targets

Live prices flow to `src/Store/upstoxs.js`, `paperTradeSlice.js` (`updatePaperHoldingsLTP`).

## Additional resources

- [reference.md](reference.md)
