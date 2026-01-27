# Notion Skills for Codex CLI

Skills that teach Codex how to work intelligently with your Notion workspace using the Notion MCP Server.

## Skills Included

### Workflow Skills
| Skill | Description |
|-------|-------------|
| `notion-knowledge-capture` | Transform conversations into structured Notion documentation |
| `notion-meeting-intelligence` | Prepare meeting materials with Notion context |
| `notion-research-documentation` | Document research findings in Notion |
| `notion-spec-to-implementation` | Convert specs into implementation plans and tasks |

### Action Skills
| Skill | Description |
|-------|-------------|
| `notion-search` | Search workspace with natural language queries |
| `notion-find` | Find pages/databases by title keywords |
| `notion-create-page` | Create pages with intelligent defaults |
| `notion-create-task` | Create tasks with property mapping |
| `notion-create-database-row` | Insert rows into any database |
| `notion-database-query` | Query databases with natural language filters |

### Agent Skills
| Skill | Description |
|-------|-------------|
| `notion-agent-setup` | Interactive setup wizard for task boards |
| `notion-agent-plan` | Autonomous task planning from Notion URLs |
| `notion-agent-build` | Autonomous task implementation |
| `notion-explain-diff` | Generate documentation explaining code changes |

## Installation

### 1. Clone to your Codex skills directory

```bash
git clone https://github.com/Yosuke-Maeda/skills.git $CODEX_HOME/skills
```

Or add as a subdirectory:

```bash
git clone https://github.com/Yosuke-Maeda/skills.git $CODEX_HOME/skills/notion
```

### 2. Configure Notion MCP Server

Add to your `~/.codex/config.toml`:

```toml
[features]
rmcp_client = true

[mcp_servers.notion]
type = "http"
url = "https://mcp.notion.com/mcp"
```

See `config.toml.example` for reference.

### 3. Authenticate with Notion

```bash
codex mcp login notion
```

This opens OAuth flow to connect your Notion workspace.

### 4. Restart Codex

Restart Codex CLI to load the skills and MCP server.

## Usage

Invoke skills with `$skill-name`:

```
$notion-search find my project roadmap
$notion-create-task Add authentication to the login page
$notion-agent-plan https://notion.so/workspace/Task-abc123
```

## Credits

- Skills by Notion
- MCP Server by Notion
