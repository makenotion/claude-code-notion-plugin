---
name: notion-search
description: Search a Notion workspace for pages, databases, and content using natural language queries. Returns human-readable summaries with links.
---

# Notion Search

Search your Notion workspace for content using natural language queries. Returns organized, scannable results with direct links to pages and databases.

## Quick Start

When the user asks to search their Notion workspace:

1. **Interpret query**: Parse the search terms from user input
2. **Execute search**: Use `Notion:notion-search` to find matching content
3. **Summarize results**: Present findings as a scannable list
4. **Suggest refinements**: If no results, offer alternative queries

## Search Workflow

### Step 1: Parse the search query

```
Interpret user input as natural-language search terms:
- Topic searches: "Q1 roadmap", "customer feedback"
- Entity searches: "bugs triage", "project alpha"
- Content searches: "deployment instructions", "API documentation"
```

### Step 2: Execute the search

```
Use Notion MCP tools to search:
- Prefer fast, high-signal tools like workspace search
- Use database queries for structured data
- Search across both pages and databases
```

### Step 3: Present results

```
For each result, include:
- Page/database title
- Type (page, database, task list, etc.)
- One-line description or key fields
- Link or identifier for direct access
```

### Step 4: Handle edge cases

```
If no results found:
- Suggest spelling variations
- Offer broader search terms
- Recommend alternative queries

If too many results:
- Ask for filters or narrower scope
- Show most relevant matches first
```

## Output Format

Present results as a human-readable summary:

```
Found 5 results for "customer feedback":

1. **Customer Feedback Database** (database)
   Collection of user feedback entries - 234 items

2. **Q4 Customer Feedback Summary** (page)
   Executive summary of customer sentiment analysis

3. **Feedback Triage Process** (page)
   How-to guide for processing incoming feedback
```

## Best Practices

- **Never dump raw JSON** - Always format for human readability
- **Include clickable links** - Users should be able to navigate directly
- **Prioritize relevance** - Show 5-10 most relevant results, not everything
- **Explain empty results** - Help users refine their search

## Common Queries

| Query Type | Example | Notes |
|------------|---------|-------|
| Topic | "roadmap" | Finds planning documents |
| Project | "Project Alpha" | Finds project-related pages |
| Content type | "meeting notes" | Finds specific document types |
| Person | "Alice's tasks" | Finds user-related content |
| Date-based | "last week standup" | May need database filtering |

## MCP Tools Used

- `Notion:notion-search` - Primary workspace search
- `Notion:notion-query-database` - For filtered database searches
