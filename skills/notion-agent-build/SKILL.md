---
name: notion-agent-build
description: Autonomous task implementation from Notion task URLs; use when implementing specific tasks with progress tracking.
metadata:
  short-description: Implement tasks with progress tracking
---

# Notion Agent Build

Autonomously implement a Notion task, updating progress and status throughout the implementation process.

## Quick start
1) Receive Notion task URL from user.
2) Fetch task details with `Notion:notion-fetch` including acceptance criteria.
3) Implement the task, updating Notion with progress via `Notion:notion-update-page`.
4) Mark task complete when acceptance criteria are met.
5) Report completion with summary of changes made.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Fetch task details
- Fetch task page with `Notion:notion-fetch`.
- Extract: title, description, acceptance criteria, dependencies.
- Identify related spec or context pages and fetch if needed.
- Understand what "done" looks like.

### 2) Start implementation
- Update task status to "In Progress" with `Notion:notion-update-page`.
- Add initial progress note with approach.
- Begin implementation work.

### 3) Track progress
- Update task periodically with progress notes:
  - What's completed
  - Current focus
  - Any blockers encountered
- Keep status field current.

### 4) Complete implementation
- Verify all acceptance criteria are met.
- Update task with completion summary:
  - What was implemented
  - Files changed
  - Any follow-up items
- Mark status as "Done" or "Complete".

### 5) Report completion
- Summarize work done.
- Link to any PRs, commits, or artifacts.
- Suggest next tasks if part of a larger plan.
