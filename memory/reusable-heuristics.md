# Reusable heuristics

These rules come from real engineering cases. Select the few that fit the current task; do not turn every small change into a full checklist. Repository instructions and CLAUDE.md files still define project policy. Keep task links and detailed evidence in the ticket folder.

## Add a rule

- Name:
- Use when:
- Do:
- Failure it prevents:

Add a new rule only when the same decision is likely to recur. If it is a one-time incident, record it in the growth log instead.

## Core execution rules

- Prefer the smallest safe change that solves the root problem.
- On documentation. Update the fewest relevant files and sections with the minimum accurate change; avoid unrelated rewrites.
- Name boundaries explicitly before adding abstractions.
- Choose the test that buys the most confidence first.
- Treat rollout and rollback as part of implementation, not post-work.
- Plan observability when production evidence can confirm or disprove the change. Define the decision the signal supports; do not add logs or metrics merely because they may be useful someday.
- Keep telemetry contracts portable across vendors: use structured logs, stable snake_case fields, domain-oriented metric names, bounded-cardinality dimensions, and existing abstractions. Isolate vendor query syntax in dashboard and alert instructions rather than application code.
- If behavior changes, check backward compatibility before cleanup or refactor work.
- Keep PRs reviewable: warn around 800 changed lines, and above 1000 changed lines propose a split by behavior or ownership unless there is a clear reason to keep one PR.

The PR size numbers are prompts for review, not an automatic split. Exclude generated noise from the judgment and explain when an atomic change must stay together.

For a production signal or monitoring plan, read [observability-planning.md](observability-planning.md) when it is relevant.

## Frame and design

- **Ticket anchor before context**
  - Use when: Earlier PRs, logs, or dashboards accompany a new request.
  - Do: State the current objective and acceptance criteria; label other material as examples or constraints.
  - Prevents: Implementing the earlier example instead of the requested behavior.

- **Keep command entrypoints orchestration-only**
  - Use when: A command handles parsing, reporting, dry-run logic, batching, and writes.
  - Do: Keep the entrypoint's flow clear and move cohesive work into named methods or services when complexity warrants it.
  - Prevents: A large control-flow method that is hard to test and review.

- **APIs belong to established API boundaries**
  - Use when: Adding an endpoint for a browser, app, partner, or integration.
  - Do: Inspect the nearest existing endpoint and its authentication, error, rate-limit, and response contracts before choosing a route.
  - Prevents: A convenient endpoint that bypasses the consumer's established contract.

- **Stable identity stores need a lifecycle contract**
  - Use when: A token, preference, or lookup key outlives one mutable record.
  - Do: Define ownership, retention, revocation, and what happens when linked records change or disappear; test the key transition.
  - Prevents: Unexplained duplicate sources of truth or a cleanup that invalidates newer state.

- **Extract repeated literals when they encode a contract**
  - Use when: The same format, status, token, or lock name appears in parsing and output paths.
  - Do: Centralize the semantic value, or use a formatter for a repeated construction rule. Leave unrelated prose alone.
  - Prevents: Validation and output drifting after a partial change.

## Data, privacy, and concurrency

- **Privacy changes need a four-layer check**
  - Use when: Changing consent, anonymization, deletion, unsubscribe, or another user-data lifecycle.
  - Do: Trace the trigger, selection query, mutation, and read or send paths after mutation.
  - Prevents: A correct mutation that never runs or a later path that still uses the data.

- **Revalidate before consequential writes**
  - Use when: A repair or batch command writes rows selected earlier.
  - Do: Recheck eligibility at the write boundary, using an appropriate transaction, lock, or conditional update.
  - Prevents: Overwriting a newer user or system decision with a stale snapshot.

- **Session-scoped coordination must follow the write path**
  - Use when: Advisory locks, temporary tables, or session variables coordinate writes across read/write connections.
  - Do: Acquire and release session state on the same physical connection that coordinates the writes; verify routing in a focused test.
  - Prevents: Separate readers each obtaining a lock while both write through one primary.

## Validation and diagnosis

- **Run structural gates at the capability boundary**
  - Use when: A command, service, parser, or importer grows new responsibilities.
  - Do: Run the repository's complexity and static checks after a coherent slice, while boundaries are still easy to change.
  - Prevents: CI forcing a late refactor after tests and docs were built around an oversized class.

- **Trace coverage from test runner to quality gate**
  - Use when: Tests run and a coverage artifact exists, but the analyzer reports low or zero coverage.
  - Do: Check report creation, artifact transfer, path rewriting, and analyzer configuration before adding tests.
  - Prevents: Writing more tests while the gate ignores their coverage.

- **Capture consumable test output once**
  - Use when: Several assertions inspect command, process, stream, or response output.
  - Do: Capture output once and reuse that value, especially for absence assertions.
  - Prevents: A later assertion passing against an emptied buffer.

## Review and delivery

- **Push-ready includes PR-description-ready**
  - Use when: A validated branch is described as ready for reviewers.
  - Do: Prepare a short reviewer narrative with behavior, tests, compatibility, rollout, and remaining risk.
  - Prevents: A technically ready branch with no usable review context.

- **PR testing should guide reviewer verification**
  - Use when: Drafting a PR description.
  - Do: Lead with a short path through the real behavior; summarize routine commands and mark unrun checks clearly.
  - Prevents: A long CI transcript that hides how to verify the change.

- **Reproduce PR checks against the current base**
  - Use when: The target branch has moved or CI tests a synthetic merge.
  - Do: Refresh the comparison base and verify the effective changed files and dependent docs before calling the PR ready.
  - Prevents: A local pass against an outdated base or a doc edit that disappears in the effective diff.

- **Logging ownership transfers must preserve failure identity**
  - Use when: An outer job, transaction, or controller takes over lifecycle logging from an inner component.
  - Do: Inspect the outer catch and rollback behavior; retain the original failure identity safely in the final log.
  - Prevents: A generic wrapper hiding the cause, or a rethrow bypassing the owner's catch path.
