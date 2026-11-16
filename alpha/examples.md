# Example alphas

Each example is a complete `alpha` argument for `alpha_validate`, `alpha_simulate` and `alpha_submit`. Each line under it says what the output carries.

## Cross-sectional momentum

```
rank(ret(90))
```

```json
{
  "family": "mom-90",
  "expression": "rank(ret(90))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "rebalance": "monthly"
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned. Monthly rebalance keeps turnover low.

## Short-term reversal

```
rank(-ret(5))
```

```json
{
  "family": "reversal-5",
  "expression": "rank(-ret(5))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "decay": 3
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned. Turnover is high; decay 3 smooths it.

## Risk-adjusted momentum

```
rank(ts_zscore(ret(20), 60) / vol(60))
```

```json
{
  "family": "mom-riskadj",
  "expression": "rank(ts_zscore(ret(20), 60) / vol(60))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "rebalance": "weekly"
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned.

## Low volatility, long only

```
rank(-vol(60))
```

```json
{
  "family": "low-vol",
  "expression": "rank(-vol(60))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "rebalance": "monthly"
  },
  "weights": {
    "scheme": "proportional",
    "side": "long"
  }
}
```

Long only, so the book carries market beta. Every name is held.

## Funding carry

```
rank(-funding(7))
```

```json
{
  "family": "carry-7",
  "expression": "rank(-funding(7))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {}
}
```

Funding is known at the close, but perps fill at delay 1; delay 0 is for US: stocks filled at the next open.

## Single-name trend filter

```
if_else(close > ts_mean(close, 200), 1, 0)
```

```json
{
  "family": "btc-trend",
  "expression": "if_else(close > ts_mean(close, 200), 1, 0)",
  "universe": {
    "name": "btc-trend",
    "instruments": [
      "BTC"
    ]
  },
  "settings": {
    "rebalance": "weekly"
  },
  "weights": {
    "scheme": "equal",
    "side": "long"
  }
}
```

One instrument, so breadth is at most 1 and the output has stats only, no curve.

## Price z-score reversion

```
clip(-ts_zscore(close, 20), -2, 2)
```

```json
{
  "family": "zrev-20",
  "expression": "clip(-ts_zscore(close, 20), -2, 2)",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "neutralization": "universe"
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned. Neutralization removes the market move.

## Volume shock with direction

```
rank(ts_zscore(volume, 30) * sign(ret(1)))
```

```json
{
  "family": "volume-shock",
  "expression": "rank(ts_zscore(volume, 30) * sign(ret(1)))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "decay": 5
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned.

## Momentum gated by credit spreads

```
if_else(macro.hy_spread < ts_mean(macro.hy_spread, 60), rank(ret(30)), 0)
```

```json
{
  "family": "credit-gate",
  "expression": "if_else(macro.hy_spread < ts_mean(macro.hy_spread, 60), rank(ret(30)), 0)",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {}
}
```

Flat while spreads are wide, so breadth averages below the universe size. The spread is published late, so delay stays 1.

## Group-neutral momentum

```
group_rank(ret(60))
```

```json
{
  "family": "sector-mom",
  "expression": "group_rank(ret(60))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ],
    "groups": {
      "layer1": [
        "ADA",
        "AVAX",
        "BNB",
        "BTC",
        "ETH",
        "SOL",
        "SUI",
        "XRP"
      ],
      "apps": [
        "AAVE",
        "DOGE",
        "LINK",
        "UNI"
      ]
    }
  },
  "settings": {
    "neutralization": "group"
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned. Ranks within each group, so the book is balanced across groups.

## Contrarian positioning

```
rank(-binance.top_ls)
```

```json
{
  "family": "crowding",
  "expression": "rank(-binance.top_ls)",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {}
}
```

Names without Binance data drop out on those days. Delay stays 1.

## Autocorrelation

```
rank(-ts_corr(ret(1), ts_delay(ret(1), 1), 60))
```

```json
{
  "family": "autocorr",
  "expression": "rank(-ts_corr(ret(1), ts_delay(ret(1), 1), 60))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {}
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned.

## Top and bottom four

```
rank(ret(30))
```

```json
{
  "family": "top-bottom",
  "expression": "rank(ret(30))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "rebalance": "weekly"
  },
  "weights": {
    "scheme": "equal",
    "side": "long_short",
    "top_n": 4
  }
}
```

Four longs and four shorts at equal weight, so breadth is near 8 and the curve is returned.

## Composite of three

```
avg(rank(ret(90)), rank(-vol(60)), rank(-funding(7)))
```

```json
{
  "family": "composite",
  "expression": "avg(rank(ret(90)), rank(-vol(60)), rank(-funding(7)))",
  "universe": {
    "name": "majors",
    "instruments": [
      "AAVE",
      "ADA",
      "AVAX",
      "BNB",
      "BTC",
      "DOGE",
      "ETH",
      "LINK",
      "SOL",
      "SUI",
      "UNI",
      "XRP"
    ]
  },
  "settings": {
    "rebalance": "weekly"
  }
}
```

Holds every name. Weights proportional to a rank give a breadth of about three quarters of the universe, so the curve is returned. Averaging ranks spreads the risk across three ideas.
