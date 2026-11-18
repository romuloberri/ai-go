# AI workspace

Everything Claude writes for you lives here, one folder per purpose.

| Folder | What it holds |
| --- | --- |
| `plans/<Ticket-ID>/` | One folder per ticket: `ticket-plan.md`, PR drafts, any other file for that ticket. |
| `memory/` | Lessons that carry across tickets. See `memory/README.md`. |
| `communication/` | Dated feedback notes, created on first use. |
| `skills/` | The skills. `~/.claude/skills` is a symlink to this folder. |
| `CLAUDE.md` | The rules Claude follows. `~/.claude/CLAUDE.md` is a symlink to this file. |

Both are versioned in this repo, so edit them here. `plans/` is git-ignored.

## Start of a ticket

1. Name the branch `<type>/<short_description>_<TICKET>`, e.g. `chore/count_skipped_measurements_EDG-1690`. The ticket must match the folder in `plans/`.
2. Say "plan ticket EDG-1690". Claude writes `plans/EDG-1690/ticket-plan.md`, with a `## Decisions` section for choices it made from research. Read it, change it, approve it.
3. Say "implement ticket EDG-1690". Without an approved plan, Claude plans first.

## Work on a step

Point at a step of a plan: "implement step 2 of the plan" or select the heading in your editor and ask. Asking to execute a plan or step is the approval. Claude then:

1. Checks the branch and stops if the name or ticket is wrong.
2. Implements only that step, then builds and runs checks.
3. Writes `PR-<step-slug>.md` next to the plan.
4. Reports what changed, the check results and one coaching note.

## Skills

| Say | Skill |
| --- | --- |
| "implement step N", "implement ticket X", "review this diff" | `dev-coach` |
| "plan ticket X", "scope this ticket" | `plan-ticket-coach` |
| "draft the PR description" | `pr-template-coach` |
| "draft a ticket for ...", "split this ticket" | `ticket-writer` |
| "what did I learn from this", "weekly review" | `growth-coach` |
| "improve this message", "review my status update" | `communication-coach` |

Name the skill once if Claude picks the wrong one: "use dev-coach".

## Memory

Claude reads these on its own: `dev-coach` reads `recurring-mistakes.md` and `review-checklist.md`, and `plan-ticket-coach` reads `reusable-heuristics.md`.

After real work Claude offers one lesson. Accept it to save it to the narrowest file. You can also ask: "add this as a heuristic" or "add this to recurring mistakes". Prune what no longer matches how you work.

## Things to know

- Claude never posts, pushes, opens a PR or submits a ticket without you asking.
- Skills change on disk but only load in a new session. Restart after editing one.
- `portable-coaching-kit/` and its `.zip` are the original from your colleague. Delete them once you no longer need them.
