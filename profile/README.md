[![Valuein — Financial Data Infrastructure](https://www.valuein.biz/valuein/colored_logo_no_bg.png)](https://valuein.biz)

[![Website](https://img.shields.io/badge/website-valuein.biz-purple)](https://valuein.biz)
[![PyPI](https://img.shields.io/pypi/v/valuein-sdk?label=valuein-sdk&cacheSeconds=300)](https://pypi.org/project/valuein-sdk/)
[![PyPI downloads](https://img.shields.io/pypi/dm/valuein-sdk?label=pypi%20downloads&cacheSeconds=3600)](https://pypi.org/project/valuein-sdk/)
[![MCP Registry](https://img.shields.io/badge/MCP-registry.modelcontextprotocol.io-blue)](https://registry.modelcontextprotocol.io)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-green)](https://github.com/valuein/valuein/blob/main/LICENSE)
[![Discord](https://img.shields.io/discord/valuein?label=discord&logo=discord&color=5865F2)](https://discord.gg/YDGh9XKWQr)
[![X / Twitter](https://img.shields.io/twitter/follow/valuein_?style=flat&logo=x)](https://x.com/valuein_)

---

**Institutional-grade U.S. fundamentals data for quants, analysts, and AI agents.**

Valuein turns the complexity of SEC EDGAR bulk filings into clean, structured, developer-friendly datasets. We bridge the gap between raw 10-Ks and quantitative research, so you spend your time building models — not cleaning data.

[Explore the data](https://valuein.biz) · [Pricing](https://valuein.biz/pricing) · [Discord](https://discord.gg/YDGh9XKWQr) · [X / Twitter](https://x.com/valuein_) · [Public repo](https://github.com/valuein/valuein)

---

## What sets us apart

Most financial-data vendors deliver restated, retroactively adjusted numbers. That's fine — until your backtest accidentally sees a 2024 restatement while simulating a 2023 trade. Valuein preserves filings exactly as they were reported and exposes the same data through every channel you already use.

| Property | What it means for you |
|---|---|
| 🕒 **Point-in-Time integrity** | Every fact is timestamped with the SEC's `accepted_at`. Filter by `filing_date <= trade_date` and your backtest can only see what the market saw. |
| ⚖️ **Survivorship-bias free** | All companies — active, delisted, bankrupt, acquired — remain in every snapshot. No artificially profitable universe. |
| 📜 **As-reported fundamentals** | 10-K, 10-Q, 8-K, 20-F, and amendments mapped directly from EDGAR. 8-K coverage extends from slow fundamental research into event-driven territory. |
| 📊 **Standardized concepts** | 11,966 raw XBRL tags normalized to ~150 canonical names — both the raw and canonical labels are on every fact row, no hidden mapping table. |
| 🌊 **Deep historical coverage** | 12M+ filings, 108M+ standardized facts, 1994–present — full market cycles for stress testing and ML training. |
| 🚀 **Cloud-native delivery** | Parquet on Cloudflare R2 streamed via DuckDB. No bulk downloads, no egress fees, millisecond analytics. |

---

## Distribution channels

The same dataset, delivered five ways so it lands where you already work. **One Stripe-issued token unlocks every channel** — no per-channel billing.

| Channel | Audience | Get started |
|---|---|---|
| 🐍 **Python SDK** | Quants, engineers, data scientists | `pip install valuein-sdk` · [PyPI](https://pypi.org/project/valuein-sdk/) |
| 🤖 **MCP server** | Claude, Cursor, Codex, custom agents | `https://mcp.valuein.biz/mcp` · [registry listing](https://registry.modelcontextprotocol.io) |
| 📊 **Excel & Power Query** | Analysts, CPAs, researchers | [Setup guide](https://github.com/valuein/valuein/blob/main/docs/excel-guide.md) |
| 🌐 **Web dashboard** | Retail, executives, non-technical | [valuein.biz](https://valuein.biz) |
| 🚛 **Bulk data API** | B2B partners, fintech platforms | `https://data.valuein.biz` · [contact us](mailto:sales@valuein.biz) |

---

## Try it in 30 seconds — no token required

```python
from valuein_sdk import ValueinClient

with ValueinClient() as client:
    df = client.query("""
        SELECT symbol, name, sector
        FROM   "references"
        WHERE  is_sp500 = TRUE AND is_active = TRUE
        ORDER  BY name
        LIMIT  10
    """)
    print(df)
```

That's a real query against the live S&P 500 sample. Add `VALUEIN_API_KEY` only when you need full universe or full history.

Want an AI agent to query for you instead? Add this to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "valuein": {
      "url": "https://mcp.valuein.biz/mcp",
      "headers": { "Authorization": "Bearer YOUR_VALUEIN_API_KEY" }
    }
  }
}
```

Same URL works for any MCP-capable client — Cursor, Codex, custom LangGraph or CrewAI agents.

---

## Featured projects

| Repository | What it is |
|---|---|
| [**valuein**](https://github.com/valuein/valuein) ⭐ | Public docs, examples, notebooks, query cookbook, and the MCP-registry manifest. **Start here.** |

The Python SDK ships from PyPI, the MCP server runs as a Cloudflare Worker, the data pipeline ingests SEC EDGAR daily, and the website is built on Next.js + Cloudflare. Source for those lives in private repos until we open-source them — follow the [public repo](https://github.com/valuein/valuein) for releases.

---

## Architecture

```
SEC EDGAR  →  Pipeline (Python + Pydantic)  →  (Parquet Files)
                                                      │
                                       ┌──────────────┼──────────────┐
                                       ▼                             ▼
                                Python SDK                       MCP server      
                                  (DuckDB)                    (mcp.valuein.biz)  
                                       │                             │
                                       └──────────────┼──────────────┘
                                                      ▼
                                          One Bearer token, every channel
                                       (Stripe-issued, validated at the edge)
```

The pipeline ingests EDGAR within ~60 seconds of acceptance, normalizes 11,966 raw XBRL tags into ~150 canonical concepts via a deterministic waterfall, writes Parquet snapshots to R2, and serves them through a Cloudflare Worker gateway with token-aware tier routing — Pro and Enterprise tokens see the full universe, Free tokens see the S&P 500, anonymous sees the last five years of S&P 500.

---

## Who it's for

- **Quantitative researchers** — point-in-time data and survivorship-bias-free coverage for rigorous backtesting and algorithmic strategy development
- **Event-driven funds** — 8-K coverage captures intra-quarter material events (CEO departures, bankruptcies, M&A) for latency-sensitive strategies
- **Financial analysts** — as-reported filings with deep history for fundamental due diligence and company research
- **Portfolio managers** — sector- and factor-relative screens with consistent, audited inputs
- **Data engineers** — Parquet-native, cloud-distributed datasets that plug straight into existing data infrastructure
- **AI / agent builders** — natural-language access to the same data through the MCP server, no SDK required
- **Academic researchers** — the complete historical universe for empirical studies without selection bias

---

## Roadmap

We're building a financial operating system — the canonical place AI agents and humans go for U.S. fundamentals.

- ✅ Point-in-time, survivorship-bias-free Parquet on R2 (1994–present)
- ✅ Python SDK with 44 pre-built SQL templates and a multi-factor alpha framework
- ✅ MCP server with 14 live tools + 8 analyst SOP prompts
- ✅ Excel template with Power Query and 8 pre-configured sheets
- 🔄 Semantic search over filing text (Risk Factors, MD&A, Business, Legal, Controls) — Vectorize backfill in progress
- 🔄 Real-time 8-K push via webhook (Custom tier)
- 🛣️ Programmatic ticker pages with JSON-LD for AEO discovery
- 🛣️ Open-source notebook templates (factor screens, DCF, earnings momentum)

---

## Contributing

We welcome examples, notebook improvements, query recipes, doc fixes, and data edge-case reports.

- 🐛 [File an issue](https://github.com/valuein/valuein/issues/new/choose) — data quality, feature request, outage, or general question
- 💬 Discuss in [Discord](https://discord.gg/q5tmcQEQUr)
- 📜 Read [CONTRIBUTING.md](https://github.com/valuein/valuein/blob/main/CONTRIBUTING.md) and our [Code of Conduct](https://github.com/valuein/valuein/blob/main/CODE_OF_CONDUCT.md)

We're actively looking for contributors to our SDK examples and community-led valuation models. Lifetime access tokens are available for high-quality contributions — see Discord for details.

---

## Get in touch

| | |
|---|---|
| 💬 **Discord** | [discord.gg/q5tmcQEQUr](https://discord.gg/q5tmcQEQUr) — community + real-time support |
| 🐦 **X / Twitter** | [@valuein_](https://x.com/valuein_) — product updates and data insights |
| 🌐 **Website** | [valuein.biz](https://valuein.biz) |
| ✉️ **Support** | [support@valuein.biz](mailto:support@valuein.biz) |
| 💼 **Sales** | [sales@valuein.biz](mailto:sales@valuein.biz) |
| 🛡️ **Security** | [security@valuein.biz](mailto:security@valuein.biz) |
| 🧾 **Compliance** | [compliance@valuein.biz](mailto:compliance@valuein.biz) |

---

<div align="center">

### Empowering better decisions through data integrity.

[Get started →](https://valuein.biz/pricing)

</div>
