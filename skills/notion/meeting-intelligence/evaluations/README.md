# Meeting intelligence evaluations

Follow the [shared evaluation protocol](../../evaluations.md) for fixture setup,
baseline comparisons, quality gates, usage measurements, and selection tests.
These scenarios are not instructions to load at runtime.

## Scenarios

| Fixture                                                        | Capability                  | Main checks                                                                  |
| -------------------------------------------------------------- | --------------------------- | ---------------------------------------------------------------------------- |
| [decision-meeting-prep.json](decision-meeting-prep.json)       | Full decision preparation   | Both requested documents, options, risks, evidence, and timed agenda         |
| [status-meeting-prep.json](status-meeting-prep.json)           | Status preparation          | Accurate task metrics and separate internal/external destinations            |
| [agenda-only.json](agenda-only.json)                           | Short internal agenda       | No unnecessary pre-read, retrieval, or writes                                |
| [post-meeting-update.json](post-meeting-update.json)           | Recurring meeting follow-up | Outcomes and actions preserved without unrequested tasks                     |
| [current-external-context.json](current-external-context.json) | Customer research           | Current external evidence, analysis, and audience separation                 |
| [save-draft.json](save-draft.json)                             | Saved draft                 | Draft status honors an explicit Notion destination                           |
| [discover-meeting-context.json](discover-meeting-context.json) | Project discovery           | Find current project, previous actions, and meeting destination              |
| [linked-actions.json](linked-actions.json)                     | Linked follow-up tasks      | Supported commitments, identity resolution, deduplication, and relations     |
| [partial-action-recovery.json](partial-action-recovery.json)   | Partial-write recovery      | Reuse persisted tasks and repair missing relations without duplicate creates |

## Retained capability coverage

Decision, status, brainstorm, sprint planning, retrospective, and 1:1 templates remain available. The four worked examples retain fuller project, executive, sprint, and customer workflows. Exercise each template and series organization with appropriate audience fixtures before a release.

## Acceptance

Require factual fidelity, requested scope, and correct persisted state before
comparing efficiency. Accept equivalent output structures and exposed tool names.
Review both full-workflow and short-request results on each tested model; do not
accept reduced token usage that drops requirements or weakens attribution.
