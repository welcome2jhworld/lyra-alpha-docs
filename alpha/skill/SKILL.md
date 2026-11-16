---
name: lyra-alpha
description: Build, test and submit Lyra alphas through the Lyra MCP with the loop validate, simulate, read the result, revise, submit. Use when the user wants to research a trading signal for Lyra, write an alpha expression, or run a Lyra simulation.
---

# Lyra alphas

An alpha is one expression over a universe of instruments. Lyra runs every backtest on its own servers. You see aggregate numbers and a short curve, never daily data.

## Setup

1. The user needs Lyra Plus or Pro and a token from `POST https://api.uselyra.dev/api/v2/mcp/tokens`.
2. Connect: `claude mcp add --transport http lyra https://api.uselyra.dev/mcp --header "Authorization: Bearer <token>"`
3. Read `https://docs.uselyra.dev/llms.txt`, or call `docs_get` with `grammar`, `operators`, `settings` and `checks`. Call `data_fields` before you use a field.

## Loop

1. Write the hypothesis in one sentence before any expression: what pays, why, and what would prove it wrong.
2. `alpha_validate` until it passes. It is free. Fix the column the error points at.
3. `alpha_simulate` once. It spends one check: Plus has 30 a day, Pro 200, shared with the Lyra app.
4. Read the result: `grade`, `report.sharpe`, `report.turnover`, `report.max_drawdown`, each year in `report.years`, and every entry in `checks`. A good whole-period sharpe carried by one year is a weak result.
5. Revise only for a reason you can state from the hypothesis, then simulate again.
6. `alpha_submit` when every check passes. It saves the next version to the user's library.
7. `alpha_propose_pod` with saved ids when the user wants to trade them. The user presses Start in the app. You cannot start a pod.

## Rules against overfitting

- Every distinct version you simulate counts as a trial of its family. `trial_no` is in the output, and the bar to pass rises with it.
- Do not sweep windows or constants to find the best number. Pick a window from the hypothesis and keep it.
- Do not change the universe to drop names that lose.
- Keep one family per idea. A new family name for the same idea is still the same idea.
- 8 variants of one expression shape within 60 minutes close simulation for the rest of the UTC day.
- The 365 days before the current quarter are sealed. They open once, only after the history passes. A failed holdout is a real failure; do not rerun it with small changes.
- A book of fewer than 5 names on average returns stats only, no curve.

## Report to the user

Give the hypothesis, the expression, trial_no, the grade, sharpe, turnover, the worst year, and which checks failed. Say plainly when the idea did not work.
