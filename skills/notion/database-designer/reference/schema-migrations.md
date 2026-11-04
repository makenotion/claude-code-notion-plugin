# Evolving an existing schema

Read this when a design changes stored values, property types, options, relation
targets, or record locations. Adding an independent empty property generally
does not require a full migration procedure.

## Establish the mapping

Fetch the current schema and identify the affected records, downstream views,
formulas, rollups, and relations visible through the connection. Report unknown
dependencies; do not imply a workspace-wide audit from a limited inspection.
Preserve rich-text mentions and formatting when rewriting values; use a faithful
record representation rather than a lossy SQL or plain-text projection.

Define source-to-destination mappings, including empty values, unmatched options,
and relation targets. Inspect every affected record before claiming a lossless
mapping, following pagination. If scope is too large for one run, agree on a
bounded batch and report coverage rather than silently stopping early.

## Preserve reversibility

Prefer adding and populating a replacement property before removing the source
when an in-place conversion could discard information. Retain original values
until mappings and dependencies are verified. Never drop unmatched values into a
default status or repoint relations based only on similar names.

If a requested change would delete or irreversibly transform data and the user
has not authorized that concrete consequence, explain the affected data and ask
before that step. Continue independent, authorized work where useful. Do not
require renewed approval for an already authorized mapping.

## Execute and reconcile

Apply independent writes in supported batches. Track source IDs, destination IDs,
and confirmed outcomes. After partial or ambiguous results, read affected state
and retry only missing changes. Do not create replacement records unnecessarily.
If tools cannot perform a required conversion, provide the exact remaining manual
step and leave the original data intact.

Verify mapped record counts and values, preserved page content and relations, and
affected view or calculation behavior. Do not claim completion based on a schema
write alone. Retire old properties or records only within the authorized scope;
otherwise report them as intentionally retained with any remaining dependencies.
