---
name: plan-with-nemus
description: Turn a brief, spec, meeting notes or a rough idea into a connected task graph in Nemus. Use when the user asks to plan, break down, scope or "put into Nemus" a piece of work, or wants tasks with dependencies rather than a flat list.
---

# Plan with Nemus

Nemus stores work as a graph: tasks are nodes, relationships are edges. A good plan here is a small graph whose edges say *why* the order matters, not a long checklist.

## Steps

1. **Pick the project.** Call `list_projects`. If the user did not name one and more than one fits, ask. Do not create a project unless they ask.
2. **Check what already exists.** Call `search_tasks` with the key nouns of the brief so you extend existing work instead of duplicating it.
3. **Draft the graph before writing it.** Aim for 5–15 tasks. For each task decide:
   - a short imperative title ("Draft pricing page copy", not "Pricing")
   - `priority` only when it differs from MEDIUM
   - `start_date` / `due_date` only when the user gave dates
   - edges: `BLOCKS` when one task cannot start until another is done, `EXPANDS` (via `parent_id`) for a sub-task of a larger task, `RELATED_TO` for useful context, `CAUSES` when one task creates the need for another
4. **Show the draft** to the user as a compact outline with the edges, and ask for a yes before writing more than ~5 tasks.
5. **Write it.** Create parents first, then children with `parent_id`. Use the `relationships` argument on `create_task` to attach edges in the same call instead of separate `create_relationship` calls.
6. **Report back** with the task keys you created and the critical path (the longest chain of `BLOCKS` edges).

## Style

- Descriptions are optional and short: one or two sentences on the outcome, or a link. No restating the title.
- Do not invent owners, estimates or dates.
- Prefer fewer, meaningful edges over connecting everything.
