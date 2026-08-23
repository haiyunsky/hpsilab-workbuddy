---
name: pre-trade-risk
description: Evaluate pre-trade stock risk with HPSILab. Use for requests such as "Evaluate the risk of buying NVDA" before a proposed equity trade.
---

# Pre-Trade Risk

Extract and uppercase the ticker from `$ARGUMENTS` or the user's request. If it is ambiguous, ask for the ticker.

Call the HPSILab MCP tool `get_pretrade_risk_scan` once with `{"symbol":"NVDA"}`, replacing `NVDA` with the requested ticker. This is a Pro tool; do not call other tools first as a capability probe.

Summarize the returned risk level, key risk drivers, volatility/downside information, warnings, and practical decision checks. Do not turn the result into a buy/sell instruction. State that it is research, not investment advice.

Treat `isError: true` or `status: error` as failure. On 401, explain the authentication action named by the server. On 402, explain the exact price, network, and payment or plan options returned by HPSILab; do not claim payment occurred. On 429, show the quota/rate-limit detail and any retry-after time. Never retry automatically.
