---
title: Your own Data Engine
summary: On Ultra, your research agent builds datasets that become fields only your own rules can read, checked like every other rule.
tags:
- custom data engine
- ultra
- datasets
- private fields
- ultra fields
- namespace
- research agent
- engineer
related:
- ultra
- data-engine
- rules
- grading
---

# Your own Data Engine

## For agents

- Lets you: Know how an Ultra dataset becomes a private field and a checked rule.
- Tools: none
- Limit: Ultra only, by invite.
- Limit: A dataset has 1 to 50,000 rows and one unit.

## How it works

```figure custom
Your ask: weekly sober-curious search interest → Engineer: dataset-sober_search.csv → Lyra checks it: point in time, one unit → Field: ultra.<ns>.sober_search → Your rule reads it → Check → Awesome Idea attaches to your pod
```

1. You give the Engineer (your workspace's research agent) a task.
2. It writes `dataset-<name>.csv` and `rule-<id>.json` files.
3. Lyra validates each dataset and stores it as point-in-time values.
4. The field is `ultra.<ns>.<name>`, where `<ns>` is your workspace.
5. Lyra parses each rule, binds it to your workspace and checks it with the same engine as every rule.
6. A rule graded Awesome Idea can attach to your pod.

## Dataset format

| Column | Required | Meaning |
|---|---|---|
| `entity` | yes | `_` for one series, or `HL:<COIN>` per instrument |
| `as_of` | yes | the date the value describes |
| `known_at` | yes | the UTC time it was first public, never before `as_of` |
| `value` | yes | a finite number |
| `unit` | no | `usd`, `pct`, `bps`, `ratio`, `score` (default) or `count` |

```csv
entity,as_of,known_at,value,unit
_,2026-10-05,2026-10-06T14:00:00Z,0.62,ratio
_,2026-10-12,2026-10-13T14:00:00Z,0.66,ratio
```

## Checks on every dataset

- 1 to 50,000 rows.
- One unit per dataset.
- One row per entity and `as_of`.
- `known_at` not before `as_of`, and not in the future.

## Who can read it

- Only rules whose id names your workspace.
- A rule from anyone else that names `ultra.<ns>.*` is refused at load.
- Read it in a rule as `obs("ultra.<ns>.<name>")`; it is delay 1.

## Limits

- A dataset is what one run wrote. A new run writes a new version.
- Rules from the workspace are checked in the family `ultra-<ns>`, so every try counts.
