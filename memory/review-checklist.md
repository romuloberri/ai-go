# Review checklist

Use this as a menu of questions for a plan, diff, or PR. Select the questions that fit the change; do not paste the whole checklist into every review. The questions come from real cases.

## Problem and design

- What is the real problem being solved? Did the current request, rather than a linked example, define it?
- Is the solution smaller than the problem, or has scope grown before the narrow fix was proved?
- What breaks if the core assumption is wrong?
- Did the change make ownership and behavior clearer at the boundary it touched?
- Does the change fix the root cause rather than patching only the visible output?
- Are documentation edits required by the task, changed contract, or repository policy? If so, are they limited to the relevant files and smallest accurate sections?
- If the design adds complexity, which requirement or failure justifies that tradeoff?
- Do names make ownership and behavior clear, or hide them?
- Does a new abstraction or repeated literal encode a real contract? Use a constant for a semantic value and a formatter for a repeated construction rule; do not extract unrelated prose.
- Does a new API use the established authentication, error, rate-limit, and response contract for its consumers?
- Does a stable identity or token store have an owner, retention rule, and revocation behavior?

## Behavior and safety

- What happens for missing, invalid, repeated, delayed, or stale input?
- If rows were selected before a write, can their eligibility change before the write?
- For user-data changes, did we trace trigger, selection, mutation, and later read or send paths?
- Is there a compatibility, migration, or rollout risk when behavior or persistence changes?
- If logging ownership moved, will the final error retain the original cause without bypassing rollback?

## Evidence and tests

- What is the highest-value negative-path test or other check that could disprove the fix?
- Do tests assert observable behavior rather than private implementation details?
- Does an output accessor consume its buffer before later assertions inspect it?
- Were structural and static checks run while the implementation boundary could still change?
- If a tool reported a warning, did we capture and rerun that exact diagnostic?
- If coverage looks wrong, did we trace the report from test runner to quality gate before adding tests?
- Is confidence based on checks performed, or only on reading the code? State what remains unverified.

## Rollout and review

- How will we know the change worked after deployment?
- Would an observability plan materially help? If so, does it name the decision, signals, queries or panels, thresholds, owner, and response? Read observability-planning.md only for that kind of change.
- Are application logs and metrics vendor-neutral, with stable structured fields and domain names? Keep vendor queries and alert setup outside application code.
- Can a reviewer understand and verify the behavior from the PR description?
- Is the PR still reviewable? Around 800 changed lines, consider a split; above 1000, propose a split by behavior or explain why the change must stay atomic.
- Is the comparison against the current target branch and effective PR diff?
- Do durable docs describe the implemented contract rather than ticket sequencing?
- Does each actionable review comment name the affected file or location so it can be mapped to the code?
