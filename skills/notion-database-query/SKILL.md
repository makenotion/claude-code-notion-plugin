---
name: notion-database-query
description: Query Notion databases with natural language filters and sorting; use when retrieving filtered data from databases.
metadata:
  short-description: Query databases with natural language
---

# Notion Database Query

Query Notion databases using natural language filters and sorting to retrieve structured data.

## Quick start
1) Parse filter conditions and sort preferences from user request.
2) Find target database with `Notion:notion-search`.
3) Execute query with `Notion:notion-query-database` using parsed filters.
4) Format results as readable table with key properties.
5) Offer to fetch full content for specific rows.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Parse query intent
- Extract filter conditions from natural language:
  - "active tasks" → Status = "Active"
  - "due this week" → Due Date in current week
  - "owned by Alice" → Assignee = "Alice"
- Identify sort preferences: "by due date", "newest first".
- Note result limit if specified.

### 2) Find database
- Search with `Notion:notion-search` for the target database.
- Fetch schema with `Notion:notion-fetch` to confirm property names.
- Map natural language filters to actual property names and values.

### 3) Execute query
- Use `Notion:notion-query-database` with filters and sorting.
- Limit results to reasonable count (20-50).
- Handle pagination for large result sets.

### 4) Format results
- Present as readable table with key columns.
- Truncate long text fields.
- Format dates readably.
- Show row count and indicate if more exist.

### 5) Handle edge cases
- No results: explain why and suggest broader filters.
- Too many results: offer to narrow with additional filters.
- Invalid filter: explain what properties are available.
