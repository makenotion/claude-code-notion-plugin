---
name: notion-find
description: Find Notion pages or databases by title keywords; use for quick lookups when you know approximate page names.
metadata:
  short-description: Find pages/databases by title
---

# Notion Find

Quickly locate Notion pages or databases by title keywords when you know what you're looking for.

## Quick start
1) Extract title keywords from user request.
2) Search with `Notion:notion-search` filtering by title match.
3) Present matching pages/databases with types and locations.
4) Fetch the selected item with `Notion:notion-fetch` if user confirms.
5) Handle ambiguity by showing options for user to choose.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Parse title keywords
- Extract the page/database name from user request.
- Handle partial names and common variations.
- Note if user wants a page vs database specifically.

### 2) Execute title search
- Use `Notion:notion-search` with title-focused query.
- Filter by object type (page/database) if specified.
- Apply teamspace filter if context is known.

### 3) Present matches
- Show matching items with full titles and types.
- Include parent page/location for context.
- Rank by title similarity and recency.

### 4) Confirm and fetch
- If single clear match, offer to fetch content.
- If multiple matches, present options for user selection.
- Use `Notion:notion-fetch` to retrieve selected item.

### 5) Handle no matches
- Suggest spelling variations or related terms.
- Offer broader search across content.
- Ask user for more details about the page.
