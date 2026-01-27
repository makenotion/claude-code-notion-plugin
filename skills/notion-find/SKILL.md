---
name: notion-find
description: Quickly locate Notion pages or databases by title keywords. Optimized for precision with fuzzy matching on titles.
---

# Notion Find

Quickly locate pages or databases in Notion by matching title keywords. Optimized for finding specific items when you know part of the name.

## Quick Start

When the user wants to find a specific page or database:

1. **Parse keywords**: Extract title search terms from user input
2. **Search titles**: Use `Notion:notion-search` focused on title matching
3. **Return matches**: Present best matches with type and location
4. **Prioritize precision**: Show 5-10 highly relevant results

## Find Workflow

### Step 1: Parse title keywords

```
Treat input as fuzzy search terms for titles:
- Partial matches: "Q1 plan" matches "Q1 Planning Document"
- Case insensitive: "claude" matches "Claude Marketplace Spec"
- Word order flexible: "spec marketplace" matches "Marketplace Spec"
```

### Step 2: Search both content types

```
Search for:
- Individual pages
- Databases
- Wiki pages
- Project pages
```

### Step 3: Present results

```
For each match, show:
- Title (exact)
- Type (page or database)
- Location/parent (if available)
- Quick identifier or link
```

### Step 4: Handle no matches

```
If nothing found:
- State clearly: "No pages or databases found matching 'X'"
- Suggest alternate search terms
- Offer to try broader search
```

## Output Format

```
Found 3 matches for "Q1 plan":

1. **Q1 Planning Document** (page)
   Located in: Engineering / Roadmaps

2. **Q1 Plans Database** (database)
   Located in: Company Wiki

3. **Q1 Planning Meeting Notes** (page)
   Located in: Meetings / January
```

## Precision vs Recall

This skill prioritizes **precision over recall**:

- Better to show 5-10 very relevant results than 50 noisy ones
- Title matches rank higher than content matches
- Exact matches appear before partial matches

## Differences from Search

| Feature | Find | Search |
|---------|------|--------|
| Focus | Title matching | Full content |
| Results | 5-10 precise | More comprehensive |
| Use case | Know the name | Exploring topics |
| Speed | Faster | More thorough |

## Best Practices

- **Be specific**: Help users narrow down when multiple matches exist
- **Show hierarchy**: Include parent pages/locations when available
- **Quick access**: Provide links or IDs for immediate navigation
- **Suggest alternatives**: If no exact match, offer similar titles

## MCP Tools Used

- `Notion:notion-search` - With title-focused parameters
