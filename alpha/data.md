# Data sheet

Every field an alpha can read. Values are not published. The first stored date of each field and its live coverage come from the `data_fields` MCP tool.

A field is known at the daily close or when its source publishes it, plus the lag in hours. A field marked `1 only` can be used with delay 1 but not delay 0.

| Field | Meaning | Unit | Scope | Known | Lag hours | Delay | Coverage |
|---|---|---|---|---|---|---|---|
| `close` | Daily close, split and dividend adjusted | usd | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `raw_close` | Daily close as printed, before splits and dividends | usd | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `ret(days)` | Close-to-close return over days | ratio | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `vol(days)` | Annualised volatility of daily returns over days | ratio | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `volume` | Daily traded volume in base units | count | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps as <coin>, HIP-3 names as xyz:<name>, US stocks as US:<TICKER> |
| `funding(days)` | Mean daily perp funding over days, annualised | ratio | instrument | at the daily close | 0 | 0 or 1 | Hyperliquid perps and HIP-3 names |
| `open_interest` | Perp open interest in USD, snapshotted after the close | usd | instrument | when published | 1 | 1 only | Hyperliquid perps and HIP-3 names |
| `funding.spread_hl_ann` | Hyperliquid vs CEX funding | ratio | instrument | when published | 0.08 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `funding.cex_ann` | Hyperliquid vs CEX funding | ratio | instrument | when published | 0.08 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.top_ls` | Binance positioning | ratio | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.taker_ratio` | Binance positioning | ratio | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `binance.oi_usd` | Binance positioning | usd | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `bybit.ls_ratio` | Bybit and OKX account long/short | ratio | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `okx.ls_ratio` | Bybit and OKX account long/short | ratio | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `whales.net_usd` | Hyperliquid whale exposure | usd | instrument | when published | 0.08 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `whales.breadth` | Hyperliquid whale exposure | ratio | instrument | when published | 0.08 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `deribit.dvol` | Deribit DVOL | pct | instrument | when published | 1 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `macro.net_liquidity_bn` | Macro liquidity and sentiment | usd | global | when published | 24 | 1 only | global only ('_') |
| `macro.hy_spread` | Macro liquidity and sentiment | pct | global | when published | 24 | 1 only | global only ('_') |
| `stables.total_usd` | Macro liquidity and sentiment | usd | global | when published | 24 | 1 only | global only ('_') |
| `sentiment.fear_greed` | Macro liquidity and sentiment | score | global | when published | 24 | 1 only | global only ('_') |
| `cot.spec_net_oi` | CFTC Commitments of Traders | ratio | instrument | when published | 96 | 1 only | Hyperliquid coins as HL:<coin>, HIP-3 names as HL:xyz:<name> |
| `sec.revenue_yoy` | SEC XBRL fundamentals | ratio | instrument | when published | 1080 | 1 only | HIP-3 equities as HL:xyz:<ticker> |
| `sec.net_margin` | SEC XBRL fundamentals | ratio | instrument | when published | 1080 | 1 only | HIP-3 equities as HL:xyz:<ticker> |
| `earnings.days_to` | Days to earnings | count | instrument | when published | 0.08 | 1 only | HIP-3 equities as HL:xyz:<ticker> |
| `fred.DFF` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.SOFR` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.DGS3MO` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.DGS2` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.DGS10` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.DGS30` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.T10Y2Y` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.T10Y3M` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.T10YIE` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.DFII10` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.BAMLH0A0HYM2` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.BAMLC0A0CM` | Rates and macro series | pct | global | when published | 96 | 1 only | global only ('_') |
| `fred.MORTGAGE30US` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `fred.VIXCLS` | Rates and macro series | score | global | when published | 96 | 1 only | global only ('_') |
| `fred.DTWEXBGS` | Rates and macro series | score | global | when published | 240 | 1 only | global only ('_') |
| `fred.DCOILWTICO` | Rates and macro series | usd | global | when published | 240 | 1 only | global only ('_') |
| `fred.CPIAUCSL` | Rates and macro series | score | global | when published | 1128 | 1 only | global only ('_') |
| `fred.CPILFESL` | Rates and macro series | score | global | when published | 1128 | 1 only | global only ('_') |
| `fred.PCEPILFE` | Rates and macro series | score | global | when published | 1488 | 1 only | global only ('_') |
| `fred.UNRATE` | Rates and macro series | pct | global | when published | 960 | 1 only | global only ('_') |
| `fred.PAYEMS` | Rates and macro series | count | global | when published | 960 | 1 only | global only ('_') |
| `fred.ICSA` | Rates and macro series | count | global | when published | 144 | 1 only | global only ('_') |
| `fred.INDPRO` | Rates and macro series | score | global | when published | 1176 | 1 only | global only ('_') |
| `fred.UMCSENT` | Rates and macro series | score | global | when published | 720 | 1 only | global only ('_') |
| `fred.M2SL` | Rates and macro series | usd | global | when published | 1440 | 1 only | global only ('_') |
| `fred.WALCL` | Rates and macro series | usd | global | when published | 48 | 1 only | global only ('_') |
| `fred.RRPONTSYD` | Rates and macro series | usd | global | when published | 96 | 1 only | global only ('_') |
| `fred.WTREGEN` | Rates and macro series | usd | global | when published | 48 | 1 only | global only ('_') |
| `fred.NFCI` | Rates and macro series | score | global | when published | 144 | 1 only | global only ('_') |
| `ust.1m` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.2m` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.3m` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.6m` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.1y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.2y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.3y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.5y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.7y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.10y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.20y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `ust.30y` | Rates and macro series | pct | global | when published | 24 | 1 only | global only ('_') |
| `lde.score` | Lyra Data Engine news and filings score, decayed, -1 to 1, price recaps left out | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.score_raw` | Lyra Data Engine score over every story, price recaps included, -1 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.recap` | Share of recent stories that only report a past price move, decayed, 0 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.up` | Share of recent stories with favourable facts, decayed, 0 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.down` | Share of recent stories with unfavourable facts, decayed, 0 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.impact` | Largest impact of the stories known that day, 0 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.count` | Stories known that day, price recaps left out | count | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.surprise` | Stories that report an outcome against expectations, signed, decayed, -1 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.impact_score` | Impact-weighted score of recent stories, -1 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks and ETFs as US:<ticker>, Hyperliquid perps as <coin>, HIP-3 names as xyz:<name> |
| `lde.industry.score` | Industry score from SIC peers and industry stories, members as of the date, -1 to 1 | ratio | instrument | when published | 0 | 1 only | US stocks as US:<ticker>, and HIP-3 names on them |
| `sec.insider.buy_usd` | Open-market insider buys filed that day (Form 4) | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker>, and HIP-3 names on them |
| `sec.insider.sell_usd` | Open-market insider sells filed that day (Form 4) | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker>, and HIP-3 names on them |
| `sec.insider.net_usd` | Insider buys minus sells filed that day (Form 4) | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker>, and HIP-3 names on them |
| `inst.holders` | 13F filers holding it, from each filer's latest report | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.holders_chg` | New holders minus exits in each filer's latest report | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.shares_chg` | Shares bought minus sold across 13F filers' latest reports | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.net_buy_usd` | Dollar value of 13F filers' share changes, latest reports | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.value_usd` | Dollar value held by 13F filers | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.top_holders` | Holders among the tracked large managers, about 50 | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `inst.top_net_buy_usd` | Dollar share changes of the tracked large managers | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `congress.buys_30d` | Stock buys Congress members disclosed over the last 30 days | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `congress.sells_30d` | Stock sells Congress members disclosed over the last 30 days | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `congress.net_usd_mid_30d` | Buys minus sells at each amount range's midpoint, disclosed over 30 days | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `etf.holders` | ETFs holding it, from each ETF's latest N-PORT | count | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `etf.held_usd` | Dollar value held by ETFs | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `etf.flow_usd` | Dollar value of ETFs' share changes, latest N-PORT vs the one before | usd | instrument | when published | 0 | 1 only | US stocks as US:<ticker> |
| `obs("etf.weight.<ETF>")` | Weight in <ETF>, percent | pct | instrument | when published | 0 | 1 only | US stocks held by that ETF, from its N-PORT reports |
| `odds("<market id>")` | Prediction market yes price, last snapshot by the close | ratio | market | at the daily close | 0 | 0 or 1 | Prediction markets by market id |
