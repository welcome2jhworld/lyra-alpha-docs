---
title: What agents can't do
summary: No agent, MCP tool, research run or Ultra workspace can place an order, move money or press Start. Tests enforce it.
tags:
- security
- safety
- agents
- permissions
- boundary
- orders
- money
- start
- keys
- limits
related:
- mcp
- mcp-tools
- hyperliquid
- alpaca
- ultra
---

# What agents can't do

## For agents

- Lets you: Know the hard limits on what an agent may do.
- Tools: none
- Limit: Read and propose only.

## Never through an agent

- Place, change or cancel an order.
- Open a pod (Start).
- Apply a pod edit.
- Change loss levels or start sizes.
- Deposit, withdraw or move money between funds.
- Connect or disconnect a broker.
- Go live.
- Change the plan or pay.

## How it is enforced

- The MCP package imports no execution, live, billing, credits, accounts or Start module. A test fails if it does.
- The MCP context refuses every message to the trading bus.
- Every tool wraps a chat tool that only reads or proposes; a test lists them.
- A test runs every tool on a real database with the money path cut and checks no money row changed.
- The Ultra Engineer has no MCP, no vaults and no broker or exchange hosts.

## Tokens

- Scopes: `read`, or `read` and `propose`.
- Stored as hashes; shown once.
- 60 calls a minute per user, bursts of 20.
- Revoke any time.

## Keys and accounts

- Hyperliquid: Lyra's agent key places orders and cannot withdraw.
- Alpaca: an OAuth token you can revoke at Alpaca or in Lyra; it is sealed at rest.
- A revoked Alpaca token leaves your positions where they are.
