---
name: whats-blocking
description: Find what is blocking a task, a milestone or a whole Nemus project, and suggest the next unblocking move. Use when the user asks "what's blocking X", "why is this stuck", "what should I do next", or "what's on the critical path".
---

# What's blocking

## Steps

1. **Find the target.** If the user named a task, locate it with `search_tasks` and open it with `get_task_context` (it returns the task, its immediate graph neighbourhood, recent comments and references). If they named a project, call `list_tasks` with status `BLOCKED` and `IN_PROGRESS`, then `list_relationships` for the project.
2. **Walk `BLOCKS` edges upstream.** For each blocker that is not `DONE`, open it with `get_task_context` and keep walking until you reach tasks with no open blockers. Those are the real starting points. Stop after about 4 levels and say so if the chain goes deeper.
3. **Read the evidence.** Recent comments and references often say why something is stuck (waiting on a person, a decision, an external party). Quote the relevant line briefly.
4. **Answer in this shape:**
   - the blocking chain, root first (task key, title, status, owner if set)
   - the one task that, if finished, unblocks the most work
   - anything that looks stale (marked `BLOCKED` with no open blocker, or `IN_PROGRESS` with no recent activity)
5. **Change nothing by default.** Offer, don't apply: setting a status, adding a comment, or removing an edge that no longer holds. Only write after the user agrees.
