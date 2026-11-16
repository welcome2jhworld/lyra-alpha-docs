---
title: Your Research
summary: 'Your own view, in one sentence, becomes a research run: a claim, a check, a read and a fund card you can start on paper.'
tags:
- your research
- research
- research run
- idea
- claim
- thesis
- draft
- private pod
- basket
- depth
- deep research
- fund card
- credits
related:
- research
- ideas
- grading
- pods
- chat
---

# Your Research

## For agents

- Lets you: Turn a user's view into a checkable claim, a research run and a pod draft.
- Tools: `test_run_check`, `build_research`, `build_runs`, `build_run`, `build_pod`
- Limit: A check uses one of the plan's daily checks unless the same spec already ran: Free 3, Plus 30, Pro and Ultra 200.
- Limit: Quick 50, Research 100, Deep 250 credits per run, charged at start; rebuilding a card costs 120; Free gets 1 for 0, then needs Plus.
- Limit: A run takes several minutes.

## From sentence to pod

```figure ideas
You: Gen Z is drinking less → Lyra: by when, and what proves it wrong? → Claim: drinks that replace alcohol beat brewers and distillers → Check: held in 10 of 15 past cases → Draft: CELH, MNST long; STZ, DEO short
```

## What a draft holds

- Claim: one testable sentence.
- Holdings: each leg, its side and weight.
- Check: the grade and the past-case count.
- Ends if: what would prove it wrong ("beer sales bounce back").
- Horizon: how long the claim is meant to hold.
- Loss levels: halve and close.
- Money: the share of your fund it takes.

## Claim types

| Type | Shape | Needs |
|---|---|---|
| `direction` | one basket beats a benchmark | `benchmark` |
| `theme` | a theme basket beats a benchmark | `benchmark` |
| `relative` | longs beat shorts | a short leg, no benchmark |
| `event` | a move after given dates | `events` |
| `odds` | a move after a prediction market crosses a level | `market`, `level`, `cross` |
| `regime` | a side while a condition holds | `condition`, `side` |
| `carry` | holding cost and funding over days | `days` |
| `rule` | a formula sets the weights | `formula` |

## Example check

Input to `test_run_check`:

```json
{"spec": {"claim": "Drinks that replace alcohol beat brewers and distillers over the next quarter",
  "family": "sober-curious", "type": "relative",
  "universe": {"long": ["US:CELH", "US:MNST"], "short": ["US:STZ", "US:DEO"]}, "benchmark": "",
  "checks": ["past_cases", "holding_cost"], "start": "2016-06-01", "horizon_days": 90,
  "capital": 3000, "leverage": 1, "market": "", "level": 0.5, "cross": "up", "condition": "",
  "side": "long", "days": 0, "formula": ""}}
```

Output shape (numbers are an example):

```json
{"grade": "leans_yes", "label": "Good Idea", "line": "10 of 15 past cases", "versions_tried": 1,
 "as_of": "2026-11-16", "past_cases": {"wins": 10, "cases": 15, "mean": 0.031,
 "period": ["2016-06-01", "2025-11-16"]}, "holding_cost_month": 0.004}
```

- `curve` is added when the book holds at least 5 names on average: at most 250 points starting at 1.
- A hand-picked basket grades at most Good Idea. Why: [How a check grades](grading.md).

## Depth by plan

| Plan | Depth | Credits | Reads |
|---|---|---|---|
| Free | Quick research | 50 | web, tickers |
| Plus | Research | 100 | web, filings, data, tickers |
| Pro, Ultra | Deep research | 250 | web, papers, filings, data, tickers, plus a second reviewer |

## What comes back

- A read: what the view claims, in plain words.
- The check: grade and past cases. [How a check grades](grading.md).
- A fund card: holdings, sizes, loss levels, holding cost.
- What ends it.
- Both land in your Lyra chat.

## Rebuild the card

- Drop symbols, add picks, lean (conviction 1 to 3 per symbol).
- Structure: `single` or `main_offset` (a main basket with an offset).
- `insist`: build despite Not sure.
- Code sets the weights, the offset, the size and the loss levels. The check stays the run's.
- Tool: `build_pod`. Example input: [MCP tool reference](mcp-tools.md).

## When Lyra holds off

- The check did not run.
- The past cases do not back it.
- The check is newer than the prices.
- Some names have too little price history.
- It would repeat a pod you already hold.
- It adds risk to your fund without enough reward.
- The money for it is too small to place every order.

## Credits

- Charged at start; the charge is the run's cost ceiling.
- A refused run is refunded.
- A run that errors early is refunded, up to 3 a month.
- Out of credits: the run is refused before any spend.
