# Turn studio notes into a team handbook

This fictional example shows a handbook for employees and a connected request
desk for operations. Adapt the procedures, visual identity, and amount of
structure to the team's actual work.

## Starting brief

> Create a private handbook for Cedar Studio, a twelve-person design team.
> People should find instructions without knowing who owns the process. Give
> operations a separate place to follow requests.
>
> We have three sets of notes, all working drafts rather than approved policy:
>
> - **Start at Cedar:** before a new teammate starts, their project lead names a
>   buddy and lists the tools they need. Operations arranges access. On day one,
>   the buddy walks through the client brief and checks that access works. Nora
>   maintains this guidance.
> - **Buy a tool:** describe the job the tool will do, expected cost, billing
>   owner, and renewal date. Eli coordinates the review before purchase. Keep
>   the review decision and receipt with the request. We have not agreed who
>   approves purchases or any spending threshold. Eli maintains this guidance.
> - **Hand off client files:** collect the agreed final files, write what is
>   included and how the recipient will use them, confirm the recipient with
>   the project lead, then get an acknowledgment. Nora maintains this guidance;
>   the team still needs to decide who follows up if no acknowledgment arrives.
>
> Current requests: Figma access for a new designer is in progress, coordinated
> by Nora, due November 4, 2026; the lead still needs to confirm the access level.
> Research repository renewal is waiting, coordinated by Eli, due November 6;
> the cost is $240 annually and the billing owner is known, but the reviewer has
> not been chosen. Client handoff for the Moss identity project is done, with
> Nora coordinating; the recipient acknowledged the files on October 28.
>
> Use a calm, welcoming style with muted green, warm yellow, and soft blue.
> Names are fictional. Do not assign real people or invent approvals or dates.

## Connected pages and collections

Use **🌿 Cedar · Team handbook** as the private home. Keep two child databases,
**📚 Procedures** and **📥 Requests**, visible beneath it in the sidebar. The home
contains linked views of these same collections, so opening a card or following
a request always reaches the original record.

Each request has a native **Procedure** relation. Show related requests on the
procedure page, with a return link to the handbook. For this example, retain Nora
and Eli as text in **Procedure owner** and **Coordinator**; they are not real
Notion people assignments.

### Procedure records

| Procedure                | When to use it                                   | Area        | Procedure owner | Review status |
| ------------------------ | ------------------------------------------------ | ----------- | --------------- | ------------- |
| 👋 Start at Cedar        | Prepare for a teammate's first day               | People      | Nora            | Working draft |
| 🛒 Buy a tool            | Review a new purchase or renewal before spending | Tools       | Eli             | Working draft |
| 📦 Hand off client files | Deliver agreed files and confirm receipt         | Client work | Nora            | Working draft |

Leave **Last reviewed** empty: importing notes does not establish a review date.
Keep the purchase approver and handoff follow-up owner as explicit open questions
in their procedures.

### Request records

| Request                          | Status      | Coordinator | Due date         | Procedure             |
| -------------------------------- | ----------- | ----------- | ---------------- | --------------------- |
| 🔑 Figma access for new designer | In progress | Nora        | November 4, 2026 | Start at Cedar        |
| 🔄 Research repository renewal   | Waiting     | Eli         | November 6, 2026 | Buy a tool            |
| 📦 Moss identity handoff         | Done        | Nora        | —                | Hand off client files |

The acknowledgment on October 28 belongs in the handoff's completion notes, not
in its due-date field. No due date was supplied for that request.

## The handbook on arrival

Set the home to full width with the default reading font and a green leaf icon.
Use a shallow original cover with simple leaf shapes in muted green and cream;
keep it short enough that the procedure cards remain on the first screen.

Under the title, use one sentence:

> Find the steps for joining the team, buying a tool, or handing off client work.

Show **Working guidance · Confirm open decisions before acting** in a compact
warm-yellow callout. It applies to these draft procedures and does not imply
that they are approved company policy.

Below it, arrange three equal columns with lightly tinted headings and direct
page mentions:

| Green section       | Yellow section   | Blue section             |
| ------------------- | ---------------- | ------------------------ |
| **Getting started** | **Buying tools** | **Client handoffs**      |
| 👋 Start at Cedar   | 🛒 Buy a tool    | 📦 Hand off client files |

Use a native tab group immediately below the routes:

- **Procedures** opens by default. Show three compact gallery cards with the
  procedure icon and title, **When to use it**, and **Review status**. Wrap the
  text. These are text cards; no decorative card images compete with the steps.
- **Owners & reviews** shows the same procedures as a table: Procedure, Area,
  Procedure owner, Review status, Last reviewed. Keep the empty review dates
  visible to the people maintaining the guide.
- **Requests** shows the two open requests with Status, Coordinator, and Due
  date. Sort dated work earliest first and retain undated work. A **Completed**
  view contains the Moss handoff; it remains connected to its procedure.

Hide repeated database titles above these views. Keep the full dates readable.
The first screen should let an employee choose a procedure immediately; the
operations queue is one tab away rather than occupying the employee's entrance.

## A complete procedure: Buy a tool

Give the page a yellow shopping-cart icon. Keep **Working draft**, **Eli**, and
**Tools** near the title as visible properties. The reading area contains:

### When to use this

Use this before buying or renewing a tool. Gather the information below so the
reviewer can understand the cost and the work it supports.

### Before you start

Have the tool name, the job it will do, expected cost, billing owner, and renewal
date. If a detail is unknown, leave it open and explain what must be confirmed.

### Steps

1. Open a request describing the purchase or renewal. Connect it to **Buy a tool**.
2. Add the expected cost, billing owner, renewal date, and why the tool is needed.
3. Ask Eli to coordinate the review. The team has not yet identified the approver;
   choosing that person is the next decision, not approval to spend.
4. Record the review decision with its source. Complete a purchase only after
   the required review has occurred.
5. Keep the receipt and renewal details with the request after purchase.

### Open decision

**Who approves purchases and renewals?** Eli coordinates review but is not named
as the approver. No spending threshold has been agreed.

### Completion check

The request contains the review decision, receipt, billing owner, and renewal
details. A submitted request or a coordinator's name alone does not mean a
purchase is approved.

At the bottom, show the related **Research repository renewal** request and a
page mention returning to **Cedar · Team handbook**. Keep the source label
**Purchase notes supplied in the starting brief** beside this draft guidance.

## A useful request: Research repository renewal

Use a blue renewal icon. Keep **Waiting**, **Eli**, and **November 6, 2026** near
the title, with the native relation to **Buy a tool**. The body reads:

> **Next action:** Eli to identify the reviewer before the renewal decision.

**Request:** Review renewal of the research repository at $240 annually.
The billing owner is known, but their identity was not supplied in these notes.
Confirm that name and the renewal date before recording them.

**Waiting on:** The team has not chosen who approves the renewal. No approval or
purchase has been recorded.

**Information to confirm:** The reason for retaining this tool, the billing
owner's name, the renewal date, and the assigned reviewer. The November 6 request
due date is not evidence of the subscription's renewal date.

**Decision and receipt:** Leave these empty until the review and purchase occur.
Return to **Buy a tool** for the steps and **Requests** for the queue.

## What makes the result usable

An employee can enter **Buying tools**, read the steps, and see the unresolved
approval question before spending. Eli can open **Requests**, find the waiting
renewal and its due date, and follow the procedure without searching another
collection. Nora can use **Owners & reviews** to see which guidance she maintains.
All three routes use the same underlying records; none requires copying a policy
or updating a second checklist.
