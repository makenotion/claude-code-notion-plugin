---
description: Set up a Notion task board for tracking tasks
---

# Notion Workspace Setup

You are helping the user set up their Notion workspace to work with the task commands in this plugin.

## Your Task

Guide the user through one of two setup paths:

### Option 1: Use a Template

If the user wants to start fresh, point them to duplicate this template:

- Template URL: https://notion.notion.site/code-with-notion-board
- Instruct them to duplicate the template to their workspace, by opening the link and clicking the duplicate button in the top bar (icon is two squares).
- Once duplicated, have them share the URL of their new board -- tell them to click the share button in the top-right and then Copy Link.

### Option 2: Use an Existing Board

If the user already has a Notion board they want to use:

- Ask them to provide the URL to their existing board
- Use the Notion MCP tools to inspect the board structure and then help them modify the board to make it ready for the tasks commands. The board needs to have:
    - A status property with Planning, In Progress and Done
    - An "Agent status" text property for the agent to report its current activities
    - An "Agent blocked" checkbox property for the agent to notify the user when it's blocked on user input

## After Setup

Once the user has a board configured:

1. Confirm you can access it via the Notion MCP
2. Let them know they can now use `/notion:tasks:plan` and `/notion:tasks:build` to build a specific task

Remember: Be conversational and helpful. This is a setup wizard, not a one-shot command.
