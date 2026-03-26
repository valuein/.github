[![Valuein — Financial Data Infrastructure](https://www.valuein.biz/valuein/colored_logo_no_bg.png)](https://valuein.biz)

---

**Institutional-grade U.S. fundamentals data for quants, analysts, and developers.**

Valuein transforms the complexity of SEC EDGAR bulk data into clean, structured, developer-friendly datasets. We bridge the gap between raw filings and actionable quantitative research — so you spend time building models, not cleaning data.

[Explore Datasets](https://valuein.biz) · [Discord](https://discord.gg/68YN8z9J) · [X / Twitter](https://x.com/valuein_)

---

## Why Valuein

Most financial data vendors deliver restated, retroactively adjusted numbers. That's fine — until your backtest accidentally sees a restated 2024 earnings figure while simulating a trade in 2023. Valuein preserves filings exactly as they were reported, giving you a reliable foundation for time-sensitive research and quantitative strategies.

### As-Reported Fundamentals

10-K, 10-Q, 20-F, and 8-K filings (including amendments) mapped directly from SEC EDGAR — not retroactively adjusted. By including 8-K current reports alongside standard filings, we capture intra-quarter material events like CEO departures and unexpected bankruptcies, crossing from slow fundamental research into event-driven territory.

### Point-in-Time (PIT) Integrity

Every fact is recorded in an immutable ledger with strict EDGAR timestamps. Your models only see the exact figures that were available to the market on a specific date, eliminating look-ahead bias in backtests and simulations.

### Survivorship-Bias Free

Our dataset includes all companies — active, merged, and delisted — that have reported to the SEC. Train your models on reality, not on an artificially profitable universe that ignores every company that went bankrupt.

### Deep Historical Coverage

105M+ facts across 12M+ filings dating back to 1993+. Multi-decade coverage spanning dot-com crashes, financial crises, and bull markets — the depth required to train robust ML models and stress-test algorithms across full market cycles.

---

## Datasets

| Dataset | Coverage | History | Access |
|---|---|---|---|
| **Sample (S&P 500 5Y)** | S&P 500 constituents | Last 5 years | Free |
| **S&P 500 Full History** | S&P 500 constituents | Full history | Free (registration required) |
| **Full Universe** | All SEC-reporting companies | Full history since 1993+ | Paid |

Start with the free S&P 500 tier to evaluate data quality and schema, then upgrade when you're ready for the full universe.

---

## Developer Experience

Financial data should be as easy to query as any other part of your stack.

```python
from valuein import Client

v = Client("your_token")
df = v.get("fact")
print(df.shape)           # rows available
print(df.dtypes)           # type validation
print(df["period"].max())  # freshness check
```

- **Python SDK** — integrate directly into research notebooks or production pipelines. Available on PyPI.
- **Cloud-native delivery** — data distributed as Parquet via Cloudflare R2 with zero egress fees. Connect DuckDB and query 105M+ facts over the network in milliseconds, no local storage required.
- **Machine-readable formats** — standardized outputs for immediate ingestion into Pandas, Polars, or SQL databases.
- **Excel integration** — 30 years of SEC fundamentals directly in Excel with daily refresh, built for analysts who prefer spreadsheets over code.

---

## Architecture

```
SEC EDGAR  →  Postgres (staging)  →  Parquet  →  R2 (distribution)
                                                       ↓
                                              Python SDK / Excel
                                              DuckDB / Direct query
```

Our pipeline processes SEC EDGAR bulk data daily, stages it in Postgres for validation, converts to optimized Parquet files, and distributes via Cloudflare R2 — delivering low-latency access without the overhead of traditional API rate limits or massive CSV downloads.

---

## Who It's For

- **Quantitative researchers** — point-in-time data and survivorship-bias-free coverage for rigorous backtesting and algorithmic strategy development.
- **Event-driven funds** — 8-K inclusion captures material events between quarterly filings, giving models a latency advantage.
- **Financial analysts** — as-reported filings with deep history for fundamental due diligence and company research.
- **Data engineers** — Parquet-native, cloud-distributed datasets ready to plug into existing data infrastructure.
- **Academic researchers** — complete historical universe for empirical studies without selection bias.

---

## Contributing

We welcome feedback, feature requests, and data edge case reports from the community. Open an issue in this repo or reach out on Discord.

We're actively looking for contributors to our SDK and community-led valuation models.

---

## Contact

- [Discord](https://discord.gg/68YN8z9J) — real-time support and community
- [X / Twitter](https://x.com/valuein_) — product updates and data insights
- [Website](https://valuein.biz)


### Empowering better decisions through data integrity.
