---
name: notion-agent-setup
description: Interactive setup wizard for connecting Notion task boards; use when configuring autonomous task workflows.
metadata:
  short-description: Set up Notion task board connection
---

# Notion Agent Setup

Interactive wizard to connect and configure a Notion task board for autonomous task execution workflows.

## Quick start
1) Guide user through MCP connection if not already set up.
2) Search for task databases with `Notion:notion-search`.
3) Let user select their task board and fetch schema with `Notion:notion-fetch`.
4) Map standard properties (Status, Priority, Assignee, Due Date).
5) Confirm configuration and save for future agent operations.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Welcome and verify connection
- Explain the setup process.
- Test Notion connection with a simple search.
- If connection fails, guide through Step 0.

### 2) Find task databases
- Search for databases with "Task", "Board", "Sprint", "Backlog" keywords.
- Present candidates with names and descriptions.
- Let user select or provide specific database name.

### 3) Analyze database schema
- Fetch selected database with `Notion:notion-fetch`.
- List all properties with types.
- Identify standard task properties automatically.

### 4) Map properties
- Confirm or ask user to map:
  - Status property (and valid status values)
  - Priority property (High/Medium/Low values)
  - Assignee property
  - Due Date property
  - Any project/epic relation properties
- Store mappings for agent use.

### 5) Confirm setup
- Summarize configuration.
- Test by querying a few tasks.
- Explain how to use notion-agent-plan and notion-agent-build skills.
