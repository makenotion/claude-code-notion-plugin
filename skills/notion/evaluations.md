# Evaluating the Notion skills

These scenarios test retained capabilities and efficient execution. They are test
specifications, not runtime instructions or a bundled automated agent runner.
Do not load this file or the evaluation directories during ordinary skill use.

## Compare behavior before optimizing

Run the same scenario in fresh sessions under three conditions:

1. No skill, with the same tools and source material.
2. The skill version before the change, including its original supporting files.
3. The revised skill and its supporting files.

For new skills, compare no-skill and new-skill runs; mark the previous-skill
condition as not applicable rather than substituting an unrelated workflow.

Use identical model versions, reasoning settings, tool schemas, tool fixtures,
and user prompts. Record the tested commit for each skill version. Test a current
strong model and a smaller or older supported model; record exact model IDs and
product surface rather than assuming family names identify the configuration.
Repeat cases enough to distinguish consistent behavior from a lucky run; report
run counts and variation. No performance gain is established by file size alone.

## Run a scenario

Each JSON file has a user `query`, a skill name, fixture `context`, and observable
`success_criteria`. The context describes what the evaluator must supply; do not
paste all tool fixtures into the agent's user message.

- Deliver `conversation` as prior conversation, when present.
- Expose the listed logical `tools` using the target client's actual names and
  schemas. Permit semantically equivalent tool calls and valid batching.
- Serve `sources`, search results, schemas, task records, and web responses only
  through appropriate tool calls. Fixture URLs and IDs are fictional identifiers;
  map them consistently to valid IDs if a client validates their shape. Do not
  contact the fictional domains or a live workspace.
- For discovery cases, `search_routes` maps a query intent to its returned results.
  Match semantically equivalent queries without requiring exact wording. Return
  only result metadata from search; source bodies remain available through fetch.
  A broad query spanning multiple listed intents returns their deduplicated union.
  Unrelated queries return no results. Use the same routing in every comparison.
  Serve `tool_access` through the access-check tool when present.
- For `query_routes`, match the query intent and honor its project, period, and
  other filters. Return `records`, or one entry of `pages` at a time using the
  supplied cursor. A subsequent page is available only when requested. Preserve
  `complete: false` and notices; repeated calls cannot reveal inaccessible rows.
  Expose record bodies through fetch at their URLs as well, preferring explicit
  `sources` content when present. Serve `users` through the user lookup tool.
  Query fixtures are initial state: subsequent queries must reflect writes.
- Keep mutations in an isolated stateful mock or disposable test workspace.
  Record creates and updates, return stable page URLs, and make subsequent reads
  reflect writes. A supplied current schema need not be fetched again.
- For `partial-create-recovery`, supply `prior_result` as previous conversation
  history and reveal existing records through tools. For `restricted-search`,
  return the stated notices with search results; additional searches cannot invent
  an accepted decision.
- For the implementation scenario, materialize `repository_files` in an isolated
  temporary directory and allow edits and tests there only.
- Do not expose the success criteria or expected answer to the agent performing
  the task. Inspect its trace, final answer, and resulting artifacts afterward.

The harness must define any additional tool responses consistently across all
three conditions. Missing fixtures are an evaluation setup problem, not evidence
that a model failed. Manual runs are acceptable; retain transcripts and artifacts.

## Grade quality first

Grade each criterion with evidence from the output, tool trace, or persisted state.
Accept equivalent structures and wording. A correct result does not require an
exact heading sequence, fixed source count, or specific client tool prefix.

Required checks include factual fidelity, requested scope, citations supporting
claims, correct destination/schema, audience separation, and truthful completion
reporting. Unsupported facts, lost requirements, unauthorized writes, leaked
internal content, or duplicate records fail the case even if token use is lower.
Two-document and comprehensive-report cases must still produce the full requested
outputs; efficiency does not excuse skipping substantive work.

## Measure efficiency among passing runs

Record these separately rather than collapsing them into a quality/token ratio:

| Measure         | What to record                                                                 |
| --------------- | ------------------------------------------------------------------------------ |
| Quality         | Passed criteria, failures, and overall successful runs                         |
| Input usage     | Total model input tokens across the run; cached tokens separately when exposed |
| Output usage    | Total output tokens; reasoning tokens separately when exposed                  |
| Context loading | Skill/reference files read and tool-result volume                              |
| Tool work       | Calls, redundant reads/searches, writes, retries, and batching                 |
| Interaction     | Unnecessary clarification turns and time to completion                         |

Use provider-reported usage where available. Mark unavailable metrics rather than
estimating token savings from word counts. Compare within a model and surface;
tokenizers, caching, and usage accounting differ across providers. Preserve raw
results, model settings, fixtures, and artifact links with each run. Report any
quality regression before recommending an efficiency improvement.

## Test skill selection separately

With all six skills available, check which skill is selected for representative
requests. Explicitly invoking a skill tests execution, not automatic discovery.

| Request                                                      | Expected selection     |
| ------------------------------------------------------------ | ---------------------- |
| Turn these scattered customer requests into a useful tracker | Database designer      |
| Draft this week’s project update, compared with last week    | Weekly project digest  |
| Create follow-up tasks from these meeting notes              | Meeting intelligence   |
| Synthesize customer feedback, preserving segment differences | Research documentation |
| Update the owner on this one task                            | None of these skills   |
| Save this conversation as a team FAQ                         | Knowledge capture      |
| Prepare an agenda from our project notes                     | Meeting intelligence   |
| Reconcile the workspace sources about our auth approach      | Research documentation |
| Create implementation tasks from this spec                   | Spec to implementation |
| Rewrite this one sentence in a warmer tone                   | None of these skills   |
| What is 12 multiplied by 8?                                  | None of these skills   |

Composite requests may legitimately use more than one skill. Check that each
selected skill contributes to the requested outcome instead of repeating work.

## Further capability checks

The per-skill READMEs map capabilities to cases and retained resources. Also vary
page ambiguity, inaccessible sources, schema changes, pagination, stale content,
and tool errors. Add scenarios from observed failures rather than adding broad
instructions speculatively. The checked-in scenarios are a starting suite, not
proof of cross-model reliability.

Authoring references: [Anthropic skill best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
and [OpenAI skill guidance](https://learn.chatgpt.com/docs/build-skills).
