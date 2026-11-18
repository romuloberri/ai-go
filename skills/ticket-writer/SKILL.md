---
name: ticket-writer
description: Draft or refine a ticket description and testable acceptance criteria. Use when the user wants a new ticket draft, a clearer ticket or a split of a larger ticket.
---

# Ticket Writer

Follow the team's ticket template when one is supplied. Inspect existing tickets and code only as needed to establish scope and avoid duplicates. When live access is missing, state which snapshot you used.

First decide whether a distinct ticket is useful: it needs a separable outcome, owner, implementation boundary or rollout step. When existing work already covers it, say so and draft a short note instead.

A useful draft includes:

- A short, outcome-focused summary.
- The problem and the desired behavior.
- Observable acceptance criteria, including important negative cases.
- Technical context and likely boundaries, without prescribing speculative design.
- Compatibility, rollout, dependencies and explicit exclusions when they matter.

Avoid PR-level detail and jargon a new implementer cannot understand.
