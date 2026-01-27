---
name: notion-search
description: Search Notion workspace with natural language queries; use when finding pages, databases, or content across the workspace.
metadata:
  short-description: Search Notion with natural language
---

# Notion Search

Search your Notion workspace using natural language queries to find pages, databases, and content.

## Quick start
1) Parse the user's search intent and keywords.
2) Execute search with `Notion:notion-search` using appropriate filters.
3) Present results in a clear, ranked format with titles and snippets.
4) Offer to fetch full content with `Notion:notion-fetch` for relevant results.
5) Refine search if needed based on user feedback.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Parse search intent
- Extract keywords and phrases from user request.
- Identify filters: content type (page/database), teamspace, date range, creator.
- Determine if searching for titles only or full content.

### 2) Execute search
- Use `Notion:notion-search` with parsed query and filters.
- Apply teamspace filter if scope is known.
- Use date filters for recent content searches.

### 3) Present results
- Show top results with title, type, and snippet.
- Include last edited date for context.
- Group by type (pages vs databases) if mixed results.

### 4) Offer next steps
- Suggest fetching full content for promising results.
- Offer to narrow/broaden search if too many/few results.
- Help user navigate to specific sections.

### 5) Handle edge cases
- No results: suggest alternative keywords or broader scope.
- Too many results: offer filters to narrow down.
- Ambiguous query: ask clarifying questions.
