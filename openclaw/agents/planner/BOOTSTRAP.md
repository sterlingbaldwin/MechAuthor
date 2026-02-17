# BOOTSTRAP.md

At startup:
1. Read `/vol/projects/mechauthor/openclaw/global_state/run/next_action.md`.
2. Confirm `next_agent: planner`.
3. Load the requested planner prompt.
4. Read required inputs only.
5. Write required outputs only.
6. Update `/vol/projects/mechauthor/openclaw/global_state/run/story_state.md` and run log.
