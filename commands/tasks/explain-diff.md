---
description: Makes a Notion doc explaining a code change.
args: task_url
---

### Task

Make me a rich explanation of the specified code change as a new Notion page.

### Input

The user will point you to some code changes to explain. If they don't explicitly specify, then explain the most recent batch of changes made in this conversation. 

### Sections

- **Background**: Explain the existing system relevant to this change. You should broadly explore surrounding code for this. We don't know how much the reader already knows, so include a deep background for beginners (note that it can be skipped if the reader is already familiar), and then a more narrow background directly relevant to the change.
- **Intuition**: Explain the core intuition for the code change. The focus here is to explain the essence, not the full details. Use concrete examples with toy data. Use figures and mermaid diagrams liberally.
- **Code**: Do a high-level walkthrough of the changes to the code. Group/order the changes in an understandable way.
- **Verification**: Explain how the code change was verified for correctness by the agent, eg. unit tests, integration tests, etc. Give the user a step by step guide on how to manually QA the change.
- **Alternatives**: Describe 1-2 alternative approaches if you are able to identify any. Each alternative should include a pros and cons list compared to the specified change. Layout the pros/cons list in 2 columns. Only include an alternative if it represents an orthogonal way of solving the problem. If you cannot identify any alternatives, omit this section.
- **Quiz**: Come up with 5 questions that test the reader's knowledge of this PR. This should be medium difficulty, difficult enough that you actually need to understand the substance of the PR to answer them, but not gotchas. The goal is to help the reader make sure that they've actually understood. Each question should have some multiple choice answers with an explanation detailing why an answer is correct or incorrect. Use toggle blocks to represent this. For example:
  ```markdown
  1. Question
     ▶ Option 1
      ❌ Explanation for why it was incorrect
     ▶ Option 2
      ❌ Explanation for why it was incorrect
     ▶ Option 3
      ✅ Explanation for why it was correct
     ▶ Option 4
       ❌ Explanation for why it was incorrect
  2. Question
     ...
  ```

### Formatting

- Use the Notion MCP tools to create a new page and return the URL of the new page.
- Please write with the clarity and flow of Martin Kleppmann, making it engaging and written in classic style. Transitions between sections should be smooth.
- Some tips on diagrams. Ideally, you should pick a small number of diagram families that can be reused throughout the explanation to explain various cases. Some useful kinds of diagrams:
  - A system diagram showing data flow or communication between components. Make sure to include example data here!
- Use callouts for key concepts or definitions, important edge cases, etc.
