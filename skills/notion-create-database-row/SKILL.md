---
name: notion-create-database-row
description: Insert rows into Notion databases with flexible property input; use when adding entries to any structured database.
metadata:
  short-description: Add rows to any Notion database
---

# Notion Create Database Row

Add new entries to any Notion database with automatic property type handling and validation.

## Quick start
1) Identify target database and row data from user request.
2) Find database with `Notion:notion-search` and fetch schema with `Notion:notion-fetch`.
3) Map user data to database properties, handling type conversions.
4) Create row with `Notion:notion-create-pages` using `data_source_id`.
5) Confirm creation with link and property summary.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Parse row data
- Extract database name from user request.
- Identify property values to set.
- Note any content for the page body.

### 2) Find and fetch database
- Search with `Notion:notion-search` for the database.
- Fetch with `Notion:notion-fetch` to get full schema.
- Identify `data_source_id` from `<data-source>` tags.

### 3) Map properties
- Match user data to property names (case-insensitive).
- Handle type conversions:
  - Select: match to valid options
  - Multi-select: parse comma-separated values
  - Date: parse natural language dates
  - Number: convert strings to numbers
  - Relation: search for related page IDs

### 4) Create the row
- Use `Notion:notion-create-pages` with database's `data_source_id`.
- Set all mapped properties.
- Include page content if provided.

### 5) Confirm and validate
- Return link to created row.
- List properties that were set.
- Warn if any properties couldn't be mapped.
