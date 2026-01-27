---
name: notion-knowledge-capture
description: Capture conversations and insights into structured Notion pages; use when saving discussion outcomes, decisions, or knowledge to wikis/databases.
metadata:
  short-description: Save conversations and insights to Notion
---

# Knowledge Capture

Turn conversations, decisions, and insights into structured Notion documentation with proper linking and discoverability.

## Quick start
1) Define the capture goal: what knowledge needs to be saved and who will use it.
2) Locate the right database with `Notion:notion-search` (wiki, how-to, FAQ, decision log, learning, documentation).
3) Extract and structure the content from conversation context using the matching template.
4) Create or update the page with `Notion:notion-create-pages` or `Notion:notion-update-page`.
5) Link/surface the new page so others can find it (add to index, set tags, link from hub pages).

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Define what to capture
- Ask for the knowledge type: concept, how-to, decision, FAQ, learning, or general documentation.
- Confirm audience (team, org, public) and purpose (reference, onboarding, decision record).
- Identify key details: title, summary, related pages/projects.

### 2) Locate the destination
- Search with `Notion:notion-search` for the target wiki, database, or hub page.
- If multiple candidates, ask the user to pick.
- Fetch the destination with `Notion:notion-fetch` to confirm schema/structure.

### 3) Extract and structure content
- Pull key points from the conversation: decisions, rationale, steps, Q&A, examples.
- Match to a template (concept, how-to, decision record, FAQ, learning).
- Add metadata: date, author, tags, status.

### 4) Create or update the page
- New page: use `Notion:notion-create-pages` with structured content and properties.
- Update existing: use `Notion:notion-update-page` to append or revise sections.
- Link back to source conversation or related pages.

### 5) Make it discoverable
- Add to wiki index or hub page.
- Set tags/categories in database properties.
- Link from related project or team pages.
- Optionally notify stakeholders via comments.

## References and examples
- `reference/` — database schemas and best practices (e.g., `database-best-practices.md`, `decision-log-database.md`, `faq-database.md`, `how-to-guide-database.md`, `learning-database.md`, `documentation-database.md`, `team-wiki-database.md`).
- `examples/` — end-to-end capture patterns (e.g., `conversation-to-faq.md`, `decision-capture.md`, `how-to-guide.md`).
