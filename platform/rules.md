---
title: Rule pods
summary: A rule pod trades a formula whose check graded Awesome Idea. A daily job sets its targets; the Trader steps in only on exceptions.
tags:
- rule
- rule pod
- formula
- alpha
- daily job
- decaying
- deviation
- awesome idea
related:
- grading
- alpha-playground
- pods
- custom-data-engine
---

# Rule pods

## For agents

- Lets you: Attach a checked rule or alpha to a pod through a proposal.
- Tools: `alpha_propose_pod`, `test_run_check`
- Limit: Only a check graded Awesome Idea can attach a rule to a pod.
- Limit: The rule job runs once a day at 02:00 UTC.

## How it runs

- A rule is a formula over Lyra's fields, a universe and a weight mapping.
- It attaches to a pod only with a check graded Awesome Idea.
- Every day at 02:00 UTC, after the close is known, the job writes the pod's targets.
- The Trader wakes only on exceptions.
- A book the Trader submits on a rule pod is a recorded deviation with a reason.
- The Risk Agent still checks every trade.

## Decay

- Lyra keeps the rule's tested range.
- A rule whose live result stays under that range is marked decaying.
- Watch flags a steady fall as fading. [Watch and the weekly letter](watch.md).

## Example formula

```text
rank(ts_zscore(ret(20), 60) / vol(60))
```

- Language and operators: [Alpha Playground](alpha-playground.md).
