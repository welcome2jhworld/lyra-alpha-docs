---
title: Lyra Labs overview
summary: Lyra is your personal portfolio manager. It turns an idea into a checked pod, runs it on paper, and takes it live only when you press Start.
tags:
- overview
- lyra
- pm
- portfolio manager
- loop
- paper
- live
- venues
- markets
- plans
related:
- getting-started
- paper-and-live
- grading
- pods
- data-engine
- plans
---

# Lyra Labs overview

## For agents

- Lets you: Learn what Lyra Labs is, the core loop, the venues and the plans in one call.
- Tools: `docs_get`, `docs_search`, `pods_fund`, `pods_templates`
- Limit: Agents read and propose; only the user presses Start, applies an edit or moves money.

## What it is

- Lyra Labs makes Lyra, a personal portfolio manager (PM) for retail investors.
- Lyra is the PM you talk to. It proposes, checks, sizes and reports.
- Your money sits in pods. A pod is one idea with its own agents, book and forecasts.
- A Risk Agent stands between every idea and every trade. It can only reduce or block.
- Every pod starts on paper. Real money moves only after you press Start.

## Who it is for

- Investors with views ("Gen Z is drinking less") who want them tested before money moves.
- People who want minutes a week, not a strategy builder.
- Quants and agents who want to write rules and test them on Lyra's servers.

## The loop

```figure overview
Idea: Gen Z is drinking less → Data: sales, filings, prices → Lyra Data Engine: fields → Research and Quant: the last 15 times, it held 10 → Pod: Analyst and Trader → Book: CELH, MNST long; STZ, DEO short → Live: after you press Start
```

1. Idea. You say it in one sentence (Your Research), or pick one of Lyra's daily ideas (Public Research).
2. Check. Lyra tests the idea on past cases with a sealed final 365 days.
3. Pod. The idea becomes a pod draft: holdings, sizes, loss levels, what ends it.
4. Paper. The pod trades paper money first, with real prices.
5. Live. You move it to real money with Start.

## Paper and Live

- Hyperliquid paper: $10,000 per fund, real prices, every plan.
- Alpaca paper: the equity of your linked Alpaca paper account, read live. None linked, no stocks on paper.
- Live: your own Hyperliquid account and your own Alpaca account. Plus and above.
- A fund is Paper or Live. A pod lives in one fund.
- Details: [Paper and Live](paper-and-live.md).

## Venues

| Venue | What trades | Paper | Live |
|---|---|---|---|
| Hyperliquid | Crypto perps, HIP-3 equity perps | $10,000 per fund | yes, your account |
| Alpaca | US stocks and ETFs | your linked Alpaca paper account's equity, read live | yes, your Alpaca account (OAuth) |

## Plans

|  | Free | Plus | Pro | Ultra |
|---|---|---|---|---|
| Price a month | $0 | from $39 | from $199 | Custom — [book a call](https://uselyra.dev/contact/) |
| Length | 30 days | monthly or yearly | monthly or yearly | monthly or yearly |
| Open pods | 1 | 3 | 7 | 7 |
| Funds | 1 | 2 | 2 | 2 |
| Live money | no | yes | yes | yes |
| Credits a period | 100 once | 1,500 / 3,000 / 6,000 | 12,000 / 25,000 / 50,000 | 50,000 |
| Trial credits |  | 300 over 7 days | 1,500 over 7 days | 1,500 over 7 days |
| Checks a day | 3 | 30 | 200 | 200 |
| Past cases shown | last 2 years | last 5 years | full history | full history |
| Research depth | Quick research | Research | Deep research | Deep research |
| Credits per research run | 50 | 100 | 250 | 250 |
| Alpha tools over MCP | no | yes | yes | yes |
| Ultra workspace | no | no | no | by invite |

Full limits: [Plans and limits](plans.md).

## What runs under it

- Lyra Data Engine: raw inputs to point-in-time fields. [Lyra Data Engine](data-engine.md).
- Check engine: past cases, a sealed holdout, CPCV. [How a check grades](grading.md).
- Pods: an Analyst and a Trader per pod. [Pods](pods.md).
- Risk Agent: limits, loss levels, overlap. [The Risk Agent](risk-agent.md).
- MCP: your own agent reads and proposes. [Connect over MCP](mcp.md).
