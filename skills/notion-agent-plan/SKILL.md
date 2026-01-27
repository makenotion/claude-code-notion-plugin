---
name: notion-agent-plan
description: Autonomously plan a task from a Notion page URL. Analyzes requirements, creates implementation plan, and updates Notion with progress. Communicates via Notion comments.
---

# Notion Agent Plan

Autonomously plan a task that is tracked in Notion. Reads task details, creates an implementation plan, and writes the plan back to the Notion page. All communication happens through Notion, not the terminal.

## Quick Start

When given a Notion task URL to plan:

1. **Fetch task**: Get page content and requirements
2. **Mark planning**: Update status and agent status
3. **Analyze & plan**: Create implementation plan
4. **Write plan**: Add plan to Notion page
5. **Mark ready**: Update status to "Ready"

## Input

The user provides a Notion task URL:
```
$ARGUMENTS = https://notion.so/workspace/Task-Name-abc123
```

## Planning Workflow

### Step 1: Fetch task details

```
Using Notion MCP, retrieve:
- Page title
- Page content and description
- Properties (status, priority, etc.)
- Acceptance criteria or requirements
- Linked pages or references
```

### Step 2: Mark planning status

```
Update the task in Notion:
- Status: "Planning"
- Agent status: "🤖 Starting..."
```

### Step 3: Build the plan

```
Analyze the task and create a plan:

1. Update Agent status: "📂 Analyzing requirements..."

2. Read and understand:
   - What needs to be done
   - Success criteria
   - Constraints or requirements
   - Related context

3. Update Agent status: "✍️ Writing the plan..."

4. Create implementation plan:
   - Break down into steps
   - Identify dependencies
   - Note potential challenges
   - Estimate complexity
```

### Step 4: Handle clarifications needed

```
If requirements are unclear:

1. Add comment to task:
   "**Message from Agent:**
   I have a few questions about the requirements:
   - Question 1?
   - Question 2?"

2. Update properties:
   - Agent blocked: ✓ (checked)
   - Agent status: "❓ Awaiting clarification"

3. Poll for response (see Polling Protocol)

4. Once answered, continue planning
```

### Step 5: Write plan to Notion

```
Add a "Plan" section to the task page:

## Plan

### Overview
[Brief summary of the approach]

### Steps
1. [First step]
2. [Second step]
3. [Third step]
...

### Dependencies
- [Any prerequisites]

### Considerations
- [Potential challenges]
- [Alternative approaches]

### Estimated Complexity
[Low/Medium/High with brief explanation]
```

### Step 6: Mark ready

```
Update the task:
- Status: "Ready"
- Agent status: "✅ Plan complete"

Add completion comment:
"**Message from Agent:**
Planning complete! The implementation plan has been added to this page.
Ready for $notion-agent-build when you want to proceed."
```

## Communication Protocol

All user communication happens through Notion (user isn't watching the terminal):

### Sending messages

1. **Add comment** to the task page
2. **Prefix** with "**Message from Agent:**" on its own line
3. **Update** Agent blocked to ✓ (checked)
4. **Update** Agent status to describe the request

### Example message
```
**Message from Agent:**

I need some clarification before I can complete the plan:

1. Should this support both iOS and Android, or just iOS?
2. What's the target completion date?

Please reply to this comment with your answers.
```

## Polling Protocol

When waiting for user response:

1. **Use a sub-agent** to poll (avoid context pollution)
2. **Set max turns** to 100 for the polling agent
3. **Poll interval**: Every 10 seconds
4. **Check for**: New comments on the task page

```
Polling loop:
1. Sleep 10 seconds (Bash)
2. Fetch task comments (Notion MCP)
3. Check for new user comment
4. If found, return to main agent
5. If not found, repeat
```

## Agent Status Updates

Keep the user informed via Agent status property:

| Phase | Agent Status |
|-------|--------------|
| Starting | 🤖 Starting... |
| Reading task | 📖 Reading requirements... |
| Analyzing | 🔍 Analyzing task... |
| Planning | ✍️ Writing the plan... |
| Waiting | ❓ Awaiting clarification |
| Complete | ✅ Plan complete |
| Error | ⚠️ [Error description] |

## Error Handling

### Invalid URL
```
If URL is invalid or inaccessible:
1. Comment on task (if possible) explaining the issue
2. Update Agent status: "⚠️ Cannot access task"
3. Ask user to verify URL and Notion connection
```

### Unclear requirements
```
If requirements are too vague to plan:
1. Ask specific clarifying questions (max 3-5 at a time)
2. Don't overwhelm with too many questions
3. Proceed with assumptions if reasonable, noting them
```

### MCP connection issues
```
If Notion MCP is not responding:
1. Report the error
2. Suggest checking MCP configuration
3. Provide setup instructions if needed
```

## Output

The skill produces:

1. **Plan section** added to the Notion task page
2. **Status updates** throughout the process
3. **Completion comment** when done
4. **Task status** changed to "Ready"

## Best Practices

- **Keep user informed**: Update Agent status at each phase
- **Ask focused questions**: Don't overwhelm with too many at once
- **Note assumptions**: If making assumptions, document them
- **Be thorough**: Plans should be actionable by $notion-agent-build

## MCP Tools Used

- `Notion:notion-get-page` - Fetch task details
- `Notion:notion-update-page` - Update status and add plan
- `Notion:notion-add-comment` - Communicate with user
- `Notion:notion-get-comments` - Check for user responses
