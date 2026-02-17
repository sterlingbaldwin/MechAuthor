# Agent Registry

## 1. Orchestrator Agent
Purpose: Controls progression and routing.
Reads: `run/story_state.md`, validation/repair flags.
Writes: `run/next_action.md`, `run/run_log.md`.
Must not write: outline, draft, memory canonical files.

## 2. Planner Agent
Purpose: Expand seed into macro narrative arc.
Reads: seed and global style/rules prompts.
Writes: `outline/overarching_plot.md`, `memory/characters/index.md`, `memory/event_log.md`, `run/story_state.md`.

## 3. Architect Agent
Purpose: Convert overarching plot into chapter plans.
Reads: `outline/overarching_plot.md`.
Writes: `outline/chapters.md`, `outline/chapters/chXX.md`, `run/story_state.md`.

## 4. Scene Builder Agent
Purpose: Build scene plans for a chapter.
Reads: `outline/chapters/chXX.md`, continuity context.
Writes: `outline/scenes/chXX_scenes.md`, `run/story_state.md`.

## 5. Writer Agent
Purpose: Produce prose scene-by-scene.
Reads: scene plan, chapter spec, memory files, style guide.
Writes: `draft/chapters/chXX_prose.md`, `draft/story.md`, `run/story_state.md`.

## 6. Continuity Editor Agent
Purpose: Update memory and detect contradictions.
Reads: new prose, existing memory state.
Writes: `memory/event_log.md`, `memory/characters/*.md`, `memory/open_threads.md`, `memory/foreshadowing.md`, validation flags in `run/story_state.md`.

## 7. Repair Agent (Optional)
Purpose: Repair malformed output or contradictions.
Reads: failed artifacts and validator findings.
Writes: corrected target file(s), clears repair flags in `run/story_state.md`.

## Phase Transitions
- `PLAN_OVERARCHING` -> `PLAN_CHAPTERS` -> `PLAN_SCENES` -> `SCENE_PROSE` -> `CONTINUITY_UPDATE`.
- Orchestrator may route to `REPAIR` when `repair_required: true`.
- Completion condition: all chapters/scenes complete, no open validation issues, `story_complete: true`.
