# HPSILab Quant Finance for WorkBuddy

> Professional quant finance tools for AI agents.

Use HPSILab's 9 public Quant Tools from WorkBuddy for stock research, options analysis, pre-trade risk, Monte Carlo simulation, and complete research reports. The same HPSILab capabilities are also available through REST APIs and the Python and TypeScript SDKs. See [HPSILab Developer V2](https://hpsilab.com/developer/v2) for the current public product definition.

This repository contains only the open-source WorkBuddy integration and distribution files. HPSILab's backend and quantitative algorithms are not included.

## Install

Installation is two commands inside WorkBuddy:

```text
/plugin marketplace add haiyunsky/hpsilab-workbuddy
/plugin install hpsilab-workbuddy@hpsilab
```

For local development, load it directly:

```bash
codebuddy --plugin-dir ./hpsilab-workbuddy
```

The plugin connects to `https://hpsilab.com/mcp`. WorkBuddy may ask you to approve the remote MCP server on first use. HPSILab supports OAuth 2.1 with Dynamic Client Registration (DCR), so an OAuth-capable MCP client can open the sign-in flow without requiring an API key in the plugin.

API keys remain available for REST, SDK, and manually authenticated MCP clients. Configure them through the client's secure authentication settings as an `Authorization: Bearer` credential. Never commit an API key. Create or manage keys at [hpsilab.com/settings](https://hpsilab.com/settings).

## Use

```text
Install plugin
     ↓
"Analyze NVDA"
     ↓
WorkBuddy
     ↓
HPSILab MCP
     ↓
Structured analysis
```

Try:

- `Analyze NVDA`
- `Analyze NVDA options`
- `Evaluate the risk of buying NVDA`
- `Run Monte Carlo for NVDA`
- `Create a complete NVDA research report`

The five included Skills minimize calls and Credit usage. Broad stock research uses the aggregate `analyze_stock` tool once. A complete report uses the composite `generate_stock_research_report` tool once rather than rebuilding it from component calls.

## Access, Credits, and errors

The plugin connects directly to `https://hpsilab.com/mcp` using Streamable HTTP. OAuth 2.1/DCR, API-key authentication, trial access, Credits, quota enforcement, and x402 are owned by HPSILab and are not reimplemented here.

- API keys use the `Authorization: Bearer` scheme when configured by the client.
- Tool calls may consume Credits according to the current HPSILab product policy.
- Wallet-enabled agents may use x402 when offered by HPSILab; other clients can use OAuth or an API key.
- A `401`, `402`, or `429` is reported to the user without automatic retry loops.
- WorkBuddy does not place trades through this plugin; HPSILab exposes research tools only.

Credit costs, trial terms, x402 availability, supported SDKs, and tool access can change. [HPSILab Developer V2](https://hpsilab.com/developer/v2) is the source of truth; this repository intentionally does not duplicate its detailed pricing table.

## Why `tools/list` returns 10 tools

Developer V2 defines 9 public Quant Tools. The MCP server additionally exposes `register_account`, an account/authentication utility that creates a free HPSILab account and returns an API key. It performs no stock, options, simulation, risk, or research analysis, so it is not counted among the 9 Quant Tools.

## Skills and MCP tools

| Skill | Primary MCP tool(s) | Calls |
| --- | --- | ---: |
| Stock Research | `analyze_stock` | 1 |
| Options Analysis | `get_iv_radar`, `get_option_pressure` | 2 |
| Pre-Trade Risk | `get_pretrade_risk_scan` | 1 |
| Monte Carlo | `get_monte_carlo` | 1 |
| Research Report | `generate_stock_research_report` | 1 |

## Development checks

Validate and load the plugin with a current WorkBuddy/CodeBuddy CLI:

```bash
codebuddy plugin validate .
codebuddy --plugin-dir .
```

Then confirm the `hpsilab` MCP server connects, its tools appear, and invoke one low-cost read-only tool. Do not repeatedly invoke Pro or non-idempotent tools during smoke tests.

## License

MIT. See [LICENSE](LICENSE).

All financial outputs are for research and informational use only and are not investment advice.
