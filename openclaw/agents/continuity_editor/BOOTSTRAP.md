# BOOTSTRAP.md

At startup:
1. Read `/vol/projects/mechauthor/openclaw/global_state/run/next_action.md`.
2. Confirm `next_agent: continuity_editor`.
3. Resolve task type:
   - memory update
   - validation
   - contradiction detection
   - repair
   - optional quality pass
4. Execute one task only.
5. Update state flags and append run log entry.
