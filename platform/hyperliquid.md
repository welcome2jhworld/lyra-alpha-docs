---
title: Hyperliquid perps
summary: Live perps trade on your own Hyperliquid account. Lyra places orders with an agent key that cannot withdraw.
tags:
- hyperliquid
- perps
- live
- deposit
- usdc
- agent key
- withdraw
- stops
- hip-3
- crypto
related:
- paper-and-live
- book
- risk-agent
- security
---

# Hyperliquid perps

## For agents

- Lets you: Explain how live Hyperliquid accounts are set up and protected.
- Tools: `pods_fund`
- Limit: No tool deposits, withdraws or opens a live fund.

## Set up

1. On Plus or above, ask Lyra to go live.
2. Choose: bring your Paper pods, or start fresh.
3. Deposit USDC. Lyra bridges it to your Hyperliquid account.
4. The fund opens once at least $150 has arrived.

## Minimums

- Fund: $150 to start.
- Pod: $150 each.
- Under $300, the fund runs one pod.
- A Hyperliquid deposit under 5 USDC is lost by Hyperliquid, so Lyra refuses it.

## Keys and money

- The account is yours.
- Lyra trades it with an agent key: it can place and cancel orders.
- An agent key cannot withdraw.
- Withdrawals go to your own address and need you.

## Protection

- Stop orders for each live leg sit on Hyperliquid.
- Loss levels close or halve pods. [Loss levels](loss-levels.md).
- The Risk Agent checks every order first.
