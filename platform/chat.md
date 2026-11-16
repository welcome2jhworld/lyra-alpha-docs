---
title: Chat with Lyra
summary: Talk to Lyra in the app or on Telegram. It answers with numbers from code and cards you act on.
tags:
- chat
- chat with lyra
- lyra
- pm
- conversation
- cards
- buttons
- decisions
- credits
- messages
related:
- research
- your-research
- telegram
- plans
- security
---

# Chat with Lyra

## For agents

- Lets you: Know what Lyra can do in chat and where an agent's proposals land.
- Tools: `pods_fund`, `pods_explain`, `pods_propose`, `pods_propose_edit`
- Limit: Each message to Lyra draws its real AI cost in credits, at least 1.
- Limit: A proposal from an agent lands in this chat as a card; the user acts on it.

## What Lyra does in chat

- Drafts a pod from your idea.
- Runs a check on a claim and reads the result back in one line.
- Starts research on a loose view.
- Proposes prebuilt pods that fit your fund.
- Shows your fund: pods, money, state, loss levels.
- Explains what the Risk Agent changed and why.
- Edits a pod's weights or loss levels when you ask.
- Closes a pod when you ask.
- Reads market data: prediction markets, 13F holdings, congress trades, rates, ETF holdings, whale positions.

## Cards

| Card | Buttons | What the button does |
|---|---|---|
| Pod proposal | Start, Edit, Stop | Start opens the pod; Edit changes it first; Stop drops it |
| Pod edit | Apply | Applies the new weights |
| Decision | Lyra's choices | Records your answer |
| Out of credits | plan or pack | Opens checkout |

- Numbers on cards come from code, not from the model.
- A card from your own agent (over MCP) is labelled "From <token name>".

## Credits

- A message to Lyra: its real AI cost, rounded up, at least 1 credit.
- 1 credit is $0.01 of AI cost.
- Running pods never draws credits.
- At zero: Lyra says so once and offers the next plan or pack. Pods keep trading and the Risk Agent keeps watching.
- Credits per plan: [Plans and limits](plans.md).

## Quiet by default

- Lyra writes when you are needed: a decision, a thesis break, a Risk Agent block that matters.
- A weekly letter covers the rest: [Watch and the weekly letter](watch.md).
