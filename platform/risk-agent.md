---
title: The Risk Agent
summary: An independent risk manager that sees every trade before it is placed. It can only reduce or block, and it reports to you.
tags:
- risk agent
- risk
- limits
- veto
- block
- reduce
- crowding
- overlap
- exposure
- platform caps
related:
- loss-levels
- pods
- watch
- security
---

# The Risk Agent

## For agents

- Lets you: Explain why a trade was reduced or blocked.
- Tools: `pods_explain`, `pods_fund`
- Limit: The Risk Agent never adds risk or opens a trade.

## Two layers

| Layer | Scope | Checks |
|---|---|---|
| Your fund | your pods | gross exposure, size per name, size per sector, loss levels, excluded names, caps you set, frozen names, overlap between pods, market beta |
| Platform | all users | Lyra's total per instrument, pro-rata scaling, pacing, capacity |

## Verdicts

- Pass: the trade goes as planned.
- Reduce: a smaller trade goes.
- Block: nothing goes.
- Every verdict is logged with its reason.
- `pods_explain` returns the plain-words note for a pod.

## Who it answers to

- You, not Lyra.
- Lyra cannot override it.
- It keeps working when you are out of credits.
