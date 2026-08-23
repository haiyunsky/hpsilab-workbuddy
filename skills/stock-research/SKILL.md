---
name: stock-research
description: Research a stock with HPSILab's aggregate quant analysis. Use for requests such as "Analyze NVDA" or a broad quantitative stock overview.
---

# Stock Research

Extract and uppercase the ticker from `$ARGUMENTS` or the user's request. If it is ambiguous, ask for the ticker.

Call the HPSILab MCP tool `analyze_stock` once with:

```json
{"symbol":"NVDA","refresh":false}
```

Replace `NVDA` with the requested ticker. Do not call the component tools afterward unless the user explicitly asks for deeper analysis; `analyze_stock` already aggregates them. Present the direction, direction score, bullish and bearish factors, source status, important risks, and data timestamp. Clearly distinguish partial results from complete results and state that the output is research, not investment advice.

Treat `isError: true`, `status: error`, or all sources being unavailable as failure. On 401, explain that authentication is required or the API key is invalid. On 402, show the server-provided payment/plan options and stop. On 429, show the limit and any retry-after time and stop. Do not automatically retry any of these responses.
