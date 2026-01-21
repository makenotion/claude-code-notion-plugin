---
description: Search the user’s Notion workspace using the Notion MCP server and Notion Workspace Skill.
argument-hint: query terms
---

Use the Notion Workspace Skill together with the `notionApi` MCP server to search the user's Notion workspace
for content related to `$ARGUMENTS`.

Behavior:

- Interpret `$ARGUMENTS` as a natural-language search query (e.g. "Q1 roadmap", "customer feedback", "bugs triage").
- Prefer fast, high-signal tools such as workspace search or database queries.
- If multiple results are found, summarize them as a short, scannable list, including:
  - Page/database title
  - Type (page, database, task list, etc.)
  - A one-line description or key fields
- If no results are found, suggest refinements or alternative queries.

When you answer, **do not** dump raw JSON. Return a human-readable summary with links/identifiers that the user can click in Notion.