# TOOLS.md

Prompt set:
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/main_system_prompt.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/10_select_next_action.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/11_update_story_state.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/12_compose_next_action.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/90_summarize_current_state.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/91_rebuild_story_state_from_files.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/92_checkpoint_snapshot.md`
- `/vol/projects/mechauthor/openclaw/agents/orchestrator/prompts/99_fail_safe_stop_or_pause.md`

Core files:
- Read: `/vol/projects/mechauthor/openclaw/global_state/run/story_state.md`
- Write: `/vol/projects/mechauthor/openclaw/global_state/run/next_action.md`
- Write: `/vol/projects/mechauthor/openclaw/global_state/run/run_log.md`
- Optional write: `/vol/projects/mechauthor/openclaw/global_state/run/story_state.md`
