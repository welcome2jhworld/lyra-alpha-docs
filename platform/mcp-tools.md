---
title: MCP tool reference
summary: Every Lyra MCP tool with its scope, plan, input schema and an example input. Generated from the tool registry.
tags:
- mcp
- tools
- reference
- schema
- inputs
- outputs
- examples
- generated
related:
- mcp
- security
- alpha/connect
---

# MCP tool reference

## For agents

- Lets you: Call any Lyra MCP tool with valid input.
- Tools: `docs_get`
- Limit: Inputs are validated against the schema; extra keys are rejected.
- Limit: A refusal starts with refused or rejected and is flagged as an error.

## Market data

### `data_prediction_markets`

Live Polymarket and Kalshi odds on earnings, Fed and macro data, recession, war and geopolitics, elections and policy, IPOs and M&A, and crypto: yes price (0 to 1), 24h and 7d change, 24h volume, resolve date, mapped tickers and themes. Filter by ticker (NVDA, BTC), theme (fed, inflation, growth, war, trade, elections, ipo, m&a, earnings, crypto, oil, or a category: macro, geopolitics, ipo_ma) or a word in the question; empty strings mean no filter. Top 25 by 24h volume.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"ticker":{"type":"string"},"theme":{"type":"string"},"query":{"type":"string"}},"required":["ticker","theme","query"]}
```

Example input:

```json
{
  "ticker": "",
  "theme": "fed",
  "query": "rate cut"
}
```

Returns: Markets with yes price, 24h and 7d change, volume and resolve date.

### `data_fund_holdings`

13F holdings of about 50 large funds (Berkshire, Bridgewater, Citadel, Pershing Square, Tiger, Coatue, ARK and others), quarter on quarter: new, added, cut, exited, shares and dollar flow. With a ticker: every tracked fund's position in it. With a manager (part of the name): that fund's biggest moves. With neither: the quarter's most bought and most sold names. quarter like 2026Q2, empty for the latest. Rows carry the filing date and lag_days (13Fs land up to 45 days after quarter end).

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"ticker":{"type":"string"},"manager":{"type":"string"},"quarter":{"type":"string"}},"required":["ticker","manager","quarter"]}
```

Example input:

```json
{
  "ticker": "CELH",
  "manager": "",
  "quarter": ""
}
```

Returns: 13F holders of a ticker or one manager's book, with quarter on quarter changes.

### `data_congress_trades`

Stock and option trades House members disclosed in periodic transaction reports (House Clerk; the Senate is not collected): member, ticker, buy or sell, amount range, trade date, disclosure date and lag_days (members have up to 45 days to disclose). Filter by ticker or member (part of the name) over the last days (default 90). With neither: most bought by members over 30 and 90 days and the latest disclosures.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"ticker":{"type":"string"},"member":{"type":"string"},"days":{"type":"number"}},"required":["ticker","member","days"]}
```

Example input:

```json
{
  "ticker": "STZ",
  "member": "",
  "days": 90
}
```

Returns: House trades: member, ticker, side, amount range, trade and disclosure dates.

### `data_rates`

Rates and macro series from FRED and the Treasury yield curve: latest value and date, change since the previous print, over 1 week and 1 month, plus 2s10s and 3m10y. series is empty for all, or a comma list of ids or words (DGS10, ust.2y, sofr, cpi, payrolls, high yield); with series and days above 0 it adds the history over that many days.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"series":{"type":"string"},"days":{"type":"number"}},"required":["series","days"]}
```

Example input:

```json
{
  "series": "DGS10",
  "days": 30
}
```

Returns: Rates and macro series with each value's date and source.

### `data_etf_holdings`

Daily issuer holdings files for SPY, DIA, MDY, the sector SPDRs (XLK, XLF, XLE, XLV, XLY, XLP, XLI, XLB, XLU, XLRE, XLC), KRE, XBI, XME, XAR, XSD and ARKK, ARKW, ARKG, ARKQ, ARKF: weight in percent, change since the previous file and over 7 days, shares. fund gives its top 25 holdings; ticker gives every tracked ETF that holds it; both empty lists the funds with their top 5.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"fund":{"type":"string"},"ticker":{"type":"string"}},"required":["fund","ticker"]}
```

Example input:

```json
{
  "fund": "XLP",
  "ticker": ""
}
```

Returns: An ETF's holdings and weights, with adds and drops.

### `data_hl_whale_positions`

Hourly positions of $250k or more held by the top 200 Hyperliquid accounts by monthly PnL: wallet (shortened), side, size in USD, entry, leverage, unrealized PnL, liquidation price and the move against days ago (opened, added, cut, flipped, closed). With a coin (BTC, xyz:NVDA): its biggest positions. With no coin: long, short and net USD per coin and the net change.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"coin":{"type":"string"},"days":{"type":"number"}},"required":["coin","days"]}
```

Example input:

```json
{
  "coin": "HYPE",
  "days": 7
}
```

Returns: Large Hyperliquid positions: side, size, entry, leverage and moves.

### `data_what_changed`

What moved in the market data over the last days (1 to 90): biggest prediction market moves and new markets, new 13F filings and their biggest changes, new Congress disclosures and most bought, biggest rate and macro moves, ETF adds, drops and weight moves, and whale position moves and net flows per coin. family is one of prediction_markets, fund_holdings, congress_trades, rates, etf_holdings, hl_whale_positions, or empty for every family.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"family":{"type":"string"},"days":{"type":"number"}},"required":["family","days"]}
```

Example input:

```json
{
  "family": "",
  "days": 7
}
```

Returns: What moved across Lyra's data in the last days.

## Checks

### `test_run_check`

Run one check spec through the quant engine and get its evidence: grade, past cases won out of cases with their period, holding cost per month, and curve, the equity [date, value] at each past case's end starting at 1, left out when the book holds fewer than 5 names on average. type rule takes a text formula over universe.long; odds needs market, level and cross; regime needs condition and side; carry takes days. Every call is recorded as a version of its family and raises the bar for the next. build_run and build_pod return a research run's spec to change: benchmark (empty for none), start (YYYY-MM-DD), horizon_days, or a symbol left out of universe.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"spec":{"type":"object","additionalProperties":false,"required":["claim","family","type","universe","benchmark","checks","start","horizon_days","capital","leverage","market","level","cross","condition","side","days","formula"],"properties":{"claim":{"type":"string"},"family":{"type":"string"},"type":{"type":"string","enum":["direction","theme","relative","follow","odds","regime","carry","rule"]},"universe":{"type":"object","additionalProperties":false,"required":["long","short"],"properties":{"long":{"type":"array","items":{"type":"string"}},"short":{"type":"array","items":{"type":"string"}}}},"benchmark":{"type":"string"},"checks":{"type":"array","items":{"type":"string","enum":["past_cases","holding_cost"]}},"start":{"type":"string"},"horizon_days":{"type":"integer"},"capital":{"type":"number"},"leverage":{"type":"number"},"market":{"type":"string"},"level":{"type":"number"},"cross":{"type":"string","enum":["up","down"]},"condition":{"type":"string"},"side":{"type":"string","enum":["long","short"]},"days":{"type":"integer"},"formula":{"type":"string"}}}},"required":["spec"]}
```

Example input:

```json
{
  "spec": {
    "claim": "Drinks that replace alcohol beat brewers and distillers over the next quarter",
    "family": "sober-curious",
    "type": "relative",
    "universe": {
      "long": [
        "US:CELH",
        "US:MNST"
      ],
      "short": [
        "US:STZ",
        "US:DEO"
      ]
    },
    "benchmark": "",
    "checks": [
      "past_cases",
      "holding_cost"
    ],
    "start": "2016-06-01",
    "horizon_days": 90,
    "capital": 3000,
    "leverage": 1,
    "market": "",
    "level": 0.5,
    "cross": "up",
    "condition": "",
    "side": "long",
    "days": 0,
    "formula": ""
  }
}
```

Returns: JSON: grade, label, line, versions_tried, as_of, past_cases, holding_cost_month, curve.

## Research

### `build_research`

Start Lyra's research team on a loose market view, once the question fits in one sentence. angle is "alone" or a short phrase naming what the view is tied to; title is a 2 to 4 word label. It charges the user's credits like a run started in the app and runs for several minutes; its read and fund card land in the user's Lyra chat, and build_run reads them. Returns the run, or why it was refused.

- Scope: `propose`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"question":{"type":"string"},"angle":{"type":"string"},"title":{"type":"string"}},"required":["question","angle","title"]}
```

Example input:

```json
{
  "question": "Gen Z is drinking less",
  "angle": "alone",
  "title": "Sober Curious"
}
```

Returns: The run id and status, or why it was refused.

### `build_runs`

The user's last 20 research runs, newest first: id, title, question, stage (done when finished), verdict, mode and when it started and ended.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{},"required":[]}
```

Example input:

```json
{}
```

Returns: Your research runs, newest first, with status.

### `build_run`

One research run: stage, the team's read, fit, the checked claim with its grade (check), and its latest fund card (card) with legs, size and loss levels once the run is done.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"run_id":{"type":"string"}},"required":["run_id"]}
```

Example input:

```json
{
  "run_id": "r_7f3a"
}
```

Returns: One run: the read, the claim, the checks, the fund card and the spec.

### `build_pod`

Rebuild the fund card of a finished research run with a change: drop symbols, add picks, lean (conviction 1 to 3 per symbol), structure single or main_offset (empty keeps it), insist to build despite Not sure. Code sets the weights, the offset, the size and the loss levels; the check stays the run's. It charges the user's credits like a change in the app, and the card lands in the user's Lyra chat, where only the user can press Start. Returns the card's numbers and the run's spec, or why it was refused.

- Scope: `propose`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"run_id":{"type":"string"},"change":{"type":"object","additionalProperties":false,"required":["drop","add","lean","structure","insist"],"properties":{"drop":{"type":"array","items":{"type":"string"}},"add":{"type":"array","items":{"type":"object","additionalProperties":false,"required":["symbol","side","conviction"],"properties":{"symbol":{"type":"string"},"side":{"type":"string","enum":["long","short"]},"conviction":{"type":"integer"}}}},"lean":{"type":"array","items":{"type":"object","additionalProperties":false,"required":["symbol","conviction"],"properties":{"symbol":{"type":"string"},"conviction":{"type":"integer"}}}},"structure":{"type":"string","enum":["","single","main_offset"]},"insist":{"type":"boolean"}}}},"required":["run_id","change"]}
```

Example input:

```json
{
  "run_id": "r_7f3a",
  "change": {
    "drop": [
      "US:DEO"
    ],
    "add": [],
    "lean": [
      {
        "symbol": "US:CELH",
        "conviction": 3
      }
    ],
    "structure": "",
    "insist": false
  }
}
```

Returns: The rebuilt card's numbers and the run's spec, or why it was refused.

## Pods

### `pods_templates`

The open prebuilt pods: card text, thesis, what breaks it, symbols, paper record against the S&P 500 and BTC over the same window (null when there is no record yet), capacity left in USD, whether the analyst has filed its thesis, and in_fund (a fund holds one pod per template).

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{},"required":[]}
```

Example input:

```json
{}
```

Returns: Prebuilt pods with their paper record.

### `pods_fund`

The user's fund: plan and limits, paper capital, each open pod's capital, equity, P&L, current target book and scorer score, and decisions waiting for the user.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{},"required":[]}
```

Example input:

```json
{}
```

Returns: Your fund: pods, money, state, loss levels.

### `pods_explain`

The Risk Agent's recent verdicts (resize or block) and risk events (loss cuts, freezes, halts) for one pod, or the whole fund when pod_id is empty, with the facts of each.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"pod_id":{"type":"string"}},"required":["pod_id"]}
```

Example input:

```json
{
  "pod_id": "p_19c2"
}
```

Returns: What the Risk Agent changed on a pod and why.

### `pods_propose`

Put one prebuilt pod in the user's Lyra chat as a proposal card with Start, Edit and Stop. It opens nothing; only the user's Start in the app opens a pod. If the template is already in the fund it proposes another open template and returns in_fund with the one it replaced.

- Scope: `propose`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"template_id":{"type":"string"}},"required":["template_id"]}
```

Example input:

```json
{
  "template_id": "core-trend"
}
```

Returns: JSON for the proposal card placed in your chat.

### `pods_propose_edit`

Propose new names and weights for one of the user's open private pods: weights is the full new book as Hyperliquid symbols with signed percent of the pod's capital; names left out are dropped. Nothing changes until the user presses Apply on the card in the app; then code sizes it and the Risk Agent checks every trade. Returns the proposal, or why it was refused.

- Scope: `propose`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"pod_id":{"type":"string"},"weights":{"type":"array","items":{"type":"object","additionalProperties":false,"required":["symbol","pct"],"properties":{"symbol":{"type":"string"},"pct":{"type":"number"}}}}},"required":["pod_id","weights"]}
```

Example input:

```json
{
  "pod_id": "p_19c2",
  "weights": [
    {
      "symbol": "US:CELH",
      "pct": 33
    },
    {
      "symbol": "US:MNST",
      "pct": 17
    }
  ]
}
```

Returns: JSON for the edit card; you apply it with Apply.

## Alpha Playground

### `alpha_validate`

Parse an alpha and check it is point-in-time: every input known by the time it trades. Returns the canonical expression, its JSON tree, size and look-back, or the error with its column. Free and unlimited. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights.

- Scope: `read`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"alpha":{"type":"object","required":["family","expression","universe"],"properties":{"family":{"type":"string"},"expression":{"type":["string","object"]},"universe":{"type":"object","required":["name","instruments"],"properties":{"name":{"type":"string"},"instruments":{"type":"array","items":{"type":"string"}},"groups":{"type":"object"}}},"settings":{"type":"object"},"weights":{"type":"object"}}}},"required":["alpha"]}
```

Example input:

```json
{
  "alpha": {
    "family": "mom",
    "expression": "rank(ts_zscore(ret(20), 60) / vol(60))",
    "universe": {
      "name": "majors",
      "instruments": [
        "BTC",
        "ETH",
        "SOL",
        "HYPE",
        "XRP"
      ]
    }
  }
}
```

Returns: The canonical expression, its JSON tree, size and look-back, or the error with its column.

### `alpha_simulate`

Backtest an alpha on Lyra's servers and return the standard output: grade, report, submission checks, breadth and, for books of 5 or more names, a curve of at most 250 points starting at 1. Uses one daily check unless the same spec ran today. Every distinct version counts as a trial of its family. Nothing is saved. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights.

- Scope: `read`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"alpha":{"type":"object","required":["family","expression","universe"],"properties":{"family":{"type":"string"},"expression":{"type":["string","object"]},"universe":{"type":"object","required":["name","instruments"],"properties":{"name":{"type":"string"},"instruments":{"type":"array","items":{"type":"string"}},"groups":{"type":"object"}}},"settings":{"type":"object"},"weights":{"type":"object"}}}},"required":["alpha"]}
```

Example input:

```json
{
  "alpha": {
    "family": "mom",
    "expression": "rank(ts_zscore(ret(20), 60) / vol(60))",
    "universe": {
      "name": "majors",
      "instruments": [
        "BTC",
        "ETH",
        "SOL",
        "HYPE",
        "XRP"
      ]
    }
  }
}
```

Returns: The standard output: grade, report, submission checks, breadth, curve.

### `alpha_submit`

Run the submission checks on an alpha and save it to the user's library as the next version of its family when every check passes. Returns the output with saved. A spec simulated today costs no extra check. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights.

- Scope: `propose`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"alpha":{"type":"object","required":["family","expression","universe"],"properties":{"family":{"type":"string"},"expression":{"type":["string","object"]},"universe":{"type":"object","required":["name","instruments"],"properties":{"name":{"type":"string"},"instruments":{"type":"array","items":{"type":"string"}},"groups":{"type":"object"}}},"settings":{"type":"object"},"weights":{"type":"object"}}}},"required":["alpha"]}
```

Example input:

```json
{
  "alpha": {
    "family": "mom",
    "expression": "rank(ts_zscore(ret(20), 60) / vol(60))",
    "universe": {
      "name": "majors",
      "instruments": [
        "BTC",
        "ETH",
        "SOL",
        "HYPE",
        "XRP"
      ]
    }
  }
}
```

Returns: The standard output with saved.

### `alpha_list`

The user's saved alphas, oldest first: id, family, version, expression, grade, passed, sharpe, turnover. family filters to one family; empty lists all.

- Scope: `read`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"family":{"type":"string"}},"required":["family"]}
```

Example input:

```json
{
  "family": "mom"
}
```

Returns: Saved alphas: id, family, version, expression, grade, passed, sharpe, turnover.

### `alpha_get`

One saved alpha by id: the standard output and the rule as saved.

- Scope: `read`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"alpha_id":{"type":"string"}},"required":["alpha_id"]}
```

Example input:

```json
{
  "alpha_id": "a_51d0"
}
```

Returns: One saved alpha: the standard output and the rule.

### `alpha_propose_pod`

Propose a pod that trades saved alphas. One id proposes that alpha; 2 to 8 ids blend them at equal risk into a new library entry under family, which uses one daily check. The proposal card lands in the user's Lyra chat. It opens nothing; only the user's Start in the app opens the pod.

- Scope: `propose`
- Plan: Plus and above

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"alpha_ids":{"type":"array","items":{"type":"string"},"minItems":1,"maxItems":8},"family":{"type":"string"}},"required":["alpha_ids","family"]}
```

Example input:

```json
{
  "alpha_ids": [
    "a_51d0",
    "a_51d1"
  ],
  "family": "mom-blend"
}
```

Returns: The proposal card placed in your chat.

## Docs

### `docs_search`

Search the Lyra Labs docs, platform and alpha pages, with a plain question. Returns up to 10 sections, best first: page, title, heading and a line of context.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"query":{"type":"string"}},"required":["query"]}
```

Example input:

```json
{
  "query": "how does a check grade"
}
```

Returns: JSON list of {page, title, heading, line}, best first.

### `docs_get`

One page of the Lyra Labs docs as Markdown with its front matter. Platform pages: overview, getting-started, paper-and-live, chat, research, ideas, your-research, grading, telegram, pods, rules, loss-levels, risk-agent, watch, book, paper-fund, hyperliquid, alpaca, data-engine, fields, custom-data-engine, alpha-playground, ultra, mcp, mcp-tools, security, for-agents, plans, faq, glossary. Alpha pages: alpha/connect, alpha/grammar, alpha/operators, alpha/data, alpha/settings, alpha/output, alpha/checks, alpha/examples.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{"page":{"type":"string"}},"required":["page"]}
```

Example input:

```json
{
  "page": "grading"
}
```

Returns: One page as Markdown.

## Market data

### `data_fields`

The field catalog: each field's syntax, meaning, unit, scope, when it is known, its lag, whether delay 0 can use it, its coverage and the first stored date. No values.

- Scope: `read`
- Plan: Free

Input schema:

```json
{"type":"object","additionalProperties":false,"properties":{},"required":[]}
```

Example input:

```json
{}
```

Returns: JSON list of every field: syntax, meaning, unit, scope, known, lag, delay 0, coverage, first date.
