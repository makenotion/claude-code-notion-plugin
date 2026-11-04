# Evaluation cases

Use the [collection protocol](../../evaluations.md) with stateful mock tools.
These are scenario specifications, not executed tests. Compare no-skill and
new-skill runs; the previous-skill condition is not applicable.

- `context-to-workspace.json`: context extraction, domain decisions, populated
  structure, evidence fidelity, and usable navigation.
- `preview-and-provenance.json`: preview-only scope, first-party references,
  and accurate source attribution.

Supply current valid tool schemas; source bodies are available through fetch,
not injected as user instructions. Preserve writes in mock state for readback.
Resolve names only when a unique matching user exists; an unmatched name
should remain unassigned with the name retained in the body. For visual grading,
inspect a rendered disposable page when available and record whether that check
was performed. Judge navigation, density, hierarchy, and an obvious next action,
not exact heading strings or a fixed count of decorative elements.

## Visual design cases

- `visual-composition.json`: open gallery inspiration, coherent styling, useful
  first screen, and navigation with real content.

Existing first-party-only cases intentionally retain that restriction in their
user prompts: source selection must follow the particular user's request.
For visual runs, render persisted mock output in Notion or use a disposable test
workspace with authorization. Record desktop and narrow-screen observations;
do not count mock structural checks as proof of rendered beauty.

`default-private-destination.json` checks that an omitted destination uses the
connection's private default. Grade visual composition against the relevant
gallery patterns, not merely the presence of an icon, cover, or callout.

## Reference workspace replay

`reference-workspace.json` supplies a fictional brief for an authorized private
workspace. Give the runner only its query/context and the runtime skill; withhold
success criteria and existing sample page IDs. Record the first result, inspect
the saved views and relations, and walk the rendered workspace in Notion. Compare
workflow, hierarchy, visible metadata and detail-page usefulness with the documented
layout guidance, not exact prose or pixels. A reviewer-polished output is
not a passing forward test. Report retries and the visual checks performed.
