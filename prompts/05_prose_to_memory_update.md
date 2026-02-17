# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `memory/event_log.md`
- `memory/open_threads.md`
- `memory/foreshadowing.md`
- `memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `run/story_state.md` when needed.
