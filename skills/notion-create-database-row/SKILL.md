---
name: notion-create-database-row
description: Insert rows into any Notion database using natural language property values. Handles property name matching and validation.
---

# Notion Create Database Row

Insert new rows into any Notion database using natural language property values. Intelligently maps user input to database properties with validation.

## Quick Start

When the user wants to add a row to a Notion database:

1. **Identify database**: Find the target database by name or ID
2. **Parse properties**: Extract key=value pairs from input
3. **Map to schema**: Match input keys to actual property names
4. **Validate values**: Check required properties and valid options
5. **Create row**: Insert with mapped values and confirm

## Create Row Workflow

### Step 1: Identify target database

```
Parse database identifier from input:
- Database name: "Bugs database", "Customer List"
- Database ID: Direct Notion ID if provided
- Contextual: "the bugs tracker", "our CRM"

If multiple matches:
- List candidates with brief descriptions
- Ask user to select the correct one
```

### Step 2: Parse property values

```
Extract properties from natural language or key=value format:

Natural language:
- "Add a high severity bug owned by Alice about login"
  -> Severity: High, Owner: Alice, Description: login issue

Key=value format:
- "Severity=High Owner=Alice Status=Open"
  -> Severity: High, Owner: Alice, Status: Open

Mixed:
- "New bug: login fails, Severity=Critical"
  -> Title: login fails, Severity: Critical
```

### Step 3: Map to database schema

```
Match input keys to actual property names:

Input: "owner"
Matches: "Owner", "Assigned To", "Assignee", "Responsible"

Input: "status"
Matches: "Status", "State", "Progress", "Stage"

Handle variations:
- Case insensitive: "STATUS" = "status" = "Status"
- Spacing tolerant: "DueDate" = "Due Date" = "due date"
- Common synonyms: "priority" = "importance" = "urgency"
```

### Step 4: Validate and prompt for missing

```
For each property:
- Required properties: Must have value, prompt if missing
- Select properties: Value must match allowed options
- Date properties: Parse natural language dates
- Person properties: Resolve to Notion users
- Relation properties: Find and link related pages

If validation fails:
- Show allowed values for select properties
- Suggest corrections for typos
- Ask for required missing values
```

### Step 5: Create and confirm

```
Create the row:
- Insert with all validated properties
- Apply defaults for unspecified optional properties

Confirm with:
- Database name
- All property values set
- Any inferred or defaulted values
- Link to the new row
```

## Output Format

```
Created new row in **Bugs Database**:

| Property | Value |
|----------|-------|
| Title | Login authentication fails |
| Severity | High |
| Owner | Alice |
| Status | Open |
| Created | Today |

[Open in Notion](notion://...)

Notes:
- Status defaulted to "Open"
- Created date set automatically
```

## Property Type Handling

| Property Type | Input Format | Example |
|--------------|--------------|---------|
| Text | Plain text | "Login bug description" |
| Number | Numeric | "42", "3.14" |
| Select | Option name | "High", "In Progress" |
| Multi-select | Comma-separated | "bug, urgent, frontend" |
| Date | Natural language | "tomorrow", "next Friday", "2024-03-15" |
| Person | Name or email | "Alice", "alice@company.com" |
| Checkbox | Boolean | "yes", "true", "checked" |
| URL | Valid URL | "https://example.com" |
| Relation | Page name/ID | "Project Alpha" |

## Handling Ambiguity

```
When property mapping is unclear:
- Show the interpreted mapping
- Ask for confirmation before creating
- Offer to adjust mappings

When values don't match options:
- Show available options
- Suggest closest match
- Ask user to choose
```

## Error Handling

```
Database not found:
- Search for similar names
- List available databases
- Ask for clarification

Required property missing:
- List missing required properties
- Ask for values one at a time

Invalid property value:
- Show allowed values
- Explain the constraint
- Ask for valid input
```

## Best Practices

- **Flexible parsing**: Accept both natural language and structured input
- **Forgiving matching**: Handle typos and naming variations
- **Transparent mapping**: Show what was interpreted
- **Validate before create**: Catch errors early, not after creation
- **Explain inferences**: Tell user what was auto-filled

## MCP Tools Used

- `Notion:notion-search` - For finding databases
- `Notion:notion-get-database` - For retrieving schema
- `Notion:notion-create-database-item` - For inserting the row
