# Notion Plugin for Codex CLI - Implementation Plan

## Executive Summary

This document outlines the research findings and implementation plan for porting the Notion Plugin from Claude Code to OpenAI's Codex CLI. The port requires adapting the plugin architecture from Claude Code's plugin system to Codex CLI's skills system, with significant structural changes but largely preservable content.

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

### 1.3 Key Differences

| Feature | Claude Code | Codex CLI | Migration Impact |
|---------|-------------|-----------|------------------|
| **Plugin System** | `.claude-plugin/` JSON configs | Skills directory with SKILL.md | **Major restructure** |
| **MCP Config** | `.mcp.json` (JSON, HTTP type) | `config.toml` (TOML format) | **Format conversion** |
| **Custom Commands** | `commands/*.md` with YAML frontmatter | Not supported | **Must absorb into skills** |
| **Skill Format** | `name:` and `description:` frontmatter | Same, but stricter limits (100/500 chars) | Minor adaptation |
| **Marketplace** | `marketplace.json` registration | `$skill-installer` from GitHub | Different distribution |
| **Invocation** | `/Plugin:command` slash commands | `$skill-name` or implicit | **Different UX** |

### 1.4 Critical Gaps

1. **No Custom Slash Commands**: Codex CLI has 16 built-in slash commands but doesn't support custom command definitions. The 10 Claude Code commands must be:
   - Absorbed into skill instructions
   - Documented as usage patterns for users to invoke manually

2. **Character Limits**: Codex skills have strict limits:
   - `name`: max 100 characters
   - `description`: max 500 characters
   - This requires condensing the current descriptions

3. **Distribution Model**: No marketplace equivalent; must use GitHub-based skill installer or direct installation.

---

## Part 2: Implementation Plan

### 2.1 Target Structure

```
codex-notion-skills/
├── README.md                           # Installation & usage guide
├── AGENTS.md                           # Optional project-level config example
├── config.toml.example                 # MCP configuration example
│
├── skills/
│   ├── notion-knowledge-capture/
│   │   ├── SKILL.md                    # Main skill file
│   │   ├── references/
│   │   │   ├── content-types.md
│   │   │   ├── database-types.md
│   │   │   └── templates.md
│   │   └── examples/
│   │       └── save-deployment-guide.md
│   │
│   ├── notion-meeting-intelligence/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   │   ├── meeting-types.md
│   │   │   ├── pre-read-template.md
│   │   │   └── agenda-template.md
│   │   └── examples/
│   │       └── customer-meeting-prep.md
│   │
│   ├── notion-research-documentation/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   │   ├── output-formats.md
│   │   │   └── citation-guide.md
│   │   └── examples/
│   │       └── product-research.md
│   │
│   └── notion-spec-to-implementation/
│       ├── SKILL.md
│       ├── references/
│       │   ├── spec-parsing.md
│       │   ├── task-creation.md
│       │   └── implementation-plan-template.md
│       └── examples/
│           └── feature-breakdown.md
│
└── installer/
    └── install.sh                      # Optional installation script
```

### 2.2 Skill Conversion Plan

#### Skill 1: Knowledge Capture

**Current (Claude Code):**
```yaml
---
name: Notion Knowledge Capture
description: Transform conversations and discussions into structured documentation in Notion
---
```

**Target (Codex CLI):**
```yaml
---
name: notion-knowledge-capture
description: Transform conversations into structured Notion documentation. Use when asked to save, document, or capture knowledge like how-to guides, FAQs, decision records, or learnings.
metadata:
  short-description: Capture knowledge to Notion
---
```

**Body Content:**
- Preserve the workflow steps
- Include command equivalents as instructions (e.g., "To search for a location, use Notion MCP search tool")
- Reference supporting files in `references/` directory

#### Skill 2: Meeting Intelligence

**Target (Codex CLI):**
```yaml
---
name: notion-meeting-intelligence
description: Prepare for meetings by gathering Notion context, enriching with research, and creating pre-read documents and agendas. Use before important meetings.
metadata:
  short-description: Meeting prep with Notion
---
```

#### Skill 3: Research & Documentation

**Target (Codex CLI):**
```yaml
---
name: notion-research-documentation
description: Search your Notion workspace, synthesize findings, and create comprehensive research documentation with citations. Use for research tasks.
metadata:
  short-description: Research across Notion
---
```

#### Skill 4: Spec to Implementation

**Target (Codex CLI):**
```yaml
---
name: notion-spec-to-implementation
description: Turn product or technical specifications into concrete Notion tasks with implementation plans and progress tracking. Use when breaking down specs.
metadata:
  short-description: Specs to Notion tasks
---
```

### 2.3 Command Migration Strategy

The 10 slash commands must be absorbed into skill documentation:

| Claude Code Command | Codex CLI Equivalent |
|---------------------|----------------------|
| `/Notion:search` | Include in all skills as "search workspace" instruction |
| `/Notion:find` | Include as "quick find by title" pattern |
| `/Notion:create-page` | Part of knowledge-capture skill |
| `/Notion:create-task` | Part of spec-to-implementation skill |
| `/Notion:create-database-row` | Document as MCP tool usage pattern |
| `/Notion:database-query` | Document as MCP tool usage pattern |
| `/Notion:tasks:setup` | Part of spec-to-implementation skill |
| `/Notion:tasks:plan` | Part of spec-to-implementation skill |
| `/Notion:tasks:build` | Part of spec-to-implementation skill |
| `/Notion:tasks:explain-diff` | Create as separate skill or merge |

**Recommendation:** Create a 5th skill `notion-agent-tasks` specifically for the async agent task workflow commands.

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

### Phase 1: Core Skill Conversion (Priority: High)

- [ ] Convert `knowledge-capture` skill to Codex format
- [ ] Convert `meeting-intelligence` skill to Codex format
- [ ] Convert `research-documentation` skill to Codex format
- [ ] Convert `spec-to-implementation` skill to Codex format
- [ ] Create `notion-agent-tasks` skill for async task workflows

### Phase 2: Supporting Content (Priority: Medium)

- [ ] Migrate reference documents to `references/` directories
- [ ] Adapt examples to work with Codex invocation patterns
- [ ] Create `config.toml.example` with MCP configuration
- [ ] Write installation script (`install.sh`)

### Phase 3: Documentation (Priority: Medium)

- [ ] Write comprehensive README with:
  - Installation instructions (3 methods)
  - MCP setup guide
  - Usage examples
  - Skill descriptions
- [ ] Create `AGENTS.md` example for project-level configuration
- [ ] Document differences from Claude Code version

### Phase 4: Testing & Validation (Priority: High)

- [ ] Test each skill with Codex CLI
- [ ] Verify MCP server connectivity
- [ ] Validate implicit invocation triggers
- [ ] Test explicit `$skill-name` invocation
- [ ] Ensure reference files are accessible

### Phase 5: Distribution (Priority: Low)

- [ ] Prepare GitHub repository structure
- [ ] Submit to OpenAI skills catalog (optional)
- [ ] Create release with installation instructions

---

## Part 4: Technical Considerations

### 4.1 MCP Authentication

Notion's hosted MCP server (`https://mcp.notion.com/mcp`) likely requires OAuth authentication. Codex CLI supports this via:

```bash
codex mcp login notion
```

The skills should include instructions for users to authenticate before first use.

### 4.2 Skill Discovery

Codex uses "progressive disclosure" - only skill names and descriptions are loaded at startup. This means:

1. Descriptions must be highly specific about triggers
2. Keywords in descriptions determine automatic activation
3. Users can always invoke explicitly with `$skill-name`

### 4.3 Context Window Management

Unlike Claude Code's unlimited context through summarization, Codex has fixed context limits. Skills should:

1. Keep instructions concise
2. Reference external files rather than inline everything
3. Use `references/` directory for detailed templates

### 4.4 Compatibility Notes

- **Model Differences**: Codex uses GPT-5-Codex models, not Claude. Some prompt patterns may need adjustment.
- **Tool Names**: MCP tool names should remain consistent, but verify with Notion's MCP server documentation.
- **Formatting**: Notion markdown formatting should work similarly, but test edge cases.

---

## Part 5: Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Notion MCP server incompatibility | Low | High | Test early, contact Notion if issues |
| Skill trigger conflicts | Medium | Medium | Use specific, unique descriptions |
| User confusion (no slash commands) | Medium | Low | Clear documentation, usage examples |
| OAuth flow issues | Medium | Medium | Document manual token setup as fallback |
| Context overflow | Low | Medium | Keep skills modular, reference external files |

---

## Part 6: Timeline Estimate

| Phase | Estimated Effort |
|-------|------------------|
| Phase 1: Core Skills | 2-3 days |
| Phase 2: Supporting Content | 1-2 days |
| Phase 3: Documentation | 1 day |
| Phase 4: Testing | 1-2 days |
| Phase 5: Distribution | 0.5 days |
| **Total** | **5-8 days** |

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
# From GitHub
$skill-installer install https://github.com/makenotion/codex-notion-skills

# Curated skills
$skill-installer <skill-name>
```

### MCP Commands
```bash
codex mcp add notion --url https://mcp.notion.com/mcp
codex mcp login notion
codex mcp list
```

### Skill Invocation
```
# Explicit
$notion-knowledge-capture

# In prompt
"Save this conversation as a how-to guide in Notion"  # Implicit trigger
```

---

## Appendix B: Sources

- [Codex CLI Documentation](https://developers.openai.com/codex/cli/)
- [Codex MCP Documentation](https://developers.openai.com/codex/mcp/)
- [Codex Skills Documentation](https://developers.openai.com/codex/skills/)
- [Create Skills Guide](https://developers.openai.com/codex/skills/create-skill/)
- [AGENTS.md Guide](https://developers.openai.com/codex/guides/agents-md)
- [OpenAI Skills Catalog](https://github.com/openai/skills)
- [Codex CLI GitHub](https://github.com/openai/codex)
