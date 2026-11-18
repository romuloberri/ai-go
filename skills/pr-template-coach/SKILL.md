---
name: pr-template-coach
description: Draft or improve a pull request description from the actual ticket, diff and checks. Use when the user needs reviewer-facing PR text or a PR readiness review.
---

# PR Template Coach

Use the repository's PR template when one exists, with its headings and checklist. Otherwise use the default format below.

Base the text on the ticket, the current diff and the checks that were run. Mark an item complete only with evidence, and label unrun checks and proposed reviewer steps as pending. Keep screenshots and operational details proportional to the change.

## Default format

Keep it under 15 lines:

```markdown
# <Short title>

<One paragraph: what was wrong or missing and why the change matters.>

<One paragraph: what changed, and whether behavior changes.>

<One line: how to verify after release, when there is something to check.>

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

Cover compatibility, migration, feature flags, rollout and rollback only when they apply.

## Saving

Write the draft to `~/code/ai/plans/<Ticket-ID>/PR-<step-slug>.md`, where the slug is the kebab-case name of the step or change. Edit an existing draft deliberately, or choose a distinct follow-up filename.
