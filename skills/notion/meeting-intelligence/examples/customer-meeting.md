# Example: Customer Meeting Prep

**User Request**: "Prep for our sales meeting with Acme Corp on Thursday. Save an internal pre-read in our sales team area and a customer agenda in the shared meeting area."

This example assumes the facts below are in the supplied CRM and product sources.
Verify current external claims with sources; suggested discussion points are analysis,
not established facts about this customer.

## Workflow

### 1. Search Customer Info

```
Notion:notion-search
query: "Acme Corp"
```

Found:

- CRM notes from initial call
- Product demo feedback
- Pricing proposal
- Competitor analysis

### 2. Fetch Details

```
Notion:notion-fetch (4 pages)
```

**Key context**:

- **Company**: 500-person fintech startup, Series B
- **Pain Points**: Manual workflows, data silos, scaling issues
- **Decision Makers**: CTO (technical), VP Product (user needs), CFO (budget)
- **Timeline**: Need solution by Q1
- **Budget**: $50-75K/year range
- **Competition**: Evaluating us vs. Competitor A and Competitor B

### 3. Resolve the two destinations

The example assumes established workspace configuration or user confirmation that
Sales Team is internal-only and Acme Shared Meetings is approved for this customer.
Do not infer access from page titles or an “Internal” label. If the audience is
unknown, resolve it before saving sensitive content.

Search for the named locations, then fetch the matching pages to confirm identity
and project context. Reuse their returned IDs in the create calls below.

```
Notion:notion-search
query: "Sales Team"

Notion:notion-search
query: "Acme Shared Meetings"

Notion:notion-fetch
id: "sales-team-parent-id"

Notion:notion-fetch
id: "acme-shared-meetings-parent-id"
```

Resolved destinations (illustrative IDs):

| Material          | Parent page                      | Established audience          |
| ----------------- | -------------------------------- | ----------------------------- |
| Internal pre-read | `sales-team-parent-id`           | Internal sales team           |
| Customer agenda   | `acme-shared-meetings-parent-id` | Sales team and Acme attendees |

Use current exposed tool schemas and reuse any required tool-access check for
these calls. Fetching page content alone does not prove its sharing permissions.

### 4. Add research context

assistant research added:

- Fintech industry compliance requirements
- Common integration needs for financial products
- Typical procurement processes for Series B companies

### 5. Create internal pre-read

```
Notion:notion-create-pages
parent: { page_id: "sales-team-parent-id" }
pages: [{
  properties: {
    title: "Acme Corp Meeting - Pre-Read (Internal)"
  },
  content: "# Acme Corp Meeting - Pre-Read (Internal)

## Company Overview
**Company**: Acme Corp (500-person fintech, Series B)
**Decision Makers**: CTO, VP Product, CFO
Source: <mention-page url='...'>CRM Notes</mention-page>

## Their Pain Points → Our Solutions
- Manual workflows → Workflow automation
- Data silos → API integrations
- Scaling issues → Enterprise features

## Competitive Position
**Our advantages over Competitor A/B**:
- Better integration ecosystem (Stripe, Plaid)
- Stronger compliance features
- Faster implementation (4 weeks vs 12 weeks)

## Pricing Strategy
Recommend: $60K/year (mid-range of their budget)

## Potential Objections & Responses
..."
}]
```

### 6. Create meeting agenda

```
Notion:notion-create-pages
parent: { page_id: "acme-shared-meetings-parent-id" }
pages: [{
  properties: {
    title: "Acme Corp - Product Demo & Q&A"
  },
  content: "# Acme Corp - Product Demo & Q&A

## Meeting Details
**Date**: Thursday, Oct 17, 2025 @ 2pm PST
**Attendees**: CTO, VP Product, CFO (Acme) | Sales Lead, Solutions Engineer (Us)
**Duration**: 60 minutes

## Objective
Demonstrate how our platform solves Acme's workflow automation and integration challenges.

## Agenda

**1. Introductions** (5 min)

**2. Understand Current Workflow** (10 min)
- Current pain points
- Integration requirements
- Success criteria

**3. Product Demo** (25 min)
- Workflow automation capabilities
- API integrations (Stripe, Plaid)
- Security & compliance features

**4. Pricing & Implementation** (10 min)

**5. Next Steps** (10 min)
"
}]
```

### 7. Verify placement and link resources

Check each create result against its intended parent. If placement is not shown,
fetch the created page and inspect its parent/path before reporting success.
Do not change sharing settings as part of preparation.

Linked the internal pre-read to CRM notes and internal pricing strategy. Linked the
customer agenda only to customer-approved pricing and integration documentation.
Kept internal page links out of the customer agenda and used separate destinations
with the appropriate audiences; titles alone do not establish access permissions.

## Outputs

**Internal Pre-Read**: Full context for sales team
**Customer Agenda**: Professional meeting structure
**Both in Notion** with links to supporting materials

## Key Success Factors

- Understood customer's specific pain points
- Researched industry context (fintech compliance)
- Mapped features to their needs
- Prepared competitive differentiators
- Structured demo around their use cases
- Pre-planned objection responses
- Clear next steps in agenda
