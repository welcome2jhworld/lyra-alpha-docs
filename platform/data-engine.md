---
title: Lyra Data Engine
summary: Lyra's own engine turns raw news, filings, flows and market data into point-in-time fields that every agent, check and alpha reads.
tags:
- data engine
- lyra data engine
- lde
- lde.score
- fields
- point in time
- look-ahead
- freshness
- news
- filings
- flows
related:
- fields
- custom-data-engine
- alpha/data
- grading
---

# Lyra Data Engine

## For agents

- Lets you: Know what data Lyra has, what each value means, and when it was known.
- Tools: `data_fields`, `data_what_changed`, `data_prediction_markets`, `data_rates`, `data_hl_whale_positions`
- Limit: Values are not published as raw series; agents read them through checks, alphas and the data_* tools.

## In, engine, out

```figure data-engine
News: brewer cuts its volume outlook → Filing: 10-Q, beverage revenue up → Data: funding at a yearly high → Lyra Data Engine → lde.score: -0.48 → sec.revenue_yoy: +0.21 → funding.spread_hl_ann: +0.12
```

## What goes in

| Input | Examples |
|---|---|
| News and posts | news feeds, GDELT, X, YouTube |
| Filings | SEC EDGAR (10-K, 10-Q, 8-K, Form 4, 13F, company facts), Korea DART |
| Prices | Hyperliquid perps (HIP-3 and delisted included), US stocks and ETFs from 2016 (delisted kept) |
| Flows and positioning | funding, open interest, Binance, Bybit and OKX long/short, Hyperliquid whales, CFTC COT |
| Holdings | 13F of large managers, ETF holdings files |
| Macro and rates | FRED, Treasury curve, ALFRED vintages, fear and greed, stablecoin supply |
| Events | earnings and macro calendars, Polymarket and Kalshi odds, congressional trades |

## What the engine does

1. Collects each source and drops duplicates.
2. Cleans text, links it to instruments, and merges the same story from many outlets.
3. Reads each story for each instrument it touches.
4. Writes every value in one format: instrument, value, unit, the date it describes (`as_of`) and the time it was first public (`known_at`).
5. Tracks staleness per dataset. A pod whose data is stale holds new adds.

## What comes out

- Fields with a name, a unit and a scope. Every field: [Field catalog](fields.md).
- `lde.score`: a signed score from -1 to 1 per instrument and day, decayed over recent stories.
  - Sign: the story reports facts favourable (+) or unfavourable (-) for the instrument.
  - Size: impact, from none to major.
  - Also `lde.up`, `lde.down`, `lde.impact`, `lde.count`, `lde.surprise`, `lde.recap`, `lde.industry.score` and `sec.insider.*`.
- Ratios, USD, percent and counts for flows, positioning, fundamentals and macro.
- Tables for odds, rates and whale positions, read with the `data_*` tools.
- Congressional trades, 13F and ETF holdings feed checks, alphas and pods as `congress.*`, `inst.*` and `etf.*` fields.

## Point in time

- Every read asks for values known by a given time.
- A value is never visible before its `known_at`.
- Release lags are applied per series; macro revisions use their first-published vintage.
- A correction appends a new row; old rows are not rewritten.
- Prices are adjusted only with splits and dividends known by then.
- Delisted names stay in the history.
- Checks and alphas run on these reads, so a backtest sees what a trader could have seen.

## Freshness

- Each field has an update cadence and a "stale after" time. [Field catalog](fields.md).
- Daily bars are known at the close; the rule job runs at 02:00 UTC.
- Published fields are delay 1: an alpha trades them on the next close.

## How alphas use it

```text
rank(lde.score)
ts_mean(funding.spread_hl_ann, 7)
obs("fred.DGS10")
```

- Field syntax and delay: [Data sheet](../alpha/data.md).
- Your own fields on Ultra: [Your own Data Engine](custom-data-engine.md).
