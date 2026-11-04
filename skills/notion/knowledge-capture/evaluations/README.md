# Knowledge capture evaluations

Follow the [shared evaluation protocol](../../evaluations.md) for fixture setup,
baseline comparisons, quality gates, usage measurements, and selection tests.
These scenarios are not instructions to load at runtime.

## Scenarios

| Fixture                                                        | Capability                     | Main checks                                                              |
| -------------------------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------ |
| [conversation-to-wiki.json](conversation-to-wiki.json)         | How-to capture                 | Exact commands, prerequisites, verification, and rollback                |
| [decision-record.json](decision-record.json)                   | Decision capture in a database | Alternatives, rationale, consequences, known metadata, and actual schema |
| [update-existing.json](update-existing.json)                   | Update existing knowledge      | Preserve unrelated content; no duplicate page or redundant search        |
| [draft-without-connection.json](draft-without-connection.json) | Draft from incomplete notes    | No fabricated consensus or metadata; usable disconnected output          |
| [content-types.json](content-types.json)                       | FAQ and learning capture       | Both formats retain facts and actions without publishing                 |

## Retained capability coverage

Concept/reference pages, wiki organization, meeting summaries, and specialized database design remain supported by the entrypoint and all six schema references. Exercise those with representative workspace fixtures before a release; the five cases do not exhaust every document type.

## Acceptance

Require factual fidelity, requested scope, and correct persisted state before
comparing efficiency. Accept equivalent output structures and exposed tool names.
Review both full-workflow and short-request results on each tested model; do not
accept reduced token usage that drops requirements or weakens attribution.
