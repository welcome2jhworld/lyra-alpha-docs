---
title: Alpha Playground
summary: Write alphas in a small expression language, test them on Lyra's servers, and run the ones that pass as pods.
tags:
- alpha
- alpha playground
- quant
- expression
- dsl
- simulate
- submit
- operators
- settings
- output
related:
- alpha/connect
- alpha/grammar
- alpha/operators
- alpha/data
- alpha/settings
- alpha/output
- alpha/checks
- alpha/examples
---

# Alpha Playground

## For agents

- Lets you: Validate, simulate, submit and propose alphas as pods.
- Tools: `alpha_validate`, `alpha_simulate`, `alpha_submit`, `alpha_list`, `alpha_get`, `alpha_propose_pod`, `data_fields`
- Limit: Plus and above.
- Limit: Simulate and submit use the plan's daily checks: Plus 30, Pro and Ultra 200.
- Limit: More than 8 versions of one shape in 60 minutes stops simulation for the day.

## The loop

1. `alpha_validate`: free, unlimited. Fix errors by column.
2. `alpha_simulate`: one daily check. Read the grade, report and submission checks.
3. Revise once with a reason. Every version is a trial.
4. `alpha_submit`: saves to your library when every check passes.
5. `alpha_propose_pod`: one alpha, or 2 to 8 blended at equal risk. The card lands in your chat.
6. Press Start in the app.

## Example

```json
{"alpha": {"family": "mom", "expression": "rank(ts_zscore(ret(20), 60) / vol(60))",
  "universe": {"name": "majors", "instruments": ["BTC", "ETH", "SOL", "HYPE", "XRP"]},
  "settings": {"delay": 1, "neutralization": "universe"}}}
```

## Reference pages

These pages are generated from the code's registries.

- [Connect over MCP](../alpha/connect.md): tokens, the URL, the tools, checks a day.
- [Expression language](../alpha/grammar.md): text and JSON forms.
- [Operators](../alpha/operators.md): every function and infix operator.
- [Data sheet](../alpha/data.md): every field, unit, when it is known.
- [Settings](../alpha/settings.md): delay, decay, neutralization, rebalance, truncation, weights, limits.
- [Output](../alpha/output.md): the standard output of a simulation.
- [Submission checks](../alpha/checks.md): what submit requires.
- [Example alphas](../alpha/examples.md): one pattern each.
- [Claude Code skill](../alpha/skill/SKILL.md): the loop as a skill.

## What a curve shows

- At most 250 points, starting at 1.
- None unless the book averages at least 5 effective names.
