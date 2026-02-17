# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `/vol/projects/MechAuthor/draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `/vol/projects/MechAuthor/memory/event_log.md`
- `/vol/projects/MechAuthor/memory/open_threads.md`
- `/vol/projects/MechAuthor/memory/foreshadowing.md`
- `/vol/projects/MechAuthor/memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `/vol/projects/MechAuthor/run/story_state.md` when needed.
