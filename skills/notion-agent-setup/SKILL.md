---
name: notion-agent-setup
description: Interactive setup wizard to configure a Notion task board for agent-driven task tracking. Guides users through template setup or existing board configuration.
---

# Notion Agent Setup

Interactive setup wizard that helps configure a Notion workspace for agent-driven task tracking. Supports both starting from a template and adapting existing boards.

## Quick Start

When the user wants to set up Notion for agent task tracking:

1. **Determine path**: Template or existing board
2. **Guide setup**: Walk through configuration steps
3. **Verify access**: Confirm MCP connectivity
4. **Enable features**: Introduce available agent commands

## Setup Paths

### Option 1: Use the Template

For users starting fresh:

1. **Share template link**:
   ```
   Template URL: https://notion.notion.site/code-with-notion-board
   ```

2. **Guide duplication**:
   - Open the link above
   - Click the duplicate button in the top bar (two squares icon)
   - Choose destination workspace

3. **Get board URL**:
   - After duplication, click Share button (top-right)
   - Click "Copy Link"
   - Share the URL with the agent

### Option 2: Use Existing Board

For users with an existing task board:

1. **Request board URL**: Ask user to share their board link

2. **Inspect board structure**: Use Notion MCP to examine properties

3. **Verify or add required properties**:

   | Property | Type | Purpose |
   |----------|------|---------|
   | Status | Select | Track task progress |
   | Agent status | Text | Agent reports current activity |
   | Agent blocked | Checkbox | Signal when user input needed |

4. **Configure Status options**: Ensure these values exist:
   - Planning
   - In Progress
   - Done

5. **Help modify if needed**: Guide user through adding missing properties

## Required Board Structure

For full agent functionality, the board needs:

### Status Property (Select)
```
Options:
- Planning (for tasks being planned)
- In Progress (for active work)
- Done (for completed tasks)
- [Optional] Blocked, Review, etc.
```

### Agent Status Property (Text)
```
Purpose: Real-time agent activity updates
Example values:
- "🤖 Starting..."
- "📂 Searching files..."
- "✍️ Writing code..."
- "🧪 Running tests..."
```

### Agent Blocked Property (Checkbox)
```
Purpose: Signal when agent needs user input
- Checked: Agent is waiting for response
- Unchecked: Agent is working autonomously
```

## Setup Workflow

### Step 1: Choose setup path

```
Ask the user:
"Would you like to:
1. Start with our template (recommended for new users)
2. Configure an existing Notion board"
```

### Step 2: Execute chosen path

**For template:**
- Provide link and duplication instructions
- Wait for user to share their new board URL
- Verify access via MCP

**For existing board:**
- Request board URL
- Inspect current structure
- Identify missing properties
- Guide user through additions

### Step 3: Verify configuration

```
Check via Notion MCP:
1. Can access the board
2. Status property exists with required options
3. Agent status property exists (text type)
4. Agent blocked property exists (checkbox type)
```

### Step 4: Confirm and introduce features

```
Once verified:
1. Confirm successful setup
2. Introduce available commands:
   - $notion-agent-plan - Plan a task from Notion
   - $notion-agent-build - Build/implement a task
```

## Conversation Style

This is an **interactive setup wizard**, not a one-shot command:

- Be conversational and helpful
- Ask one question at a time
- Provide clear instructions for each step
- Confirm completion of each step before moving on
- Offer troubleshooting if something doesn't work

## Troubleshooting

### Can't access board
```
- Verify the URL is correct
- Check that the board is shared appropriately
- Ensure Notion MCP connection is configured
```

### Missing properties
```
- Guide user to add properties manually:
  1. Open the board in Notion
  2. Click "+" to add property
  3. Select appropriate type
  4. Name it exactly as required
```

### Wrong property types
```
- Properties must be correct types:
  - Status: Select (not Text)
  - Agent status: Text (not Select)
  - Agent blocked: Checkbox (not Text)
```

## Post-Setup

After successful setup, the user can:

1. **Create tasks** in their Notion board
2. **Use $notion-agent-plan** to plan tasks from Notion URLs
3. **Use $notion-agent-build** to implement tasks
4. **Monitor progress** via Agent status updates in Notion

## Best Practices

- **Verify before proceeding**: Always confirm each step completed
- **Be patient**: Setup may take several exchanges
- **Offer alternatives**: If one approach fails, suggest another
- **Test the connection**: Don't assume - verify MCP access works

## MCP Tools Used

- `Notion:notion-get-page` - For inspecting board structure
- `Notion:notion-get-database` - For checking properties
- `Notion:notion-update-database` - For adding properties (if supported)
