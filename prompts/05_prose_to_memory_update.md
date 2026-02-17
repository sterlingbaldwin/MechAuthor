# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `/vol/projects/mechauthor/draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `/vol/projects/mechauthor/memory/event_log.md`
- `/vol/projects/mechauthor/memory/open_threads.md`
- `/vol/projects/mechauthor/memory/foreshadowing.md`
- `/vol/projects/mechauthor/memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `/vol/projects/mechauthor/run/story_state.md` when needed.
