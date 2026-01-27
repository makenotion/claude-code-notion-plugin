---
name: notion-create-task
description: Create tasks in Notion task databases with intelligent property mapping. Automatically identifies task databases and sets appropriate defaults.
---

# Notion Create Task

Create new tasks in Notion task databases with sensible defaults. Automatically identifies the appropriate task database and maps properties intelligently.

## Quick Start

When the user wants to create a new task:

1. **Parse task details**: Extract title and optional properties
2. **Find task database**: Identify the appropriate tasks database
3. **Map properties**: Match user input to database properties
4. **Create task**: Insert new row with mapped values
5. **Confirm creation**: Return task details and link

## Create Task Workflow

### Step 1: Parse task input

```
Extract from user input:
- Task title (required)
- Due date (optional): "tomorrow", "next Friday", "2024-03-15"
- Status (optional): "todo", "in progress", "blocked"
- Owner/Assignee (optional): person name or email
- Project (optional): related project or page
- Priority (optional): high, medium, low
- Tags (optional): labels or categories

Examples:
- "Fix login bug by Friday" -> Title: "Fix login bug", Due: Friday
- "Review PR for Alice, high priority" -> Title: "Review PR", Owner: Alice, Priority: High
```

### Step 2: Identify task database

```
Find the appropriate task database:
- Look for databases named "Tasks", "To-Do", "Action Items"
- Check database description for task-related keywords
- Verify database has task-like properties (Status, Due Date)

If multiple candidates:
- Ask user to choose
- Remember selection for future tasks
```

### Step 3: Map properties

```
Map user input to database properties:
- Handle property name variations:
  - "Due" / "Due Date" / "Deadline"
  - "Owner" / "Assignee" / "Assigned To"
  - "Status" / "State" / "Progress"
- Apply defaults for unspecified properties:
  - Status: "To Do" or first status option
  - Priority: "Medium" if property exists
```

### Step 4: Validate and create

```
Before creating:
- Check required properties are set
- Validate property values against allowed options
- Ask for missing required values

Create the task:
- Insert new row in database
- Set all mapped properties
```

### Step 5: Confirm creation

```
Return to user:
- Task title
- Key properties set (due date, owner, etc.)
- Link to the task
- Any properties that were defaulted
```

## Output Format

```
Created new task:

**Title**: Fix login bug
**Due Date**: Friday, March 15
**Status**: To Do
**Owner**: Alice
**Priority**: High

[Open in Notion](notion://...)

Note: Priority was set to "High" as requested. Project was not specified.
```

## Property Mapping

| User Input | Common Property Names |
|------------|----------------------|
| due, deadline | Due Date, Due, Deadline |
| owner, assignee | Owner, Assignee, Assigned To |
| status | Status, State, Progress |
| priority | Priority, Importance, Urgency |
| project | Project, Related Project, Parent |
| tags, labels | Tags, Labels, Categories |

## Smart Defaults

When properties aren't specified:

- **Status**: First option in status property (usually "To Do")
- **Due Date**: Not set (tasks can be undated)
- **Priority**: "Medium" if priority property exists
- **Owner**: Not set unless user is identifiable

## Error Handling

```
If task database not found:
- Ask user to specify which database to use
- Offer to search for databases with specific names

If required property missing:
- Ask for the specific value
- Explain which properties are required

If property value invalid:
- Show allowed values
- Ask user to choose from options
```

## Best Practices

- **Minimize friction**: Create tasks with minimal required input
- **Smart inference**: Parse natural language dates and priorities
- **Property flexibility**: Handle various property naming conventions
- **Confirm silently mapped values**: Show what was set automatically

## MCP Tools Used

- `Notion:notion-search` - For finding task databases
- `Notion:notion-query-database` - For understanding database schema
- `Notion:notion-create-database-item` - For creating the task
