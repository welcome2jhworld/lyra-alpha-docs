---
title: Loss levels
summary: 'Two levels per pod: at the first, its capital is reduced; at the second, it closes. Measured from the pod''s peak.'
tags:
- loss levels
- stop
- drawdown
- reduce
- reduced
- close
- peak
- risk
- limits
related:
- risk-agent
- pods
- chat
---

# Loss levels

## For agents

- Lets you: Read a pod's loss levels.
- Tools: `pods_fund`
- Limit: No MCP tool changes loss levels; the user sets them in chat or the app.

## Defaults

| Level | Default | Does |
|---|---|---|
| Reduce | -5% from the pod's peak | Cuts the pod's capital by 50% |
| Close | -7.5% from the pod's peak | Closes the pod |

## Bounds

- The close level is between 3% and 50%.
- The reduce level is between 0 and the close level. 0 turns it off.
- Set them for the fund (every pod's default) or for one pod.
- Lyra suggests every default; you change it in one line ("close Sober Curious at -10%").

## Who acts

- The Risk Agent enforces both levels. It does not ask first.
- On a live Hyperliquid account, stop orders sit on the venue as well.
