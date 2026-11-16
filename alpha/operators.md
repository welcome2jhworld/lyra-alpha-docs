# Operators

Arguments named x, a, b, c and of take expressions. days, lo, hi, n, std, above and below take numbers. market, metric and entity take quoted strings.

## Functions

| Call | Meaning |
|---|---|
| `ret(days)` | Close-to-close return over days. |
| `vol(days)` | Annualised standard deviation of daily returns over days. |
| `funding(days)` | Mean daily perp funding over days, annualised. |
| `odds(market)` | Yes price of one prediction market, the same value for every instrument. |
| `obs(metric, entity)` | A stored metric for an entity. Instrument metrics can be written by name alone. |
| `ts_delay(x, days)` | x as it was days ago. |
| `ts_delta(x, days)` | x minus x days ago. |
| `ts_mean(x, days)` | Rolling mean of x over days. |
| `ts_std_dev(x, days)` | Rolling standard deviation of x over days. |
| `ts_zscore(x, days)` | x minus its rolling mean, over its rolling standard deviation. |
| `ts_rank(x, days)` | Where today's x sits among the last days values, from 0 (lowest) to 1 (highest). |
| `ts_decay_linear(x, days)` | Weighted mean over days, newest day weighted most. |
| `ts_max(x, days)` | Rolling maximum over days. |
| `ts_min(x, days)` | Rolling minimum over days. |
| `ts_argmax(x, days)` | Days since the rolling maximum. |
| `ts_argmin(x, days)` | Days since the rolling minimum. |
| `ts_sum(x, days)` | Rolling sum over days. |
| `ts_product(x, days)` | Rolling product over days. |
| `ts_corr(a, b, days)` | Rolling correlation of a and b over days. |
| `ts_cov(a, b, days)` | Rolling covariance of a and b over days. |
| `sign(x)` | -1, 0 or 1. |
| `abs(x)` | Absolute value. |
| `log(x)` | Natural log; empty where x is not positive. |
| `sigmoid(x)` | 1 / (1 + exp(-x)). |
| `not(x)` | 1 where x is not positive, else 0. |
| `clip(x, lo, hi)` | x held between lo and hi. |
| `rank(x)` | Cross-sectional rank across the universe, from -0.5 to 0.5. |
| `zscore(x)` | Cross-sectional z-score across the universe. |
| `demean(x)` | x minus the universe mean. |
| `scale(x)` | x divided by the sum of absolute values across the universe. |
| `group_rank(x)` | rank within each universe group. |
| `group_zscore(x)` | zscore within each universe group. |
| `group_neutralize(x)` | demean within each universe group. |
| `group_scale(x)` | scale within each universe group. |
| `winsorize(x, std=)` | x held within std standard deviations of the universe mean. |
| `bucket(x, n)` | Cross-sectional bucket number, 0 to n - 1. |
| `threshold(x, above=, below=)` | 1 above above, -1 below below, else 0. |
| `add(of)` | Sum of 2 to 8 inputs. |
| `mul(of)` | Product of 2 to 8 inputs. |
| `avg(of)` | Mean of 2 to 8 inputs. |
| `min(of)` | Smallest of 2 to 8 inputs. |
| `max(of)` | Largest of 2 to 8 inputs. |
| `power(a, b)` | a to the power b. |
| `and(a, b)` | 1 where a and b are both positive, else 0. |
| `or(a, b)` | 1 where a or b is positive, else 0. |
| `if_else(c, a, b)` | a where c is positive, else b. |

## Infix

| Symbol | Meaning |
|---|---|
| `+` | a plus b. |
| `-` | a minus b, or minus x with one input. |
| `*` | a times b. |
| `/` | a over b; empty where b is 0. |
| `>` | 1 where a > b, else 0. |
| `<` | 1 where a < b, else 0. |
| `>=` | 1 where a >= b, else 0. |
| `<=` | 1 where a <= b, else 0. |
| `==` | 1 where a equals b, else 0. |
| `-` | a minus b, or minus x with one input. |

Precedence from loose to tight: comparisons (>, <, >=, <=, ==), then `+ -`, then `* /`, then unary minus. Comparisons do not chain; use `and(a, b)`.
