# Settings

| Setting | Default | Allowed |
|---|---|---|
| `delay` | 1 | 0 / 1 |
| `decay` | 0 | 0 to 60 |
| `neutralization` | none | none / universe / group |
| `rebalance` | daily | daily / weekly / monthly / quarterly |
| `truncation` | 0.1 | above 0 to 3 |

`delay` 1 trades on the next close after the signal; delay 0 trades on the same close and needs every input known at the close. `decay` applies ts_decay_linear over that many days to the final signal. `neutralization` demeans the signal across the universe or within each group. `rebalance` sets how often the book is rebuilt; it is held in between. `truncation` caps each name's weight as a share of capital.

## Weights

`weights.scheme` is `proportional` (default), `equal`, `rank` or `inverse_vol`. `weights.side` is `long_short` (default), `long` or `short`. Optional: `top_n`, `neutral`, `vol_days`, `gross`, `vol_target`.

```json
{"scheme": "proportional", "side": "long_short"}
```

## Limits

| Limit | Value |
|---|---|
| Nodes in one expression | 64 |
| Expression depth | 12 |
| Look-back, days, summed along the deepest path | 750 |
| Instruments in a universe | 1 to 60 |
| Instruments for a cross-sectional operator | at least 3 |
| Inputs to add, mul, avg, min, max | 2 to 8 |
| days in ret, funding, ts_delay, ts_delta | 1 to 400 |
| days in vol and rolling operators | 2 to 400 |
