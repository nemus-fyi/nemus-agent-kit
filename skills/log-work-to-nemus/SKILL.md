---
name: log-work-to-nemus
description: "Record what was done in a coding or writing session on the matching Nemus task: update status, add a short comment, and attach the PR, branch or doc link. Use when the user says \"update Nemus\", \"log this\", \"mark it done\", or finishes work that maps to a Nemus task."
---

# Log work to Nemus

## Steps

1. **Find the task.** If the user gave a task key or ID, use it. Otherwise call `search_tasks` with words from the branch name, PR title or commit messages, and confirm the match with the user if there is more than one candidate.
2. **Update status.** Set `IN_PROGRESS` when work started, `DONE` only when the user says it is finished or the PR is merged. Use `update_task`.
3. **Add one comment** with `add_comment`: what changed and anything left open, in two or three sentences. No raw logs, diffs or secrets.
4. **Attach links** with `add_task_reference`: the PR, branch, design or doc. Check `list_task_references` first so you don't add duplicates.
5. **Capture follow-ups.** If the session surfaced new work, propose it as new tasks linked to this one (`RELATED_TO`, or `BLOCKS` if it gates something) and create them only after the user agrees.
