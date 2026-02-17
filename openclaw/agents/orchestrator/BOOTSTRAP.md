# BOOTSTRAP.md

At startup:
1. Read `/vol/projects/mechauthor/openclaw/global_state/run/story_state.md`.
2. Validate required fields exist.
3. If invalid state: run rebuild/repair route and log it.
4. Select next action using orchestrator prompts.
5. Write `/vol/projects/mechauthor/openclaw/global_state/run/next_action.md` with:
   - `next_agent`
   - `task`
   - `reason`
   - `chapter`
   - `scene`
   - `read_files`
   - `write_files`
