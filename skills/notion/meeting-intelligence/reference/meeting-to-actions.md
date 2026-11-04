# Turn meeting outcomes into linked actions

Use when the user requests follow-up task creation or reconciliation after a
meeting. A summary alone does not require task records.

## Extract commitments

Read the supplied notes or transcript, retrieving the transcript when necessary
and available. Distinguish agreed decisions, committed actions, proposed follow-ups,
and unresolved discussion. Preserve only stated or confirmed owners and dates.
Use the meeting date and timezone to resolve relative dates where unambiguous;
otherwise leave the date unset and flag it. Resolve people to actual workspace
identities; do not choose among same-name users by guesswork.

## Resolve destinations and existing work

Use the supplied or established meeting, task, and project locations. Follow known
links or search narrowly if needed. Fetch the relevant schemas once and identify
the correct data sources, status values, person fields, and relation targets.
An existing meeting note may already be the meeting record; do not create a
duplicate just to fit a template. If a required destination is ambiguous, prepare
the supported content while resolving it; do not create an unsolicited private page.

Check existing tasks linked to the meeting or project for the same commitment.
Compare source, objective, and scope rather than title alone. Reuse matching tasks
and update changed commitments within the request. Similar tasks for other work
are not duplicates. Preserve completed work unless the meeting explicitly changes
it; raise conflicts instead of reopening a task by inference.

## Write and verify

Update or create the requested meeting record, preserving prior notes. Create only
missing committed tasks; keep proposals and questions in the meeting record unless
the user requests tasks for them. Set meeting and project relations when those
properties exist and point to the correct data sources. Otherwise use source links
and report the schema limitation; do not redesign databases as a side effect.

Create prerequisite records before dependent relations. Batch independent task
creates when supported. Track successful IDs; after a timeout or partial failure,
query the relevant records to resolve uncertain outcomes and retry only missing
work. If state cannot be established, report the uncertainty instead of blindly
repeating the create. Apply the same duplicate check on a user-requested rerun.

Verify supported decisions, task contents, owners, dates, and relation targets.
Return the meeting link, created or updated task links, and unresolved items.
Do not notify participants unless requested.
