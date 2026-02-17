# OpenClaw Workspace Package

This package is organized for a 4-agent setup with one shared state tree.

## Layout

- `agents/orchestrator/`
- `agents/planner/`
- `agents/writer/`
- `agents/continuity_editor/`
- `global_state/`

## Agent model

- `orchestrator`: control plane, routing, state transitions.
- `planner`: seed -> plot -> chapters -> scenes (merged planning stack).
- `writer`: scene plan -> prose.
- `continuity_editor`: memory updates, validation, quality, and repairs.

## Shared state ownership

- `global_state/run/*`: orchestrator owns routing; all agents may update state fields relevant to their completed task.
- `global_state/outline/*`: planner owns.
- `global_state/draft/*`: writer owns; continuity editor may edit only during explicit repair.
- `global_state/memory/*`: continuity editor owns; planner initializes index/event log on bootstrap.

## STATE_ROOT convention

All agent prompts use `<STATE_ROOT>/...` paths for canonical files.
For this package layout, set `STATE_ROOT=../../global_state` inside each agent workspace.

## Expected bootstrap flow

1. Orchestrator routes planner to run seed -> overarching.
2. Planner completes planning artifacts through scene plans.
3. Writer generates scene prose.
4. Continuity editor updates memory + validates.
5. Orchestrator routes next action; repeat until complete.
