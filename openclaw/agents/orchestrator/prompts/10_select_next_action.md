# Orchestrator Task: Select Next Action

Goal: Decide the next agent and task from `<STATE_ROOT>/run/story_state.md`.

Output:
- `<STATE_ROOT>/run/next_action.md`

Routing rules:
- If `repair_required: true`, route to repair.
- Else if `validation_required: true`, route to continuity validation.
- Else route by `current_phase`.
