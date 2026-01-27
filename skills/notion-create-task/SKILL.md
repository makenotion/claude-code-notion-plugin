---
name: notion-create-task
description: Create tasks in Notion databases with proper property mapping; use when adding action items, todos, or tracked work items.
metadata:
  short-description: Create tasks with property mapping
---

# Notion Create Task

Create tasks in Notion task databases with automatic property mapping for status, priority, assignee, and due dates.

## Quick start
1) Parse task details: title, description, priority, due date, assignee.
2) Find target task database with `Notion:notion-search`.
3) Fetch database schema with `Notion:notion-fetch` to get properties.
4) Map task details to database properties and create with `Notion:notion-create-pages`.
5) Confirm task creation with link and property summary.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Parse task details
- Extract task title (action-oriented, starts with verb).
- Identify priority (high/medium/low) from context.
- Parse due date if mentioned (today, tomorrow, next week, specific date).
- Note assignee if specified.

### 2) Find task database
- Search with `Notion:notion-search` for "Tasks", "Task Board", or similar.
- If multiple databases, ask user which to use.
- If user specifies database name, search for that specifically.

### 3) Get database schema
- Fetch database with `Notion:notion-fetch` to see properties.
- Identify property names for: Status, Priority, Due Date, Assignee.
- Note required properties and valid options (e.g., status values).

### 4) Create the task
- Map parsed details to database property names.
- Use `Notion:notion-create-pages` with `data_source_id` from database.
- Set Status to initial value (e.g., "To Do", "Not Started").
- Include task description in page content.

### 5) Confirm creation
- Return link to created task.
- Summarize properties set (status, priority, due date).
- Offer to create related tasks if user has more.
