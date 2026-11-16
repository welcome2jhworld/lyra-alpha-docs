# Connect over MCP

The alpha tools are for Plus and above. A token carries read, or read and propose; alpha_propose_pod needs propose. Create one while signed in:

```bash
curl -X POST https://api.uselyra.dev/api/v2/mcp/tokens -H "Authorization: Bearer <session>" -H "Content-Type: application/json" -d '{"name": "Claude Code", "scopes": ["read", "propose"]}'
```

The response carries the token once. Keep it out of files you commit.

## Claude Code

```bash
claude mcp add --transport http lyra https://api.uselyra.dev/mcp --header "Authorization: Bearer lyra_pat_..."
```

## Other clients

Streamable HTTP at `https://api.uselyra.dev/mcp` with the header `Authorization: Bearer <token>`.

## Tools

| Tool | What it does |
|---|---|
| `alpha_validate` | Parse an alpha and check it is point-in-time: every input known by the time it trades. Returns the canonical expression, its JSON tree, size and look-back, or the error with its column. Free and unlimited. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights. |
| `alpha_simulate` | Backtest an alpha on Lyra's servers and return the standard output: grade, report, submission checks, breadth and, for books of 5 or more names, a curve of at most 250 points starting at 1. Uses one daily check unless the same spec ran today. Every distinct version counts as a trial of its family. Nothing is saved. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights. |
| `alpha_submit` | Run the submission checks on an alpha and save it to the user's library as the next version of its family when every check passes. Returns the output with saved. A spec simulated today costs no extra check. alpha holds family (a lowercase slug), expression (text or JSON tree), universe {name, instruments, groups}, settings {delay, decay, neutralization, rebalance, truncation} and optional weights. |
| `alpha_list` | The user's saved alphas, oldest first: id, family, version, expression, grade, passed, sharpe, turnover. family filters to one family; empty lists all. |
| `alpha_get` | One saved alpha by id: the standard output and the rule as saved. |
| `alpha_propose_pod` | Propose a pod that trades saved alphas. One id proposes that alpha; 2 to 8 ids blend them at equal risk into a new library entry under family, which uses one daily check. The proposal card lands in the user's Lyra chat. It opens nothing; only the user's Start in the app opens the pod. |
| `docs_search` | Search the Lyra Labs docs, platform and alpha pages, with a plain question. Returns up to 10 sections, best first: page, title, heading and a line of context. |
| `docs_get` | One page of the Lyra Labs docs as Markdown with its front matter. Platform pages: overview, getting-started, paper-and-live, chat, research, ideas, your-research, grading, telegram, pods, rules, loss-levels, risk-agent, watch, book, paper-fund, hyperliquid, alpaca, data-engine, fields, custom-data-engine, alpha-playground, ultra, mcp, mcp-tools, security, for-agents, plans, faq, glossary. Alpha pages: alpha/connect, alpha/grammar, alpha/operators, alpha/data, alpha/settings, alpha/output, alpha/checks, alpha/examples. |
| `data_fields` | The field catalog: each field's syntax, meaning, unit, scope, when it is known, its lag, whether delay 0 can use it, its coverage and the first stored date. No values. |

## Checks a day

| Plan | Checks |
|---|---|
| plus | 30 |
| pro | 200 |
| ultra | 200 |

## Docs for agents

`https://docs.uselyra.dev/llms.txt` lists every page. `https://docs.uselyra.dev/llms-full.txt` is all pages in one file. The Claude Code skill is at `https://docs.uselyra.dev/alpha/skill/SKILL.md`.
