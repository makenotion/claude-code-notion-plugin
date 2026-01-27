---
name: notion-agent-build
description: Autonomously build/implement a task from a Notion page URL. Executes the plan, makes code changes, runs tests, and updates Notion with progress. Communicates via Notion comments.
---

# Notion Agent Build

Autonomously build and implement a task that is tracked in Notion. Executes the implementation, makes code changes, runs tests, and reports results. All communication happens through Notion, not the terminal.

## Quick Start

When given a Notion task URL to build:

1. **Fetch task**: Get page content, plan, and requirements
2. **Mark in progress**: Update status and agent status
3. **Implement**: Execute the plan and make changes
4. **Verify**: Run tests and validation
5. **Mark done**: Update status and report results

## Input

The user provides a Notion task URL:
```
$ARGUMENTS = https://notion.so/workspace/Task-Name-abc123
```

## Build Workflow

### Step 1: Fetch task details

```
Using Notion MCP, retrieve:
- Page title and description
- Implementation plan (if created by $notion-agent-plan)
- Acceptance criteria
- Requirements and constraints
- Linked references
```

### Step 2: Mark in progress

```
Update the task in Notion:
- Status: "In Progress"
- Agent status: "🤖 Starting..."
```

### Step 3: Execute implementation

```
Work through the task:

1. Update Agent status: "📂 Searching relevant files..."

2. Explore codebase:
   - Find relevant files
   - Understand existing patterns
   - Identify modification points

3. Update Agent status: "🎨 Implementing changes..."

4. Make changes:
   - Follow the plan (if exists)
   - Write clean, maintainable code
   - Follow project conventions
   - Add tests if appropriate

5. Update Agent status: "🧪 Running tests..."

6. Verify:
   - Run existing tests
   - Run new tests
   - Check for regressions
```

### Step 4: Handle blockers

```
If blocked or need clarification:

1. Add comment to task:
   "**Message from Agent:**
   I've hit a blocker:
   [Description of the issue]

   Options:
   A) [First option]
   B) [Second option]

   Which would you prefer?"

2. Update properties:
   - Agent blocked: ✓ (checked)
   - Agent status: "❓ [Brief description]"

3. Poll for response (see Polling Protocol)

4. Once answered, continue building
```

### Step 5: Generate diff explanation

```
If code changes were made:
1. Run $notion-explain-diff to create documentation
2. This creates a detailed explanation page in Notion
3. Link the explanation from the task
```

### Step 6: Mark done and report

```
Update the task:
- Status: "Done"
- Agent status: "✅ Complete"

Add completion comment:
"**Message from Agent:**
Task complete! Here's a summary:

**Changes made:**
- [List of changes]

**Tests:**
- [Test results]

**Documentation:**
- [Link to diff explanation if applicable]

Ready for review!"
```

## Communication Protocol

All user communication happens through Notion (user isn't watching the terminal):

### Sending messages

1. **Add comment** to the task page
2. **Prefix** with "**Message from Agent:**" on its own line
3. **Update** Agent blocked to ✓ (checked)
4. **Update** Agent status to describe the situation

### Progress updates (no response needed)
```
"**Message from Agent:**
Progress update - 50% complete.
Currently implementing the authentication flow.
No action needed from you."
```

### Questions requiring response
```
"**Message from Agent:**
I need your input:

The existing color scheme uses #3366FF for primary buttons.
Should I:
A) Keep the existing color
B) Update to the new brand color #0055FF

Please reply with A or B."
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
3. Check for new user comment after our message
4. If found, return to main agent with response
5. If not found, repeat
```

## Agent Status Updates

Keep the user informed via Agent status property:

| Phase | Agent Status |
|-------|--------------|
| Starting | 🤖 Starting... |
| Exploring | 📂 Searching relevant files... |
| Implementing | 🎨 Implementing [feature]... |
| Testing | 🧪 Running tests... |
| Documenting | 📝 Generating documentation... |
| Blocked | ❓ [Brief question] |
| Complete | ✅ Complete |
| Error | ⚠️ [Error description] |

## Error Handling

### Invalid URL
```
If URL is invalid or inaccessible:
1. Update Agent status: "⚠️ Cannot access task"
2. Ask user to verify URL and Notion connection
```

### No plan exists
```
If task has no implementation plan:
1. Option A: Create a quick plan inline
2. Option B: Suggest running $notion-agent-plan first
3. Option C: Ask for requirements directly
```

### Tests fail
```
If tests fail:
1. Update Agent status: "🧪 Tests failing..."
2. Attempt to fix
3. If can't fix, report specific failures
4. Ask for guidance if needed
```

### Build/compile errors
```
If code doesn't compile:
1. Update Agent status: "⚠️ Build errors"
2. Attempt to fix
3. Report specific errors if stuck
4. Don't leave broken code
```

## Integration with Other Skills

### $notion-agent-plan
- Build can use plans created by the plan skill
- If no plan exists, suggest planning first for complex tasks

### $notion-explain-diff
- Automatically run after making code changes
- Creates documentation page explaining the changes
- Links documentation from the task

## Output

The skill produces:

1. **Implemented changes** (code, config, etc.)
2. **Test results** confirming the changes work
3. **Status updates** throughout the process
4. **Completion comment** summarizing results
5. **Diff explanation** (via $notion-explain-diff) if code changed
6. **Task status** changed to "Done"

## Best Practices

- **Keep user informed**: Update Agent status at each phase
- **Don't break things**: Run tests, verify changes work
- **Ask don't assume**: When uncertain, ask via Notion
- **Document changes**: Use $notion-explain-diff for code changes
- **Clean up**: Don't leave debug code or broken states

## MCP Tools Used

- `Notion:notion-get-page` - Fetch task details and plan
- `Notion:notion-update-page` - Update status properties
- `Notion:notion-add-comment` - Communicate with user
- `Notion:notion-get-comments` - Check for user responses
