---
title: Watch and the weekly letter
summary: Each pod watches its names, news and drivers, checks its own structure and record, and Lyra sends one letter a week.
tags:
- watch
- wakes
- monitors
- letter
- weekly letter
- fading
- drift
- news
related:
- pods
- risk-agent
- telegram
- chat
---

# Watch and the weekly letter

## For agents

- Lets you: Know what wakes a pod and what the weekly letter holds.
- Tools: `pods_fund`
- Limit: Letters are read in the app and sent to Telegram; there is no MCP tool for them.

## What wakes the Trader

| Wake | When |
|---|---|
| Daily | 00:10 UTC |
| US open | 20 minutes before the US open, for pods with stocks |
| Funding | 15 minutes before funding, for carry pods |
| News | a story or filing that moves one of the pod's names |
| Filings and ratings | for pods with stocks |
| Price | a move of 3% for stocks, 5% for crypto |
| Drivers | a driver in the thesis moves past its threshold |


## What the monitors check

| Check | Watches | On drift | On a large move |
|---|---|---|---|
| `break_due` | A dated forecast in the thesis is due |  | the Trader wakes |
| `swing` | Yearly swing against the plan | noted in the letter | Lyra asks you |
| `offset` | How much the book moves with the market | the Trader wakes | Lyra asks you |
| `concentration` | The largest name's share of the book | rebalanced | Lyra asks you |
| `leverage` | Gross exposure against the plan | rebalanced | Lyra asks you |
| `funding` | Holding cost a month against the plan | noted in the letter | Lyra asks you |
| `overlap` | Overlap with another pod | noted in the letter | Lyra asks you |
| `cone` | Result against its tested range | noted in the letter | Lyra asks you |
| `cusum` | A steady fall below the tested result |  | marked fading |

- A decision reads like "Sober Curious: Swinging 31% a year, planned under 20%. Cut it back?"

## The weekly letter

- One per open fund, for the week to the last Sunday.
- What each pod did, what changed, what is next.
- The fund's paper or live result next to S&P 500 and BTC, over the same week.
- In the app under letters, and on Telegram.
