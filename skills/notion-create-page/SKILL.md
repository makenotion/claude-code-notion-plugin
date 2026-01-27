---
name: notion-create-page
description: Create Notion pages with intelligent defaults and proper structure; use when adding new documentation, notes, or content pages.
metadata:
  short-description: Create pages with smart defaults
---

# Notion Create Page

Create well-structured Notion pages with intelligent defaults for titles, content organization, and placement.

## Quick start
1) Gather page details: title, content, and desired location.
2) Find parent page/database with `Notion:notion-search` if not specified.
3) Structure content with appropriate headings and formatting.
4) Create page with `Notion:notion-create-pages` using proper parent.
5) Confirm creation and provide link to new page.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Gather page requirements
- Get title (generate descriptive one if not provided).
- Collect content to include in the page.
- Ask about location: standalone, under parent, or in database.

### 2) Determine placement
- Search for parent page with `Notion:notion-search` if specified.
- Fetch parent with `Notion:notion-fetch` to confirm structure.
- Default to standalone page if no parent specified.

### 3) Structure content
- Organize with clear headings (##, ###).
- Use bullet points for lists.
- Add code blocks for technical content.
- Include links to related pages where relevant.

### 4) Create the page
- Use `Notion:notion-create-pages` with structured content.
- Set parent using `page_id` or `data_source_id` as appropriate.
- Include any metadata or properties if in a database.

### 5) Confirm and link
- Return the URL to the created page.
- Suggest linking from related pages for discoverability.
- Offer to update parent page with reference to new page.
