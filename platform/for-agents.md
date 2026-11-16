---
title: Docs for agents
summary: Every page is Markdown with front matter. Read llms.txt for the map, llms-full.txt for everything, and index.json for structure.
tags:
- llms.txt
- llms-full.txt
- index.json
- manifest
- docs_search
- docs_get
- markdown
- context7
- agents
related:
- mcp
- mcp-tools
- overview
---

# Docs for agents

## For agents

- Lets you: Load Lyra's docs into an agent in the fewest calls.
- Tools: `docs_search`, `docs_get`
- Limit: docs_search returns at most 10 sections, best first.

## Files

| URL | Holds |
|---|---|
| `https://docs.uselyra.dev/llms.txt` | The page map, most useful first |
| `https://docs.uselyra.dev/llms-full.txt` | Every page in one file |
| `https://docs.uselyra.dev/index.json` | Pages, nav, tools, plans, limits, fields as JSON |
| `https://docs.uselyra.dev/<page>.md` | One page as Markdown |
| `https://docs.uselyra.dev/alpha/<page>.md` | One alpha page as Markdown |
| `https://docs.uselyra.dev/<page>` | The same page for people |

## Page shape

- Front matter: `title`, `summary`, `tags`, `related`.
- `# Title`, then `## For agents`: what it lets you do, the tools, the limits.
- Then `##` sections, one fact per line.
- A `figure` block holds the plain-text version of a diagram.

## Docs tools

`docs_search` input and output:

```json
{"query": "how does a check grade"}
```

```json
[{"page": "grading", "url": "https://docs.uselyra.dev/grading", "title": "How a check grades", "heading": "The four grades",
  "line": "| Good Idea | Past cases agree, but not every test above passed |"}]
```

`docs_get` takes a page name: `overview`, `grading`, `alpha/grammar`, and so on.

## In one call

- MCP prompt `lyra-overview`.
- MCP resource `lyra://docs/index.json`.
