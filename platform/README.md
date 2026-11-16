# Lyra Labs docs

Lyra is a personal portfolio manager for retail investors: it turns an idea into a checked pod, runs it on paper, and takes it live only when you press Start.

## Start

- [Lyra Labs overview](overview.md): Lyra is your personal portfolio manager. It turns an idea into a checked pod, runs it on paper, and takes it live only when you press Start.
- [Getting started](getting-started.md): From sign-in to a first pod on paper in about ten minutes.
- [Paper and Live](paper-and-live.md): Every pod runs on paper first. Live trades your own accounts, and only you start it.

## Your PM

- [Chat with Lyra](chat.md): Talk to Lyra in the app or on Telegram. It answers with numbers from code and cards you act on.
- [Research](research.md): Research has two tabs: Public Research, where Lyra posts daily ideas, and Your Research, where your own views become checked pods.
- [Ideas](ideas.md): Lyra posts 3 ideas a day in Research, Public Research. Each comes from a daily scan, tested against past cases and a false-discovery control.
- [Your Research](your-research.md): Your own view, in one sentence, becomes a research run: a claim, a check, a read and a fund card you can start on paper.
- [How a check grades](grading.md): A check counts how often the idea held in the past, keeps the last 365 days sealed, and raises the bar with every version you try.
- [Telegram](telegram.md): Link Telegram to hear from Lyra when you are needed, answer decisions with a tap, and talk to Lyra on the go.

## Pods

- [Pods](pods.md): A pod is one idea with its own Analyst, Trader, book and forecasts. Lyra runs several in one fund.
- [Rule pods](rules.md): A rule pod trades a formula whose check graded Awesome Idea. A daily job sets its targets; the Trader steps in only on exceptions.
- [Loss levels](loss-levels.md): Two levels per pod: at the first, its capital is halved; at the second, it closes. Measured from the pod's peak.
- [The Risk Agent](risk-agent.md): An independent risk manager that sees every trade before it is placed. It can only reduce or block, and it reports to you.
- [Watch and the weekly letter](watch.md): Each pod watches its names, news and drivers, checks its own structure and record, and Lyra sends one letter a week.

## Money

- [The Book and venues](book.md): The Book is every leg your pods hold. Each leg goes to one venue by one routing table.
- [Paper fund](paper-fund.md): Every account starts with a Paper fund: Hyperliquid paper at $10,000 per fund, and the equity of your linked Alpaca paper account, read live.
- [Hyperliquid perps](hyperliquid.md): Live perps trade on your own Hyperliquid account. Lyra places orders with an agent key that cannot withdraw.
- [Connect Alpaca](alpaca.md): Connect your own Alpaca account with OAuth to trade US stocks and ETFs, on paper or live.

## Lyra Data Engine

- [Lyra Data Engine](data-engine.md): Lyra's own engine turns raw news, filings, flows and market data into point-in-time signals that every agent, check and alpha reads.
- [Field catalog](fields.md): Every field and table in the Lyra Data Engine: meaning, unit, update cadence, when it is known, and coverage. Generated from code.
- [Your own Data Engine](custom-data-engine.md): On Ultra, your research agent builds datasets that become fields only your own rules can read, checked like every other rule.

## Quant

- [Alpha Playground](alpha-playground.md): Write alphas in a small expression language, test them on Lyra's servers, and run the ones that pass as pods.
- [Ultra workspace](ultra.md): An invite-only workspace where a research agent gathers data and writes candidate rules, inside a hard budget, with no access to brokers or keys.
- [Connect over MCP](../alpha/connect.md): Tokens, the MCP URL, the tools and the daily checks.
- [Expression language](../alpha/grammar.md): Text and JSON forms of an expression.
- [Operators](../alpha/operators.md): Every function and infix operator.
- [Data sheet](../alpha/data.md): Every field: meaning, unit, when it is known, coverage.
- [Settings](../alpha/settings.md): Delay, decay, neutralization, rebalance, truncation, weights, limits.
- [Output](../alpha/output.md): The standard output of a simulation.
- [Submission checks](../alpha/checks.md): What alpha_submit requires, the quota and repeated variants.
- [Example alphas](../alpha/examples.md): Fourteen complete alphas, one pattern each.

## Agents and API

- [Connect over MCP](mcp.md): Give your own AI agent a token and it can read your fund, run checks, research and propose, through the Lyra MCP.
- [MCP tool reference](mcp-tools.md): Every Lyra MCP tool with its scope, plan, input schema and an example input. Generated from the tool registry.
- [What agents can't do](security.md): No agent, MCP tool, research run or Ultra workspace can place an order, move money or press Start. Tests enforce it.
- [Docs for agents](for-agents.md): Every page is Markdown with front matter. Read llms.txt for the map, llms-full.txt for everything, and index.json for structure.

## Reference

- [Plans and limits](plans.md): What each plan unlocks: pods, funds, live money, credits, checks, research depth, alpha tools and Ultra. Generated from code.
- [FAQ](faq.md): Short answers to the questions people ask first.
- [Glossary](glossary.md): Every Lyra term in one line.
