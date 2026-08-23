# HPSILab Quant Finance for WorkBuddy

> Professional quant finance tools for AI agents.

Use HPSILab's hosted Quant Finance MCP from WorkBuddy for stock research, options analysis, pre-trade risk, Monte Carlo simulation, and complete research reports. This repository contains only the open-source WorkBuddy integration and distribution files. HPSILab's backend and quantitative algorithms are not included.

## Install

After this repository is published, installation is two commands inside WorkBuddy:

```text
/plugin marketplace add haiyunsky/hpsilab-workbuddy
/plugin install hpsilab-workbuddy@hpsilab
```

Before publication, load it locally for development:

```bash
codebuddy --plugin-dir ./hpsilab-workbuddy
```

The default connection works without a secret and uses HPSILab's anonymous trial. WorkBuddy may ask you to approve the remote MCP server on first use.

For a persistent authenticated connection, either complete WorkBuddy's standard OAuth flow when prompted or set an HPSILab API key before starting WorkBuddy:

```bash
export HPSILAB_API_TOKEN="hpsi_your_key"
```

PowerShell:

```powershell
$env:HPSILAB_API_TOKEN = "hpsi_your_key"
```

Never commit an API key. Create or manage keys at [hpsilab.com/settings](https://hpsilab.com/settings).

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

The plugin connects directly to `https://hpsilab.com/mcp` using Streamable HTTP. Authentication, anonymous access, Credits, quota enforcement, and x402 payment challenges are owned by HPSILab and are not reimplemented here.

- Anonymous callers currently receive a limited daily trial.
- API keys are sent as `Authorization: Bearer` from `HPSILAB_API_TOKEN`.
- `get_pretrade_risk_scan` and `generate_stock_research_report` are Pro tools and may consume Credits or return an x402 payment challenge.
- A `401`, `402`, or `429` is reported to the user without automatic retry loops.
- WorkBuddy does not place trades through this plugin; HPSILab exposes research tools only.

Current access and pricing are documented by [HPSILab](https://hpsilab.com/pricing).

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
