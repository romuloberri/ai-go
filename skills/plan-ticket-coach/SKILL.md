---
name: plan-ticket-coach
description: Write an implementation plan (ticket-plan.md) for a ticket and get it approved. Use when the user asks to plan, analyze or scope a ticket, and before implementing a ticket that has no approved plan. Does not edit code.
---

# Plan Ticket Coach

Memory notes live in ~/code/ai/memory/. Read reusable-heuristics.md before planning, and observability-planning.md when production evidence can change the rollout. Treat them as prompts, not universal rules.

Read the ticket, its acceptance criteria and important comments. When live access is missing, state which snapshot the plan uses and what may be missing. Do not infer requirements from a branch name or a linked example.

## Plan the work

- Objective, success condition, scope, exclusions and assumptions.
- The existing code boundary and contracts, before choosing an approach.
- The simplest viable solution, alternatives only when they matter, and the risk that would justify more complexity.
- Reviewable behavior slices.
- Failure paths, compatibility, external effects, rollout, rollback and the highest-value checks, in proportion to risk.
- How a reviewer can verify the real behavior.

A small isolated task needs a short plan. Data migration, privacy, payment or production-impacting work needs stronger failure and rollback analysis.

## Decisions

When research leads you to choose between approaches, record it in a `## Decisions` section. Each entry has:

- Question: what had to be decided.
- Evidence: what you inspected.
- Options: the realistic alternatives.
- Choice: what the plan does, and the tradeoff it accepts.
- Revisit when: the condition that would change the choice.

Mark each decision open until the user approves the plan, then confirmed. Put questions that evidence cannot answer in an `Open questions` list.

## Save and approve

Write `ticket-plan.md` in `~/code/ai/plans/<Ticket-ID>/`, keeping existing notes. Record the current branch and the intended branch, named `<type>/<short_description>_<TICKET>`.

Show the plan and wait for explicit approval. When the approach changes materially, revise it and ask again. After approval, use dev-coach to implement.
