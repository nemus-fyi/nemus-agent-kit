---
name: project-catch-up
description: Give a short catch-up on a Nemus project or on the user's own assignments: what moved, what is stuck, what needs attention. Use when the user asks for a status update, standup, weekly summary, "where are we", or "what's on my plate".
---

# Project catch-up

## Steps

1. **Scope it.** For "my plate" questions call `list_my_assignments` (optionally per project). For a project, call `summarize_project`; it returns counts and structure you can build on. Check `list_notifications` with `unread_only` for anything addressed to the user.
2. **Fill in only what the summary lacks.** Use `list_tasks` filtered by status for detail, and `get_task_context` for the two or three tasks that matter most. Avoid paging through every task.
3. **Write a short update**, at most ~10 lines:
   - **Moved:** tasks that reached `DONE` or `IN_PROGRESS`
   - **Stuck:** `BLOCKED` tasks and what blocks them
   - **Needs you:** unread notifications, assignments that are due soon or overdue
   - **Next:** the one or two tasks that would unblock the most
4. **Keep it in chat.** Only pin a view to the Drawboard (`pin_view`) or save a Dynamic View (`create_dynamic_view`) if the user asks to keep it.
