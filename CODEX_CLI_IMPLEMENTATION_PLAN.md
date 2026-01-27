# Notion Plugin for Codex CLI - Implementation Plan

## Executive Summary

This document outlines the research findings and implementation plan for porting the Notion Plugin from Claude Code to OpenAI's Codex CLI.

**Key Finding:** The 4 workflow skills (knowledge-capture, meeting-intelligence, research-documentation, spec-to-implementation) are **already in the OpenAI curated skills catalog** at `https://github.com/openai/skills/tree/main/skills/.curated`. The main work is converting the 10 Claude Code slash commands into standalone Codex skills that can be invoked with `$skill-name`.

---

## Part 1: Research Findings

### 1.1 Current Claude Code Plugin Architecture

The existing Notion plugin for Claude Code consists of:

| Component | Location | Purpose |
|-----------|----------|---------|
| Plugin Config | `.claude-plugin/plugin.json` | Plugin metadata (name, version, author) |
| Marketplace Config | `.claude-plugin/marketplace.json` | Marketplace registration |
| MCP Config | `.mcp.json` | HTTP-based MCP server connection |
| Skills (4) | `skills/notion/*/SKILL.md` | Workflow instructions |
| Commands (10) | `commands/*.md` | Slash command definitions |
| Examples | `skills/*/examples/` | Real-world workflow examples |
| References | `skills/*/reference/` | Templates and patterns |
| Evaluations | `skills/*/evaluations/` | Test scenarios |

**Total: 66 markdown files, 4 JSON config files, ~810 lines of skill documentation**

### 1.2 Codex CLI Skills Architecture

Codex CLI uses a different paradigm:

| Component | Location | Purpose |
|-----------|----------|---------|
| Skills | `~/.codex/skills/<name>/SKILL.md` or `.codex/skills/<name>/SKILL.md` | Workflow instructions |
| MCP Config | `~/.codex/config.toml` | TOML-based MCP configuration |
| AGENTS.md | `~/.codex/AGENTS.md` or repo root | Project-level instructions |
| Scripts | `skills/<name>/scripts/` | Executable automation |
| References | `skills/<name>/references/` | Supporting documentation |

### 1.3 Existing Curated Notion Skills

The following Notion skills **already exist** in the OpenAI skills catalog:

| Skill | Location | Status |
|-------|----------|--------|
| `notion-knowledge-capture` | `.curated/notion-knowledge-capture/` | ✅ Already ported |
| `notion-meeting-intelligence` | `.curated/notion-meeting-intelligence/` | ✅ Already ported |
| `notion-research-documentation` | `.curated/notion-research-documentation/` | ✅ Already ported |
| `notion-spec-to-implementation` | `.curated/notion-spec-to-implementation/` | ✅ Already ported |

These can be installed via: `$skill-installer notion-knowledge-capture`

### 1.4 Key Insight: Commands → Skills

Codex CLI deprecated custom prompts in favor of the Skills system. This means:

1. **Skills ARE the replacement for custom commands** - Users invoke them with `$skill-name`
2. **Each Claude Code command should become a standalone skill** - Not "absorbed" into workflow skills
3. **Explicit invocation works** - `$notion-search` replaces `/Notion:search`
4. **Implicit invocation also works** - Saying "search my Notion workspace" triggers the skill automatically

### 1.5 Migration Mapping

| Claude Code Command | Codex Skill Name | Invocation |
|---------------------|------------------|------------|
| `/Notion:search` | `notion-search` | `$notion-search` |
| `/Notion:find` | `notion-find` | `$notion-find` |
| `/Notion:create-page` | `notion-create-page` | `$notion-create-page` |
| `/Notion:create-task` | `notion-create-task` | `$notion-create-task` |
| `/Notion:create-database-row` | `notion-create-db-row` | `$notion-create-db-row` |
| `/Notion:database-query` | `notion-query-database` | `$notion-query-database` |
| `/Notion:tasks:setup` | `notion-agent-setup` | `$notion-agent-setup` |
| `/Notion:tasks:plan` | `notion-agent-plan` | `$notion-agent-plan` |
| `/Notion:tasks:build` | `notion-agent-build` | `$notion-agent-build` |
| `/Notion:tasks:explain-diff` | `notion-explain-diff` | `$notion-explain-diff` |

---

## Part 2: Implementation Plan

### 2.1 Target Structure

```
codex-notion-skills/
├── README.md                           # Installation & usage guide
├── config.toml.example                 # MCP configuration example
│
├── skills/
│   │
│   │ # ═══════════════════════════════════════════════════════════
│   │ # ACTION SKILLS (converted from Claude Code slash commands)
│   │ # ═══════════════════════════════════════════════════════════
│   │
│   ├── notion-search/
│   │   └── SKILL.md                    # Search workspace
│   │
│   ├── notion-find/
│   │   └── SKILL.md                    # Quick find by title
│   │
│   ├── notion-create-page/
│   │   └── SKILL.md                    # Create new page
│   │
│   ├── notion-create-task/
│   │   └── SKILL.md                    # Create task in database
│   │
│   ├── notion-create-db-row/
│   │   └── SKILL.md                    # Insert database row
│   │
│   ├── notion-query-database/
│   │   └── SKILL.md                    # Query database with filters
│   │
│   │ # ═══════════════════════════════════════════════════════════
│   │ # AGENT SKILLS (for async agent task workflows)
│   │ # ═══════════════════════════════════════════════════════════
│   │
│   ├── notion-agent-setup/
│   │   └── SKILL.md                    # Configure task board for agent
│   │
│   ├── notion-agent-plan/
│   │   └── SKILL.md                    # Plan task from Notion URL
│   │
│   ├── notion-agent-build/
│   │   └── SKILL.md                    # Build/implement task
│   │
│   └── notion-explain-diff/
│       └── SKILL.md                    # Explain code changes
│
└── installer/
    └── install.sh                      # Optional installation script
```

**Note:** The 4 workflow skills (knowledge-capture, meeting-intelligence, research-documentation, spec-to-implementation) are already in the curated catalog and don't need to be recreated.

### 2.2 Command → Skill Conversion Examples

Each Claude Code command becomes a standalone Codex skill with proper YAML frontmatter and trigger description.

#### Example 1: Search Command → Skill

**Claude Code (`commands/search.md`):**
```yaml
---
description: Search the user's Notion workspace using the Notion MCP server
argument-hint: query terms
---
```

**Codex CLI (`skills/notion-search/SKILL.md`):**
```yaml
---
name: notion-search
description: Search Notion workspace for pages, databases, or content. Use when asked to find, search, or look up information in Notion with natural language queries.
metadata:
  short-description: Search Notion workspace
---

Search the user's Notion workspace using the Notion MCP tools.

## Behavior

1. Interpret the query as natural-language search terms (e.g., "Q1 roadmap", "customer feedback")
2. Use the Notion MCP `search` tool for fast, high-signal results
3. If multiple results found, summarize as a scannable list:
   - Page/database title
   - Type (page, database, task list, etc.)
   - One-line description or key fields
4. If no results found, suggest refinements or alternative queries

**Output:** Human-readable summary with links/identifiers. Never dump raw JSON.
```

#### Example 2: Create Page Command → Skill

**Codex CLI (`skills/notion-create-page/SKILL.md`):**
```yaml
---
name: notion-create-page
description: Create a new Notion page with sensible structure. Use when asked to create, make, or add a new page in Notion, optionally under a specific parent.
metadata:
  short-description: Create Notion page
---

Create a new Notion page for the user.

## Workflow

1. Parse the request for:
   - Page title (required)
   - Parent page/database (optional)
2. If parent is ambiguous, ask brief clarification
3. Create page with sensible default structure based on title:
   - "Meeting notes" → Attendees, Agenda, Notes, Action items
   - "Project" pages → Overview, Goals, Timeline, Tasks, Risks
4. Confirm creation with: page title, parent location, link

**Safety:** Don't overwrite existing pages. If same name exists in same parent, confirm with user.
```

#### Example 3: Agent Plan Command → Skill

**Codex CLI (`skills/notion-agent-plan/SKILL.md`):**
```yaml
---
name: notion-agent-plan
description: Plan a task tracked in Notion by fetching details, creating an implementation plan, and updating the task status. Use when given a Notion task URL to plan.
metadata:
  short-description: Plan task from Notion
---

Plan a task that is tracked in Notion. The user monitors progress via Notion, not this session.

## Input

A Notion task URL provided by the user.

## Workflow

1. **Fetch task details** from Notion via MCP
   - Get title, description, properties
   - Look for acceptance criteria, requirements, specs
   - Read linked pages if needed

2. **Mark as planning**
   - Set status to "planning"
   - Update "Agent status" field: 🤖 Starting...

3. **Create plan**
   - Analyze requirements and create implementation plan
   - Update "Agent status" at each step (e.g., "📂 Searching files...", "✍️ Writing plan...")
   - If clarification needed, use Communication Protocol

4. **Complete planning**
   - Write plan into task page under "Plan" section
   - Update status to "Ready"
   - Notify user via Communication Protocol

## Communication Protocol

To communicate with user:
1. Add comment prefixed with "**Message from Claude:**"
2. Set "Agent blocked" to true
3. Set "Agent Status" to short message (e.g., "❓ Choose approach")
4. Poll every 10 seconds for user response (use sub-agent with max 100 turns)
```

### 2.3 Full Command Migration Table

| Command | Skill Name | Trigger Keywords | Complexity |
|---------|------------|------------------|------------|
| `search` | `notion-search` | search, find, look up, query | Simple |
| `find` | `notion-find` | find by title, locate page | Simple |
| `create-page` | `notion-create-page` | create page, new page, make page | Simple |
| `create-task` | `notion-create-task` | create task, add task, new task | Simple |
| `create-database-row` | `notion-create-db-row` | add row, insert row, create entry | Simple |
| `database-query` | `notion-query-database` | query database, filter, sort | Medium |
| `tasks/setup` | `notion-agent-setup` | setup task board, configure agent | Medium |
| `tasks/plan` | `notion-agent-plan` | plan task, create plan from URL | Complex |
| `tasks/build` | `notion-agent-build` | build task, implement task | Complex |
| `tasks/explain-diff` | `notion-explain-diff` | explain changes, document diff | Medium |

### 2.4 MCP Configuration Migration

**Current `.mcp.json` (Claude Code):**
```json
{
  "mcpServers": {
    "notion": {
      "type": "http",
      "url": "https://mcp.notion.com/mcp"
    }
  }
}
```

**Target `config.toml` (Codex CLI):**
```toml
[mcp_servers.notion]
url = "https://mcp.notion.com/mcp"
# Optional: If Notion requires OAuth
# bearer_token_env_var = "NOTION_OAUTH_TOKEN"

# Timeout settings
startup_timeout_sec = 10
tool_timeout_sec = 60
```

**If OAuth is required:**
```bash
codex mcp login notion
```

### 2.5 Distribution Strategy

**Option A: GitHub Repository (Recommended)**
1. Create `makenotion/codex-notion-skills` repository
2. Users install via: `$skill-installer install https://github.com/makenotion/codex-notion-skills`

**Option B: OpenAI Skills Catalog**
1. Submit to `openai/skills` repository
2. Place in `.curated/` folder after review
3. Users install via: `$skill-installer notion-knowledge-capture`

**Option C: Manual Installation**
1. Users clone repo
2. Copy skills to `~/.codex/skills/`
3. Add MCP config to `~/.codex/config.toml`

---

## Part 3: Implementation Tasks

### Phase 1: Action Skills (Priority: High)

Convert basic Claude Code commands to standalone Codex skills:

- [ ] Create `notion-search` skill from `commands/search.md`
- [ ] Create `notion-find` skill from `commands/find.md`
- [ ] Create `notion-create-page` skill from `commands/create-page.md`
- [ ] Create `notion-create-task` skill from `commands/create-task.md`
- [ ] Create `notion-create-db-row` skill from `commands/create-database-row.md`
- [ ] Create `notion-query-database` skill from `commands/database-query.md`

### Phase 2: Agent Skills (Priority: High)

Convert async agent workflow commands to Codex skills:

- [ ] Create `notion-agent-setup` skill from `commands/tasks/setup.md`
- [ ] Create `notion-agent-plan` skill from `commands/tasks/plan.md`
- [ ] Create `notion-agent-build` skill from `commands/tasks/build.md`
- [ ] Create `notion-explain-diff` skill from `commands/tasks/explain-diff.md`

### Phase 3: Configuration & Infrastructure (Priority: Medium)

- [ ] Create `config.toml.example` with MCP configuration
- [ ] Write installation script (`install.sh`)
- [ ] Create directory structure for GitHub repository

### Phase 4: Documentation (Priority: Medium)

- [ ] Write comprehensive README with:
  - Installation instructions (skill-installer, manual)
  - MCP setup guide (`codex mcp add` and `codex mcp login`)
  - Usage examples for each skill
  - Skill quick-reference table
- [ ] Document relationship to existing curated workflow skills
- [ ] Add migration guide for Claude Code users

### Phase 5: Testing & Validation (Priority: High)

- [ ] Test each action skill with Codex CLI
- [ ] Test each agent skill with Codex CLI
- [ ] Verify MCP server connectivity and OAuth flow
- [ ] Validate implicit invocation triggers work correctly
- [ ] Test explicit `$skill-name` invocation
- [ ] Test skill combinations (action + workflow skills together)

### Phase 6: Distribution (Priority: Medium)

- [ ] Create GitHub repository `makenotion/codex-notion-skills`
- [ ] Submit action skills to OpenAI skills catalog (`.curated/` or `.community/`)
- [ ] Create release with installation instructions
- [ ] Update Claude Code plugin README to reference Codex version

---

## Part 4: Technical Considerations

### 4.1 MCP Authentication

Notion's hosted MCP server (`https://mcp.notion.com/mcp`) requires OAuth authentication. Codex CLI supports this via:

```bash
# Add the Notion MCP server
codex mcp add notion --url https://mcp.notion.com/mcp

# Authenticate via OAuth
codex mcp login notion
```

Each skill should include a prerequisite check for MCP connectivity.

### 4.2 Skill Discovery & Triggers

Codex uses "progressive disclosure" - only skill names and descriptions are loaded at startup:

1. **Descriptions are critical** - They determine both manual discovery and automatic activation
2. **Keywords matter** - Include action verbs like "search", "create", "find", "plan"
3. **Be specific** - "Search Notion workspace" is better than "Search"
4. **Explicit always works** - Users can invoke `$notion-search` directly

**Example Trigger Patterns:**
```
User: "Search my Notion for Q1 planning docs"
→ Triggers: notion-search (implicit)

User: "$notion-create-task Fix login bug"
→ Triggers: notion-create-task (explicit)

User: "Help me plan this task" + provides Notion URL
→ Triggers: notion-agent-plan (implicit)
```

### 4.3 Skill Layering with Workflow Skills

The action skills complement the existing curated workflow skills:

```
┌─────────────────────────────────────────────────────────────┐
│                    WORKFLOW SKILLS                          │
│   (Already in curated catalog - complex multi-step flows)   │
│                                                             │
│   • notion-knowledge-capture                                │
│   • notion-meeting-intelligence                             │
│   • notion-research-documentation                           │
│   • notion-spec-to-implementation                           │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ can use
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                     ACTION SKILLS                           │
│      (New skills - single-purpose operations)               │
│                                                             │
│   • notion-search          • notion-query-database          │
│   • notion-find            • notion-agent-setup             │
│   • notion-create-page     • notion-agent-plan              │
│   • notion-create-task     • notion-agent-build             │
│   • notion-create-db-row   • notion-explain-diff            │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ uses
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      NOTION MCP                             │
│           (https://mcp.notion.com/mcp)                      │
│                                                             │
│   Tools: search, read_page, create_page, update_page,       │
│          query_database, create_database_row, etc.          │
└─────────────────────────────────────────────────────────────┘
```

### 4.4 Context Management

Codex skills should be self-contained and concise:

1. **Keep SKILL.md focused** - Core workflow only
2. **Use `references/` sparingly** - Only for complex templates
3. **No need to duplicate** - Workflow skills exist; action skills are simple

### 4.5 Compatibility Notes

- **Model Differences**: Codex uses OpenAI models (GPT-4.1, etc.), not Claude. Prompt patterns may need minor adjustment.
- **MCP Tool Names**: Should match between Claude Code and Codex - both use Notion's official MCP server.
- **Polling for Agent Skills**: Codex supports similar async patterns with sub-agents.

---

## Part 5: Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| MCP tool name differences | Low | Medium | Verify tool names match Notion MCP spec |
| Skill trigger overlap | Medium | Low | Use unique, specific descriptions |
| OAuth flow issues | Low | Medium | Document `codex mcp login` clearly |
| Agent polling differences | Medium | Medium | Test async patterns early |
| User migration confusion | Low | Low | Clear mapping table in docs |

---

## Part 6: Timeline Estimate

| Phase | Estimated Effort |
|-------|------------------|
| Phase 1: Action Skills (6 skills) | 1 day |
| Phase 2: Agent Skills (4 skills) | 1 day |
| Phase 3: Configuration | 0.5 days |
| Phase 4: Documentation | 0.5 days |
| Phase 5: Testing | 1 day |
| Phase 6: Distribution | 0.5 days |
| **Total** | **4-5 days** |

---

## Appendix A: Codex CLI Reference

### Installation
```bash
npm install -g @openai/codex
# or
brew install --cask codex
```

### Skill Installation
```bash
# Install workflow skills from curated catalog
$skill-installer notion-knowledge-capture
$skill-installer notion-meeting-intelligence
$skill-installer notion-research-documentation
$skill-installer notion-spec-to-implementation

# Install action skills from GitHub (once published)
$skill-installer install https://github.com/makenotion/codex-notion-skills
```

### MCP Setup
```bash
# Add Notion MCP server
codex mcp add notion --url https://mcp.notion.com/mcp

# Authenticate via OAuth
codex mcp login notion

# Verify connection
codex mcp list
```

### Skill Invocation Examples
```
# Explicit invocation with $
$notion-search Q1 roadmap
$notion-create-page Meeting Notes for Sprint Planning
$notion-create-task Fix login bug; due Friday; assigned to me
$notion-agent-plan https://notion.so/task/abc123

# Implicit invocation (Codex auto-selects skill)
"Search my Notion workspace for customer feedback"
"Create a new project page called API Redesign"
"Plan the task at this URL: https://notion.so/..."
```

---

## Appendix B: Comparison Table

| Feature | Claude Code Plugin | Codex CLI Skills |
|---------|-------------------|------------------|
| Invoke search | `/Notion:search query` | `$notion-search query` |
| Create page | `/Notion:create-page Title` | `$notion-create-page Title` |
| Create task | `/Notion:create-task Title` | `$notion-create-task Title` |
| Plan task | `/Notion:tasks:plan URL` | `$notion-agent-plan URL` |
| Knowledge capture | Uses skill implicitly | `$notion-knowledge-capture` |
| Meeting prep | Uses skill implicitly | `$notion-meeting-intelligence` |
| MCP config | `.mcp.json` | `~/.codex/config.toml` |
| Installation | `/plugin marketplace add` | `$skill-installer` |

---

## Appendix C: Sources

- [Codex CLI Documentation](https://developers.openai.com/codex/cli/)
- [Codex MCP Documentation](https://developers.openai.com/codex/mcp/)
- [Codex Skills Documentation](https://developers.openai.com/codex/skills/)
- [Create Skills Guide](https://developers.openai.com/codex/skills/create-skill/)
- [OpenAI Skills Catalog](https://github.com/openai/skills)
- [Curated Notion Skills](https://github.com/openai/skills/tree/main/skills/.curated)

---

## Summary

This implementation plan outlines the port of the Notion Plugin from Claude Code to Codex CLI:

1. **Workflow skills already exist** - The 4 main skills are in the OpenAI curated catalog
2. **Commands become skills** - Each of the 10 slash commands becomes a standalone skill invocable with `$skill-name`
3. **MCP configuration** - Convert from `.mcp.json` to `config.toml` format
4. **Distribution via GitHub** - Publish to `makenotion/codex-notion-skills` for `$skill-installer`

**Key insight:** Codex deprecated custom prompts in favor of Skills. This is the right abstraction for porting Claude Code commands - each command maps 1:1 to a skill that users invoke with `$` prefix or through natural language (implicit invocation).
