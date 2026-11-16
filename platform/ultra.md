---
title: Ultra workspace
summary: An invite-only workspace where a research agent gathers data and writes candidate rules, inside a hard budget, with no access to brokers or keys.
tags:
- ultra
- workspace
- engineer
- research agent
- invite
- budget
- runs
- artifacts
- attach
related:
- custom-data-engine
- rules
- plans
- security
---

# Ultra workspace

## For agents

- Lets you: Start a workspace run and attach a checked candidate rule to a pod.
- Tools: none
- Limit: Ultra plan and an invite.
- Limit: One run at a time; each run $5 and 30 minutes at most.
- Limit: Workspace spend cap $150; the workspace lasts 30 days.

## Facts

- Plan: Ultra, by invite.
- One live workspace per user.
- One run at a time.
- Each run: at most $5 and 30 minutes, then it stops.
- Workspace spend cap: $150. Workspace length: 30 days.
- A task is 3 to 4,000 characters.

## The Engineer

- Gathers and cleans data, and writes candidate rules in Lyra's rule language.
- Runs in a sandbox with no MCP, no vaults and no keys.
- Reaches only the hosts Lyra allows for the workspace, never a broker, exchange, billing or sign-in host.
- Hands in work only as files: `dataset-<name>.csv` and `rule-<id>.json`.
- Paused tool calls are denied.

## API

```http
GET  /api/v2/ultra
POST /api/v2/ultra/runs                          {"ask": "Build a weekly sober-curious interest series and a rule on it"}
POST /api/v2/ultra/artifacts/{artifact_id}/attach {"pod_id": "p_19c2"}
```

| Refusal | Means |
|---|---|
| `needs_ultra` | The plan is not Ultra |
| `not_invited` | No workspace invite |
| `expired` | The workspace ended |
| `over_cap` | The spend cap is used up |
| `busy` | A run is already going (HTTP 409) |

## After a run

- Datasets become fields: [Your own Data Engine](custom-data-engine.md).
- Candidate rules are checked like every rule. Attach needs a check graded Awesome Idea.
