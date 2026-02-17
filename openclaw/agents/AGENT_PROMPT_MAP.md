# Agent Prompt Map (4-Agent Setup)

## orchestrator

System prompt:
- `orchestrator/prompts/main_system_prompt.md`

Task prompts:
- `orchestrator/prompts/10_select_next_action.md`
- `orchestrator/prompts/11_update_story_state.md`
- `orchestrator/prompts/12_compose_next_action.md`
- `orchestrator/prompts/90_summarize_current_state.md`
- `orchestrator/prompts/91_rebuild_story_state_from_files.md`
- `orchestrator/prompts/92_checkpoint_snapshot.md`
- `orchestrator/prompts/99_fail_safe_stop_or_pause.md`

Primary state updates:
- `<STATE_ROOT>/run/next_action.md`
- `<STATE_ROOT>/run/story_state.md`
- `<STATE_ROOT>/run/run_log.md`

## planner

System prompt:
- `planner/prompts/main_system_prompt.md`

Task prompts:
- `planner/prompts/00_root_seed_to_overarching.md`
- `planner/prompts/01_overarching_to_chapters.md`
- `planner/prompts/02_chapters_to_chapter_spec.md`
- `planner/prompts/03_chapter_spec_to_scenes.md`

Primary state updates:
- `<STATE_ROOT>/outline/*`
- `<STATE_ROOT>/run/story_state.md`
- `<STATE_ROOT>/run/run_log.md`
- bootstrap only: `<STATE_ROOT>/memory/characters/index.md`, `<STATE_ROOT>/memory/event_log.md`

## writer

System prompt:
- `writer/prompts/main_system_prompt.md`

Task prompts:
- `writer/prompts/04_scene_plan_to_prose.md`

Primary state updates:
- `<STATE_ROOT>/draft/chapters/chXX_prose.md`
- `<STATE_ROOT>/draft/story.md`
- `<STATE_ROOT>/run/story_state.md`
- `<STATE_ROOT>/run/run_log.md`

## continuity_editor

System prompt:
- `continuity_editor/prompts/main_system_prompt.md`

Task prompts:
- `continuity_editor/prompts/05_prose_to_memory_update.md`
- `continuity_editor/prompts/20_validate_continuity.md`
- `continuity_editor/prompts/21_detect_contradictions.md`
- `continuity_editor/prompts/22_repair_outline_or_memory.md`
- `continuity_editor/prompts/23_repair_prose_scene.md`
- `continuity_editor/prompts/24_style_and_voice_check.md`
- `continuity_editor/prompts/30_pacing_check.md`
- `continuity_editor/prompts/31_theme_density_check.md`
- `continuity_editor/prompts/32_character_arc_check.md`
- `continuity_editor/prompts/33_foreshadowing_update.md`
- `continuity_editor/prompts/34_open_threads_update.md`

Primary state updates:
- `<STATE_ROOT>/memory/*`
- repair only: `<STATE_ROOT>/draft/chapters/chXX_prose.md`
- `<STATE_ROOT>/run/story_state.md`
- `<STATE_ROOT>/run/run_log.md`
