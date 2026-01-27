---
name: notion-explain-diff
description: Generate educational Notion pages explaining code changes; use when documenting diffs with context, intuition, and verification steps.
metadata:
  short-description: Document code changes in Notion
---

# Notion Explain Diff

Create comprehensive Notion documentation explaining code changes with background, intuition, walkthrough, and verification steps.

## Quick start
1) Identify code changes to explain (diff, PR, or recent commits).
2) Research surrounding code for context.
3) Create explanation page with `Notion:notion-create-pages` including all sections.
4) Add diagrams and quiz for educational value.
5) Return link to the explanation page.

## Workflow

### 0) If any MCP call fails because Notion MCP is not connected, pause and set it up:
1. Add the Notion MCP:
   - `codex mcp add notion --url https://mcp.notion.com/mcp`
2. Enable remote MCP client:
   - Set `[features].rmcp_client = true` in `config.toml` **or** run `codex --enable rmcp_client`
3. Log in with OAuth:
   - `codex mcp login notion`

After successful login, the user will have to restart codex. You should finish your answer and tell them so when they try again they can continue with Step 1.

### 1) Gather change context
- Get the diff or identify changes from PR/commits.
- Read surrounding code to understand the system.
- Identify the "why" behind the changes.

### 2) Structure the explanation
Create page with these sections:
- **Background**: System context for beginners + direct context for experts
- **Intuition**: Core insight, the "aha moment" of the change
- **Code Walkthrough**: Logical grouping of changes with explanations
- **Verification**: How it was tested + manual QA guide
- **Alternatives** (optional): Other approaches considered
- **Quiz**: 5 questions to verify understanding

### 3) Create the page
- Use `Notion:notion-create-pages` with structured content.
- Include Mermaid diagrams for data/control flow.
- Use callouts for key concepts and warnings.
- Add toggle blocks for quiz answers.

### 4) Add educational elements
- Write in clear, engaging style.
- Include concrete examples with sample data.
- Create diagrams showing before/after state.
- Write quiz questions that test real understanding.

### 5) Link and share
- Link to related task or spec if applicable.
- Return URL to the explanation page.
- Suggest sharing with team for review knowledge.
