# Search strategies

## Start from known context

Fetch a supplied page or data source directly. Otherwise search with short,
specific terms and the known project or location. Fetch important matches before
using them as evidence. Reuse fetched content and deduplicate by stable source ID.
Do not search just to rediscover a supplied URL or fetch a minimum number of pages.

## Choose filters from the live schema

Tool prefixes and parameters vary by connection. Read the exposed tool schema;
if a tool-access check is available, reuse its result for the task. Inspect
response notices for dropped filters, missing sources, or partial coverage.

| Need                 | Strategy                                                                                 |
| -------------------- | ---------------------------------------------------------------------------------------- |
| Project context      | Scope to the known page, data source, or teamspace when supported                        |
| Author expertise     | Filter by known creator/editor when supported; do not assume author implies authority    |
| Recent developments  | Use supported edited-date filters; creation date alone misses updates to old pages       |
| Historical evolution | Retrieve dated decisions and revisions, then distinguish effective dates from edit dates |
| Specific record      | Use title or exact filters supported by the connection                                   |

If a requested filter is unavailable, verify the relevant condition from fetched
sources when possible. Otherwise disclose the coverage limit. An empty result
under restricted access does not establish that the information does not exist.

## Expand only to resolve gaps

- Too much noise: narrow terms or scope using project vocabulary.
- Missing evidence: try synonyms, broaden scope, or follow source links.
- Conflicting claims: fetch the underlying decisions and look for explicit
  supersession, effective dates, and accountable owners.
- Independent subquestions: batch or parallelize searches when supported and
  useful; do not repeat equivalent queries.
- Exhaustive inventories or aggregate metrics: follow available pagination and
  verify completeness. A sample cannot establish a workspace-wide count.

Prioritize authoritative and relevant sources. A recent edit can concern formatting,
so do not treat it as proof of a newer decision. For comprehensive work, cover all
requested dimensions and relevant contradictory evidence. Stop when the question
is supported and remaining uncertainty can be stated clearly.

## Connected sources

Search may include connected Slack, Drive, GitHub, Jira, or other sources only
when the connection supports them. Inspect the returned source type and use an
appropriate exposed tool to read it. Do not pass a non-Notion result to Notion
fetch by assumption. If full text cannot be read, distinguish the available
excerpt from a verified source and state the limitation. Cite original URLs.
