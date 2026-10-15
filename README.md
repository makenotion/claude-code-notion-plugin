# Notion Plugin for Claude Code

This repository provides an official Claude Code plugin that bundles:

- **Notion Skills** (from the Notion Cookbook) that teach Claude how to work intelligently inside your Notion workspace  
- The **[Notion MCP Server](https://developers.notion.com/docs/mcp)**, which enables Claude to securely search, read, and update your Notion content  
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
Claude Code automatically connects to Notion's hosted MCP server at:

```
https://mcp.notion.com/mcp
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
| `/Notion:search` | Search your entire Notion workspace |
| `/Notion:create-page` | Create a new page under a given parent |
| `/Notion:database-query` | Query a database by name or ID |
| `/Notion:create-task` | Create a task in a Tasks-style database |
| `/Notion:create-database-row` | Insert a row in any database |
| `/Notion:find` | Quick title-based search for pages/databases |
| `/Notion:tasks:setup` | Set up a Notion task board for tracking |
| `/Notion:tasks:build <url>` | Build a task from a Notion page URL |
| `/Notion:tasks:plan <url>` | Make a plan for a task from a Notion page URL |
| `/Notion:tasks:explain-diff` | Generate a Notion doc explaining code changes |

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

## Installation (Neotask)

Install from [Neotask Construct](https://construct.neotask.ai/p/notion-plugin):

```bash
neotask construct install notion-plugin
```

---

## 🔑 Authentication

The Notion MCP server supports **OAuth**!

---

## 🙌 Credits

- **Skills** by the Notion
- **MCP Server** by Notion  
- **Plugin Specification** by Anthropic 
