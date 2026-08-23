---
name: research-report
description: Create a complete HPSILab stock research report with quantitative analysis and charts. Use for requests such as "Create a complete NVDA research report".
---

# Research Report

Extract and uppercase the ticker from `$ARGUMENTS` or the user's request. If it is ambiguous, ask for the ticker.

Call the HPSILab MCP tool `generate_stock_research_report` exactly once with:

```json
{"symbol":"NVDA","refresh":false,"force_images":false}
```

Replace `NVDA` with the requested ticker. This Pro tool already composes the aggregate analysis and chart generation; do not call `analyze_stock` or `generate_stock_images` separately. Return the server's Markdown report and preserve chart links, source status, warnings, and as-of dates. Note partial modules explicitly. State that the output is research, not investment advice.

This tool is non-idempotent and can consume 30 Credits or require x402 payment. Never retry it automatically. On 401, explain the authentication action returned by the server. On 402, show the exact payment/plan details and do not claim payment occurred. On 429, show the quota detail and any retry-after time, then stop.
