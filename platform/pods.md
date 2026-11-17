---
title: Pods
summary: A pod is one idea with its own Analyst, Trader, book and forecasts. Lyra runs several in one fund.
tags:
- pod
- pods
- analyst
- trader
- trade agent
- book
- forecasts
- thesis
- prebuilt
- template
- private
- states
related:
- rules
- loss-levels
- risk-agent
- watch
- book
---

# Pods

## For agents

- Lets you: List, explain and propose pods, and propose weight edits.
- Tools: `pods_templates`, `pods_fund`, `pods_explain`, `pods_propose`, `pods_propose_edit`
- Limit: Open pods per plan: Free 1, Plus 3, Pro 7, Ultra 7.
- Limit: An agent proposes; the user's Start opens a pod and the user's Apply applies an edit.

## Inside a pod

```figure pods
Analyst: own drinks that replace alcohol, short brewers and distillers → Trader: CELH 30%, MNST 20%, short STZ 20%, short DEO 20% → Book: the legs as held → Rule fires: CELH raised its sales outlook, CELH 30% to 33% → Risk: pod -5% from peak, capital reduced
```

| Part | Does |
|---|---|
| Analyst | Writes the thesis, its drivers as dated forecasts, and what would break it; reviews it every 7 days |
| Trader | Keeps the book in line with the thesis; wakes on watch rules and sets targets |
| Book | The legs as held, on each venue |
| Forecasts | Dated and locked; the scorer settles them against real data |

- Users see the Analyst and the Trader together as the Trade Agent.
- No pod grades itself.

## Prebuilt and private

| | Prebuilt | Private |
|---|---|---|
| Source | Lyra's template catalog | your idea or a research run |
| Agents | one Trade Agent serves every holder | yours alone |
| Your tweaks | capital, limits, filters | everything |

## States

| State | Means |
|---|---|
| `funding` | Waiting for money to arrive |
| `active` | Trading |
| `halved` | Reduced: capital cut by 50% at the reduce loss level |
| `paused` | Not trading; positions kept |
| `closed` | Positions closed |

## The order path

1. The Trader (or the daily rule job on a rule pod) sets targets.
2. Targets become one intent per pod.
3. The Risk Agent for your fund passes, reduces or blocks.
4. The platform Risk Agent caps Lyra's total per instrument across users.
5. Execution trades only the verdict, on the venue for each leg.
6. Fills book into the pod. Marks update its equity daily.

## Benchmarks

- Every pod is shown next to S&P 500 and BTC buy-and-hold.
