# Spec to implementation evaluations

Follow the [shared evaluation protocol](../../evaluations.md) for fixture setup,
baseline comparisons, quality gates, usage measurements, and selection tests.
These scenarios are not instructions to load at runtime.

## Scenarios

| Fixture                                                                  | Capability                     | Main checks                                                                     |
| ------------------------------------------------------------------------ | ------------------------------ | ------------------------------------------------------------------------------- |
| [basic-spec-implementation.json](basic-spec-implementation.json)         | Plan only                      | Functional/non-functional requirements, acceptance criteria, and open questions |
| [spec-to-tasks.json](spec-to-tasks.json)                                 | Task creation                  | Requirement coverage, actual schema, dependencies, and links                    |
| [partial-create-recovery.json](partial-create-recovery.json)             | Interrupted writes             | Inspect uncertain outcomes and create only missing work                         |
| [spec-change-progress.json](spec-change-progress.json)                   | Spec changes and progress      | Preserve completed work and reconcile affected requirements                     |
| [implement-small-spec.json](implement-small-spec.json)                   | Actual implementation          | Inspect code, implement, validate, and report evidence                          |
| [discover-spec-and-destination.json](discover-spec-and-destination.json) | Spec and destination discovery | Resolve the current spec and database before saving a plan                      |

## Retained capability coverage

Quick/standard plans, spec parsing, task templates, progress updates, milestone summaries, and API/UI/migration examples remain available. Validate larger dependency graphs and milestone reporting with complete task fixtures before a release.

## Acceptance

Require factual fidelity, requested scope, and correct persisted state before
comparing efficiency. Accept equivalent output structures and exposed tool names.
Review both full-workflow and short-request results on each tested model; do not
accept reduced token usage that drops requirements or weakens attribution.
