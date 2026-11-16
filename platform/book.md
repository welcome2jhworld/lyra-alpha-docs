---
title: The Book and venues
summary: The Book is every leg your pods hold. Each leg goes to one venue by one routing table.
tags:
- book
- positions
- venues
- routing
- hyperliquid
- alpaca
- legs
- orders
- fills
- perps
- stocks
related:
- hyperliquid
- alpaca
- paper-fund
- pods
---

# The Book and venues

## For agents

- Lets you: Know where a leg trades and why an order was refused.
- Tools: `pods_fund`
- Limit: Execution trades only Risk Agent verdicts. No tool places an order.

## Routing table

| Leg | Side | Fund | Goes to |
|---|---|---|---|
| Perp (crypto, HIP-3) | long | paper | Hyperliquid |
| Perp (crypto, HIP-3) | short | paper | Hyperliquid |
| Perp (crypto, HIP-3) | long | live | Hyperliquid |
| Perp (crypto, HIP-3) | short | live | Hyperliquid |
| US stock or ETF | long | paper | Alpaca |
| US stock or ETF | short | paper | Alpaca |
| US stock or ETF | long | live | Alpaca |
| US stock or ETF | short | live | refused: stock legs are long only; shorts and offsets go on a Hyperliquid perp |

- `US:<TICKER>` legs are US stocks or ETFs. They go to Alpaca on that ticker.
- Coins (`BTC`) and HIP-3 names (`xyz:<name>`) are perps on Hyperliquid.
- Alpaca needs an active connection for the fund's mode. Without one, stock legs are refused.

## Stock legs on equity perps

- With Alpaca connected, a pod's long stock legs on equity perps go to Alpaca on their real tickers.
- Only when they all fit in the room the `US:` legs leave.
- Longs that would need margin stay together on the equity perps.
- Shorts and crypto stay on Hyperliquid.
- A switch closes the old listing and opens the new one in one verdict.
- An Alpaca long holds while its connection is revoked or the market is closed.

## Alpaca room

- `US:` legs take the Alpaca cash room first: the pod's capital; on paper, at most the equity of your linked Alpaca paper account, read live.
- Held legs come before new ones.
- A leg that does not fit is cut to what is left.
- Fractional shares only for longs. Shorts are whole shares.
- Shorts (paper only) need Alpaca to mark the name shortable and easy to borrow.

## Orders and fills

- Orders net per account, then slice over time.
- Orders outside US market hours stay queued until they fill.
- Every fill books into the pod's ledger.
