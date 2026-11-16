# Output

`alpha_simulate`, `alpha_submit` and `alpha_get` return one JSON object. There is no daily series.

| Field | Meaning |
|---|---|
| `id` | Library id; null until the alpha is submitted and saved. |
| `family` | Your name for the idea. Versions count within a family. |
| `version` | Library version; null until saved. |
| `expression` | The canonical text form of what was tested. |
| `grade` | held_up (Awesome Idea) / leans_yes (Good Idea) / no_sign (Not sure) / cant_test_yet (Impossible to verify). |
| `passed` | True when every submission check passed. |
| `trial_no` | How many distinct versions of this family you have tested. The bar rises with it. |
| `as_of` | The day the test ran. |
| `data_end` | The last day of data in the test. |
| `report` | Whole-period numbers and the same numbers for each calendar year. |
| `checks` | The submission checks, each with passed, value and limit. |
| `breadth` | Effective number of names held on an average day. |
| `curve` | Up to 250 [date, equity] points starting at 1. Present only when breadth is at least 5. |

## Report numbers

The report and each entry of `report.years` carry these numbers. `report` also carries `delay`, `rebalance` and `years`; each year carries `year`.

| Number |
|---|
| `days` |
| `sharpe` |
| `annual_return` |
| `turnover` |
| `max_drawdown` |
| `fitness` |
| `margin_bps` |

`sharpe` is annualised over 365 days, or 252 weekday sessions for a stock universe. `turnover` is the mean daily traded share of gross, per session for stocks. `fitness` is sharpe times the square root of abs(annual_return) over max(turnover, 0.125). `margin_bps` is net return per unit traded, in basis points.

## Simulation

History starts 2000-01-01 or at the first day of data. The 365 days before the current quarter are a sealed holdout. Past cases are 30-day blocks. Perps fill at the 02:00 UTC hourly average after the close, stocks at the next open. Returns are net of fees, spread, impact, borrow, margin and perp funding.
