# Design Document

## Multi-Agent Iterative Long-Form Fiction Generator Using OpenClaw

---

# 1. Overview

This system is an autonomous long-form fiction generator built entirely inside OpenClaw using:

* Cron-triggered looping execution
* Structured markdown files for state
* Multiple specialized agent definitions
* Iterative layer-based narrative expansion

The major architectural evolution in this version is:

> Instead of a single agent handling all layers, we use **multiple specialized agents**, each responsible for one layer of narrative expansion or validation.

This improves:

* Prompt clarity
* Structural reliability
* Narrative coherence
* Model specialization
* Recoverability

The system becomes a **modular narrative pipeline**, orchestrated by a control agent.

---

# 2. Core Philosophy

The system is data-only.

Each agent run behaves like a pure function:

```
(current file state) -> (updated files + next state)
```

There is no executable code.
All logic lives in:

* Prompt definitions
* Agent specialization
* Markdown state files
* Cron-triggered iteration

---

# 3. High-Level Architecture

We now split responsibilities into distinct agent roles.

## Agent Roles

1. **Orchestrator Agent**
2. **Planner Agent**
3. **Architect Agent**
4. **Scene Builder Agent**
5. **Writer Agent**
6. **Continuity Editor Agent**
7. (Optional) Repair / Validator Agent

Each agent has:

* A dedicated system prompt
* A clear file read/write boundary
* A defined role in the story lifecycle
* Optionally, a different model

---

# 4. Narrative Expansion Layers

The story grows through structured expansion:

```
Seed
  → Overarching Plot
      → Chapters
          → Scenes
              → Prose
```

Each layer is handled by a different agent.

---

# 5. Agent Definitions

---

## 5.1 Orchestrator Agent (Control Plane)

### Purpose

Controls iteration flow.

### Responsibilities

* Reads `run/story_state.md`
* Decides which agent runs next
* Writes `run/next_action.md`
* Logs execution
* Detects completion

### It does NOT:

* Write prose
* Modify story structure
* Alter character state

### Model

Cheapest, fastest available.

### Files Read

* `run/story_state.md`
* Possibly validation flags

### Files Written

* `run/next_action.md`
* `run/run_log.md`

---

## 5.2 Planner Agent (Seed → Overarching Plot)

### Purpose

Expand user seed into macro narrative arc.

### Output

* `outline/overarching_plot.md`
* Initialize `memory/characters/index.md`
* Initialize `memory/event_log.md`

### Focus

* Core conflict
* Major turning points
* Ending state
* Character list
* Central themes

### Model

Mid-tier.

---

## 5.3 Architect Agent (Overarching → Chapters)

### Purpose

Break overarching plot into 4–5 thematically consistent chapters.

### Output

* `outline/chapters.md`
* `outline/chapters/chXX.md`

Each chapter includes:

* Theme
* Goal
* Emotional arc
* Structural beats

### Model

Mid-tier.

---

## 5.4 Scene Builder Agent (Chapter → Scene Structure)

### Purpose

Create scene plans for one chapter at a time.

### Output

* `outline/scenes/chXX_scenes.md`

Each scene contains:

* Characters
* Goal
* Conflict
* Event
* Outcome
* Emotional shift

### Model

Mid-tier.

---

## 5.5 Writer Agent (Scene → Prose)

### Purpose

Generate narrative prose for a single scene.

### Output

* `draft/chapters/chXX_prose.md`
* Append to `draft/story.md`

### Input Context

* Scene plan
* Chapter spec
* Character sheets
* Event log
* Themes
* Style guide

### Model

Highest-quality model.

---

## 5.6 Continuity Editor Agent (Prose → Memory Update)

### Purpose

Maintain narrative consistency and update state.

### Output

* Update `memory/event_log.md`
* Update per-character files
* Update `memory/open_threads.md`
* Update `memory/foreshadowing.md`
* Flag contradictions

### Traits

* Pedantic
* Rules-driven
* Non-creative

### Model

Cheaper, reliable model.

---

## 5.7 Optional Repair Agent

Triggered if:

* Validation fails
* Output malformed
* Continuity contradiction detected

Can:

* Rewrite scene
* Adjust memory
* Repair outline inconsistencies

---

# 6. Cron Execution Flow

Every 15 minutes:

1. Cron triggers Orchestrator.
2. Orchestrator reads `story_state.md`.
3. Orchestrator selects next agent.
4. Writes `next_action.md`.
5. That agent runs.
6. Agent updates files + advances `story_state.md`.
7. Loop repeats.

---

# 7. story_state.md (Control Structure)

Example:

```
current_phase: SCENE_PROSE
current_chapter: 2
current_scene: 3
total_chapters: 5
scenes_in_current_chapter: 6
story_complete: false
validation_required: false
repair_required: false
```

This file is the sole progression authority.

---

# 8. File Responsibilities by Agent

| Agent         | Reads               | Writes                    |
| ------------- | ------------------- | ------------------------- |
| Orchestrator  | story_state         | next_action               |
| Planner       | seed                | overarching_plot          |
| Architect     | overarching_plot    | chapters                  |
| Scene Builder | chapter_spec        | chapter_scenes            |
| Writer        | scene_plan + memory | prose                     |
| Editor        | prose               | memory + validation flags |

Agents do not overwrite files outside their domain.

---

# 9. Memory System (Unchanged but Now Agent-Enforced)

Memory remains in:

```
memory/
  event_log.md
  continuity_rules.md
  open_threads.md
  foreshadowing.md
  characters/
    index.md
    <character>.md
```

Now the Continuity Editor is solely responsible for updating it.

This separation prevents prose from corrupting canonical state.

---

# 10. Advantages of Multi-Agent Design

### 10.1 Prompt Isolation

Each agent has a narrow purpose.
No giant “do everything” system prompt.

### 10.2 Model Specialization

* Writer uses premium model.
* Orchestrator uses cheap model.
* Editor uses fast deterministic model.

### 10.3 Failure Isolation

If prose is bad:

* Re-run Writer only.
  If continuity breaks:
* Run Editor repair only.

### 10.4 Iterative Scalability

Future agents can be added:

* Thematic Density Agent
* Pacing Optimizer
* Character Arc Validator
* Style Polisher

Without touching core pipeline.

---

# 11. Conceptual Model

We now have a two-layer system:

## Layer A: Narrative Expansion Tree

```
Seed
  → Plot
      → Chapters
          → Scenes
              → Prose
```

## Layer B: Agent Orchestration Graph

```
Orchestrator
   ↓
Planner
   ↓
Architect
   ↓
Scene Builder
   ↓
Writer
   ↓
Continuity Editor
   ↓
Orchestrator
```

This forms a controlled loop.

---

# 12. System Completion Condition

The story is complete when:

* All chapters processed
* All scenes written
* No open threads remain unresolved
* No validation flags present
* story_complete = true

At that point:
Orchestrator halts.

---

# 13. Summary

We now have:

* A layered narrative compiler
* Multi-agent specialization
* Deterministic control flow
* File-based memory system
* Cron-driven autonomous expansion
* Isolated responsibilities
* Model-specific task routing

This architecture transforms the system from:

> “A looping storyteller”

into

> “A distributed autonomous fiction production pipeline.”

---

If you want, next we can:

* Write the agent registry spec (exact OpenClaw agent configs)
* Define file read/write boundaries per agent formally
* Or simulate a full iteration cycle across all agents


---

## 14. Summary

We have designed:

* A five-layer narrative expansion engine
* Purely prompt-driven architecture
* Markdown-based persistent memory
* Cron-driven autonomous iteration
* State-tracked progression
* Character-consistent storytelling
* Thematically evolving prose

This is effectively:

**An autonomous long-form fiction compiler built from iterative LLM expansion layers.**

---


Here is a complete initial set of prompt files (just the list), organized by purpose and in a practical execution order. This covers the full pipeline (seed -> plot -> chapters -> scenes -> prose) plus the “glue” prompts you’ll want for validation, repair, and steady-state looping.

## Prompt file list

### A) Global wrappers and shared rules

* `prompts/main_system_prompt.md`
* `prompts/style_guide.md`
* `prompts/output_format_contract.md`
* `prompts/file_io_rules.md`

### B) Core pipeline layer prompts

* `prompts/00_root_seed_to_overarching.md`
* `prompts/01_overarching_to_chapters.md`
* `prompts/02_chapters_to_chapter_spec.md`
* `prompts/03_chapter_spec_to_scenes.md`
* `prompts/04_scene_plan_to_prose.md`
* `prompts/05_prose_to_memory_update.md`

### C) State management and iteration control

* `prompts/10_select_next_action.md`
* `prompts/11_update_story_state.md`
* `prompts/12_compose_next_action.md`

### D) Consistency, validation, and repair

* `prompts/20_validate_continuity.md`
* `prompts/21_detect_contradictions.md`
* `prompts/22_repair_outline_or_memory.md`
* `prompts/23_repair_prose_scene.md`
* `prompts/24_style_and_voice_check.md`

### E) Optional but very useful “quality passes”

* `prompts/30_pacing_check.md`
* `prompts/31_theme_density_check.md`
* `prompts/32_character_arc_check.md`
* `prompts/33_foreshadowing_update.md`
* `prompts/34_open_threads_update.md`

### F) Emergency / reset / operator utilities

* `prompts/90_summarize_current_state.md`
* `prompts/91_rebuild_story_state_from_files.md`
* `prompts/92_checkpoint_snapshot.md`
* `prompts/99_fail_safe_stop_or_pause.md`

If you want a tighter “MVP prompt set” (minimum viable prompts) that still works end-to-end, it would be:

* `main_system_prompt.md`
* `style_guide.md`
* `00_root_seed_to_overarching.md`
* `01_overarching_to_chapters.md`
* `02_chapters_to_chapter_spec.md`
* `03_chapter_spec_to_scenes.md`
* `04_scene_plan_to_prose.md`
* `05_prose_to_memory_update.md`
* `20_validate_continuity.md`
* `22_repair_outline_or_memory.md`

Say the word and I’ll turn whichever list you choose into a numbered “prompt registry” (IDs, when it runs, which files it reads/writes) without writing the prompt contents yet.


----------------------------

Recommended design

Split by “responsibility boundary”, not by file count. A good starting set is 4-6 agents.

1) Planner Agent (Seed -> Overarching)

Role: Expand seed into macro arc, major beats, core conflict.
Output: outline/overarching_plot.md, initializes characters list.
Traits: Deterministic, structured, no prose.
Model: mid-tier is usually fine.

2) Architect Agent (Overarching -> Chapters + Chapter Specs)

Role: Create 4-5 chapters, each thematically coherent, with goals and turning points.
Output: outline/chapters.md + outline/chapters/chXX.md
Traits: Outline discipline, continuity aware.
Model: mid-tier.

3) Scene Builder Agent (Chapter Spec -> Scene List)

Role: Produce scene plans with causality and consequences.
Output: outline/scenes/chXX_scenes.md
Traits: Extremely structured, checks constraints (scene count, POV, time progression).
Model: mid-tier.

4) Writer Agent (Scene Plan -> Prose)

Role: Write the actual story text scene-by-scene.
Output: draft/chapters/chXX_prose.md and/or append to draft/story.md
Traits: Strong voice, sensory details, emotion, pacing.
Model: your “best” model.

5) Continuity Editor Agent (Prose -> Memory Update + Validation)

Role: Update character sheets + event log + open threads; detect contradictions.
Output: memory/* updates + optionally “issues.md”.
Traits: Pedantic, rules-first, no creativity.
Model: cheaper/fast is often fine.

6) Orchestrator Agent (Decide what to run next)

Role: Reads story_state.md, chooses next agent, writes run/next_action.md.
Output: run/next_action.md, updates run/run_log.md.
Traits: Minimal, reliable, “control plane”.
Model: cheapest/fastest.

That gives you clean boundaries and lets you swap models per agent.

How the cron loop works with multiple agents

You keep your existing cron loop, but it becomes:

Cron fires.

Orchestrator reads run/story_state.md.

Orchestrator writes run/next_action.md like:

next_agent: writer
task: write_scene_prose
chapter: 2
scene: 3
read_files:
  - prompts/writer_scene_to_prose.md
  - outline/scenes/ch02_scenes.md
  - outline/chapters/ch02.md
  - memory/characters/*.md
  - memory/event_log.md
write_files:
  - draft/chapters/ch02_prose.md
  - memory/event_log.md
  - memory/characters/*.md
  - run/story_state.md


Cron triggers the chosen agent definition with that context.

That agent produces updates and advances story_state.md.

Key point: the Orchestrator stays dumb. It does not write story. It routes.

Why agent-per-layer is especially good here

Prompts become shorter and stricter.

You can tune “temperature”/style per agent without polluting the others.

Writer can be creative without risking structural corruption.

Editor can be strict without killing voice.

You can rerun a single step by re-pointing next_action.md.

Practical file impact

This pairs nicely with your existing prompts/ structure, but prompts become agent-scoped. For example:

prompts/
  orchestrator/
    select_next_action.md
  planner/
    seed_to_overarching.md
  architect/
    overarching_to_chapters.md
    chapters_to_chapter_spec.md
  scene_builder/
    chapter_spec_to_scenes.md
  writer/
    scene_plan_to_prose.md
  editor/
    prose_to_memory_update.md
    validate_continuity.md


Agent definitions then simply point at:

a system prompt for that agent

a default “task prompt” template

model selection for that agent

Step-by-step approach to implement in OpenClaw (no code)

Create 5-6 OpenClaw agent definitions (Planner, Architect, SceneBuilder, Writer, Editor, Orchestrator).

Give each one:

a tight system prompt

allowed file read/write constraints (if OpenClaw supports)

model choice

Cron always runs Orchestrator.

Orchestrator launches the next agent (or writes instructions that your existing launcher reads).

Each worker agent writes outputs + updates story_state.md.

Orchestrator detects completion or issues and routes accordingly (e.g., call Repair agent if validation fails).

If you want, the next thing I can do is write a clean registry:

agent name

purpose

model

which prompts it owns

which files it is allowed to read/write

what it must update in story_state.md

No prompt contents yet, just the spec layer so you can build OpenClaw agent configs confidently.