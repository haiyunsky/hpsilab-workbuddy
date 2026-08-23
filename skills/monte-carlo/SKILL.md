---
name: monte-carlo
description: Run HPSILab's stock-price Monte Carlo simulation. Use for requests such as "Run Monte Carlo for NVDA".
---

# Monte Carlo

Extract and uppercase the ticker from `$ARGUMENTS` or the user's request. If it is ambiguous, ask for the ticker.

Call the HPSILab MCP tool `get_monte_carlo` once with `{"ticker":"NVDA"}`, replacing `NVDA` with the requested ticker.

Report the simulation horizon, number of paths when supplied, expected/mean close, likely range and confidence level, probability of finishing higher, as-of date, and limitations. Do not invent missing parameters or interpret simulated paths as forecasts or guarantees. State that the output is research, not investment advice.

On `isError: true`, 401, 402, or 429, explain the returned condition and stop. Include retry-after information when present, but never retry automatically.
