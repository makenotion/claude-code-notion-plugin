# Organize a webhook release and its technical docs

This fictional example shows a release overview connected to a small engineering
library. The brief supplies the technical facts; the resulting pages keep current
behavior, accepted decisions and proposed changes distinct.

## Starting brief

> Create a Notion engineering home for Beacon, our webhook delivery service. We
> track this small release in Notion. Use the notes below to organize the release
> work and technical docs. We need to decide whether retry safety is ready for the
> next rollout review on November 9, 2026. There is no committed release date.
>
> Current behavior: the dispatcher puts a delivery in the queue, and a worker
> sends it to the customer's endpoint. Timeouts and 5xx responses are retried.
> Each attempt has its own attempt ID; the delivery ID stays the same. A 2xx
> response ends retries. The retry schedule is not included in these notes.
>
> Accepted decision, October 22: keep the delivery ID stable across retries and
> include it in the webhook payload. Customers can use it to deduplicate events.
> This does not guarantee exactly-once processing at the receiver.
>
> Proposed change: persist the receiver's response before acknowledging the queue
> message. We still need a decision on recovery if the worker crashes after the
> receiver accepts a request but before that response is stored.
>
> Work: repeat-delivery recovery is blocked, P0, Sam; persist responses is in
> progress, P1, Jules; add timeout coverage is in progress, P1, Priya; document
> customer deduplication is not started, P2, unassigned; stable delivery IDs and
> 2xx completion handling are done, P1, Jules and Sam respectively.
>
> Existing operating notes: if deliveries back up, check queue depth and oldest
> message age, then separate receiver failures from worker failures. Capture
> delivery IDs and response codes before escalating to the on-call engineer. Do
> not bulk replay deliveries until duplicate-processing risk is understood.
> Dashboard links, replay commands and the on-call route still need confirming.

Names are fictional labels for this example, not identities to assign in a real
Notion workspace. Unspecified dates, links and settings remain unset.

## Connected pages

```text
📡 Beacon engineering
├── 🛠 Release work
│   ├── Resolve repeat-delivery recovery
│   ├── Persist receiver responses
│   ├── Add timeout coverage
│   ├── Document customer deduplication
│   ├── Keep delivery IDs stable
│   └── Stop retries after a 2xx response
└── 📚 Technical docs
    ├── Delivery flow today
    ├── Keep delivery IDs stable across retries
    ├── Persist responses before queue acknowledgement
    └── Investigate a delivery backlog
```

Release work and Technical docs are the two underlying databases. The home embeds
filtered views of these databases. Related work and Related docs are reciprocal
relations so a reader can move from the blocker to the proposal and back.

## Home layout

Use a full-width page, a blue signal icon and the default readable prose font.
Keep the title compact, without a tall cover. The first row has two columns:

| Left: release decision, about 44%                                                             | Right: work by status, about 56%                                         |
| --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Retry safety**                                                                              | Native bar chart titled **Work by status**                               |
| **Decision pending:** resolve recovery after receiver acceptance and before response storage. | Blocked: **1**; In progress: **2**; Not started: **1**; Done: **2**.     |
| Mention **Resolve repeat-delivery recovery** with its orange warning icon.                    | Count all six records, including completed work.                         |
| **Next review:** November 9, 2026. Release date not set.                                      | Color blocked orange, in progress blue, done green and not started gray. |

The summary is a snapshot from the brief. The chart counts live records; it does
not label four remaining items as a release-readiness percentage.

Below that row, use **Open work** and **Specs & runbooks** tabs. Open work is the
default. A separate **Completed** view keeps finished work reachable. Hide repeated
database titles and wrap long issue titles. Show Title, Status, Priority and
Engineer together; keep Related docs and other details inside the records.

## Release work

| Title                             | Status      | Priority | Engineer   | Related docs                                                                            |
| --------------------------------- | ----------- | -------- | ---------- | --------------------------------------------------------------------------------------- |
| Resolve repeat-delivery recovery  | Blocked     | P0       | Sam        | Persist responses before queue acknowledgement; Keep delivery IDs stable across retries |
| Persist receiver responses        | In progress | P1       | Jules      | Persist responses before queue acknowledgement                                          |
| Add timeout coverage              | In progress | P1       | Priya      | Delivery flow today; Persist responses before queue acknowledgement                     |
| Document customer deduplication   | Not started | P2       | Unassigned | Keep delivery IDs stable across retries                                                 |
| Keep delivery IDs stable          | Done        | P1       | Jules      | Keep delivery IDs stable across retries                                                 |
| Stop retries after a 2xx response | Done        | P1       | Sam        | Delivery flow today                                                                     |

Open work filters out Done without excluding unassigned records. Group by Status
and sort by Priority within each group. Completed filters to Done. Pin Status,
Priority and Engineer on work pages; keep document relations visible beneath them.
Use an orange warning icon for the blocker, blue tools for active implementation,
a purple writing icon for the documentation task and green checks for done work.

### Inside “Resolve repeat-delivery recovery”

**Why this blocks the review**

The receiver can accept a delivery before Beacon stores its response. If the
worker crashes in that interval, the queue message may be handled again. Persisting
responses alone does not settle how that repeat should be treated.

**Decision needed**

Describe the recovery behavior for this crash interval before deciding whether
retry safety is ready. Customer deduplication remains relevant because the accepted
stable-ID decision does not promise exactly-once processing.

**Review with**

- **Persist responses before queue acknowledgement** — proposed ordering and the
  unresolved crash interval.
- **Keep delivery IDs stable across retries** — accepted delivery identity contract.

**Next step**

Sam: bring the recovery proposal to the November 9 review. Keep this item blocked
until the decision is recorded. A release date has not been committed.

## Technical library

The Specs & runbooks tab contains a compact table with Title, Topic and Document
status. Owners remain empty because the brief names work owners, not doc owners.

| Title                                          | Topic        | Document status | Icon                    |
| ---------------------------------------------- | ------------ | --------------- | ----------------------- |
| Delivery flow today                            | Architecture | Current         | Blue diagram            |
| Keep delivery IDs stable across retries        | Decisions    | Accepted        | Green check             |
| Persist responses before queue acknowledgement | Proposals    | Proposed        | Purple branching arrows |
| Investigate a delivery backlog                 | Operations   | Draft           | Orange wrench           |

Each document exposes its status and related work at the top. Use one main column
for technical explanations, with short headings and technical identifiers in
monospace. The runbook remains Draft because its operational destinations are not
yet confirmed.

### Inside “Persist responses before queue acknowledgement”

**Proposed change**

Store the receiver response before acknowledging the queue message. The current
flow sends a queued delivery and retries timeouts or 5xx responses. This proposal
changes the ordering of response storage and acknowledgement; it does not establish
a new retry schedule.

**Identity contract**

The delivery ID stays the same across attempts. Each attempt has a separate attempt
ID. See **Keep delivery IDs stable across retries** for the accepted decision.

**Unresolved recovery case**

The receiver accepts a request, then the worker crashes before recording the
response. A later attempt may reach the receiver again. Recovery behavior for this
interval is undecided; do not describe the proposal as deployed or approved.

**Related work**

Resolve repeat-delivery recovery · Persist receiver responses · Add timeout coverage.

### Inside “Investigate a delivery backlog”

1. Inspect queue depth and oldest message age. **Dashboard destination: to confirm.**
2. Separate receiver failures from worker failures using the affected delivery IDs
   and response codes. Capture those details for the investigation.
3. Escalate to the on-call engineer with the observed backlog and error pattern.
   **On-call route: to confirm.**
4. Before any bulk replay, establish the risk of duplicate processing. Replay
   commands are not provided in the notes; this page does not invent one.

Related reading: **Delivery flow today** explains retries and completion;
**Keep delivery IDs stable across retries** explains customer deduplication.

## Handoff

> Beacon engineering now puts the retry-safety decision beside the current work
> counts. Open “Resolve repeat-delivery recovery” first; its linked proposal and
> accepted decision explain what needs resolving before the November 9 review.
> The technical library separates current behavior from proposals. The backlog
> runbook still needs its dashboard and on-call destinations confirmed.
