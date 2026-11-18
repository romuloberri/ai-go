# Recurring mistakes

These patterns are anonymized from real work. Use them to notice a trigger early, then follow the linked rule in reusable-heuristics.md. Keep task links and sensitive details out of shared copies.

## Add a pattern

- Pattern:
- Typical trigger:
- What was missed:
- Earlier signal:
- Better response:
- Review question:
- Evidence or task link:

Record a pattern after a concrete case. Promote it to a reusable heuristic only when the better response applies beyond that case.

## Early warning signs

Five recurring risks to watch for:

- Expanding scope before proving the narrow fix.
- Writing happy-path tests without the main failure path.
- Accepting local correctness without deployment or observability thinking.
- Adding abstractions before the second real use case exists.
- Underestimating compatibility risk when changing contracts or persistence.

## Case-derived patterns

- **An analyzer warning is fixed from a guessed cause**
  - Trigger: Runtime tests pass, but an IDE or static tool still reports an error.
  - Missed: The exact message, highlighted expression, and reporting tool were not captured.
  - Ask: “Can the proposed change explain this specific diagnostic, and did I rerun the same tool?”
  - Better response: Capture the exact diagnostic, verify the symbol and local pattern, then rerun that tool.

- **Identity data is normalized at a new local boundary**
  - Trigger: A feature introduces a table or service keyed by email or another natural identifier.
  - Missed: Trimming or case conversion can change which records represent the same identity.
  - Ask: “Which component owns canonicalization, and does this code reuse that contract?”
  - Related heuristic: Stable identity stores need a lifecycle contract.

- **Ticket sequencing leaks into durable feature documentation**
  - Trigger: A feature spans several implementation tickets.
  - Missed: Future maintainers need the current contract, not the old delivery sequence.
  - Ask: “Will this paragraph still help after the ticket plan is forgotten?”
  - Better response: Document implemented invariants and current limits; keep ticket sequencing in the work item or PR.

- **Final PR checks use an outdated base**
  - Trigger: The target branch advances after an earlier local validation.
  - Missed: CI may test an effective merge where a date-only doc edit disappears or additional dependent docs become stale.
  - Ask: “Is my base current, and does this change still appear in the effective diff?”
  - Related heuristic: Reproduce PR checks against the current base.

## Additional case-derived patterns

More patterns, useful when the trigger appears:

- **Coverage looks missing despite passing tests:** Trace report creation, transfer, and analyzer paths before adding more tests. Related heuristic: Trace coverage from test runner to quality gate.
- **A logging refactor hides the original failure:** Inspect the outer owner's catch and rollback behavior before wrapping or rethrowing. Related heuristic: Logging ownership transfers must preserve failure identity.
- **Later assertions read an emptied output buffer:** Capture command or process output once and reuse it. Related heuristic: Capture consumable test output once.
