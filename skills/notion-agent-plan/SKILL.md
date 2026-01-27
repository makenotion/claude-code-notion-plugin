---
name: notion-agent-plan
description: Autonomous task planning from Notion spec URLs; use when breaking down specs into implementation tasks.
metadata:
  short-description: Plan tasks from Notion specs
---

# Notion Agent Plan

Autonomously break down Notion specification pages into concrete, implementable tasks in your task database.

## Quick start
1) Receive Notion spec URL from user.
2) Fetch spec content with `Notion:notion-fetch` and analyze requirements.
3) Break down into sized tasks (1-2 days each) with acceptance criteria.
4) Find task database and create tasks with `Notion:notion-create-pages`.
5) Link tasks back to spec and report created task summary.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Fetch and analyze spec
- Fetch the spec page with `Notion:notion-fetch`.
- Extract requirements, acceptance criteria, and constraints.
- Identify scope, dependencies, and technical approach.
- Note ambiguities to clarify with user.

### 2) Break down into tasks
- Create task breakdown following logical implementation order.
- Size each task to 1-2 days of work.
- Write clear titles starting with action verbs.
- Include acceptance criteria for each task.

### 3) Confirm with user
- Present proposed tasks with estimates.
- Allow user to adjust scope, add/remove tasks.
- Clarify any ambiguities identified in spec.

### 4) Create tasks in Notion
- Find task database with `Notion:notion-search`.
- Fetch schema with `Notion:notion-fetch` for property mapping.
- Create each task with `Notion:notion-create-pages`:
  - Set properties: Status, Priority, relations to spec
  - Include context and acceptance criteria in content

### 5) Report and link
- Summarize created tasks with links.
- Update spec page with "Implementation Tasks" section.
- Suggest starting point for implementation.
