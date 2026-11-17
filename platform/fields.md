---
title: Field catalog
summary: 'Every field and table in the Lyra Data Engine: meaning, unit, update cadence, when it is known, and coverage. Generated from code.'
tags:
- fields
- catalog
- data sheet
- datasets
- coverage
- lag
- freshness
- stale
- tables
- generated
related:
- data-engine
- alpha/data
- custom-data-engine
---

# Field catalog

## For agents

- Lets you: Pick a field for an alpha or check and know when it is known.
- Tools: `data_fields`
- Limit: data_fields adds each field's first stored date; values are not published.

## Prices

| Field | Meaning | Unit | Scope | Updates | Known | Lag hours | Delay | Stale after | Coverage |
|---|---|---|---|---|---|---|---|---|---|
| `close` | Daily close, split and dividend adjusted | usd | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `raw_close` | Daily close as printed, before splits and dividends | usd | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `ret(days)` | Close-to-close return over days | ratio | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `vol(days)` | Annualised volatility of daily returns over days | ratio | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `volume` | Daily traded volume in base units | count | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `funding(days)` | Mean daily perp funding over days, annualised | ratio | instrument | daily | at the daily close | 0 | 0 or 1 |  | Hyperliquid perps and HIP-3 names |
| `open_interest` | Perp open interest in USD, snapshotted after the close | usd | instrument | daily | when published | 1 | 1 only |  | Hyperliquid perps and HIP-3 names |

## Series

| Field | Meaning | Unit | Scope | Updates | Known | Lag hours | Delay | Stale after | Coverage |
|---|---|---|---|---|---|---|---|---|---|
| `funding.spread_hl_ann` | Hyperliquid vs CEX funding | ratio | instrument | every 1 h | when published | 0.08 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `funding.cex_ann` | Hyperliquid vs CEX funding | ratio | instrument | every 1 h | when published | 0.08 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.top_ls` | Binance positioning | ratio | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.taker_ratio` | Binance positioning | ratio | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.oi_usd` | Binance positioning | usd | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `bybit.ls_ratio` | Bybit and OKX account long/short | ratio | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `okx.ls_ratio` | Bybit and OKX account long/short | ratio | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `whales.net_usd` | Hyperliquid whale exposure | usd | instrument | every 1 h | when published | 0.08 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `whales.breadth` | Hyperliquid whale exposure | ratio | instrument | every 1 h | when published | 0.08 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `deribit.dvol` | Deribit DVOL | pct | instrument | every 1 h | when published | 1 | 1 only | 3 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `macro.net_liquidity_bn` | Macro liquidity and sentiment | usd | global | every 6 h | when published | 24 | 1 only | 8 days | global only ('_') |
| `macro.hy_spread` | Macro liquidity and sentiment | pct | global | every 6 h | when published | 24 | 1 only | 8 days | global only ('_') |
| `stables.total_usd` | Macro liquidity and sentiment | usd | global | every 6 h | when published | 24 | 1 only | 8 days | global only ('_') |
| `sentiment.fear_greed` | Macro liquidity and sentiment | score | global | every 6 h | when published | 24 | 1 only | 8 days | global only ('_') |
| `cot.spec_net_oi` | CFTC Commitments of Traders | ratio | instrument | every 12 h | when published | 96 | 1 only | 10 days | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `sec.revenue_yoy` | SEC XBRL fundamentals | ratio | instrument | daily | when published | 1080 | 1 only | 120 days | HIP-3 equities as HL:xyz:<ticker> |
| `sec.net_margin` | SEC XBRL fundamentals | ratio | instrument | daily | when published | 1080 | 1 only | 120 days | HIP-3 equities as HL:xyz:<ticker> |
| `earnings.days_to` | Days to earnings | count | instrument | every 6 h | when published | 0.08 | 1 only | 18 h | HIP-3 equities as HL:xyz:<ticker> |
| `fred.DFF` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.SOFR` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DGS3MO` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DGS2` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DGS10` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DGS30` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.T10Y2Y` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.T10Y3M` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.T10YIE` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DFII10` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.BAMLH0A0HYM2` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.BAMLC0A0CM` | Rates and macro series | pct | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.MORTGAGE30US` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `fred.VIXCLS` | Rates and macro series | score | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.DTWEXBGS` | Rates and macro series | score | global | every 6 h | when published | 240 | 1 only | 4 days | global only ('_') |
| `fred.DCOILWTICO` | Rates and macro series | usd | global | every 6 h | when published | 240 | 1 only | 4 days | global only ('_') |
| `fred.CPIAUCSL` | Rates and macro series | score | global | every 6 h | when published | 1128 | 1 only | 4 days | global only ('_') |
| `fred.CPILFESL` | Rates and macro series | score | global | every 6 h | when published | 1128 | 1 only | 4 days | global only ('_') |
| `fred.PCEPILFE` | Rates and macro series | score | global | every 6 h | when published | 1488 | 1 only | 4 days | global only ('_') |
| `fred.UNRATE` | Rates and macro series | pct | global | every 6 h | when published | 960 | 1 only | 4 days | global only ('_') |
| `fred.PAYEMS` | Rates and macro series | count | global | every 6 h | when published | 960 | 1 only | 4 days | global only ('_') |
| `fred.ICSA` | Rates and macro series | count | global | every 6 h | when published | 144 | 1 only | 4 days | global only ('_') |
| `fred.INDPRO` | Rates and macro series | score | global | every 6 h | when published | 1176 | 1 only | 4 days | global only ('_') |
| `fred.UMCSENT` | Rates and macro series | score | global | every 6 h | when published | 720 | 1 only | 4 days | global only ('_') |
| `fred.M2SL` | Rates and macro series | usd | global | every 6 h | when published | 1440 | 1 only | 4 days | global only ('_') |
| `fred.WALCL` | Rates and macro series | usd | global | every 6 h | when published | 48 | 1 only | 4 days | global only ('_') |
| `fred.RRPONTSYD` | Rates and macro series | usd | global | every 6 h | when published | 96 | 1 only | 4 days | global only ('_') |
| `fred.WTREGEN` | Rates and macro series | usd | global | every 6 h | when published | 48 | 1 only | 4 days | global only ('_') |
| `fred.NFCI` | Rates and macro series | score | global | every 6 h | when published | 144 | 1 only | 4 days | global only ('_') |
| `ust.1m` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.2m` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.3m` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.6m` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.1y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.2y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.3y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.5y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.7y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.10y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.20y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |
| `ust.30y` | Rates and macro series | pct | global | every 6 h | when published | 24 | 1 only | 4 days | global only ('_') |

## Prediction markets

| Field | Meaning | Unit | Scope | Updates | Known | Lag hours | Delay | Stale after | Coverage |
|---|---|---|---|---|---|---|---|---|---|
| `odds("<market id>")` | Prediction market yes price, last snapshot by the close | ratio | market | every 1 h | at the daily close | 0 | 0 or 1 |  | Prediction markets by market id |

## Tables

| Table | MCP tool | Updates | Covers |
|---|---|---|---|
| Prediction markets | `data_prediction_markets` | every 1 h | markets tagged with tickers and themes |
| Rates and macro series | `data_rates` | every 6 h | global only ('_') |
| Hyperliquid whale positions | `data_hl_whale_positions` | every 1 h | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |

## Reading the columns

- Known: at the daily close, or when the source publishes it.
- Lag hours: added to known before a value can be used.
- Delay: `1 only` fields trade on the next close.
- Stale after: past this age without an update, Lyra treats the field as stale.
