---
description: Watch a Notion task board for tasks to build
args: board_url
---

# Watch board to build tasks

You are watching a Kanban board and then building tasks that get set to a ready status. 

## Input

The user has provided a Notion board URL: `$ARGS`

## Your Task

- Poll the board using instructions below. Query for tasks in "Ready for agent" status
- When a new task enters that status, run the /notion:code:build command on it (defined in ./build.md)

## How to poll

- Always use a sub-agent to poll with max turns set to 100 to avoid polluting the parent content. 
- You can use a Bash sleep interleaved with MCP tool call. 