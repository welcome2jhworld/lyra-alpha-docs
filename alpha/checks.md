# Submission checks

`alpha_submit` saves an alpha to your library only when every check passes.

| Check | Passes when |
|---|---|
| `sharpe` | at least 1.25 with delay 1, 2.0 with delay 0 |
| `turnover` | at most 0.7 |
| `self_correlation` | below 0.7 against every alpha in your library, over at least 60 shared days |
| `pod_correlation` | below 0.7 against the current book of every open pod you hold |
| `holdout` | the sealed 365 days before the current quarter opened and agreed with the history |
| `trials` | the result clears a bar that rises with trial_no |
| `breadth` | the book holds at least 10 names on a median day |
| `capacity` | at most 5% of trades exceed the capacity cap |
| `cpcv` | most combinatorial purged cross-validation paths are positive |

## Quota

`alpha_validate` is free and unlimited. `alpha_simulate`, `alpha_submit` and a blended `alpha_propose_pod` share the plan's daily checks with checks in the Lyra app. A spec already tested today costs nothing. Checks reset at 00:00 UTC.

| Plan | Checks a day |
|---|---|
| plus | 30 |
| pro | 200 |
| ultra | 200 |

## Repeated variants

8 or more distinct variants of one expression shape within 60 minutes close `alpha_simulate` and `alpha_submit` for the rest of the UTC day. A shape ignores numbers and instruments, so changing a window or a symbol is still the same shape.
