# Continuity Editor Task: Prose -> Memory Update

Goal: Update canonical memory after prose generation.

Inputs:
- `/vol/projects/mechauthor/openclaw/global_state/draft/chapters/chXX_prose.md`
- existing memory files

Outputs:
- `/vol/projects/mechauthor/openclaw/global_state/memory/event_log.md`
- `/vol/projects/mechauthor/openclaw/global_state/memory/open_threads.md`
- `/vol/projects/mechauthor/openclaw/global_state/memory/foreshadowing.md`
- `/vol/projects/mechauthor/openclaw/global_state/memory/characters/*.md`

Also:
- Set `validation_required` or `repair_required` in `/vol/projects/mechauthor/openclaw/global_state/run/story_state.md` when needed.
