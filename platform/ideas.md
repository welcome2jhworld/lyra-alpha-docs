---
title: Ideas
summary: Lyra posts 3 ideas a day in Research, Public Research. Each comes from a daily scan, tested against past cases and a false-discovery control.
tags:
- ideas
- daily ideas
- public research
- scan
- patterns
- second look
- discovery
- fdr
- like
- start on paper
related:
- research
- your-research
- grading
- pods
---

# Ideas

## For agents

- Lets you: Explain where the daily ideas come from and how much to trust them.
- Tools: `test_run_check`, `pods_fund`
- Limit: Ideas are read in the app; there is no MCP tool for them and they are never pushed.

## How Lyra finds them

- Every day after the close, for liquid perps and every instrument in a running pod.
- Patterns:
  - a 55-day closing high
  - a 55-day closing low
  - funding in its top 5% of a year
  - funding in its bottom 5% of a year
- Each firing runs as an event check on point-in-time prices.

## Stages

| Stage | When |
|---|---|
| Discovery | It passes the running false-discovery test (level 0.05) and the check gate |
| Second look | It just misses (raw p under 0.1), yet the same rise shows in the latest 20% of tested days (p under 0.05, at least 5 cases) and in at least 60% of 3 or more similar instruments |
| Not sure | Neither |

- Second look reads only days before the sealed period starts.
- An idea keeps the check's grade only at Discovery.

## Where it shows

- Research, Public Research tab.
- 3 ideas a day, kept by day, newest first.
- Each idea: ♡ like, Check, Start on paper.
- Ideas that touch your pods show on those pods.
- Ideas are never pushed.
