---
name: notion-database-query
description: Query Notion databases with natural language filters and sorting. Returns structured, readable results in table format.
---

# Notion Database Query

Query Notion databases using natural language filters and sorting. Returns results in a clean, readable table format optimized for decision-making.

## Quick Start

When the user wants to query a Notion database:

1. **Identify database**: Find the target database by name or ID
2. **Parse filters**: Extract filter conditions from natural language
3. **Execute query**: Run query with filters and sorting
4. **Format results**: Present as readable table with key properties
5. **Handle empty**: Suggest alternatives if no results

## Query Workflow

### Step 1: Identify target database

```
Parse database identifier:
- By name: "Tasks database", "Bug tracker"
- By context: "my tasks", "the project board"
- By ID: Direct Notion database ID

If multiple matches:
- Show candidates with descriptions
- Ask user to select
```

### Step 2: Parse filter conditions

```
Extract filters from natural language:

"Show me active bugs owned by Alice"
-> Filter: Status = "Active" AND Owner = "Alice"

"Tasks due this week"
-> Filter: Due Date >= Monday AND Due Date <= Friday

"High priority items not completed"
-> Filter: Priority = "High" AND Status != "Completed"

Supported operators:
- Equals: "is", "=", "equals"
- Not equals: "not", "!=", "isn't"
- Contains: "contains", "includes", "has"
- Greater/Less: "after", "before", ">", "<"
- Date ranges: "this week", "last month", "today"
```

### Step 3: Parse sort preferences

```
Extract sorting from input:

"sorted by due date"
-> Sort: Due Date ascending

"newest first"
-> Sort: Created descending

"by priority then due date"
-> Sort: Priority descending, Due Date ascending

Default: Most recently edited first
```

### Step 4: Execute and limit results

```
Query parameters:
- Apply parsed filters
- Apply sorting
- Limit to reasonable count (20-50 rows)
- Request more only if user asks

Handle pagination:
- Show first batch
- Offer to load more
- Indicate total count if available
```

### Step 5: Format results

```
Present as readable table:
- Show key properties (Name, Status, Owner, Due)
- Truncate long text fields
- Format dates readably
- Include row count

Add summary if helpful:
- "Showing 15 of 45 matching items"
- "All items are due this week"
```

## Output Format

```
Found 15 tasks matching "active, owned by Alice":

| Task | Status | Due | Priority |
|------|--------|-----|----------|
| Fix login bug | In Progress | Mar 15 | High |
| Review PR #123 | To Do | Mar 14 | Medium |
| Update docs | In Progress | Mar 18 | Low |
... (12 more)

Showing 15 of 15 total results.
```

## Filter Examples

| Natural Language | Filter Applied |
|-----------------|----------------|
| "active tasks" | Status = "Active" |
| "owned by Alice" | Owner = "Alice" |
| "due this week" | Due Date in current week |
| "high priority" | Priority = "High" |
| "not completed" | Status != "Completed" |
| "created today" | Created = today |
| "bugs with no owner" | Type = "Bug" AND Owner is empty |
| "overdue items" | Due Date < today AND Status != "Done" |

## Sort Examples

| Natural Language | Sort Applied |
|-----------------|--------------|
| "by due date" | Due Date ascending |
| "newest first" | Created descending |
| "alphabetically" | Name ascending |
| "by priority" | Priority descending |
| "recently updated" | Last Edited descending |

## Handling No Results

```
When query returns no matches:

1. State clearly: "No tasks found matching your filters"

2. Analyze why:
   - "No items have Status = 'Active'"
   - "Alice has no assigned tasks"

3. Suggest alternatives:
   - "Try 'In Progress' instead of 'Active'?"
   - "Show all tasks regardless of owner?"

4. Offer to broaden search:
   - Remove most restrictive filter
   - Show all items in database
```

## Handling Large Results

```
When many results:

1. Show summary first:
   "Found 234 matching items"

2. Offer to filter more:
   "Want to narrow by date or owner?"

3. Show reasonable subset:
   "Showing first 25 sorted by due date"

4. Offer pagination:
   "Show next 25 results?"
```

## Best Practices

- **Avoid raw JSON**: Always format for readability
- **Show key properties**: Focus on decision-relevant columns
- **Indicate totals**: Let users know if there's more
- **Suggest refinements**: Help narrow down large result sets
- **Explain empty results**: Don't just say "no results"

## MCP Tools Used

- `Notion:notion-search` - For finding databases
- `Notion:notion-query-database` - For executing queries with filters
