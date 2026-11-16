---
title: Connect over MCP
summary: Give your own AI agent a token and it can read your fund, run checks, research and propose, through the Lyra MCP.
tags:
- mcp
- model context protocol
- agent
- token
- claude code
- connect
- api
- scopes
- proposals
- prompt
- resources
related:
- mcp-tools
- security
- for-agents
- alpha/connect
---

# Connect over MCP

## For agents

- Lets you: Connect an agent to Lyra and know what it may call.
- Tools: `docs_get`, `docs_search`
- Limit: 60 tool calls a minute per user, bursts of 20.
- Limit: At most 10 active tokens per user.
- Limit: Alpha tools need Plus or above.

## Agent and Lyra

```figure mcp
Your agent → read: fund, data, docs → propose: a card in your Lyra chat → Lyra → You: Start, Apply, money moves
```

## Tokens

| Scope | Allows |
|---|---|
| `read` | every read tool (always included) |
| `propose` | tools that put a card in your Lyra chat |

Create one while signed in:

```bash
curl -X POST https://api.uselyra.dev/api/v2/mcp/tokens \
  -H "Authorization: Bearer <session>" -H "Content-Type: application/json" \
  -d '{"name": "Claude Code", "scopes": ["read", "propose"]}'
```

- The response carries the token once. It starts with `lyra_pat_`.
- Lyra keeps only a hash.
- List: `GET /api/v2/mcp/tokens`. Revoke: `DELETE /api/v2/mcp/tokens/{id}`.

## Clients

Claude Code:

```bash
claude mcp add --transport http lyra https://api.uselyra.dev/mcp --header "Authorization: Bearer lyra_pat_..."
```

Any client: Streamable HTTP at `https://api.uselyra.dev/mcp` with `Authorization: Bearer <token>`.

## Prompt and resources

| Kind | Name | Returns |
|---|---|---|
| Prompt | `lyra-overview` | The overview page and the page list, in one message |
| Resource | `lyra://docs/index.json` | The manifest: pages, tools, plans, limits, fields |
| Resource | `lyra://docs/<page>.md` | One page as Markdown |

## Tools

| Tool | Scope | Plan |
|---|---|---|
| `data_prediction_markets` | `read` | Free |
| `data_fund_holdings` | `read` | Free |
| `data_congress_trades` | `read` | Free |
| `data_rates` | `read` | Free |
| `data_etf_holdings` | `read` | Free |
| `data_hl_whale_positions` | `read` | Free |
| `data_what_changed` | `read` | Free |
| `test_run_check` | `read` | Free |
| `build_research` | `propose` | Free |
| `build_runs` | `read` | Free |
| `build_run` | `read` | Free |
| `build_pod` | `propose` | Free |
| `pods_templates` | `read` | Free |
| `pods_fund` | `read` | Free |
| `pods_explain` | `read` | Free |
| `pods_propose` | `propose` | Free |
| `pods_propose_edit` | `propose` | Free |
| `alpha_validate` | `read` | Plus and above |
| `alpha_simulate` | `read` | Plus and above |
| `alpha_submit` | `propose` | Plus and above |
| `alpha_list` | `read` | Plus and above |
| `alpha_get` | `read` | Plus and above |
| `alpha_propose_pod` | `propose` | Plus and above |
| `docs_search` | `read` | Free |
| `docs_get` | `read` | Free |
| `data_fields` | `read` | Free |

Full inputs and examples: [MCP tool reference](mcp-tools.md).

## Where proposals land

- In your Lyra web chat, labelled "From <token name>".
- A pod edit is a card you apply with Apply.
- Nothing opens, changes or moves money until you act.
