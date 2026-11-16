---
title: Connect Alpaca
summary: Connect your own Alpaca account with OAuth to trade US stocks and ETFs, on paper or live.
tags:
- alpaca
- oauth
- connect
- broker
- us stocks
- etf
- paper
- live
- shorts
- market hours
related:
- book
- paper-fund
- paper-and-live
- security
---

# Connect Alpaca

## For agents

- Lets you: Explain how stock legs reach the user's Alpaca account.
- Tools: `pods_fund`
- Limit: No tool connects or disconnects Alpaca.
- Limit: Live stock legs are long only.

## Connect

1. Start the connection for `paper` or `live`.
2. Alpaca asks you to approve Lyra (scopes: trading, data).
3. Alpaca sends you back to Lyra, which finishes the connection.
4. One connection per mode. Disconnect drops the token.

API:

```http
POST /api/v2/alpaca/connect   {"env": "paper"}
POST /api/v2/alpaca/finish    {"code": "...", "state": "..."}
DELETE /api/v2/alpaca/connections/paper
```

## Rules

- Paper connects to Alpaca paper; Live to your Alpaca live account.
- Shorts: paper only; refused on live.
- Shorts need Alpaca to mark the name shortable and easy to borrow; whole shares.
- Fractional shares for longs.
- Outside market hours, orders stay queued until they fill.

## Revoked or expired

- If Alpaca rejects the token, the connection is marked revoked once.
- You get one notice from the Risk Agent.
- Positions stay where they are. Nothing is sold for you.

## Reconcile

- On connect and once a day, Lyra reads your Alpaca account.
- It books fills Alpaca made that its ledger missed.
- It reports shares it does not hold.
- It never places an order while reconciling.
