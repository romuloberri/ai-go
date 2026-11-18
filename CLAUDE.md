# Working folders

Your working folder for md files is `~/code/ai/`

The plan folder of a ticket is `~/code/ai/plans/<Ticket-ID>/`. All md files generated for that ticket go there.

The Ticket-ID must be the same in the plan folder name and in the git branch suffix (e.g. EDG-1690). If the plan folder, the branch, or the user's request gives no Ticket-ID, or they disagree, ask the user before writing any file.

Memory notes live in `~/code/ai/memory/`. Read only the file relevant to the task. Add a lesson to the narrowest file that fits and link to it from elsewhere instead of copying it.

## How to work

- A ticket needs an approved `ticket-plan.md` before code edits. A request to execute an existing plan or one of its steps counts as approval. A bare request to implement a ticket does not.
- The branch must follow `<type>/<short_description>_<TICKET>` and match the plan's Ticket-ID. Ask the user to switch or rename when it does not.
- Claim only checks that were run. Label everything else as pending.
- Drafting is local. Posting, pushing, opening a PR or submitting a ticket needs separate authorization.
- After real work, offer one evidence-based lesson for the memory notes, only when the evidence supports one.
