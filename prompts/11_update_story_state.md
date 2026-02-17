# State Task: Update Story State

Goal: Apply deterministic updates to `run/story_state.md` after task completion.

Requirements:
- Increment scene/chapter counters safely.
- Update phase when chapter/scene boundaries are crossed.
- Set `story_complete: true` only when all completion checks pass.
