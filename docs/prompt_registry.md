# Prompt Registry

This registry uses the **full set**. IDs are stable and map 1:1 to filenames.

| ID | File | Owner Agent | When It Runs | Reads | Writes |
| --- | --- | --- | --- | --- | --- |
| PR-001 | `prompts/main_system_prompt.md` | Global wrapper | Loaded by all agents before task prompts | Global rules only | None |
| PR-002 | `prompts/style_guide.md` | Global wrapper | Loaded by Planner/Writer/quality checks | Style rules | None |
| PR-003 | `prompts/output_format_contract.md` | Global wrapper | Loaded by all output-producing agents | Format rules | None |
| PR-004 | `prompts/file_io_rules.md` | Global wrapper | Loaded by all file-writing agents | I/O boundary rules | None |
| PR-005 | `prompts/00_root_seed_to_overarching.md` | Planner | Initial phase (`PLAN_OVERARCHING`) | Seed input, PR-002 | `outline/overarching_plot.md`, `memory/characters/index.md`, `memory/event_log.md`, `run/story_state.md` |
| PR-006 | `prompts/01_overarching_to_chapters.md` | Architect | After Planner completes (`PLAN_CHAPTERS`) | `outline/overarching_plot.md` | `outline/chapters.md`, `run/story_state.md` |
| PR-007 | `prompts/02_chapters_to_chapter_spec.md` | Architect | Per chapter during chapter-spec expansion | `outline/chapters.md` | `outline/chapters/chXX.md`, `run/story_state.md` |
| PR-008 | `prompts/03_chapter_spec_to_scenes.md` | Scene Builder | Per chapter during scene planning (`PLAN_SCENES`) | `outline/chapters/chXX.md`, memory context | `outline/scenes/chXX_scenes.md`, `run/story_state.md` |
| PR-009 | `prompts/04_scene_plan_to_prose.md` | Writer | Per scene during prose phase (`SCENE_PROSE`) | `outline/scenes/chXX_scenes.md`, `outline/chapters/chXX.md`, memory files, PR-002 | `draft/chapters/chXX_prose.md`, `draft/story.md`, `run/story_state.md` |
| PR-010 | `prompts/05_prose_to_memory_update.md` | Continuity Editor | After each scene prose generation (`CONTINUITY_UPDATE`) | New prose + all memory files | `memory/event_log.md`, `memory/characters/*.md`, `memory/open_threads.md`, `memory/foreshadowing.md`, `run/story_state.md` |
| PR-011 | `prompts/10_select_next_action.md` | Orchestrator | Every control loop tick | `run/story_state.md`, validation flags | `run/next_action.md` |
| PR-012 | `prompts/11_update_story_state.md` | Orchestrator or active worker | Immediately after any successful task | `run/story_state.md`, task completion metadata | `run/story_state.md` |
| PR-013 | `prompts/12_compose_next_action.md` | Orchestrator | After selecting route | `run/story_state.md`, routing decision | `run/next_action.md`, `run/run_log.md` |
| PR-014 | `prompts/20_validate_continuity.md` | Continuity Editor | When `validation_required: true` or at configured cadence | Latest prose, memory files | Validation section in `run/run_log.md`, flags in `run/story_state.md` |
| PR-015 | `prompts/21_detect_contradictions.md` | Continuity Editor | As part of continuity validation | Draft + memory + outline evidence | Contradiction report in `run/run_log.md`, `run/story_state.md` flags |
| PR-016 | `prompts/22_repair_outline_or_memory.md` | Repair Agent | When contradiction points to structure/memory | Failed report + target files | Repaired outline/memory files, cleared flags in `run/story_state.md` |
| PR-017 | `prompts/23_repair_prose_scene.md` | Repair Agent | When contradiction points to a prose scene | Target scene prose + contradiction report | Repaired `draft/chapters/chXX_prose.md`, optional `draft/story.md`, updated `run/story_state.md` |
| PR-018 | `prompts/24_style_and_voice_check.md` | Quality/Editor | Optional pass after scene/chapter prose | Prose targets + PR-002 | Style verdict in `run/run_log.md`, optional `run/story_state.md` flags |
| PR-019 | `prompts/30_pacing_check.md` | Quality pass | Optional periodic check (scene/chapter cadence) | `draft/story.md`, chapter prose files | Pacing findings in `run/run_log.md` |
| PR-020 | `prompts/31_theme_density_check.md` | Quality pass | Optional periodic check | `draft/story.md`, `outline/overarching_plot.md` | Theme findings in `run/run_log.md` |
| PR-021 | `prompts/32_character_arc_check.md` | Quality pass | Optional after each chapter | Chapter prose + character files + event log | Arc findings in `run/run_log.md`, optional repair flags |
| PR-022 | `prompts/33_foreshadowing_update.md` | Quality/Editor | Optional after chapter close | Current prose + `memory/foreshadowing.md` | Updated `memory/foreshadowing.md` |
| PR-023 | `prompts/34_open_threads_update.md` | Quality/Editor | Optional after chapter close | Current prose + `memory/open_threads.md` | Updated `memory/open_threads.md` |
| PR-024 | `prompts/90_summarize_current_state.md` | Operator utility | On-demand operator summary | run/outline/draft/memory files | Summary note in `run/run_log.md` |
| PR-025 | `prompts/91_rebuild_story_state_from_files.md` | Operator utility | Recovery when state is missing/corrupt | outline/draft/memory/run artifacts | Rebuilt `run/story_state.md`, recovery note in `run/run_log.md` |
| PR-026 | `prompts/92_checkpoint_snapshot.md` | Operator utility | Scheduled or manual checkpoint | `run/story_state.md` + key artifacts | Checkpoint entry in `run/run_log.md` |
| PR-027 | `prompts/99_fail_safe_stop_or_pause.md` | Operator utility | Triggered after repeated failures or unsafe state | `run/story_state.md`, recent log history | Halt/pause flags in `run/story_state.md`, stop entry in `run/run_log.md` |

## MVP Subset Mapping

If using the MVP subset, activate these IDs only:
- PR-001
- PR-002
- PR-005
- PR-006
- PR-007
- PR-008
- PR-009
- PR-010
- PR-014
- PR-016
