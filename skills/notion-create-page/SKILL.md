---
name: notion-create-page
description: Create new Notion pages with intelligent defaults and structure based on page type. Supports optional parent specification and prevents accidental overwrites.
---

# Notion Create Page

Create new pages in Notion with sensible default structures based on the page title and type. Handles parent page specification and prevents accidental overwrites.

## Quick Start

When the user wants to create a new Notion page:

1. **Parse input**: Extract page title and optional parent
2. **Resolve parent**: If specified, find the parent page/database
3. **Generate structure**: Create appropriate sections based on title
4. **Create page**: Use `Notion:notion-create-pages` to create
5. **Confirm creation**: Return title, location, and link

## Create Page Workflow

### Step 1: Parse the request

```
Extract from user input:
- Page title (required)
- Parent page or database (optional)
- Any specific content requirements

Examples:
- "Meeting notes for Q1 review" -> Title: "Q1 Review Meeting Notes"
- "New project page under Engineering" -> Title: "New Project", Parent: Engineering
```

### Step 2: Resolve parent location

```
If parent is specified:
- Search for matching page/database
- If ambiguous, ask for clarification
- If not found, offer to create at workspace root

If no parent specified:
- Create at workspace root
- Or ask user for preferred location
```

### Step 3: Check for duplicates

```
Before creating:
- Search for existing pages with same title in same location
- If found, ask user:
  - Reuse existing page?
  - Create new page with different name?
  - Create anyway (will have duplicate title)?
```

### Step 4: Generate page structure

Based on title keywords, create appropriate sections:

**Meeting Notes** (keywords: meeting, notes, standup, review):
```
## Attendees
-

## Agenda
1.

## Discussion Notes


## Action Items
- [ ]

## Next Steps

```

**Project Page** (keywords: project, initiative, program):
```
## Overview


## Goals
-

## Timeline
| Milestone | Date | Status |
|-----------|------|--------|
|           |      |        |

## Tasks


## Risks & Blockers


## Resources

```

**Generic Page**:
```
## Overview


## Details


## Related

```

### Step 5: Create and confirm

```
After creation, return:
- Page title
- Parent location
- Direct link or identifier
- Brief confirmation message
```

## Output Format

```
Created new page:

**Title**: Q1 Planning Meeting Notes
**Location**: Engineering / Meetings
**Link**: [Open in Notion](notion://...)

The page has been set up with sections for:
- Attendees
- Agenda
- Discussion Notes
- Action Items
- Next Steps
```

## Smart Defaults by Page Type

| Page Type | Detected By | Sections Included |
|-----------|-------------|-------------------|
| Meeting Notes | "meeting", "notes", "standup" | Attendees, Agenda, Notes, Actions |
| Project | "project", "initiative" | Overview, Goals, Timeline, Tasks, Risks |
| Spec/RFC | "spec", "rfc", "proposal" | Summary, Background, Proposal, Alternatives |
| How-To | "how to", "guide", "tutorial" | Overview, Prerequisites, Steps, Troubleshooting |
| Generic | Default | Overview, Details, Related |

## Safety Features

- **No overwrites**: Always checks for existing pages first
- **Clarification prompts**: Asks before proceeding with ambiguous input
- **Parent verification**: Confirms parent location exists before creating

## Best Practices

- **Intelligent defaults**: Generate useful structure, not empty pages
- **Respect hierarchy**: Place pages in logical locations
- **Confirm actions**: Always report what was created and where
- **Link related content**: Suggest linking to/from related pages

## MCP Tools Used

- `Notion:notion-search` - For finding parent pages and checking duplicates
- `Notion:notion-create-pages` - For creating the new page
