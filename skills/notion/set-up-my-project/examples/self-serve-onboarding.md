# Set up a product team's onboarding project

This worked example uses fictional people, dates, and product information.
Adapt the structure and writing to the actual project rather than copying the
sample records into a user's work.

## Starting brief

> Set up Self-serve onboarding in our existing Atlas Projects database. Use its
> shared Tasks, Docs, and Meetings collections. The goal is to help a new team
> create its first shared project without a sales call. We are building toward a
> November 20, 2026 release, with a prototype review on November 6.
>
> Priya leads product, Noor leads design, and Theo leads engineering. Noor is
> testing the first-run prototype, due November 2. Theo is blocked on whether a
> newly created account can invite teammates; resolve that by November 3. Theo
> is also building the setup flow, due November 6. Priya has finished defining
> the activation event. Accessibility review has no owner or date yet.
>
> The product brief is accepted. The first-run design is in review. We agreed to
> show the invitation step after the first project is created, but we have not
> agreed who may send invitations. Billing and enterprise provisioning are out
> of scope. Draft useful completion criteria from this context.
>
> We hold a 30-minute weekly project review on Mondays. Prepare the November 2
> agenda and a reusable weekly-review template. Attendees and the invitation
> decision maker are not confirmed. Show me the project before asking questions.

Names remain text in this fictional example. In real use, set people properties
only after identifying the corresponding accounts. Leave unconfirmed attendance,
review ownership, and task dates unset.

## Connected pages and records

Reuse Atlas Projects and its shared collections. Self-serve onboarding is a
Projects record whose body is the project home. The sidebar retains the existing
Projects, Tasks, Docs, and Meetings destinations; individual task pages do not
become separate top-level destinations.

| Collection | Populated records                                                              | Connection                                                                                   |
| ---------- | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| Projects   | 🚀 Self-serve onboarding                                                       | Home for this project                                                                        |
| Tasks      | Five tasks listed below                                                        | Each relates to Self-serve onboarding; implementation tasks also link to their relevant docs |
| Docs       | 📄 Product brief; 🎨 First-run design; ⚖️ Decision: invite after first project | Each relates to the project; document type and review state stay visible                     |
| Meetings   | 🗓️ Project review · November 2                                                 | Relates to the project and links to its pre-reads                                            |

Create a native **Weekly project review** template in Meetings. Keep that template
separate from the November 2 prepared agenda and from held meeting notes. The
weekly rhythm belongs in the project context; no calendar invitation or scheduled
recurrence is created by this setup.

Every home view filters by the Self-serve onboarding project relation. A task
belonging to another Atlas project remains in the shared Tasks collection but
does not appear in this project's task views.

## Project home

Use a full-width page with a blue rocket icon and the default readable font.
Pin **Status: Building**, **Lead: Priya**, and **Target date: November 20, 2026**
near the title. Keep secondary metadata in details. Use a quiet blue accent for
the next milestone and red only for the actual blocked task.

The first screen follows this order:

1. **Self-serve onboarding**, its pinned properties, and one outcome sentence:
   “Help a new team create its first shared project without a sales call.”
2. A short 65/35 row: milestone on the left, collaborators on the right.
3. Native **Tasks**, **Docs & decisions**, **Meetings**, and **Overview** tabs.
   Tasks opens first, with actionable rows visible beneath the project context.

The milestone row contains:

| Next milestone — blue accent                                                                                       | Team                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **Prototype review · November 6** — Resolve who can invite teammates before reviewing the complete first-run flow. | **Noor · Design:** first-run flow and prototype testing. **Theo · Engineering:** invitation permissions and implementation. |

Priya's project lead role is already visible in the header. Keep the full scope
in Overview: account setup, first project, and invitations are included; billing
and enterprise provisioning are excluded. Do not repeat that scope above Tasks.

### Tasks tab

Use a compact table showing Task, Status, Owner, and Due date. Put the blocked
invitation decision first, followed by other open tasks by due date; keep the
undated accessibility review visible. The five records are:

| Task                              | Status  | Owner      | Due date         |
| --------------------------------- | ------- | ---------- | ---------------- |
| 🚧 Resolve invitation permissions | Blocked | Theo       | November 3, 2026 |
| 🧪 Test first-run prototype       | Doing   | Noor       | November 2, 2026 |
| 🛠️ Build setup flow               | Doing   | Theo       | November 6, 2026 |
| ♿ Review accessibility           | To do   | Unassigned | No date          |
| ✅ Define activation event        | Done    | Priya      | No date          |

Store unassigned owners and unknown dates as empty properties, not literal
“Unassigned” or “No date” values. The table above makes those unknowns explicit.
**Open tasks** excludes Done and shows four records. **Completed** shows the
activation-event task. Neither view deletes or duplicates records.

### Docs & decisions tab

Use a compact list with title, document type, and review state. The product brief
is **Brief / Accepted**; the first-run design is **Design / In review**; the
invitation-sequence decision is **Decision / Accepted**. An accepted sequence
must not imply that invitation permissions have also been approved.

### Meetings tab

Show **Project review · November 2**, with date November 2, 2026 and status
**Prepared**. Open it to the agenda below. Offer **Weekly project review** through
the native New menu, so preparing the next meeting starts with the same useful
structure without copying old decisions or outcomes.

## Task detail: Resolve invitation permissions

Use a red barrier icon. Keep Status, Owner, Due date, and Project visible in the
record layout. The body contains useful work rather than repeating those fields:

> **Decision needed**
>
> Can the creator of a new account invite teammates immediately after creating
> the first project, or does someone need to approve that action?
>
> **Why this blocks the flow**
>
> The accepted sequence puts invitations after project creation. Engineering
> still needs the permission rule to implement that step; design needs it to
> show the correct action or explanation.
>
> **Proposed completion criteria**
>
> - Record the agreed invitation rule and who approved it.
> - Describe the behavior for an account that can invite and one that cannot.
> - Update the first-run design to match the agreed behavior.
> - Link the rule from the setup-flow task before implementing invitations.
>
> **Related work**
>
> First-run design · Decision: invite after first project · Build setup flow

Turn Related work into mentions of the actual created records and native doc
relations. Keep a visible project relation back to Self-serve onboarding. The
criteria are proposed elaboration of the brief, not an already accepted policy.

## Document detail: Decision: invite after first project

> **Decision**
>
> Show the invitation step after the creator has made the first project.
>
> **What this establishes**
>
> The first-run sequence is account setup, project creation, then invitations.
> The prototype and setup flow should use this order.
>
> **Still open**
>
> Who may send invitations has not been decided. Resolve invitation permissions
> tracks that question. This record does not approve an invitation policy.
>
> **Related work**
>
> First-run design · Resolve invitation permissions · Build setup flow

Use the native Decision type and Accepted state from the brief. Leave decision
maker and decision date unset. Do not invent approval history or a rationale the
team never provided.

## Prepared meeting: Project review · November 2

Keep the date and Prepared status visible. Leave Participants unset. The
following agenda is proposed; its questions come from the current project:

| Time       | Topic                            | Preparation                                                    |
| ---------- | -------------------------------- | -------------------------------------------------------------- |
| 5 minutes  | Review current work              | Open tasks; Noor's prototype work and Theo's setup-flow work   |
| 15 minutes | Resolve invitation permissions   | First-run design and the accepted invitation-sequence decision |
| 5 minutes  | Confirm readiness for November 6 | Identify what must change in the prototype before the review   |
| 5 minutes  | Agree follow-ups                 | Update existing tasks with agreed owners and dates             |

Under **Notes**, provide “What changed?” and “What remains unresolved?” capture
prompts. Leave **Decisions** empty until the discussion happens. Link **Actions**
to the project's Tasks view; record agreed follow-ups there instead of maintaining
a second task list in the meeting body.

The reusable Weekly project review template has the same four agenda sections,
pre-read area, and project relation, with date, participants, notes, and outcomes
empty. Set the project relation for each new meeting and link its actions and
resulting decisions back to that meeting.

## Delivery and later tuning

Share the actual project home link before asking anything else. A concise handoff
could say:

> Self-serve onboarding is ready in Atlas Projects, with connected tasks, docs,
> and a prepared November 2 review. Start with Resolve invitation permissions;
> it identifies the decision blocking the first-run flow.
>
> Who should approve the invitation rule, and who should join the weekly review?

Do not repeat questions about placement, known leads, or the Monday rhythm.
When the user answers, update this same home and agenda. If another brief leaves
placement open, deliver a private initial home first, then ask which Projects
database to use or whether the user wants a new one.
