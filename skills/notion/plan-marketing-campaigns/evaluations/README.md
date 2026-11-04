# Evaluation cases

Use the [collection protocol](../../evaluations.md) with stateful mock tools.
These are scenario specifications, not executed tests. Compare no-skill, previous-skill, and revised-skill runs when measuring
regression or improvement. A single live run is a behavioral smoke test, not
evidence of cross-model reliability.

- `context-to-workspace.json`: context extraction, domain decisions, populated
  structure, evidence fidelity, and usable navigation.
- `preview-and-provenance.json`: preview-only scope, first-party references,
  and honest handling of inaccessible gallery layouts.
- `resume-limited-tools.json`: uncertain-write recovery, reuse, and useful
  fallback when databases and views cannot be created.

Supply current valid tool schemas; source bodies are available through fetch,
not injected as user instructions. Preserve writes in mock state for readback.
Resolve names only when a unique matching user exists; an unavailable match
should remain unassigned with the name retained in the body. For visual grading,
inspect a rendered disposable page when available and record whether that check
was performed. Judge navigation, density, hierarchy, and an obvious next action,
not exact heading strings or a fixed count of decorative elements.

## Visual design cases

- `visual-composition.json`: open gallery inspiration, coherent styling, useful
  first screen, and navigation with real content.
- `limited-design-capabilities.json`: text-only fallback, sparse information,
  and honest visual verification.

Existing first-party-only cases intentionally retain that restriction in their
user prompts: source selection must follow the particular user's request.
For visual runs, render persisted mock output in Notion or use a disposable test
workspace with authorization. Record desktop and narrow-screen observations;
do not count mock structural checks as proof of rendered beauty.

`default-private-destination.json` checks that an omitted destination uses the
connection's private default. Grade visual composition against the relevant
gallery patterns, not merely the presence of an icon, cover, or callout.

## Connected workspace case

- `connected-campaign-workspace.json`: sidebar architecture, native campaign
  relations, visible record properties, distinct working bodies, and rendered
  navigation across the system. Run with only the query and source brief, not
  these grading criteria or design coaching. Keep sample data separate from
  existing work and preserve the raw output. Parent-agent manual redesigns do
  not count as skill passes.

## Reference workspace replay

- `reference-workspace.json`: isolated fictional campaign-system brief. Give the
  runner only the query/context and runtime skill, withholding scoring criteria
  and existing sample IDs. Check saved relations/views and rendered navigation.
- [Recorded desktop smoke test](reference-workspace-results.md): observed outcomes,
  instruction revisions, and the limits of this single live test.
