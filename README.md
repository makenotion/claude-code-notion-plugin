# Notion Plugin for Claude Code

This repository provides an official Claude Code plugin that bundles:

- **Notion Skills** (from the Notion Cookbook) that teach Claude how to work intelligently inside your Notion workspace  
- The **Notion MCP Server** (`@notionhq/notion-mcp-server`), which enables Claude to securely search, read, and update your Notion content  
- A curated set of **Slash Commands** that make common Notion workflows fast and natural  

This plugin allows Claude Code users to install everything — Skills + MCP server — with **one click**.

---

## 🚀 Features

### ✅ Fully packaged Notion Skills
Includes all four high-quality Skills from the Notion Cookbook:

- **Knowledge Capture**
- **Meeting Intelligence**
- **Research Documentation**
- **Spec to Implementation**

These instructions teach Claude how to structure, write, summarize, capture, and maintain content in your Notion workspace.

### ✅ Integrated Notion MCP Server  
Claude Code automatically launches:

```
npx -y @notionhq/notion-mcp-server
```

This provides Claude with tools to:

- Search your workspace  
- Retrieve pages & databases  
- Create and update pages  
- Append notes or blocks  
- Insert database rows  
- Work with properties safely  

### ✅ Powerful Slash Commands  
This plugin ships with a set of helpful commands:

| Command | Description |
|--------|-------------|
| `/notion-search` | Search your entire Notion workspace |
| `/notion-create-page` | Create a new page under a given parent |
| `/notion-database-query` | Query a database by name or ID |
| `/notion-create-task` | Create a task in a Tasks-style database |
| `/notion-create-database-row` | Insert a row in any database |
| `/notion-find` | Quick title-based search for pages/databases |

These commands leverage both the Notion Skills and the MCP server.

---

## 📦 Installation (Claude Code)

### 1. Add this plugin's marketplace
In Claude Code, run:

```bash
/plugin marketplace add makenotion/claude-code-notion-plugin
```

### 2. Install the plugin

```bash
/plugin install notion-workspace-plugin@notion-plugin-marketplace
```

### 3. Restart Claude Code  
This ensures the MCP server starts correctly.

---

## 🔑 Authentication

The Notion MCP server supports **OAuth**!

---

## 🙌 Credits

- **Skills** by the Notion
- **MCP Server** by Notion  
- **Plugin Specification** by Anthropic 
- **COYS** 