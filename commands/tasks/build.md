---
description: Build a task from a Notion page URL
args: task_url
---

# Build Task from Notion

You are building a task that is tracked in Notion. The user is only watching the Notion board and isn't watching this session, so all feedback to the user must be sent through the Notion MCP.

## Input

The user has provided a Notion task URL: `$ARGS`

## Your Task

1. **Fetch the task details** from Notion using the MCP tools
   - Get the page content including title, description, and any relevant properties
   - Look for acceptance criteria, requirements, or specifications
   - Read any linked pages or references if needed

2. **Mark in progress**
   - Change the status of the task to "In progress".
   - Update the "Agent status" field to contain a short generic text description: 🤖 emoji followed by a word like "Starting..." or "Working..."

3. **Build it**
   - Work on the task per the specification. If this is a codebase, implement the code changes.
   - At each step, update the "Agent status" field to explain what's currently happening, so the user can see what's going on. Keep it brief: a relevant emoji followed by a few words. Examples: "📂 Searching relevant files...", "🎨 Updating color scheme...", "🧪 Running tests..."
   - If you need to get user input to clarify the spec or answer other questions, follow the Communication Protocol below.

4. **Update the task status**
   Once complete:
   - Update the task status in Notion to "Done"
   - If you made a code change, run /notion:tasks:explain-diff to generate a page explaining the code change.
   - Follow the Communication Protocol below and briefly tell the user the results of the task. Link to the diff explanation if appropriate for a code change.

## Communication Protocol

Every time you want to communicate with the user, follow the following steps.

- Add a comment to the task. Prefix your comment with "Message from Claude:" on its own line in bold.
- Set the "Agent blocked" column to true, and the Agent Status column to a short message explaining the request, like "❓ Choose a color scheme" or "❓ Give architecture feedback"
- Poll every 15 seconds to see if the user has responded with their own comment. (Follow polling instructions below)

## Notes

- If the URL is invalid or inaccessible, ask the user to verify the URL and their Notion connection
- If requirements are unclear, ask clarifying questions before implementing

## How to poll

- Always use a sub-agent to poll with max turns set to 100 to avoid polluting the parent content. 
- You can use a Bash sleep interleaved with MCP tool call. 