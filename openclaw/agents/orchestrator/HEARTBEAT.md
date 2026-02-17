# HEARTBEAT.md

Per cycle checklist:
1. Load state.
2. Resolve route:
   - `repair_required: true` -> continuity_editor repair task
   - `validation_required: true` -> continuity validation task
   - else route by `current_phase`
3. Emit next action.
4. Append one run log entry.
5. Exit.
