# Nemus

The `nemus` MCP server connects to the user's Nemus workspace, a graph-based task manager where tasks are nodes and relationships (BLOCKS, EXPANDS, RELATED_TO, CAUSES) are edges.

- Start with `list_projects`; ask which project if more than one fits.
- Use `get_task_context` to read a task with its neighbourhood before reasoning about it.
- Prefer `create_task` with the `relationships` argument over separate edge calls.
- Do not create, delete or change tasks without the user's agreement; read freely.
- Answers belong in chat. Only use `pin_view` or `create_dynamic_view` when the user asks to keep a view.
