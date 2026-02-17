# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `<STATE_ROOT>/draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `<STATE_ROOT>/memory/event_log.md`
- `<STATE_ROOT>/memory/open_threads.md`
- `<STATE_ROOT>/memory/foreshadowing.md`
- `<STATE_ROOT>/memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `<STATE_ROOT>/run/story_state.md` when needed.
