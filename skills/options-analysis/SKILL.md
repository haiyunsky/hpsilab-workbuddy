---
name: options-analysis
description: Analyze a stock's options volatility and positioning with HPSILab. Use for requests such as "Analyze NVDA options".
---

# Options Analysis

Extract and uppercase the ticker from `$ARGUMENTS` or the user's request. If it is ambiguous, ask for the ticker.

Make exactly these two HPSILab MCP calls, preferably in parallel:

1. `get_iv_radar` with `{"ticker":"NVDA","refresh":false}`
2. `get_option_pressure` with `{"ticker":"NVDA"}`

Replace `NVDA` with the requested ticker. Combine IV level/structure, squeeze score, risk reversal, Max Pain, Gamma Wall, likely weekly high, and squeeze target. Preserve each tool's as-of date and warnings. Do not add `analyze_stock` unless the user also requests a broad equity view.

Use any successful result if the other call fails and label the answer partial. On 401, 402, or 429, report the server response and stop that failed branch without retrying. Never loop. State that the output is research, not investment advice.
