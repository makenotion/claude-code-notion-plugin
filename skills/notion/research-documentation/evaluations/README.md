# Research documentation evaluations

Follow the [shared evaluation protocol](../../evaluations.md) for fixture setup,
baseline comparisons, quality gates, usage measurements, and selection tests.
These scenarios are not instructions to load at runtime.

## Scenarios

| Fixture                                                                | Capability                      | Main checks                                                          |
| ---------------------------------------------------------------------- | ------------------------------- | -------------------------------------------------------------------- |
| [basic-research.json](basic-research.json)                             | Workspace synthesis             | Resolve accepted decision versus later-edited proposal               |
| [research-to-database.json](research-to-database.json)                 | Full comparison                 | All requested dimensions, verified pricing, citations, and schema    |
| [quick-answer.json](quick-answer.json)                                 | Short answer                    | One sufficient source, requested length, no publication              |
| [restricted-search.json](restricted-search.json)                       | Incomplete/conflicting evidence | Disclose coverage limits and unresolved decisions                    |
| [update-report.json](update-report.json)                               | Existing report update          | Targeted correction without replacing unrelated material             |
| [discover-and-synthesize.json](discover-and-synthesize.json)           | Successful discovery            | Select relevant sources, synthesize facts, and find the destination  |
| [feedback-counts-and-segments.json](feedback-counts-and-segments.json) | Feedback synthesis              | Deduplicated customers, segment differences, and counterexamples     |
| [feedback-unknown-identities.json](feedback-unknown-identities.json)   | Incomplete feedback             | Unknown identities and access limits do not become prevalence claims |

## Retained capability coverage

Quick brief, summary, comparison, and comprehensive templates remain available, as do citation and search references and all four worked examples. The database comparison case requires extensive coverage; also exercise the comprehensive template when formal methodology and appendices are requested.

## Acceptance

Require factual fidelity, requested scope, and correct persisted state before
comparing efficiency. Accept equivalent output structures and exposed tool names.
Review both full-workflow and short-request results on each tested model; do not
accept reduced token usage that drops requirements or weakens attribution.
