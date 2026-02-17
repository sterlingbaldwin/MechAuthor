# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `/vol/projects/MechAuthor/openclaw/global_state/draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `/vol/projects/MechAuthor/openclaw/global_state/memory/event_log.md`
- `/vol/projects/MechAuthor/openclaw/global_state/memory/open_threads.md`
- `/vol/projects/MechAuthor/openclaw/global_state/memory/foreshadowing.md`
- `/vol/projects/MechAuthor/openclaw/global_state/memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `/vol/projects/MechAuthor/openclaw/global_state/run/story_state.md` when needed.
